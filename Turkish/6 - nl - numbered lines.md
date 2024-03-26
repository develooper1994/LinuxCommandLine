[VIDEO](https://youtu.be/BIRgKVqjzqg)

> `nl` alternatifi, bat: https://www.youtube.com/watch?v=wyaG3rkw_EE

# [6 - `nl` - numbered lines](https://youtu.be/BIRgKVqjzqg)
[`cat`](#1-cat-concatenate.md)'in daha çok satır için özelleştirilmiş versiyonudur. İki komut arasındaki en önemli fark, boş satırlar için `cat -n`  satır sayısını arttırırken `nl` varsayılan olarak satır sayısını arttırmamaktadır.

    `$cat -n cpu_usage_total.sh`
    ```shell
    1  #!/bin/bash
    2  PID=$1
    3  if [ -z "$PID" ]; then
    4          echo Usage: $0 PID
    5          exit 1
    6  fi
    7
    8  LOG_FILE="$2"
    9
    10  # İlk değer atamaları
    11  avg=0
    12  t=1
    ```

    `$nl cpu_usage_total.sh`
    ```` shell
    1  #!/bin/bash
    2  PID=$1
    3  if [ -z "$PID" ]; then
    4          echo Usage: $0 PID
    5          exit 1
    6  fi

    7  LOG_FILE="$2"

    8  # İlk değer atamaları
    9  avg=0
    10  t=1
    ```

- Boş satırlar için satır arttırmak istiyorsanız.

    `$nl -ba cpu_usage_total.sh`
- `-n --number-format=FORMAT`
  - FORMAT='rn' satır sayılarını sıfırla doldurma ve satır sayılarını sağa dayalı yazdır.

    `$nl -n'rn' cpu_usage_total.sh`
  - FORMAT='rz' satır sayılarını sıfırla doldur ve satır sayılarını sağa dayalı yazdır.

    `$nl -n'rz' cpu_usage_total.sh`
  - FORMAT='ln' satır sayılarını sıfırla doldurma ve satır sayılarını sola dayalı yazdır.

    `$nl -n'ln' cpu_usage_total.sh`

- `nl` komutunun varsayılan seçenekleri: `-bt -d'\:' -fn -hn -i1 -l1 -n'rn' -s<TAB> -v1 -w6`. `-s` seçeneğiyle birlikte ne yazarsanız satır başlarını bu karakterlerle doldurur.
`$nl -bt -d'\:' -fn -hn -i1 -l1 -n'rn' -v1 -w6 -s' <satır başlarına getirmek istediğiniz ifade> ' cpu_usage_total.sh`