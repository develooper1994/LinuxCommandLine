[VIDEO](https://youtu.be/jTseiHef8k8)

# [5 - `pr`](https://youtu.be/jTseiHef8k8)
[`cat`](#1-cat-concatenate.md)'in diğer bir versiyonudur. Hatta `cat` komutundan eskidir. Varsayılan olarak **sayfalandırma(pagination)** işlemi yapar.

- `cat` gibi kullamak üzere başlığı ve sayfalandırmayı devre dışı bırakmak yeterlidir.

    `$pr -tT file`
- Satır sayısı ile görüntülemek için `-n` seçeneğini ekleyin.

    `$pr -tTn file`
- Satır sayısının kaçtan başlamasını istiyorsanız `-N <sayı>`

    `$pr -tTn -N 500 file`
- Biraz sağa kaydırmak için `-o <karakter>`

    `$pr -tTn -o 20 file`
- Aşağıda terminalde iki diziyi karşılaştırmak üzere bir örnek bulunmaktadır.
  - `ls` komutunda `-1v` seçeneğiyle sonucu tek satırda değilde birden fazla satırda yazdırmaktadır.
  - `pr` komutunun `-m` seçeneğiyle `birleştirme(merge)` işlemi yapılmaktadır.

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