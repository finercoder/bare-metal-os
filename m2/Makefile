complete: floppya

run: complete
	bochs -f opsys.bxrc

kernel: kernel.o kernel_asm.o
	ld86 -o kernel -d kernel.o kernel_asm.o

kernel.o: kernel.c
	bcc -ansi -c -o kernel.o kernel.c

kernel_asm.o: kernel.asm
	as86 kernel.asm -o kernel_asm.o

bootload: bootload.asm
	nasm bootload.asm

floppya: kernel message.txt bootload
	dd if=/dev/zero of=floppya.img bs=512 count=2880
	dd if=bootload of=floppya.img bs=512 count=1 conv=notrunc
	dd if=kernel of=floppya.img bs=512 conv=notrunc seek=3
	dd if=message.txt of=floppya.img bs=512 count=1 seek=30 conv=notrunc

clean:
	rm -f *.o kernel bootload
