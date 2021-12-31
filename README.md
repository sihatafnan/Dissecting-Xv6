# Dissecting-Xv6
### Installation in Debian System
Clone the official Xv6 repository from [here](https://github.com/mit-pdos/xv6-public).We need an emulator to boot Xv6.We will use qemu for this purpose.To install qemu, run from your terminal ```sudo apt install qemu```.Then from where Xv6 was cloned , run `make` to compile Xv6.Then to launch the emulator , run `make qemu` and you will see qemu in a different window.If qemu doesn't launch , then run `sudo apt install qemu-system-x86` and then run `make qemu` again.This time , it should work.
Still, you might face problems like [this](https://stackoverflow.com/questions/70515788/booting-xv6-with-qemu) [here](https://www.reddit.com/r/ManjaroLinux/comments/p4445x/help_xv6_installation_on_manjaro/) is a way around.

To run qemu in the same terminal you're using , run `make qemu-nox` instead of `make qemu`.

### Adding New System Call

