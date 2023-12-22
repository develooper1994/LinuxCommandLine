[VIDEO](https://youtu.be/dC6JloOWy1o)

# [Linux'ta Concatenate Komutu ve Kullanımı](https://youtu.be/dC6JloOWy1o)

"Cat", aslında "concatenate" kelimesinin kısaltılmış halidir ve birçok farklı işlevi bulunmaktadır. Bu komut, sadece metin dosyalarını değil, aynı zamanda bazı medya türlerini de ardışık olarak birleştirebilir.

En yaygın kullanımı dosya içeriklerini ekrana yazdırmaktır. Ancak, benim için en önemli kullanımı, dosya türlerini birleştirmektir. Örneğin, metin dosyalarını ardışık olarak birleştirebilir ve tek bir dosya gibi gösterebilirsiniz.

Örnek olarak, 1'den 3'e kadar olan dosyaları oluşturdum.

``` shell
$ echo 1 > 1.txt
$ echo 2 > 2.txt
$ echo 3 > 3.txt
```

- tek tek

    ``` shell
    $ cat 1.txt
    1

    $ cat 2.txt
    2

    $ cat 3.txt
    3
    ```
- tek seferde. Fakat hangi çıktı hangi dosya isminde bilinmiyor.

    ``` shell
    $ cat {1..3}.txt
    1
    2
    3
    ```

Bunları ardışık olarak birleştirdim. Bu şekilde, dosyaları alt alta görüntüleyebiliyoruz.

``` shell
$ cat 1.txt 2.txt 3.txt > 123.txt
$ cat 123.txt
1
2
3
```

Bir başka kullanım senaryosu ise dosyalara eklemeler yapmak istediğinizde ortaya çıkar. Örneğin, bir dosyaya eklemeler yaparken sadece sonuncusu görünüyorsa, bunu ">>(büyüktür işareti)" kullanarak çözebilirsiniz. Örneğin:

``` shell
$ echo "Arda" >> günlük
$ echo "Fakat sadece günlük kalmış" >> günlük
$ cat günlük
Arda
Fakat sadece günlük kalmış
```

> Cat komutu, dosyaları birleştirmenin yanı sıra farklı switch'leri de destekler. 

Örnek dosyayı oluşturdum.

``` bash
seq 5 > asd
```

- "-n" ve "-b" switchlari dosyanın satır numaralarını gösterirken

    ``` shell
    $ cat -b asd
        1  1
        2  2
        3  3
        4  4
        5  5
    ```

- "-e" switch'i satır sonu karakterlerini gösterir.(-vE)

    ``` shell
    $ cat -e asd
    1$
    2$
    3$
    4$
    5$
    ```

- Ayrıca, "-E" seçeneği dosyanın sonundaki satır sonu karakterini gösterirken,
- "-T" seçeneği görüntülenen satırlarda tab karakterlerini belirtir.

Cat komutu aynı zamanda büyük dosyalar oluşturmak için de kullanılabilir. Örneğin:

``` shell
$ echo "asd" > büyük_dosya
```

Bu komut, "asd" kelimesini içeren büyük bir dosya oluşturur. Ardından, dosya içerisindeki satır sonu karakterleri veya diğer switch'leri test edebilirsiniz.

Genel olarak, "cat" komutu, dosyaları birleştirme, içeriklerini gösterme ve farklı seçeneklerle kullanma esnekliği sağlar. Bu, Linux kullanıcıları için oldukça yararlı bir araçtır.

Cat komutu ile ilgili temel kullanımları ve bazı yaygın switch'leri gördük. Bu komut, dosya içeriklerini birleştirmek ve ekrana yazdırmak için kullanılabilir.

## Gereksiz kullanımı

cat zaten dosya ismi verilmez ise zaten stdout gönderir. Dosyayı bir daha işleme yönlendirmeye gerek yok.

``` shell
$ cat asd
```

``` shell
$ cat < asd
```

``` shell
$ cat stdout < asd
```

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