# File Path Resolve

Linux operation system has a file path resolve algoritm

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










## Solution


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
