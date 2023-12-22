# File Path Resolve

Linux operation system has a file path resolve algorithm

> There are some shorthand notations:

- '.' and '~+' current path($PWD) if there was before
- '..' parent directory
- '/' root directory
- '~' home directory
- '~-' and '-' old path($OLDPWD) if there was before

When these expressions come together, they can create long lines.
The expression become simpler when file path resolved.
Processing becomes easier with simplified file path.

## Scenario

Let's say you need to start automatic process when plug in usb stick to device.
Most probably initiated process will be mounted on available directory according to udev rules.

It is necessary to find out which directory the process was started from.
In fact, what needs to be done is string split operation like in any other programming languages, but It is needs to be done with bash script, there are few commands.

## Research

> Here are commands i found on the subject.

### `dirname[^1]`

Its purpose is to give the directory of the directory or file.
What is does it removes file name along with the '/' separator.

- It doesn't output a new line character if command used with `-z` option. 
Can be used with `xargs -0`.

> But there's a problem.

    1. It gives away relative file path('.') if it doesn't place to command full file path.
    2. It doesn't give any output to the last command output.
    3. It performs string operation whatever file path is full or relative.

``` shell
echo $PWD                                   # /home/username
dirname $PWD                                # /home
echo $?                                     # last exit code
dirname file                                # .
echo $?                                     # last exit code
dirname $PWD/file                           # /home/username
echo $?                                     # last exit code
dirname yok/boyle/bir/dosya/veya/dizin      # yok/boyle/bir/dosya/veya
dirname /yok/boyle/bir/dosya/veya/dizin     # /yok/boyle/bir/dosya/veya
dirname yok                                 # .
echo $?                                     # last exit code
```

### `basename`[^2]

Its purpose is similar to [dirname](DosyaYolu.md#dirname). This command takes file name in place of file path.
What it does it removes file path along with the '/' seperator.

- It doesn't output any new line character if command used with `-z` option.
Can be used with `xargs -0`
- The command can operate on multiple strings and output multiple strings with `basename -a`.

    ``` shell
    basename -a yok/boyle bir/sey
    # boyle
    # sey
    ```

- Typing `basename -s <seperator> <string>` can be used to remove file extension.

    ``` shell
    basename -s .pyc $sysroot/python/site/numpy.pyc
    # curl
    ```

There are some special variables. `$0` is one of them and i can't continue without mansion it. It used to print file name of the bash script currently running on.
There is one big catch! It gives file name with full path if the bash script initiates with full file path.

> Problems are the same as dirname

``` shell
echo $PWD                                   # /home/username
basename $PWD                               # username
echo $?                                     # last exit code
basename file                               # file
echo $?                                     # last exit code
basename $PWD/file                          # /home/username
echo $?                                     # last exit code
basename yok/boyle/bir/dosya/veya/dizin     # dizin
basename /yok/boyle/bir/dosya/veya/dizin    # dizin
basename yok                                # yok
echo $?                                     # last exit code
```

### `readlink`[^3]

Base functionality is file name resolution.

1. The command resolve(follows) directory or file **symbolic** links.
2. It resolves the file path and throughput file name with **Canonical(in line with rules, simplified)**.

- It doesn't produce any new line character if it used with `-z` option. Can be used with `xargs -0`

```shell
readlink -f file
readlink -f $PWD/file
```

### `realpath`[^4]

Main functionality is resolving(follow) similar to [readlink](DosyaYolu.md#readlink).
The main difference with `readlink` is that `readlink` by default only gives result 
if it is a symbolic link, while `realpath` output result regardless of whether it is symbolic.

``` shell
readlink /usr/../usr/..    #
realpath /usr/../usr/..    # /
```

1. It doesn't output new line character if it used with `-z` option. Can be used with `xargs -0`
2. `-s` option behavior stands out from other commands used to resolve file path.

    > Let's presume "/usr/bin/X11/" is symbolic link to "/usr/bin/".

    ``` shell
    realpath /../usr/bin/X11/./xterm        # /usr/bin/xterm
    realpath -s /../usr/bin/X11/./xterm     # /usr/bin/X11/xterm
    ```



## Solution

I have a method for this problem. 
`dirname $(readlink -f file)` or `dirname $(realpath file)` resolve file path correctly.
I have to say, i don't know which one is better.

## Test

``` shell
echo $PWD
dirname $PWD
dirname file
dirname $PWD/file
readlink -f $PWD/file
readlink -f file
dirname $(readlink -f file)
dirname $(readlink -f file_link)
dirname $(readlink -e file_link)
echo $(readlink -e file_link)
echo $(readlink -f file_link)
echo $(readlink -e file_link)
echo $(readlink -e )
echo $(readlink -e dir)
echo $(readlink -e .)
dirname .
echo $(readlink -e .)
dirname file
dirname file_link
echo $(readlink -e file)
dirname $(readlink -e file)
realpath file
realpath .
dirname $(realpath file)
echo $(realpath file)
echo $(readlink -m file)
```

[^1]: <https://linux.die.net/man/1/readlink>
[^2]: <https://linux.die.net/man/1/basename>
[^3]: <https://man7.org/linux/man-pages/man1/readlink.1.html>
[^4]: <https://man7.org/linux/man-pages/man3/realpath.3.html>
