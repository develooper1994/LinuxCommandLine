[VIDEO](https://youtu.be/2A2IgaO--FM)

# [4 - `head`-`tail`](https://youtu.be/2A2IgaO--FM)

`head`ve `tail` [`cat`](#1-cat-concatenate.md)'in özelleştirilmiş bir halidir. Pratikte her zaman bir dosyanın bir kısmını görmeye ihtiyaç olur. Sadece başını görüntülemek üzere `head`, sonunu görüntülemek üzere `tail` komutları bulunur. Örnek vermek açısından sistem loglarını görüntüleyin. `/var/log/syslog` dosyasını `cat` ile ekrana yazdırırsanız çok uzun bir görüntü elde edeceksiniz. Sadece başındaki satırı göntülemek üzere imleci en tepeye kadar çıkartmak gerekir. Bunu yerine `head` ile sadece başındaki 10 satır, `tail` ile sadece son 10 satır görüntülenebilir.

- `n` seçeneğiyle kaç satır yazdırılacağı belirlenebilir.

    `$head -n 5 file`
- `-c`seçeneğiyle kaç karakter yazdırılacağı belirlenebilir. 

    `$head -c 5 file`
- `-v` seçeneği olmasada dosya isimlerini birbirlerinden ayırmak üzere dosya içeriğinden önce bir başlık yazdıracaktır.

    `$head cpu_usage_total.sh foo.c`
    `$head -v cpu_usage_total.sh foo.c`
    ```shell 
    ==> cpu_usage_total.sh <==
    #!/bin/bash
    PID=$1
    if [ -z "$PID" ]; then
            echo Usage: $0 PID
            exit 1
    fi

    LOG_FILE="$2"

    # İlk değer atamaları

    ==> foo.c <==
    int main(){}
    ```

- `-q` ile başlık dosyalarının yazdırılması engellenir.

    `$head -q cpu_usage_total.sh foo.c`
    ```shell 
    #!/bin/bash
    PID=$1
    if [ -z "$PID" ]; then
            echo Usage: $0 PID
            exit 1
    fi

    LOG_FILE="$2"

    # İlk değer atamaları
    int main(){}
    ```

- Aynı seçenekler `tail` komutu için de geçerlidir.

  - `$tail -n 5 file`
  - `$tail -c 5 file`
  - `$tail cpu_usage_total.sh foo.c`
  - `$tail -v cpu_usage_total.sh foo.c`
  - `$tail -q cpu_usage_total.sh foo.c`

## Dosya Güncellemelerini Yazdırma

Dosya güncellemelerini yazdırmak için `tail` komutu için özel bir `-f` kullanılabilir. Pratikte `/sys/var/syslog` ve `/proc/$(pidof app)/fd/stdout` dosyalarının takip ederken kullanmaktayım.
