[VIDEO](https://youtu.be/dC6JloOWy1o)

# [Linux'ta Concatenate Komutu ve Kullanımı](https://youtu.be/dC6JloOWy1o)

[`Cat`]([^1]), aslında "concatenate" kelimesinin kısaltılmış halidir ve birçok farklı işlevi bulunmaktadır. Bu komut, sadece metin dosyalarını değil, aynı zamanda bazı medya türlerini de ardışık olarak birleştirebilir.

Genel olarak, [`cat`]([^1]) komutu, dosyaları birleştirme, içeriklerini gösterme ve farklı seçeneklerle kullanma esnekliği sağlar. Bu, Linux kullanıcıları için oldukça yararlı bir araçtır.

## Dosyaları Birleştirmek

En yaygın kullanımı dosya içeriklerini ekrana yazdırmaktır. Ancak, benim için en önemli kullanımı, dosyaları birleştirmektir. Örneğin, metin dosyalarını ardışık olarak birleştirebilir ve tek bir dosya gibi gösterebilirsiniz.

- Örnek olarak, 1'den 3'e kadar olan dosyaları oluşturdum.

    ``` shell
    $ echo 1 > 1.txt
    $ echo 2 > 2.txt
    $ echo 3 > 3.txt
    ```

- ardından dosyaları tek tek yazdırdım.

    ``` shell
    $ cat 1.txt
    1

    $ cat 2.txt
    2

    $ cat 3.txt
    3
    ```

- sonrasında tek seferde yazdırdım. Fakat hangi çıktı hangi dosya isminde bilinmiyor.

    ``` shell
    $ cat {1..3}.txt
    1
    2
    3
    ```

- {1..3}.txt dosyalarını ardışık olarak birleştirdim ve yine tek dosya olarak görüntüleyebildim.

    ``` shell
    $ cat 1.txt 2.txt 3.txt > 123.txt
    $ cat 123.txt
    1
    2
    3
    ```

# Dosya Yönlendirmesi

Bir başka kullanım senaryosu ise dosya yönlendirmesi yapmak istediğinizde ortaya çıkar. 
[`Cat`]([^1]) stdout çıktısı verir ve bu çıktıyı da bir dosyaya yönlendirebilirsiniz.

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

## [`Cat`]([^1]) Seçenekleri

> [`Cat`]([^1]) komutu, dosyaları birleştirmenin yanı sıra farklı seçeneklerle de kullanılabilir.

Örnek dosyayı oluşturdum.

``` bash
seq 5 > asd
```

- `-n` ve `-b` seçenekleri dosyanın satır numaralarını gösterirken

    ``` shell
    $ cat -b asd
        1  1
        2  2
        3  3
        4  4
        5  5
    ```

- `-e` anahtarı satır sonu karakterlerini gösterir.(`-vE`)

    ``` shell
    $ cat -e asd
    1$
    2$
    3$
    4$
    5$
    ```

- Ayrıca, `-E` seçeneği dosyanın sonundaki satır sonu karakterini gösterirken,
- `-T` seçeneği görüntülenen satırlarda tab karakterlerini belirtir.

## Gereksiz kullanımı

- [`Cat`]([^1]) zaten dosya ismi verilmez ise zaten `stdout` gönderir. 

    ``` shell
    $ cat asd
    ```

- Dosyayı bir daha işleme yönlendirmeye gerek yok.

    ``` shell
    $ cat < asd
    ```

- Dosyayı bir daha `stdout` yönlendirmeye gerek yok.

    ``` shell
    $ cat stdout < asd
    ```

- Dosyayı bir daha üzerinde çalıştın tty yönlendirmeye gerek yok.

    ``` shell
    $ cat asd > $(tty)
    ```

## Örnekler

- Örnek dosya rastgele karakterlerle oluşturuldu.

    ``` shell
    $ cat > asd
    sdfsdfgoşsadlkf
    sadasd

    sdfgasdfkjsdkmgfğpwertü



    wert


    asdfafs          asdasdf                    asdf
    qwe
    ```

- `-s` squzee ile fazladan boşluklar sıkıştırıldı.

    ``` shell
    $ cat -s asd
    sdfsdfgoşsadlkf
    sadasd

    sdfgasdfkjsdkmgfğpwertü

    wert

    asdfafs          asdasdf                    asdf
    qwe
    ```

- `-v` ile unicode gösterim devre dışı bırakıldı.

    ``` shell
    $ cat -v asd
    sdfsdfgoM-EM-^_sadlkf
    sadasd

    sdfgasdfkjsdkmgfM-DM-^_pwertM-CM-<



    wert


    asdfafs          asdasdf                    asdf
    qwe
    ```

- `-n` ile satır sayısı eklendi ve önceki bilgiler birleştirildi.

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

- `-s` satır sayısı olduğunda daha anlaşılır oluyor.

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
