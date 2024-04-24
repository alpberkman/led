# led
Line EDitor
A simple program that allows editing keyboard inputs for any program. It works in a similar manner to rlwrap.

## Build
The Makefile in the root directory will call the Makefile in the /csrc directory, which in turn will build it and put the object code and the binary in /bin directory.

## Usuage
For full usuage first call led_init() and then the led_slave(). led_slave takes the same arguments as execve. This program does the following:
1. Change the terminal to raw mode.
2. Prepare a pipe for passing the stdin.
3. Fork and exec. The child process gets it's input from led.
4. According to settings led will intercept the keyboard inputs.

Since the keyboard input is intercepted you cannot quit with Ctrl-c. Currently there are 3 control characters:
- Ctrl-q: Quit the program
- Ctrl-f: Flush the input buffer
- Ctrl-e: Send EOF to slave program. This will most probably kill the slave program, however led will keep working. Use Ctrl-q to quit it.
All other characters are passed to the slave.

## Extending
led uses a LUT to execute special functions depending on the ascii code. led_register_key() function can be used to register more functions. There are some usefull macros in /csrc/led.h. led_getkey() function can also be used in a similar manner to getchar(), however it has a timout functionality, so if it doesn't receive anything in 100 milliseconds it will return 0.

## Important
...

## Credit
Thanks to https://github.com/paigeruten / https://github.com/snaptoken for deconstructing https://github.com/antirez 's kilo text editor and explaining how to set the terminal to raw mode (https://viewsourcecode.org/snaptoken/kilo/02.enteringRawMode.html and https://viewsourcecode.org/snaptoken/kilo/03.rawInputAndOutput.html).
