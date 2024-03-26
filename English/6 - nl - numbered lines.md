[VIDEO](https://youtu.be/BIRgKVqjzqg)

> alternative of `nl`, bat: https://www.youtube.com/watch?v=wyaG3rkw_EE

# [6 - `nl` - numbered lines](https://youtu.be/BIRgKVqjzqg)
Specialized version of [`cat`](#1-cat-concatenate.md) with line numbers. The most important different between two command is `cat -n` increases line numbers but `nl` doesn't for empty lines.

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

- To increase for empty lines.

    `$nl -ba cpu_usage_total.sh`
- `-n --number-format=FORMAT`
  - FORMAT='rn' means don't fill the lines numbers with zeros and align lines numbers to right.
  
    `$nl -n'rn' cpu_usage_total.sh`
  - FORMAT='rz' means fill the lines numbers with zeros and align lines numbers to right.
  
    `$nl -n'rz' cpu_usage_total.sh`
  - FORMAT='ln' means don't fill the lines numbers with zeros and align lines numbers to right.

    `$nl -n'ln' cpu_usage_total.sh`

- Default options of `nl`: `-bt -d'\:' -fn -hn -i1 -l1 -n'rn' -s<TAB> -v1 -w6`. It fills what characters you typed on with `-s` option.
`$nl -bt -d'\:' -fn -hn -i1 -l1 -n'rn' -v1 -w6 -s' <satır başlarına getirmek istediğiniz ifade> ' cpu_usage_total.sh`