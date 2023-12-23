[VIDEO](https://youtu.be/HfkMWo9ogh0)

# [`Tac` ve `Rev`](https://youtu.be/HfkMWo9ogh0)


## [`Tac`][^tac]



``` shell
$ seq 9 | xargs -n 3
$ cat numbers 
1 2 3
4 5 6
7 8 9
```

[`tac`][^tac] bottom to top.

``` shell
$ tac numbers
7 8 9
4 5 6
1 2 3
```

- `-s`

``` shell
$ tac -s :
q:w:e
<Ctrl+D>
e
w:q:
```

> Note: I hope you get the joke between [`cat`][^cat] and [`tac`][^tac].

## [`Rev`][^rev]

There is one more command. [`Rev`][^rev]

``` shell
$ rev numbers
3 2 1
6 5 4
9 8 7
```


### [`Cat`][^cat] vs [`Tac`][^tac] vs [`Rev`][^rev]



- [`Cat`][^cat]

    ``` shell
    $ cat
    qwe
    qwe
    asd
    asd
    ```

- [`tac`][^tac]

    ``` shell
    $ tac
    qwe
    asd
    asd
    qwe
    ```

- [`rev`][^rev]

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
