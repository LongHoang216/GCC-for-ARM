This is the procedure how to compile a main.c file into an ARM file that can be used for ARM microcontroller

Compile start-up file: 
arm-none-eabi-gcc -mcpu=cortex-m4 -c -x assembler-with-cpp -o "startup.o" "startup.s"

Compile main.c file: 
arm-none-eabi-gcc -mcpu=cortex-m4 -std=gnu11 -c main.c -o "main.o"

Create ELF file: (This file is used for debug with GDB)
arm-none-eabi-gcc -o [file-name].elf main.o startup.o -mcpu=cortex-m4 -T"linker.ld" -Wl,-Map="[map-file-name].map" -Wl,--gc-sections -static

Extract BIN file from ELF file: (This file is used to apply to ST Utility)
arm-none-eabi-objcopy -O binary [file-name].elf [file-name].bin