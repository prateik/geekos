#summary Project Goals

# Introduction #

The overall goal of GeekOS is to be a small, simple, realistic
implementation of an operating system kernel.

The version of GeekOS hosted here is a complete rewrite of
the original version.  It attempts to improve on the
original in a number of ways:

  * Support multiple target architectures (initially x86)
  * Use a standard C coding style (similar to [Linux kernel style](http://lxr.linux.no/linux/Documentation/CodingStyle))
  * Use consistent coding standards: especially, in ErrorHandling code
  * Use only the GNU compiler/assembler/linker (NASM is no longer required)
  * Simplified design (especially with regards to the virtual filesystem)
  * Multiboot compliant (boots from a CD image using grub)