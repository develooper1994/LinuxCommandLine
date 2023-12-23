[VIDEO](https://youtu.be/HfkMWo9ogh0)

# [`Tac` ve `Rev`](https://youtu.be/HfkMWo9ogh0)

Yeni bir komut daha göstereceğim. Bu komutla beraber artık ekrana bir şeyler yazdırmaya odaklanacağım. Aslında Unix/Linux ekosisteminde bir sürü komut vardır. Daha sonra diğer komutları da göstereceğim.

## [`Tac`][^tac]

Numbers 3 satır ve 3 sütundan oluşan bir text dosyasıdır.

``` shell
$ seq 9 | xargs -n 3
$ cat numbers 
1 2 3
4 5 6
7 8 9
```

[`tac`][^tac] aşağıya doğru ters yazdırır.

``` shell
$ tac numbers
7 8 9
4 5 6
1 2 3
```

- `-s` seçeneğiyle split işlemi de gerçekleştirilebilir.

``` shell
$ tac -s :
q:w:e
<Ctrl+D>
e
w:q:
```

> Not: [`cat`][^cat] ve [`tac`][^tac] arasındaki espriyi anlamışsınızdır.

## [`Rev`][^rev]

[`Rev`][^rev] de bu sefer sağdan sola ters yazdırır. Çalışmasını değiştirecek bir seçeneği yoktur.

``` shell
$ rev numbers
3 2 1
6 5 4
9 8 7
```

### [`Cat`][^cat] vs [`Tac`][^tac] vs [`Rev`][^rev]

Diyelimki [`cat`][^cat], [`tac`][^tac], [`rev`][^rev], ... gibi programları kendim yazmaya çalışıyorum. 
- [`Cat`][^cat] gibi veriyi sıralı yazdırmak için program içinde buffer tutmama gerek kalmaz. Çıktıyı hemen yansıtır.

    ``` shell
    $ cat
    qwe
    qwe
    asd
    asd
    ```

Fakat bir veriyi bir şekilde sırasının dışında yazdırmak istersem bir buffer ile işlem yapmam gerekir. Program veriyi tutmalı, işlemin bittiğini anlamalı ve veriyi işlemelidir. Kullanıcı girdi işleminin bittiğini '**Ctrl+D**' ile programa iletir ve program kapanır. Kapanırken de veriyi işleyebilir.

- [`tac`][^tac] çıktıyı aşağıdan yukarıya doğru yazdırdığından buffer kullanıp '**Ctrl+D**' girdiyi gerçekleştiğinde işlemelidir.

    ``` shell
    $ tac
    qwe
    asd
    asd
    qwe
    ```

- [`rev`][^rev] sadece sağdan sola ters yazdırdığından çıktıyı bekletmek zorunda değildir.

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
