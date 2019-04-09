                      Cucumber Linux from Scratch
                                Week 9
                            April 10, 2019

# Getting Started with Cucumber Linux Development

## Development Jobs

There are several different jobs that must be done to successfully maintain a
distribution. Throughout this interest group, I hope you will find one
particular job or set of jobs that you personally enjoy working on. A brief
description of each job along with plans for what the development team will be
working on in the near future is available at
https://github.com/cucumberlinux/bureaucratic-stuff/blob/master/action_plan_april_2019.md.
I invite you to take a look at it and see if anything interests you.

## Mailing Lists and IRC

The vast majority of communication within the Cucumber Linux Project takes
place via email and IRC, as is the case with most open source projects. 

There are several mailing lists you can subscribe to, a full list of which can
be found at https://cucumberlinux.com/mailing_lists.php. As developers, the
most relevant mailing list for you to subscribe to will be (surprise surprise)
the development mailing list. The security mailing list is also a very good one
to be subscribed to as this is where announcements about new security updates
are published.

The IRC channel for Cucumber Linux is #cucumberlinux on freenode.net. You
should familiarize yourself with this as it is where the bulk of our planning
meetings take place.

## The Ports Tree

The ports tree contains the buildscripts for all of the packages in Cucumber
Linux. It can be found on GitHub at https://github.com/cucumberlinux/ports.
This repository is also the place that pull requests are submitted at, so you
will be spending a *lot* of time here. 

Before cloning the repository, make sure to read the README. You may also wish
to make your own fork of the repository before you do this, as this will make
your life easier when you want to submit pull requests. To perform the initial
cloning of the ports tree, there is a shell script called portstrap in the
utilities/tools directory of the ports tree. This script automates the tasks
that must be done to clone and setup the ports tree properly.

## Your First Contributions

Open Issues for Cucumber Linux are tracked using the GitHub issue tracker. Each
version of Cucumber Linux has a separate Kanban Board which can be viewed at
https://github.com/orgs/cucumberlinux/projects. Navigate to the board for
Cucumber Linux 2.0 and take a look at the To Do column. Any issue that does not
already have a developer assigned to it is up for grabs. Good first issues are
tagged as such. Select one of these issues, assign yourself to it and begin
working on it. Submit a pull request when you are done to the official ports
repository.

# Resources

* Cucumber Linux GitHub Project Page: https://github.com/cucumberlinux
* Cucumber Linux Ports Tree: https://github.com/cucumberlinux/ports
* Cucumber Linux Bureaucratic Stuff: https://github.com/cucumberlinux/bureaucratic-stuff
* Cucumber Linux Mailing Lists: https://cucumberlinux.com/mailing_lists.php

vi:syntax=markdown
