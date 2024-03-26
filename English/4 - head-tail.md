[VIDEO](https://youtu.be/2A2IgaO--FM)

# [4 - `head`-`tail`](https://youtu.be/2A2IgaO--FM)

`head` and `tail` is altered version of [`cat`](#1-cat-concatenate.md).
Users needs to see a part of a file in practice. There are `head` to display only the beginning and `tail` to display the end. To give an example, view the system logs. You probably will get lengthy output if you print `/var/log/syslog` file with `cat`. You have scroll back to top to display only the beginning. Instead, only the first 10 lines can be displayed with `head`, and only the last 10 lines can be displayed with `tail`.

- You can specify how many lines to print with the `-n` option.

    `$head -n 5 file`
- You can specify how many files to print with the `-c` option.

    `$head -c 5 file`
- It prints title before the file content to distinguish file names from each other, even without `-v`

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
- It don't print title with `-q`. makes it `quit`.

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

- All these options are the valid for `tail` command.

  - `$tail -n 5 file`
  - `$tail -c 5 file`
  - `$tail cpu_usage_total.sh foo.c`
  - `$tail -v cpu_usage_total.sh foo.c`
  - `$tail -q cpu_usage_total.sh foo.c`

## Monitoring File Updates

A special `-f` option can be used for the `tail` command to monitor file updates. I use it when monitoring `/sys/var/syslog` and `/proc/$(pidof app)/fd/stdout` files, in practice.