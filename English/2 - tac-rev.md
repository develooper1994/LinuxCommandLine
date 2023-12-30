[VIDEO](https://youtu.be/HfkMWo9ogh0)

# [`Tac` ve `Rev`](https://youtu.be/HfkMWo9ogh0)

I am going to show a new command show thing one screen. There are lots of commands to do that. New command will explained in the following sections.

## [`Tac`][^tac]

Number is a text file consist of 3 rows and 3 columns.

``` shell
$ seq 9 | xargs -n 3
$ cat numbers 
1 2 3
4 5 6
7 8 9
```

[`tac`][^tac] prints bottom to top.

``` shell
$ tac numbers
7 8 9
4 5 6
1 2 3
```

- Split operation can be performed with `-s` option.

``` shell
$ tac -s :
q:w:e
<Ctrl+D>
e
w:q:
```

> Note: I hope you get the joke between [`cat`][^cat] and [`tac`][^tac].

## [`Rev`][^rev]

There is one more command. [`Rev`][^rev] prints rights to left in this time.There is no option to change runtime behavior.

``` shell
$ rev numbers
3 2 1
6 5 4
9 8 7
```


### [`Cat`][^cat] vs [`Tac`][^tac] vs [`Rev`][^rev]

Let's say I am trying to remake [`cat`][^cat], [`tac`][^tac], [`rev`][^rev], ... like programs.

- [`Cat`][^cat] like programs does not need a buffer to print thing in order. Prints as it is.

    ``` shell
    $ cat
    qwe
    qwe
    asd
    asd
    ```

However, processing with a buffer memory is required if you need to print out of order. The software must keep the data in memory, understand that the transaction is finished and process the data. The user notifies the program that the input is finished with '**Ctrl+D**' and the software closes. It can process the input at closing stage.

- Since [`tac`][^tac] output from bottom to top, it must use buffer memory and process the input when '**Ctrl+D**' occurs.

    ``` shell
    $ tac
    qwe
    asd
    asd
    qwe
    ```

- Since [`rev`][^rev] only outputs right to left, it has to wait for the output.

    ``` shell
    $ rev
    qwe
    ewq
    asd
    dsa
    ```

[^cat]: <https://www.man7.org/linux/man-pages/man1/cat.1.html>
[^tac]: <https://man7.org/linux/man-pages/man1/tac.1.html>
[^rev]: <https://man7.org/linux/man-pages/man1/rev.1.html>
