[VIDEO](https://youtu.be/wyaG3rkw_EE)


[nl]: (https://www.youtube.com/watch?v=BIRgKVqjzqg)


# [3 - `bat` - numbered and colored lines with syntax highlight](https://youtu.be/wyaG3rkw_EE)

`bat` is actually a colored representing of [`cat`](#1-cat-concatenate.md). `bat` is not a standard command and depending on your package manger you may need to install it from internet with `sudo apt install bat`.

First of all, let me say that the `bat` command is mostly used to print codes in color in according to syntax. it reminds `lolcat` but pays attention to syntax. Also similar to `less` but `less` doesn't colorize the code. `more` provides page by page display. I can describe `bat` command as a colorized version of `less`.

> I have a script in my hand to print with `bat`. Press `q` button to quit.

``` shell
$bat -n cpu_usage_total.sh
-----------------------
1 | #!/bin/sh
-----------------------
...
```

> Note: Colorized text in the editor is hard to show. I recommend go and watch the video.

> Note: Colorized code with `cat` is possible but syntax colorization rules have to define for all languages. (I am not going to emphasize on colorization rules but if you are curious search for `$LSCOLORS` special variable.)

The most practical usage is you are working on a project and you just want to observe a small part of code without waiting to opening IDE. You can't get similar experience like ide with `cat` command. `bat` is handy in these types of situations.

useful `bat` options:
- `-L` gives list of available programing languages for syntax colorization.
- `-A` prints non printable characters.
- Additionally, some options in `cat` command are expressed with different letters.