# MoonFinder-x86

A hybrid C/C++ and x86-64 Assembly project that detects full moons in images and highlights them with a red circle[cite: 20, 24]. The project implements custom image processing kernels with hardware-level memory optimizations.

## Pipeline
1. **Grayscale Conversion**: Converts RGB input to Grayscale[cite: 20].
2. **Blur Filter (3x3)**: Reduces noise and softens edges[cite: 20].
3. **Sobel Edge Detection**: Calculates gradients (x and y directions) to find prominent edges[cite: 20].
4. **Hough Transform**: Votes for potential circle centers based on edge pixels and brightness thresholds[cite: 21, 22].

## Tech Stack
- **C / C++**: High-level logic, file I/O, and Hough Transform implementation[cite: 8, 22].
- **x86-64 Assembly (NASM)**: SIMD-accelerated (using `xmm` registers) implementations of Blur and Sobel convolution filters for processing 16 pixels in parallel[cite: 9, 10, 18].

## Build & Run
Ensure `gcc`, `g++`, and `nasm` are installed on your Linux environment[cite: 24].

```bash
# Compile ASM objects
nasm -f elf64 blur.asm -o blur.o
nasm -f elf64 conv_sobel.asm -o conv_sobel.o

# Compile and link
gcc -c moon_asm.c -o moon_asm.o
gcc moon_asm.o blur.o conv_sobel.o -lm -o moon_asm

# Run on a single image
./moon_asm input.jpg output.jpg
