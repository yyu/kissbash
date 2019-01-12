# kissbash - A [Simple and Stupid](https://en.wikipedia.org/wiki/KISS_principle) Bash Script Library

Despite [what people say](https://stackoverflow.com/a/11369935), I decide to write a bash script library.

If nobody cares, at least it will benefit myself.

# How to use

Set the `KISSBASH_PATH` environment variable and you are good to go.

```bash
$ git clone https://github.com/yyu/kissbash.git ~/.kissbash
$ export KISSBASH_PATH=~/.kissbash/kissbash
```

## Example

```bash
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

# Document

## `console/lines`

### `echos`

One argument:
```bash
$ . $KISSBASH_PATH/console/lines
$ (echos 2; echo hello) | cat -n
     1	
     2	
     3	hello
```

More than one argument:
```bash
$ . $KISSBASH_PATH/console/lines
$ (echos 3 .; echo hello) | cat -n
     1	...hello
```

### `serr_with_color`

```bash
$ . $KISSBASH_PATH/console/lines
$ echo hello | serr_with_color red
hello
```
You should see red `hello` in your console.

### `tee_serr_with_color`

```bash
$ . $KISSBASH_PATH/console/lines
$ echo hello | tee_serr_with_color red
hello
hello
$ echo hello | tee_serr_with_color red > /dev/null
hello
```
You should see red `hello` for stderr and normal `hello` for stdout.

### `line_pre_echo_control`

```bash
$ . $KISSBASH_PATH/console/lines
$ echo -e "\none\n"; echo two; echo three

one

two
three
$ echo -e "\none\n"; echo two | line_pre_echo_control up1; echo three

one
two
three
```

## `exec/explicitly`

```bash
$ . $KISSBASH_PATH/exec/explicitly
$ explicitly echo "2+3" | bc
echo 2+3
5
```

## testing

    $ t/test-all
    Running /Users/forresty/___/github/kissbash/t/bash/test-assoc-array
    PASS test_bash_version_too_low
    PASS test_bash_version_ok
    PASS test_bash_version_high

    Running /Users/forresty/___/github/kissbash/t/util/test-explicitly-exec
    PASS test_explicitly_good

    **************************************DONE**************************************

    for details,
    cat /var/folders/yd/c3kph1693ns3rtft7jwscyj5snhf_t/T/tmp.qWVmW057
    ```

Tip: `t/test-all -v` will automatically show details.
