# Dissecting-Xv6
### Installation in Debian System
Clone the official Xv6 repository from [here](https://github.com/mit-pdos/xv6-public).We need an emulator to boot Xv6.We will use qemu for this purpose.To install qemu, run from your terminal ```sudo apt install qemu```.Then from where Xv6 was cloned , run `make` to compile Xv6.Then to launch the emulator , run `make qemu` and you will see qemu in a different window.If qemu doesn't launch , then run `sudo apt install qemu-system-x86` and then run `make qemu` again.This time , it should work.
Still, you might face problems like [this](https://stackoverflow.com/questions/70515788/booting-xv6-with-qemu) then [here](https://www.reddit.com/r/ManjaroLinux/comments/p4445x/help_xv6_installation_on_manjaro/) is a way around.

To run qemu in the same terminal you're using , run `make qemu-nox` instead of `make qemu`.

### Modifying Source Codes
After qemu is being launched , you will see following system calls by running `ls`
![](images/1.png)

We can modify the source code and see the effects instantly.Lets say we want to replace the `$` sign with something else.To do this , go to `sh.c` file and change inside `getcmd` method.

```printf(2, ANSI_COLOR_GREEN "afnan@Xv6:$ " ANSI_COLOR_RESET);```

Add two lines at the top of this file
```
#define ANSI_COLOR_GREEN   "\x1b[32m"
#define ANSI_COLOR_RESET   "\x1b[0m"
```

Now quit from the qemu terminal pressing `cntrl+A` , release and then type x immediately(as you can see it's a tedious task and we will create a system call to exit from the terminal).Then run `make qemu-nox` again and see the result now
![](images/2.png)

#### Adding a System call
Let's create a system call to exit from the qemu terminal.We name it as `shutdown`.So we want to do something that would enable us to exit from the terminal by just writing the command `shutdown`.

First create a file named `shutdown.c`.Then in Makefile , add it in the UPROGS
```
UPROGS=\
	_cat\
	_echo\
	_forktest\
	_grep\
	_init\
	_kill\
	_ln\
	_ls\
	_mkdir\
	_rm\
	_sh\
	_stressfs\
	_usertests\
	_wc\
	_zombie\
  _shutdown\
```
Add it also in EXTRA
```
EXTRA=\
	mkfs.c ulib.c user.h cat.c echo.c forktest.c grep.c kill.c\
	ln.c ls.c mkdir.c rm.c stressfs.c usertests.c wc.c zombie.c shutdown.c\
```
Now you can exit from the qemu terminal and run `make qemu-nox` again and see that `ls` will list `shutdown` as a system call.But running this command won't do anything for now.We've to add this system call to 4 following files

* sycall.c
* syscall.h
* usys.S
* user.h






