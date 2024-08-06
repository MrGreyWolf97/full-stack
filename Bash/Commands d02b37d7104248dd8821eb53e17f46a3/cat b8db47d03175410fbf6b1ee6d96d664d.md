# cat

The `cat` (short for "concatenate") command in Bash is a standard Unix utility that reads files sequentially, writing them to standard output.

The name is derived from its functionality to concatenate files.

It can be used to display text files, combine files, and create new ones.

---

Here are some of the most useful options for the `cat` command:

1. `n`, `-number`: Number all output lines, starting with 1. This is useful when you want to know the line numbers.
2. `b`, `-number-nonblank`: Number non-empty output lines, overriding `n`. This will not number blank lines, which can be useful for readability.
3. `s`, `-squeeze-blank`: Squeeze multiple adjacent blank lines into a single blank line. This can be useful for condensing files with lots of empty space.
4. `E`, `-show-ends`: Display a dollar sign (`$`) at the end of each line, making it easier to see line breaks, especially for files with lines that don't end with newline characters.
5. `T`, `-show-tabs`: Display TAB characters as `^I`. This can be useful for visualizing tabs when examining files.
6. `A`, `-show-all`: Equivalent to `vET`. This will show non-printing characters (except for line breaks and tab spaces), and it will show `$` at the end of each line and `^I` for tab characters.
7. `e`: Equivalent to `vE`. It will show non-printing characters and `$` at the end of each line.
8. `v`, `-show-nonprinting`: Use `^` and `M-` notation, except for line feed (LF) and tab (TAB) characters. This displays non-printing characters so you can see if there's anything unusual in your file.To use the `cat` command, simply type `cat` followed by the file(s) you wish to view. For example:

```bash
cat file.txt

```

This command will display the contents of `file.txt` on your screen.

To combine options with the `cat` command, you can list them after a single dash or as separate flags. For example, if you want to number all lines and squeeze multiple blank lines into one, you can use:

```bash
cat -nb file.txt

```

Or you can list the options separately:

```bash
cat -n -b file.txt

```

You can also use `cat` to concatenate multiple files and display their contents in sequence:

```bash
cat file1.txt file2.txt file3.txt

```

Or redirect the output to create a new concatenated file:

```bash
cat file1.txt file2.txt file3.txt > combined.txt

```

Remember to refer to the manual page (`man cat`) on your system for the most accurate information, as there may be other options available or specific details to your operating system's implementation of the `cat` command.