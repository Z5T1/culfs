                          Cucumber Linux from Scratch
                                    Week 2
                              September 23, 2018

# Configure the Cucumber Linux Virtual Machine

# Building Software from Source

## Example 1: HexChat

In this example, we will install HexChat, a popular IRC client. We will start
by building it the 'Quick and Dirty Way', where we will just focus on learning
how to compile it. Then, we will explore what each command does and learn how
to download and compile it the 'Good and Decent Way'.

### The Quick and Dirty Way

Download HexChat from http://hexchat.net:

    wget https://dl.hexchat.net/hexchat/hexchat-2.10.2.tar.xz

Extract the source tarball and cd into the directory:

    tar -xJf hexchat-2.10.2.tar.xz
    cd hexchat-2.10.2

Run the following commands:

    ./configure
    make
    sudo make install

### Explanation of Commands

    wget https://dl.hexchat.net/hexchat/hexchat-2.10.2.tar.xz

This downloads the source tar archive (if you do not know, tar archives are
like zip files for Unix). They are sometimes also referred to as "tarballs" (I
have a habit of doing this). If you go on the website for a package, it is
usually pretty easy to find the download link for the source tarball.

If you are having trouble locating the link for the source tarball, the Beyond
Linux from Scratch book contains download links for the source for many common
packages and can be quite helpful. See
http://www.linuxfromscratch.org/blfs/view/stable/.

---

    tar -xJf hexchat-2.10.2.tar.xz
    cd hexchat-2.10.2

This extracts the tarball. Here's an explanation of what each tar flag does:
* -x Extracts the tarball
* -J States that we are using a xz compressed tarball. This flag is optional
  with GNU tar, but mandatory when using BSD tar and most other tar
  implementations.
* -f hexchat-2.10.2.tar.xz States that we are extracting the file
  hexchat-2.10.2.tar.xz.

Most source tarballs are kind enough to place all of their files in a directory
with the same name as the tar file, minus the file extension. Now we `cd` into
that directory to get to the source code.

Sidenote: if a tar archive does not place its files in a seperate directory, it
will litter the current working directory wil files. This type of tar archive
is called a tar bomb.

---

    ./configure

Configures the source tree for compilation. There are several flags that can be
passed to this script, and there are several environment variables that can be
set, both of which effect the way the package is compiled.

To see a list of some of the flags and variables that are supported, run:

    ./configure --help

Some flags to take note of:

    --prefix
    --libdir
    --sysconfdir
    --localstatedir

We will be making extensive use of these flags specifically in the near future.

---

    make

Compiles the actual source code into the binaries.

---

    sudo make install

Installs the binaries. Note that this is the only part of the process that
needs to be run as root.

### The Good and Decent Way

#### Downloading and Verifying the Source Code

Previously, we made no effort to verify the integrity of the source code. This
is very bad, as it makes it possible for an attacker to corrupt the source
archive when we download it and possible slip something malicious in there.
This is not hypothetical; it has actually happened (read about the VSFTPD :)
backdoor). There are generally two ways to go about veryifying the integerity:
* Checksums
* Signatures

## Example 2: SuperTuxKart

Download SuperTuxKart from https://supertuxkart.net/Main_Page

Extract the source tarball.

Follow the compilation instructions in INSTALL.md. Notice that SuperTuxKart
uses `cmake`, whereas HexChat used `./configure`.

vi:syntax=markdown

