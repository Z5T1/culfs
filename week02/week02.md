                          Cucumber Linux from Scratch
                                    Week 2
                              September 23, 2018

# Configure the Cucumber Linux Virtual Machine

## Configuring Networking

See https://wiki.cucumberlinux.com/wiki/sysconfig:networking

## Adding an Unprivileged User

See https://wiki.cucumberlinux.com/wiki/sysconfig:user_management

## Setting up a Graphical Login

See https://wiki.cucumberlinux.com/wiki/sysconfig:graphical_login_screen

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

In this example we will verify the integrity of the source tarball, compile
HexChat, make a package file out of it and install the package with the
system's package manager.

In preparation for this, uninstall the version of HexChat we just installed;
otherwise the two builds will conflict. From the original HexChat source
directory run:

    sudo make uninstall

#### Downloading and Verifying the Source Code

Previously, we made no effort to verify the integrity of the source code. This
is very bad, as it makes it possible for an attacker to corrupt the source
archive when we download it and possible slip something malicious in there.
This is not hypothetical; it has actually happened (read about the VSFTPD :)
backdoor). There are generally two ways to go about veryifying the integerity:
* Checksums
* Signatures

##### Signatures

Signatures make use of a public key to cryptographically verify the integrity
of the tarballs. This requires you to download an additional signature file
(these usually end in *.sig, *.sign or *.asc). Using this method also requires
you to obtain the public key that was used to create the signatures. It is not
always easy to securely obtain the public key.

To verify the signature for the HexChat tarball, download the signature:

    wget https://dl.hexchat.net/hexchat/hexchat-2.10.2.tar.xz.asc

Now, import the public key that was used to create the signature:

    gpg --recv-keys '108B F221 2A05 1F4A 72B1  8448 B3C7 CE21 0DE7 6DFC'

Finally, use GPG to verify the signature:

    gpg --verify hexchat-2.10.2.tar.xz.asc

##### Checksums

Checksums make use of hashing functions to verify the integrity. Some common
hashing algorithms that are used for verifying source tarballs are MD5, SHA1,
SHA256 and SHA512. Note that you should /never/ use MD5 hashes anymore, and you
should try to avoid using SHA1 when possible.

Here are the checksums for the HexChat tarball:

MD5 (Do not ever use):

    c8e7477ac941295deaeb1732591ab20b  hexchat-2.10.2.tar.xz

SHA1 (Try to avoid this):

    3ce831cde92f2f9999a217523d124e5b4cd08333  hexchat-2.10.2.tar.xz

SHA256 (This one is good):

    87ebf365c576656fa3f23f51d319b3a6d279e4a932f2f8961d891dd5a5e1b52c  hexchat-2.10.2.tar.xz

SHA512 (This one is even better):

    799be6ca02d4f7bad98c005e0fb7dba151717b52841d7f2dd3ed86b80a20de934825a1e58aab4621ac751a605103e68e368a95e9709c48f52b9e5333e5e290ab  hexchat-2.10.2.tar.xz

To verify the SHA256 checksum, save the SHA256 line above to the file
sha256sums. Then run the following command:

    sha256sum -c sha256sums

The `-c` flag says to check the checksums in the file 'sha256sums'.

Now verify it again using the SHA512 checksum.

Food for thought:
* Why should we never use MD5?
* Why should we try to avoid SHA1 and why is this less of an issue than MD5
  (although still an issue)?
* Why is SHA512 better than SHA256?

#### Building (Again)

As before, we extract the source tarball and `cd` to its directory. After this,
run `./configure`, only using the following flags:

    ./configure --prefix=/usr --libdir=/usr/lib64 --sysconfdir=/etc --localstatedir=/var

We will discuss what each of these flags does in depth. Now that the source
tree has been configured for this build, compile HexChat using `make`. In this
build, we will exploit parallelism by compiling using multiple cores. Run:

    make -jN

where 'N' is the number of cpu cores you have. To determine how many cores you
have, run `nproc`.

#### Installing the Binaries

This time, we will create a package archive. To do this, we must first make a
"staging" directory. This will effectively serve as a seperate root directory
that contains only this package's files.

    mkdir /tmp/staging

Now install the binaries to the staging directory. To do this, make use of the
DESTDIR variable in the makefile, which says to install to a root directory
other than /.

    sudo make install DESTDIR=/tmp/staging

It is important to note that this variable is NOT always DESTDIR; it can vary
on a package to package basis. Make sure you know what it is for the package
you are currently installing.

Now, compress the staging directory into a package tarball:

    cd /tmp/staging
    sudo makepkg -l y -c n ../hexchat-2.10.2-x86_64-1.txz

Notice the package naming convention: NAME-VERSION-ARCHITECTURE-BUILDNUMBER.txz.

Finally, install your new package:

    sudo installpkg /tmp/hexchat-2.10.2-x86_64-1.txz

You may wish to move the package file to a more permanant location, as all the
files in /tmp will be deleted on the next reboot.

## Example 2: OpenTTD

In this example, we will be building OpenTTD. OpenTTD is a clone of the game
"Transport Tycoon Deluxe." Their website is http://www.openttd.org/. At this
point, you should be beginning to feel a little more comfortable compiling
software from source, so explicit instructions will not be given. Look back at
example 1 if you are unsure of a command.

OpenTTD has two dependencies that are not part of Cucumber Linux. 
* SDL
* ICU

Make sure to install them first. If you are unsure of how to proceed in
installing them, see the hints section.

Once you have installed the dependencies, follow the instructions at
https://wiki.openttd.org/Compiling_on_(GNU/)Linux_and_*BSD.

## Example 3: SuperTuxKart

SuperTuxKart is a 3D open-source arcade racer with a variety characters,
tracks, and modes to play. It is basically a rip off of MarioKart. This example
is a more advanced one than the previous two, and there are even fewer hints
provided. This is intended to be a bit of a challenge, but once you have
successfully built and installed this package, it is indicitive that you are
well on your way to mastering the process of building software from source.

Download SuperTuxKart from https://supertuxkart.net/Main_Page.

Extract the source tarball.

Follow the compilation instructions in INSTALL.md. Notice that SuperTuxKart
uses `cmake`, whereas HexChat used `./configure`.

# Hints

Here are some hints that help address many of the common issues encountered
when compiling software:
* If you're ever unsure of how to proceed in compiling a package, read the
  README and INSTALL files at the root of the package's source tree. If you're
  still having issues, take a look at the buildscript from another distro. There
  are links to many the location of several other distros' buildscript
  repositories in the resources section.

# Resources

Recording of this week's presentation: https://z5t1.com/culfs/week02.ogv

## Buildscript Repositories

Other distros maintain repositories of their own buildscripts. These can be
great places to look if you're ever unsure of how to build a package. They are
listed from most helpful to least helpful (in my opinion, of course and only as
they are relevant to Cucumber Linux):
* Cucumber Linux: https://mirror.cucumberlinux.com/cucumber/cucumber-1.1/source/
* Beyond Linux from Scratch: http://www.linuxfromscratch.org/blfs/view/8.3/
* Slackware: https://mirrors.slackware.com/slackware/slackware-current/source/
* Slackbuilds.org: https://slackbuilds.org/
* Arch User Repository: https://aur.archlinux.org/

vi:syntax=markdown

