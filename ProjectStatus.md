# Project Status #

This page describes the current status of the version of GeekOS
hosted here.

## General Status ##

Builds on x86.  You need to have ruby
installed for the "make depend" target to work,
and mkisofs is required to build the bootable
CD image.

I have only tested booting using [Bochs](http://bochs.sourceforge.net/).

## Subsystems ##

**Interrupts**: working (x86 using i8259A PIC)

**Threads**: working, including timer-based preemption,
and synchronization using mutexes and condition variables

**Memory allocation**: heap allocation works

**Virtual memory**: not implemented yet

**Devices**:

  * a general framework for defining and enumerating devices is in place
  * timer: works
  * VGA text console: works
  * ramdisk: implemented but not tested

**Virtual filesystem**: a design is in place, along with
a partial (untested) implementation.  The goal is that
the generic VFS layer does all the work of maintaining
the tree of directories and files, including the
required locking.  The individual filesystem drivers
will just need to implement callbacks for reading and
writing data and metadata using a block device.