[VIDEO](https://youtu.be/Cz_isoQFWL4)
# [Dosya Yolunu Elde Etmek](https://youtu.be/Cz_isoQFWL4)

Linux işletim sisteminde bir dosya yolu çözme algoritması bulunmaktadır. 

- '.' ve '~+' varsa önceki($PWD) dizinini
- '..' bir üst dizini
- '/' root dizinini
- '~' home dizinini
- '~-' ve '-' varsa önceki($OLDPWD) dizinini

belirtmektedir.

İşte bu ifadeler yanyana geldiğinde uzun satırlar oluşturabilmektedir. 
Dosya yolu çözümlendiğinde ifade basitleşmektedir.
Basitleşen dosya yolu ile işlem yapmak kolaylaşmaktadır.

## Senaryo

Bir cihazda sdcard veya usb ile otomatik bir işlem başlatmak istiyorsunuz.
Başlatılan işlem büyük ihtimalle udev yöneticisi kurallarına göre boş olan dizine mount edilecektir.

Başlatılan işlemin hangi dizinden çalıştığı bulunarak işlem yapılması gerekiyor.
Aslında yapılması gereken, diğer programlama dillerindeki string split işlemidir
fakat bash script ile yapılması gerekiyorsa birkaç komut vardır.

## Araştırma

> Konu ile ilgili bulduğum komutlar şunlardır:

### [`dirname`][readlink]

Amacı dosyanın veya dizinin içinde bulunduğu dizini vermektir.
Yaptığı işlem ise dosya ismini '/' ayracıyla birlikte siler.

- `-z` seçeneğiyle birlikte kullanılırsa yeni satır karakteri üretmez. `xargs -0` ile kullanılabilir. `xargs -0` ile kullanılabilir.

> Fakat burada iki sorun vardır.

    1. Tam dosya veya dizin yolu verilmez ise göreceli dosya konumu('.') verir.
    2. Son program çıktısı olarak hata kodu da vermez.
    3. Tam dosyanın veya dizinin olup olmadığını bakmadan string işlemi yapar.

``` shell
echo $PWD                                   # /home/username
dirname $PWD                                # /home
echo $?                                     # son programın çıkış kodu
dirname file                                # .
echo $?                                     # son programın çıkış kodu
dirname $PWD/file                           # /home/username
echo $?                                     # son programın çıkış kodu
dirname yok/boyle/bir/dosya/veya/dizin      # yok/boyle/bir/dosya/veya
dirname /yok/boyle/bir/dosya/veya/dizin     # /yok/boyle/bir/dosya/veya
dirname yok                                 # .
echo $?                                     # son programın çıkış kodu
```

### [`basename`][basename]

Amacı [dirname](13-DosyaYolu.md#dirname) ile benzerdir. Burada dosya yolunu almak yerine dosya ismini alır.
Yaptığı işlem ise dosya yolunu '/' ayracıyla birlikte siler.

-`-z` seçeneğiyle birlikte kullanılırsa yeni satır karakteri üretmez. `xargs -0` ile kullanılabilir. `xargs -0` ile kullanılabilir.
- `basename -a` ile birden fazla string işlenip birden fazla çıktı elde edilebilir.

    ``` shell
    basename -a yok/boyle bir/sey
    # boyle
    # sey
    ```

- `basename -s <ayraç> <string>` dizinle birlikte dosya eklentisini silmek üzere kullanılabilir. Belki bu sayede;

    ``` shell
    basename -s .pyc $sysroot/python/site/numpy.pyc
    # curl
    ```

Bazı özel değişkenler vardır. `$0` onlardan biridir ve konuyla ilgili olduğundan bahsetmeden geçemem. çalışan bash scriptin adını verir. 
Fakat bir sorun var, dosya tam dosya adıyla çalıştırıldığında sadece dosya adı yerine dosya yoluyla birlikte çıktı üretir.

> Buradaki sorunlar dirname sorunlarıyla aynıdır.

``` shell
echo $PWD                                   # /home/username
basename $PWD                               # username
echo $?                                     # son programın çıkış kodu
basename file                               # file
echo $?                                     # son programın çıkış kodu
basename $PWD/file                          # /home/username
echo $?                                     # son programın çıkış kodu
basename yok/boyle/bir/dosya/veya/dizin     # dizin
basename /yok/boyle/bir/dosya/veya/dizin    # dizin
basename yok                                # yok
echo $?                                     # son programın çıkış kodu
```

### [`readlink`][readlink]

Temel işlevi dosya yolu çözümleme işlemini yapmaktır.

1. Dosyanın veya dizinin **sembolink** bağlantıyı takip eder ve dosya yolu çözümlemesi yapar.
2. Dosyanın veya dizinin **kanonik(kurallara uygun)** adını verir.

- `-z` seçeneğiyle birlikte kullanılırsa yeni satır karakteri üretmez. `xargs -0` ile kullanılabilir. `xargs -0` ile kullanılabilir.

```shell
readlink -f file
readlink -f $PWD/file
```

### [`realpath`][realpath]

Temel [readlink](13-DosyaYolu.md#readlink) gibi işlevi dosya yolu çözümleme işlemini yapmaktır.
`readlink` ile arasındaki en büyük fark `readlink` varsayılan olarak sadece sembolik link ise sonuç verirken `realpath` sembolik olup olmadığına bakmaksızın sonuç vermektedir.

``` shell
readlink /usr/../usr/..    #
realpath /usr/../usr/..    # /
```

1. `-z` seçeneğiyle birlikte kullanılırsa yeni satır karakteri üretmez. `xargs -0` ile kullanılabilir.
2. `-s` anahtarının davranışı diğer path çözümlemesi yapan komutlardan ayrılır.

    > "/usr/bin/X11/" "/usr/bin/" dizinini gösteren bir dizin olduğunu kabul edelim [realpath]

    ``` shell
    realpath /../usr/bin/X11/./xterm        # /usr/bin/xterm
    realpath -s /../usr/bin/X11/./xterm     # /usr/bin/X11/xterm
    ```

## Çözüm

Bu sorun için çözüm yolum var.
`dirname $(readlink -f file)` veya `dirname $(realpath file)` kullanımı dosya yolu sorununu çözecektir. 
İki seçenekten hangisinin daha iyi olduğu arasında kaldığımı söylemem gerek.

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

[readlink]: <https://linux.die.net/man/1/readlink>
[basename]: <https://linux.die.net/man/1/basename>
[readlink]: <https://man7.org/linux/man-pages/man1/readlink.1.html>
[realpath]: <https://man7.org/linux/man-pages/man3/realpath.3.html>
