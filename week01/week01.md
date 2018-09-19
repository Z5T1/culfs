                          Cucumber Linux from Scratch
                                    Week 1
                              September 16, 2018

# Introduction

## What will we be Doing in this Group?

Setting out to build our own Linux systems from scratch. Ultimately, each
person will end up creating his own unique version of Cucumber Linux.

Here's a rough outline:

1. We'll start out by having everyone install the binary version of Cucumber
   Linux 1.1. This will serve as our host system for building Cucumber Linux
   from Scratch.
2. Next, we'll take an in depth look at how to build software from source, in
   order to make sure everyone is on the same page before we dive into compiling
   an entire operating system.
3. Then, we each build Cucumber Linux from Scratch. This process will basically
   follow the process in the Linux from Scratch book; we will start out with
   just the source code and compile an entire binary system from that.
4. After this we can start to get into more advanced topics like fixing
   security vulnerabilities, security hardening, customizing your system, adding
   your own packages or anything else that the group's interested in.

## Who am I?

I'm Scott Court, BDFL @ Cucumber Linux. I'm a Junior CSEC major at RIT who
loves Unix, C and operating systems.

## A Very Brief History of Cucumber Linux

Started as my Summer project in May 2016.

Development really took off in September 2016.

First stable release in July 2017.

I've learned a lot about Linux, operating systems and security along the way
and now I'm here to share my learning experience with all of you by recreating
it first hand.

If you're interested in learning more about the history of Cucumber Linux, you
can view a presentation I gave on the topic at
https://cucumberlinux.com/~scott/presentations/An%20Overview%20of%20How%20I%20Created%20Cucumber%20Linux.pdf
(video is available at https://youtu.be/uTfkcJsjKe8?t=2509).

# Installing Cucumber Linux

## Why Use Cucumber Linux?

Why are we using Cucumber Linux as our host system? It's not just because I
made it, there are a couple of legitimate reasons:
1. Cucumber Linux is the only distro I have tested this process on, so it's the
   only place I'm positive the entire process works; there are some other
   distros where I know this doesn't work, so I'd rather not have to spend time
   debugging issues that arrise as a result of using a specific distro for the
   host system.
2. Shockingly, Cucumber Linux is the distro that I am most familiar with, so I
   will be most able to help resolve issues on a Cucumber Linux system.

## Install Cucumber Linux in a Virtual Machine

See https://wiki.cucumberlinux.com/wiki/install:guide

### Note on Step 1

I used Cucumber Linux 1.1 x86_64 Full Edition. You must use the full edition of
Cucumber Linux 1.1; otherwise, some required packages will be missing. I also
strongly recommend using the 64 bit version.

### Note on Step 3

When you get to step 3, I used a GPT partition table with the following
partitions:

    +-----------+--------+----------------------------------------------------+
    | Partition | Size   | Filesystem | Purpose/Mount Point                   |
    +-----------+--------+----------------------------------------------------+
    | /dev/sda1 | 4MB    | <none>     | BIOS Boot Partition (Make sure to use |
    |           |        |            | hex code ef02 for the Partition Type) |
    +-----------+--------+----------------------------------------------------+
    | /dev/sda2 | 512MB  | ext2       | /boot                                 |
    +-----------+--------+----------------------------------------------------+
    | /dev/sda3 | 4GB    | swap       | swap                                  |
    +-----------+--------+----------------------------------------------------+
    | /dev/sda4 | 59.5GB | btrfs      | /                                     |
    +-----------+--------+----------------------------------------------------+

You can use whatever partitioning scheme you'd like of course; however, make
sure your root partition is at least 56GB in size.

### Note on Step 5

When you get to step 5, make sure to install all of the package groups *except*
the multilib group (this applies only if you are using the x86_64 architecture).

# Resources for this Week
* Recording of this week's presentation: http://z5t1.com/culfs/week01.ogv
* Cucumber Linux Installation Guide: https://wiki.cucumberlinux.com/wiki/install:guide

I appologize, but the video and audio are out of sync in this week's recording.
I will try to improve this for next week.

## Virtual Machine Snapshot
Every week, I will be working on my own virtual machine. I encourage all of you
to work on your own machines as well. That being said, the work we do in this
interest group is cumulative; if you miss one week, you will not be able to do
the next week's activity until you get your VM caught up. I realize it is not
reasonable to expect everyone to be able to attend every single week, so each
week I will be takng a snapshot of my VM and making that available for you to
use the following week if your VM isn't quite up to speed. So if you start to
get behind with your VM, don't worry; you all have enough to worry about
already. You can just make a copy of mine next week.

Unfortunately, the virtual machine image is too large for me to upload
anywhere, so if you need a copy you will have to get it from me in person. You
can do this by either tracking me down on campus or by arriving to the meeting
15 minutes early on the day you want to download it.

The Virtual Machine snapshot taken at the end of this week is called 'Week01'.

vi:syntax=markdown

