CC = g++ -O2 -g -Wno-deprecated -Wno-write-strings 
LDFLAGS := -pthread -L./
tag = -i

BIN=./bin/
SOURCE=./source/

ifdef linux
tag = -n
endif


# generates main gtesting.o and test scripts

test: Record.o Comparison.o ComparisonEngine.o Schema.o File.o  BigQ.o Pipe.o GenericDBFile.o HeapFile.o SortedFile.o DBFile.o y.tab.o lex.yy.o test.o 
	$(CC) -o $(BIN)test $(BIN)Record.o $(BIN)Comparison.o $(BIN)ComparisonEngine.o $(BIN)Schema.o $(BIN)File.o  $(BIN)BigQ.o $(BIN)Pipe.o ${BIN}GenericDBFile.o ${BIN}HeapFile.o ${BIN}SortedFile.o $(BIN)DBFile.o $(BIN)y.tab.o $(BIN)lex.yy.o $(BIN)test.o -lfl $(LDFLAGS)
	
main: Record.o Comparison.o ComparisonEngine.o Schema.o File.o y.tab.o lex.yy.o  BigQ.o Pipe.o GenericDBFile.o HeapFile.o SortedFile.o DBFile.o main.o
	$(CC) -o $(BIN)main $(BIN)Record.o $(BIN)Comparison.o $(BIN)ComparisonEngine.o $(BIN)Schema.o $(BIN)File.o $(BIN)y.tab.o $(BIN)lex.yy.o $(BIN)BigQ.o $(BIN)Pipe.o ${BIN}GenericDBFile.o ${BIN}HeapFile.o ${BIN}SortedFile.o $(BIN)DBFile.o $(BIN)main.o -lfl $(LDFLAGS)
	
test.o: $(SOURCE)test.cc
	$(CC) -g -c  $< -o $(BIN)$@ $(LDFLAGS)

main.o: $(SOURCE)main.cc
	$(CC) -g -c  $< -o $(BIN)$@
 	
Comparison.o: $(SOURCE)Comparison.cc
	$(CC) -g -c  $< -o $(BIN)$@
	
ComparisonEngine.o: $(SOURCE)ComparisonEngine.cc
	$(CC) -g -c  $< -o $(BIN)$@

GenericDBFile.o: $(SOURCE)GenericDBFile.cc
	$(CC) -g -c  $< -o $(BIN)$@

HeapFile.o: $(SOURCE)HeapFile.cc
	$(CC) -g -c  $< -o $(BIN)$@

SortedFile.o: $(SOURCE)SortedFile.cc
	$(CC) -g -c  $< -o $(BIN)$@

DBFile.o: $(SOURCE)DBFile.cc
	$(CC) -g -c  $< -o $(BIN)$@

File.o: $(SOURCE)File.cc
	$(CC) -g -c  $< -o $(BIN)$@

Record.o: $(SOURCE)Record.cc
	$(CC) -g -c  $< -o $(BIN)$@

Pipe.o: $(SOURCE)Pipe.cc
	$(CC) -g -c  $< -o $(BIN)$@ $(LDFLAGS)

BigQ.o: $(SOURCE)BigQ.cc
	$(CC) -g -c  $< -o $(BIN)$@ $(LDFLAGS)

Schema.o: $(SOURCE)Schema.cc
	$(CC) -g -c  $< -o $(BIN)$@
	
y.tab.o: $(SOURCE)Parser.y
	yacc -d $(SOURCE)Parser.y
	mv y.tab.* $(SOURCE)
	sed $(tag) $(SOURCE)y.tab.c -e "s/  __attribute__ ((__unused__))$$/# ifndef __cplusplus\n  __attribute__ ((__unused__));\n# endif/" 
	g++ -c $(SOURCE)y.tab.c -o $(BIN)$@

lex.yy.o: $(SOURCE)Lexer.l
	lex  $(SOURCE)Lexer.l
	mv lex.* $(SOURCE)
	gcc  -c $(SOURCE)lex.yy.c -o $(BIN)$@

gtesting.o: gtest-all.o gtest_main.o
	$(CC) $(BIN)Record.o $(BIN)Comparison.o $(BIN)ComparisonEngine.o $(BIN)Schema.o $(BIN)File.o $(BIN)y.tab.o $(BIN)lex.yy.o $(BIN)DBFile.o $(BIN)gtest_main.o $(BIN)gtest-all.o $(SOURCE)gtesting.cc -o $(BIN)$@ $(LDFLAGS)

clean: 
	rm -f $(BIN)*.o
	rm -f $(BIN)*.out
	rm -f $(BIN)y.tab.c
	rm -f $(BIN)lex.yy.c
	rm -f $(BIN)y.tab.h
	rm -f $(BIN)*.bin
	rm -f $(BIN)main $(BIN)test




