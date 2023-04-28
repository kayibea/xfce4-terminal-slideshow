
# Xfce4 Terminal Slideshows

This is a simple script to change the background of xfce4-terminal to a random image from a directory in a given interval. It can be used to create slideshows in the terminal.

![Demo](demo.gif)

## Installation

1. Clone this repository
2. Set the `image_files` variable in the `xfce4-term-ss` script to the directory containing the images you want to use
3. Copy the `xfce4-term-ss` script to a directory in your `$PATH` (e.g. `/usr/local/bin` or `~/.local/bin`)
4. Make the script executable (`chmod +x xfce4-term-ss`)
5. Add the following code to your `.bashrc` or `.zshrc`:

```bash
# Run the script to change the Xfce4 Terminal background image
if [ "$(ps -o comm= $PPID)" = "xfce4-terminal" ]; then
  pid_file=/tmp/xfce4-term-ss.pid
  if ! [ -e $pid_file ] || ! ps -p $(cat $pid_file) > /dev/null 2>&1; then
    nohup xfce4-term-ss > /dev/null 2>&1 &
    echo $! > $pid_file
  fi
fi
```

## Usage

The execution is automatically started when you open a new terminal window. The script will change the background image every 60 seconds. You can change the interval in the `xfce4-term-ss` script.

The script will also automatically stop when you close the last terminal window.

**Note:** If you are having issues with the script, try to run it manually in a terminal window to see if there are any errors.

## License

This project is licensed under the MIT License

## Acknowledgments

* [xfce4-terminal](https://docs.xfce.org/apps/terminal/start) - The terminal emulator used
