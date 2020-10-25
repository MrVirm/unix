# $@ = target file
# $< = first dependency
# $^ = all dependencies

# First rule is the one executed when no parameters are fed to the Makefile
all: run

# Notice how dependencies are built as needed
kernel.bin: kernel_entry.o obj/kernel.o
	i686-elf-ld -o $@ -Ttext 0x1000 $^ --oformat binary

kernel_entry.o: kernel_entry.s
	nasm $< -f elf -o $@

obj/kernel.o: ../kernel/kernel.c
	i686-elf-gcc -ffreestanding -c $< -o $@

# Rule to disassemble the kernel - may be useful to debug
kernel.dis: kernel.bin
	ndisasm -b 32 $< > $@

boot.bin: boot.s
	nasm $< -f bin -o $@

os-image.bin: boot.bin kernel.bin
	cat $^ > $@

run: os-image.bin
	qemu-system-i386 -fda $<

clean:
	rm *.bin *.o *.dis


