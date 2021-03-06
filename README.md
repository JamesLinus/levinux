# Levinux - A Micro Linux for Education
<a href="http://mikelev.in/ux/"><img src="http://levinux.com/micro-linux-education.png" alt="Micro Linux for Education" /></a>

## What Is This Project About?
The [micro Linux distribution](http://mikelev.in/ux/) known as Levinux
(download ~25 MB) is a tiny virtual Linux server that runs from USB or Dropbox
with a double-click (no install or admin rights required) on Macs, Windows or
Linux PCs—making it the perfect learning environment and launching-off point
for other projects, requiring just enough operating system and a quick
introduction to generic nix systems.

Levinux combines with another Github project of mine called Pipulate, so that
you can see a live Python/Flask app running from http://localhost:8888. There
will be a minimal (busybox) webserver on http://localhost:8080 after first run.
But what's going on under the hood to make this all possible? Easy, Levinux is
the remix of QEMU and Tiny Core Linux into something perfect for nix newbs.

--------------------------------------------------------------------------------
## An Appeal To The Github Community
The main limiting factor in this project is my inability to make the perfect
QEMU binary for use with Tiny Core Linux for each platform (Windows, Mac and
GNOME/Unity). I'm currently using the smallest and most highly compatible and
widely distributed versions pointed to by qemu.org, but they are becoming
forever more brittle as OSes evolve. The QEMU binaries need a fresh compile
from a talented and trusted source each platform who knows how to bake-in
dependencies like the curses library (but not SDL). There's also a pruning job
down to just what's necessary to get the non-graphics version of core.gz, so I
suspect it will take a lot of qemu config file customizations. I've seen the
binaries as small as 1MB on older versions of QEMU, but modern compiles seem to
come in arount 60MB. Times 3 platforms, and the "keep it small" tennant of
Levinux goes away. So, anyone up to the challenge? 

- Selecting the right QEMU version and patches code-base on each platform to
  start with.
- Trim the qemu configuration file down to the bare minimum to support the
  also-minimal vimlinuz Linux kernel distributed with Tiny Core Linux.
- Rounding up all the dependencies to support text-only mode (curses, ncurses,
  pdcurses, etc.) and static compile them into the qemu binary.
- Help with testing on the current and last few versions of each OS.

# Installation Instructions

Download the zip, unarchive it and...

1. If on Windows, double-click Pipulate.vbs.
2. If on Mac OSX, double-click Pipulate.
3. If on Linux, double-click Pipulate.sh and select Run in Terminal.

## Machine-specific issues

1. Windows may prompt you to allow it to run and unblock firewall.
2. Mac OS X may require you to right-click or Control-click and open.
3. Ubuntu 14.04 Nautilus / Edit / Preferences / Behavior / Executable Text
   Files, "Select Ask Each Time"

## Including additional packages

Inclusion of additional packages is simple, but requires a few steps be taken to optimize and set up.

1. Download the package and any dependencies from http://distro.ibiblio.org/tinycorelinux/6.x/x86/tcz/ (dependencies are listed in the {package}.tcz.dep file).
2. Add the downloaded `.tcz` files to `/Reset/Server/Ingredients/Custom`
3. Add the name of the downloaded package **without the `.tcz` file extension** to `/Reset/Server/Ingredients/extras.lst`

**Optional:** `/Reset/Server/Ingredients/install_extras.sh` can be duplicated and point at a file other than `extras.lst`.  This can allow for different packages to be grouped and have group output silenced by pointing the output to `/dev/null`

**Note:** Ensure you do not write below the last line in the `extras.lst` file

## Upgrade Instructions
Generally speaking, Levinux will use the most recent version of TinyCore Linux available.  If it is out of date, it will be upgraded in a timely manner.  For the time being, this upgrade will be performed by @miklevin himself to ensure the validity of the image.  

That being said, if you want to upgrade on your own, the process is simple:

1. Download the latest core-current.iso from http://distro.ibiblio.org/tinycorelinux/downloads.html Use the ~9MB file labeled Core.
2. Open the .iso image and go into the boot directory. Some versions of Windows may require special software for this.
3. Copy the files named core.gz and vmlinuz into the MacOS directory and overwrite the existing versions.

That's it.  Start the levinux application and it should show the version number.
