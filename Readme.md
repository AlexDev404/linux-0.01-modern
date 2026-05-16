# Linux 0.01 — Modern Build

A modernized build of the original Linux 0.01 kernel (written by Linus Torvalds in 1991), updated to compile with contemporary toolchains on modern 32-bit and 64-bit x86 systems. The assembly files have been ported from the original GAS syntax to NASM, and the C code compiles cleanly with modern GCC.

The kernel boots from a floppy image and runs in emulators such as QEMU and Bochs.

## Prerequisites

Install the following packages (Debian/Ubuntu):

```bash
sudo apt-get update
sudo apt-get install build-essential gcc gcc-multilib nasm qemu-system-x86
```

You also need the hard-disk image included in the repository:

```bash
unzip hd_oldlinux.img.zip
```

## Building

Build the kernel image:

```bash
make
```

This produces a raw boot image called `Image`.

### Generating a Bootable Floppy Image

To generate a full 1.44 MB floppy disk image suitable for use with emulators:

```bash
make bootimage
```

This creates a file called `bootimage` — a zero-padded 1.44 MB image with the kernel written at the start.

## Running

### QEMU

```bash
make run
```

### Bochs

Make sure `bochsrc.txt` is in the project root, then:

```bash
bochs -f bochsrc.txt
```

## Other Make Targets

| Target       | Description                                      |
|--------------|--------------------------------------------------|
| `make`       | Build the kernel `Image`                         |
| `make bootimage` | Build a padded 1.44 MB bootable floppy image |
| `make run`   | Launch the kernel in QEMU                        |
| `make dump`  | Disassemble `tools/system` to `System.dum`       |
| `make clean` | Remove all build artifacts                       |
| `make dep`   | Regenerate header dependency information         |

## Credits

- **Linus Torvalds** — original Linux 0.01 kernel (1991)
- **Mariuz** — initial modernisation fork ([mariuz/linux-0.01](https://github.com/mariuz/linux-0.01))
- **Isoux** — NASM port, GCC/Clang build fixes, and ongoing maintenance
