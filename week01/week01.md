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

When you get to step 5, make sure to install all of the package groups *except*
the multilib group if you are using the x86_64 architecture. 

## Configure the new Cucumber Linux System

# Building Software from Source

## Example 1: HexChat

Download HexChat from http://hexchat.net.

Extract the source tarball and cd into the directory.

Run the following commands:

    ./configure
    make
    sudo make install

## Example 2: SuperTuxKart

Download SuperTuxKart from https://supertuxkart.net/Main_Page

Extract the source tarball.

Follow the compilation instructions in INSTALL.md. Notice that SuperTuxKart
uses `cmake`, whereas HexChat used `./configure`.

vi:syntax=markdown
