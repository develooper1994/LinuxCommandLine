[VIDEO](https://youtu.be/jTseiHef8k8)

# [5 - `pr`](https://youtu.be/jTseiHef8k8)

It is a different version of [`cat`](#1-cat-concatenate.md). It is even older then `cat`. By default it performs **pagination**.

- It is enough to remove title and disable pagination To use like `cat`.

    `$pr -tT file`
- Add `-n` option to display by number of lines.

    `$pr -tTn file`
- If you want to number of rows to start from `-N <number>`

    `$pr -tTn -N 500 file`
- Align to right a little bit with `-o <karakter>`

    `$pr -tTn -o 20 file`
- Below is an example to compare two strings the terminal.
  - Output can be printed in multiple rows instead of one row with `-1v` option of the `ls` command.
  - `Merge` operation is performed with `-m` option of the `pr` command.

    `$pr -mt <(ls -1v a1) <(ls -1v a2)`
    ```shell
    file1.txt                           file1.txt
    file2.txt                           file2.txt
    file3.txt                           file3.txt
    file4.txt                           file4.txt
    file5.txt                           file5.txt
    file6.txt                           file6.txt
    file7.txt                           file7.txt
    file8.txt                           file8.txt
    file9.txt                           file9.txt
    file10.txt                          file10.txt
                                        file11.txt
    ```