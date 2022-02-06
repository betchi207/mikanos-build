all: hello.efi

%.o: %.c
	clang -target x86_64-pc-win32-coff -o $@ -c $<
	# clang -target x86_64-pc-win32-coff -mno-red-zone -fno-stack-protector -fshort-wchar -Wall -o $@ -c $<

%.efi: %.o
	mkdir -p ./mnt/efi/boot
	rm -f ./mnt/efi/boot/*
	lld-link /subsystem:efi_application /entry:EfiMain /out:./mnt/efi/boot/bootx64.efi hello.o

.PHONY: run
run: hello.efi
	../../devenv/run_qemu ./mnt

clean:
	rm -rf mnt
