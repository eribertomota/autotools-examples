bin_PROGRAMS= generate ascii upper
generate_SOURCES= generate.c
generate_LDADD= -lm
ascii_SOURCES= ascii.c
upper_SOURCES= upper.c

EXTRA_DIST= doit

table.tmp.h: dragons.txt
	./doit dragons.txt

tests: table.tmp.h
	cat ../src/librcd.c | sed -e "s|russian_table|table.tmp|;s|librcd\.h|../src/librcd.h|" > librcd.tmp.c
	gcc -o test test.c
	gcc -o debug debug.c

clean-local:
	-rm -f *.tmp.[ch] test debug
