# Dosya Yolunu Elde Etmek

## Senaryo

Bir cihazda sdcard veya usb ile otomatik bir işlem başlatmak istiyorsunuz.
Başlatılan işlem büyük ihtimal udev yöneticisi kullarına göre boş olan dizine mount edilecektir.

Başlatılan dizin hangi dizine mount ettiğini bularak işlem yapmanız gerekiyor.
Aslında yapılması gereken diğer programlama dillerindeki string split işlemidir
fakat bash script ile yapılması gerekiyorsa birkaç komut vardır.

## Araştırma

> Konu ile ilgili bulduğum komutlar şunlardır:

### `dirname`[^1]

Amacı dosyanın veya dizinin içinde bulunduğu dizini vermektir.
Yaptığı işlem ise dosya ismini '/' ayracıyla birlikte siler.

- `dirname -z` seçeneğiyle birlikte kullanılırsa stdout dosyasına
yeni satır karakteri göndermez.

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

### `basename`

Amacı dirname ile benzerdir. Burada dosya yolunu almak yerine dosya ismini alır. 
Yaptığı işlem ise dosya yolunu '/' ayracıyla birlikte siler.

- `basename -z` seçeneğiyle birlikte kullanılırsa stdout dosyasına
yeni satır karakteri göndermez.
- `basename -a` ile birden fazla string işlenip birden fazla çıktı elde edilebilir.

    ``` shell
    basename -a yok/boyle bir/sey
    # boyle
    # sey
    ```
- `basename -s <ayraç> <string>` dizinle birlikte dosya eklentisini silmek üzere kullanılabilir. Belki bu sayede

    ``` shell
    basename -s .pyc $sysroot/python/site/numpy.pyc
    # curl
    ```

Script yazarken $0 kendi adını verir. Fakat dosya tam dosya adıyla 
çalıştırıldığında sadece dosya adı yerine dosya yoluyla birlikte çıktı üretir.

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

### `readlink`

Temel işlevi dosya yolu çözümleme işlemini yapmaktır.

1. Dosyanın veya dizinin **sembolink** bağlantıyı takip eder ve dosya yolu çözümlemesi yapar.
2. Dosyanın veya dizinin **kanonik(kurallara uygun)** adını verir ve dosya yolu çözümlemesi yapar.
- `readlink -z` seçeneğiyle birlikte kullanılırsa stdout dosyasına
yeni satır karakteri göndermez.

```shell
readlink -f file
readlink -f $PWD/file
```

### `realpath`

## Çözüm

dirname $(readlink -f file)

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
[^2]:
[^3]:
[^4]:
[^5]:
[^6]:
[^7]:
[^8]:
[^9]:
