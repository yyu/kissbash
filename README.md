# kissbash - A Simple and Stupid Bash Script Library

Despite [what people say](https://stackoverflow.com/a/11369935), I decide to write a bash script library.

If nobody cares, at least it will benefit myself.

# How to use

Set the `KISSBASH_PATH` environment variable and you are good to go. For example,

```bash
$ git clone https://github.com/yyu/kissbash.git
$ export KISSBASH_PATH=`pwd`/kissbash/s
$ cat > /tmp/myscript << "EOF"
. "$KISSBASH_PATH/console/lines"
echos 3; echo line1
echo line2 | line_pre_echo_control up1 up1 up1
echo line3
echos 10
cat /tmp/myscript | line_pre_echo_control up1 up1
echos 7
EOF
```

output:

    $ bash4 /tmp/myscript

    line2
    line3
    line1

    echos 7
    cat /tmp/myscript | line_pre_echo_control up1 up1
    echos 10
    echo line3
    echo line2 | line_pre_echo_control up1 up1 up1
    echos 3; echo line1
    . "$KISSBASH_PATH/console/lines"

    $

