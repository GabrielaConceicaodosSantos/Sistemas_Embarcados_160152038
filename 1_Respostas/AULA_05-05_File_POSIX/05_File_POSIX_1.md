1. Considerando a biblioteca-padrão da linguagem C, responda:
  (a) Quais são as funções (e seus protótipos) para abrir e fechar arquivos?

      FILE* -> Ponteiro para arquivo

        Abertura de arquivos:
        FILE *fopen(const char *filename, const char *mode)
        b. Fechar arquivos:

int fclose(FILE *stream)
(b) Quais são as funções (e seus protótipos) para escrever em arquivos?

int fgetpos(FILE *stream, fpos_t *pos)
Gets the current file position of the stream and writes it to pos.

size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE *stream)
The C library function size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE *stream) writes data from the array pointed to, by ptr to the given stream.

int putc(int char, FILE *stream)
Writes a character (an unsigned char) specified by the argument char to the specified stream and advances the position indicator for the stream.

int puts(const char *str)
Writes a string to stdout up to but not including the null character. A newline character is appended to the output.

int fprintf(FILE *stream, const char *format, ...)
Sends formatted output to a stream.

(c) Quais são as funções (e seus protótipos) para ler arquivos?

size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream)
The C library function size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream) reads data from the given stream into the array pointed to, by ptr.

int fscanf(FILE *stream, const char *format, ...)
Reads formatted input from a stream.

int fgetc(FILE *stream)
Gets the next character (an unsigned char) from the specified stream and advances the position indicator for the stream

char *fgets(char *str, int n, FILE *stream)
The C library function char *fgets(char *str, int n, FILE *stream) reads a line from the specified stream and stores it into the string pointed to by str. It stops when either (n-1) characters are read, the newline character is read, or the end-of-file is reached, whichever comes first.

(d) Quais são as funções (e seus protótipos) para reposicionar um ponteiro para arquivo?

int fseek(FILE *stream, long int offset, int whence)
The C library function int fseek(FILE *stream, long int offset, int whence) sets the file position of the stream to the given offset.

stream − This is the pointer to a FILE object that identifies the stream.

offset − This is the number of bytes to offset from whence.

whence − This is the position from where offset is added. It is specified by one of the following constants
Constant Description SEEK_SET Beginning of file SEEK_CUR Current position of the file pointer SEEK_END End of file

void rewind(FILE *stream)
Sets the file position to the beginning of the file of the given stream.

int remove(const char *filename)
Deletes the given filename so that it is no longer accessible.

(e) Quais bibliotecas devem ser incluídas no código para poder utilizar as funções acima?

Para as funções acima, somente a sdtio.h. Caso queira se utilizar a função exit(), deve-se adicionar a biblioteca stdlib.h.

O que é a norma POSIX?
Portable Operating System Interface - Interface Portável entre Sistemas Operacionais

Para tornar possível escrever programas que pudessem ser executados em qualquer sistema Unix, o IEEE desenvolveu esta norma padrão para o Unix. O POSIX define uma interface mínima de chamada ao sistema que os sistemas em conformidade com o Unix devem suportar.

O Padrão POSIX é constituído por uma série de regras que determinam como o programador deve escrever o código-fonte de seu sistema de modo que ele possa ser portável entre os sistemas operacionais baseados no Unix.

Portável nesse caso significa que bastará recompilar o programa, usando o compilador adequado para torná-lo compatível com o sistema desejado, sem a necessidade de fazer alterações no código fonte.

Considerando a norma POSIX, responda:
(a) Quais são as funções (e seus protótipos) para abrir e fechar arquivos?

Para abrir arquivos:
int open(const char *pathname, int flags, mode_t mode); 
Para fechar arquivos:
#include <unistd.h> 
int close(int fd); 
(b) Quais são as funções (e seus protótipos) para escrever em arquivos?

#include <unistd.h> 
ssize_t write(int fd, const void *buf, size_t count); 
(c) Quais são as funções (e seus protótipos) para ler arquivos?

#include <unistd.h> 
ssize_t read(int fd, void *buf, size_t count); 
(d) Quais são as funções (e seus protótipos) para reposicionar um ponteiro para arquivo?

lseek(int fd, off_t offset, int whence);
(e) Quais bibliotecas devem ser incluídas no código para poder utilizar as funções acima?

#include <fcntl.h>	// Para a funcao open() #include <unistd.h>	// Para a funcao close() #include <stdlib.h>	// Para a função exit()
