SHELL := /bin/zsh
.PHONY: clean gdb show

all: a aa
libb.so: b.c
	gcc -shared $< -o $@
a: a.c libb.so
	gcc $< -L. -lb -o $@
aa: a.c libb.so
	gcc $< -Wl,-rpath='$$ORIGIN' -Wl,--enable-new-dtags -L. -lb -o $@ # older ld needs --enable-new-dtags
show: all
	ldd a aa | egrep --color '^|.*libb.*'
	readelf -d a | egrep --color '.*RUNPATH.*' || :
	readelf -d aa | egrep --color '.*RUNPATH.*'
	./a || :
	./aa
gdb:
	@:
clean:
	$(RM) a aa libb.so
