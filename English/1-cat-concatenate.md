[VIDEO](https://youtu.be/dC6JloOWy1o)

# [Linux'ta Concatenate Command](https://youtu.be/dC6JloOWy1o)

[`Cat`]([^1]) is abbreviation of "concatenate" word. There are several functionalities.
This command not just combine sequentially text files also it can concatenate some data and media file types.

[`cat`]([^1]) command combines, prints have different usage options in general. It is very handful tool for linux users.

## Combining Files

Its most common usage is printing stuff to the screen. Combining files is the most important usage for me.

- Let's create files named 1 to 3 and fill with file names.

    ``` shell
    $ echo 1 > 1.txt
    $ echo 2 > 2.txt
    $ echo 3 > 3.txt
    ```

- print files one by one

    ``` shell
    $ cat 1.txt
    1

    $ cat 2.txt
    2

    $ cat 3.txt
    3
    ```

- print all in one time. Which output is which file name is unknown.

    ``` shell
    $ cat {1..3}.txt
    1
    2
    3
    ```

- I merged {1..3}.txt files sequentially and was able to view them as a single file.

    ``` shell
    $ cat 1.txt 2.txt 3.txt > 123.txt
    $ cat 123.txt
    1
    2
    3
    ```

## File Redirection

(I will elaborate on this issue later)
Another usage scenario occurs when you want to redirect files. 
[`Cat`]([^1]) outputs to the `stdout` file and you can redirect this special file to another file

``` shell
$ echo "Arda" >> günlük
$ echo "Fakat sadece günlük kalmış" >> günlük
$ cat günlük >> günlük2
$ cat günlük2
Arda
Fakat sadece günlük kalmış
Arda
Fakat sadece günlük kalmış
```

## [`Cat`]([^1]) Options

Let's create the example file.

``` bash
seq 5 > asd
```

- `-n` and  `-b` options shows the line numbers.

    ``` shell
    $ cat -b asd
        1  1
        2  2
        3  3
        4  4
        5  5
    ```

- `-E` option shows line break character.
- `-v` disables unicode presentation.
- Moreover, `-e` option shows line break character and disables unicode presentation(`-vE`)

    ``` shell
    $ cat -e asd
    1$
    2$
    3$
    4$
    5$
    ```

## Unnecessary Usage

- [`Cat`]([^1]) gives output to `stdout` file in first place if the file name is not specified.

    ``` shell
    $ cat asd
    ```

- There is no point to redirect file to process.

    ``` shell
    $ cat < asd
    ```

- There is no point redirect file to `stdout`

    ``` shell
    $ cat stdout < asd
    ```

- There is no point redirect file to tty

    ``` shell
    $ cat asd > $(tty)
    ```

## Examples

- Example file created with random character.

    ``` shell
    $ cat > asd
    sdfsdfgoşsadlkf
    sadasd

    sdfgasdfkjsdkmgfğpwertü



    wert


    asdfafs          asdasdf                    asdf
    qwe
    ```

- More than one empty lines squeezed `-s`.

    ``` shell
    $ cat -s asd
    sdfsdfgoşsadlkf
    sadasd

    sdfgasdfkjsdkmgfğpwertü

    wert

    asdfafs          asdasdf                    asdf
    qwe
    ```

- Unicode notation disabled with `-v`.

    ``` shell
    $ cat -v asd
    sdfsdfgoM-EM-^_sadlkf
    sadasd

    sdfgasdfkjsdkmgfM-DM-^_pwertM-CM-<



    wert


    asdfafs          asdasdf                    asdf
    qwe
    ```

- The number of lines add with `-n` and the previous information was merged.

    ``` shell
    $ cat -vn asd
        1  sdfsdfgoM-EM-^_sadlkf
        2  sadasd
        3
        4  sdfgasdfkjsdkmgfM-DM-^_pwertM-CM-<
        5
        6
        7
        8  wert
        9
        10
        11  asdfafs          asdasdf                    asdf
        12  qwe
    ```

- `-s`. Output is more intelligible.

    ``` shell
    $ cat -vns asd
        1  sdfsdfgoM-EM-^_sadlkf
        2  sadasd
        3
        4  sdfgasdfkjsdkmgfM-DM-^_pwertM-CM-<
        5
        6  wert
        7
        8  asdfafs          asdasdf                    asdf
        9  qwe
    ```

[^1]: <https://www.man7.org/linux/man-pages/man1/cat.1.html>