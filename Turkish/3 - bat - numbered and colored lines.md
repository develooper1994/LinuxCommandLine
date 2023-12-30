[VIDEO](https://youtu.be/wyaG3rkw_EE)


[nl](https://www.youtube.com/watch?v=BIRgKVqjzqg)


# [3 - `bat` - satır numaralı ve söz dizimine göre renklendirmiş yazdırma](https://youtu.be/wyaG3rkw_EE)

`bat` aslında [`cat`](#1-cat-concatenate.md)'in diğer bir hali özelleştirilmiş bir halidir. `bat` standart bir komut değildir ve paket yöneticinize bağlı olarak muhtemelen bunu internetten `sudo apt install bat` ile yüklemeniz gerekebilir.

Öncelikle bunu söyleyeyim `bat` komutu daha çok bir kodları söz dizilimine göre renkli yazdırmak için kullanılıyor. `lolcat` ile benzerdir fakat `bat` söz dizilimine dikkat eder. `less` komutuna benzer fakat `less` varsayılan olarak renkli gösterim yapmaz. `more` ise sayfa sayfa gösterim sağlar. `bat` komutu renklendirilmiş `less` komutu olarak tarif edebilirim.

> Elimde bir tane script var şimdi `bat` ile yazdırayım. Çıkış yapmak üzere `q` tuşuna basın.

``` shell
$bat -n cpu_usage_total.sh
-----------------------
1 | #!/bin/sh
-----------------------
...
```

> Not: `bat` renkli gösterimi oldukça zor. Videoyu izlemenizi tavsiye ederim.

> Not: `cat` de bir şekilde hani renkli şek yazdırmak mümkündür fakat her dil için ayrı söz dilim kuralı belirlemek gerekir. (Renklendime kuralları üzerinde uzun uzun durmaycağım fakat örnek olması açıından `$LSCOLORS` özel değişkenine bakabilirsiniz.)

Komutunun en pratik kullanımı bir şekilde elinizde bir proje var, ideyi açmak uzun sürdüğünü varsayıyorum. Sadece ufak bir kod parçasının incelemesi gerekmektedir. `cat` ile baksanız ide benzeri bir deneyim elde edemeyeceksiniz. İşte `bat` böyle durumlarda kullanışlıdır.

`bat` ile ilgili kullanışlı birkaç seçenek vardır.
- `-L` ile söz diziminin renklendirmesi hazır olan yazılım dillerinin listesini verir.
- `-A` ile aslında ekranda görünmeyen karakterleri de görünür hale getirebilirsiniz.
- Ayrıca `cat` komutundaki bazı seçeneklerde farklı harflerle ifade ediliyor.
