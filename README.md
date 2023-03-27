# _printf()

Prints text to terminal based on a given format string to standard output. Mimicking glibc printf.

Syntax: _printf(\<format string\>, args...)

## Current features
Implemented specifiers:
* Decimal integers (%d)
* Unsigned decimal integers (%u)
* Strings (%s)
* Hex integers (%x %X)
* Octal integers (%o)
* Binary integers (%b)
* Pointer notation for integers (%p)
* Print a string, but print hidden characters as hex codes (%S)
* Reversed strings (%r)
* [Rot13'd](https://en.wikipedia.org/wiki/ROT13) strings (%R)

Implemented flags and options:
* Width
* Precision
* +/space to set sign
* \- to left justify
* \# to display hex/octal binary prefix
* \* and .\* to accept variables for width and precision
* hh, h, and l length flags

## Getting started
The simplest way to add this to your project would be to compile the whole codebase with your project. Likely you'll want to compile and include it as a static library to avoid logistical hassles though. To do so for a single project using gcc run these commands from the root printf directory:
```
gcc -c \*.c
ar rcs libprintf.a \*.o
```
After this, copy the resulting printf.a file and printf.h to your project directory. Include printf.h where appropriate in your source files. Then using GCC as an example, when compiling add the -l flag with the library file name like so:
```
gcc <your stuff here> libprintf.a
```

## Usage Examples
The simplest example is just printing out a string literal as the format string, like so:
```
_printf("Hello printf!");
```
This will output the text "Hello printf!" to the terminal, like so:
```
Hello printf!
```
Rountinely, you will want to use printf to print out strings from variables or numbers. We can take in variables passed as further arguments by using %, then flags (optional), then a specifier for the type of thing we are printing. If we have an integer and a string, we will use %d and %s respectively, like so:
```
char str[] = "world";
int number = 42;
_printf("Hello %s %d!", str, number);
```
We will get the output:
```
Hello world 42!
```
Printf takes the specifiers in the order they appear in the format string, so in this case our string variable must be before our integer variable, or else printf will try printing the string like an integer and vice versa, would could cause a crash! There are various options to change how and where the text is output which can be combined together, and a complete readable listing can be found at http://www.cplusplus.com/reference/cstdio/printf/

There are a few non-standard specifiers in this version of printf. One is %S, which prints normally invisible characters as hex codes. Like so:
```
char str[]="\x14<-I can see you->\x15";
_printf("%S", str);
```
When this is run we should get:
```
\x14<-I can see you->\x15
```
There is a specifiers to print a string in reverse (%S):
```
char str[] = "SdrakcaB";
_printf(%r,str);
```
Will net us:
```
BackwardS
```
The rot13 specifier (%R) will shift all characters 13 letters forward, turning every "a" into an "n" and so on. Finally, there is a binary number specifier (%b):
```
int number = 19;
_printf("%b", number);
```
This should get us the binary number output:
```
10011
```

## Testing
The tests folder includes a mains.c file which will run a series of pairs of printf statements on many different combinations of specifiers, flag and options using both this version of print and stdlib printf, and output this to stdout. To run these tests, compile the entire project then run the resulting executable:
```
gcc -o printftest *.c tests/mains.c
./printftest
`0x11. C - printf team project

Group Project:                                                                      
                                                                                    
0. I'm not going anywhere. You can print that wherever you want to. I'm here and I'm
 a Spur for life                                                                    
Write a function that produces output according to a format.                        
                                                                                    
                                                                                    
1. Education is when you read the fine print. Experience is what you get if you don'
t                                                                                   
Handle the following conversion specifiers:

2. With a face like mine, I do better in print                                      
Handle the following custom conversion specifiers:                                  
                                                                                    
3. What one has not experienced, one will never understand in print                 
Handle the following conversion specifiers:                                         
                                                                                    
4. Nothing in fine print is ever good news                                          
Use a local buffer of 1024 chars in order to call write as little as possible.      
                                                                                    
5. My weakness is wearing too much leopard print                                    
Handle the following custom conversion specifier:                                   
                                                                                    
6. How is the world ruled and led to war? Diplomats lie to journalists and believe t
hese lies when they see them in print                                               
Handle the following conversion specifier: p.                                       
                                                                                    
7. The big print gives and the small print takes away                               
Handle the following flag characters for non-custom conversion specifiers:          
                                                                                    
8. Sarcasm is lost in print                                                         
Handle the following length modifiers for non-custom conversion specifiers:         
                                                                                    
l                                                                                   
h                                                                                   
Conversion specifiers to handle: d, i, u, o, x, X                                   
                                                                                    
9. Print some money and give it to us for the rain forests                          
Handle the field width for non-custom conversion specifiers.                        
                                                                                    
10. The negative is the equivalent of the composer's score, and the print the perfor
mance                                                                               
Handle the precision for non-custom conversion specifiers.                          
                                                                                    
11. It's depressing when you're still around and your albums are out of print       
Handle the 0 flag character for non-custom conversion specifiers.                   
                                                                                    
12. Every time that I wanted to give up, if I saw an interesting textile, print what
 ever, suddenly I would see a collection                                            
Handle the - flag character for non-custom conversion specifiers.                   
                                                                                    
13. Print is the sharpest and the strongest weapon of our party                     
Handle the following custom conversion specifier:                                   
                                                                                    
14. The flood of print has turned reading into a process of gulping rather than savo
ring                                                                                
Handle the following custom conversion specifier:                                   
                                                                                    
15. *                                                                               
All the above options work well together. 
``

## Authors
Hussein Abdullahi  
Oluchi Emma-Eze
