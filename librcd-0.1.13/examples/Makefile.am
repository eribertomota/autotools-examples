bin_PROGRAMS= example
example_SOURCES= example.c
example_LDADD= ../src/librcd.la
EXTRA_DIST= input.txt

test: example
	cat input.txt | ./example
