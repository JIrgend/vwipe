# vwipe
![GitHub CI badge](https://github.com/martijnvanbrummelen/vwipe/workflows/ci_ubuntu_latest/badge.svg)
![GitHub CI badge](https://github.com/martijnvanbrummelen/vwipe/workflows/ci_ubuntu_16.04/badge.svg)

vwipe is a program that will securely erase disks. It can operate as both a command line
tool without a GUI or with an ncurses GUI as shown in the example below. It can wipe multiple
disks simultaneously.

This is a fork of nwipe, having the goal to use vector optimized PRNG implementations, to improve speed.

The user can select from a variety of recognised secure erase methods which include:

* Zero Fill          - Fills the device with zeros, one round only.
* RCMP TSSIT OPS-II  - Royal Candian Mounted Police Technical Security Standard, OPS-II
* DoD Short          - The American Department of Defense 5220.22-M short 3 pass wipe (passes 1, 2 & 7).
* DoD 5220.22M       - The American Department of Defense 5220.22-M full 7 pass wipe.
* Gutmann Wipe       - Peter Gutmann's method (Secure Deletion of Data from Magnetic and Solid-State Memory).
* PRNG Stream        - Fills the device with a stream from the PRNG.
* Verify only        - This method only reads the device and checks that it is all zero.
* HMG IS5 enhanced   - Secure Sanitisation of Protectively Marked Information or Sensitive Information

It also includes the following pseudo random number generators:
* Mersenne Twister
* ISAAC

It is a fork of the dwipe command used by
Darik's Boot and Nuke (dban).  vwipe is included with [partedmagic](https://partedmagic.com) and
[ShredOS](https://github.com/nadenislamarre/shredos) if you want a quick and easy bootable CD or USB version.

vwipe was created out of a need to run the DBAN dwipe command outside
of DBAN, in order to allow its use with any host distribution, thus
giving better hardware support.

![Example wipe](/images/example_wipe.gif)

## Compiling & Installing

`vwipe` requires the following libraries to be installed:

* ncurses
* pthreads
* parted

### Debian & Ubuntu prerequisites

If you are compiling `vwipe` from source, the following libraries will need to be installed first:

```bash
sudo apt install \
  build-essential \
  pkg-config \
  automake \
  libncurses5-dev \
  autotools-dev \
  libparted-dev \
  dmidecode
```

### Fedora prerequisites

```bash
sudo bash
dnf update
dnf groupinstall "Development Tools"
dnf groupinstall "C Development Tools and Libraries"
yum install ncurses-devel
yum install parted-devel
yum install dmidecode
```
Note. dmidecode is optional, it provides SMBIOS/DMI host data to stdout or the log file.

### Compilation

For a development setup, see [the hacking section below](#Hacking).

First create all the autoconf files:
```
./init.sh
```

Then compile & install using the following standard commands:
```
./configure
make
make install
```

Then run vwipe !
```
cd src
sudo ./vwipe
```
or
```
sudo vwipe
```

### Hacking

If you wish to submit pull requests to this code we would prefer you enable all warnings when compiling.
This can be done using the following compile commands:

```
./configure --prefix=/usr CFLAGS='-O0 -g -Wall -Wextra'
make
make install
```

The `-O0 -g` flags disable optimisations. This is required if you're debugging with
`gdb` in an IDE such as Kdevelop. With these optimisations enabled you won't be
able to see the values of many variables in vwipe, not to mention the IDE won't step
through the code properly.

The `-Wall` and `-Wextra` flags enable all compiler warnings. Please submit code with zero warnings.

Also make sure that your changes are consistent with the coding style defined in the `.clang-format` file, using:
```
make format
```
You will need `clang-format` installed to use the `format` command.


Once done with your coding then the released/patch/fixed code can be compiled,
with all the normal optimisations, using:
```
./configure --prefix=/usr && make && make install
```

## Bugs

Bugs can be reported on GitHub:
https://github.com/martijnvanbrummelen/vwipe

## License

GNU General Public License v2.0
