# File Handling, Revisit of Constructors

C/C++ I / O are based on streams, which are sequence of bytes flowing in and out of the programs.

Streams acts as an intermediaries between the programs and the actual IO devices.

C++ IO operations are device independent. The same set of operations can be applied to different types of IO devices.

## Stream Hierarchy

<ios>         <istream>       <iostream>          <fstream>
ios base      |istream        (cin)               <-- ifstream
ios        <--|iostream                           <-- fstream
              |ostream        (cout, err, clog)   <-- ofstream
              <ostream>

## File Streams

- ifstream – stream class to read from files
- ofstream – stream class to write to files.
- fstream - stream class to both read (from) and write (to) files.
- The stream objects cin, cout, cerr and clog are declared in iostream
  header file and are automatically added to our program, when iostream
  header file is included in our program.
- In contrast, we are responsible for creating and setting up our own file streams.

## Steps for File IO:

1. Create file stream objects
```c
ifstream fsIn;    // input
ofstream fsOut;   // output
fstream fsBoth;   // input & output
```

2. Open the file
```c
fsIn.open("data.txt",fileopenmode);
```
OR Combine the two steps
```c
ifstream fsIn("data.txt", fileopenmode);
```

3. Check if the file is opened properly. Every stream object has an is_open( )
method that returns "true" if a file is open and associated with the stream
object, otherwise it returns "false".
```c
if(fsOut.is_open()) cerr<<"Failed to open file"
```

4. Read and write to files using the functions defined in the stream's pubic interface

5. Close the file after use.
```c
fsIn.close(); //Close files
fsOut.close();
fsBoth.close();
```

All istreams ( and ifstreams ) have a method eof( ) that returns a boolean value of true
if an attempt is made to read past the end of the file, and false otherwise.

# Formatted Output

```c
int a = 1 ;
char c = 'A';
string s = "Sam P";

ofstream fOut;
fOut.open("example.txt");

fOut << a << " " << c << " " <<s;
fOut.close();
```

```example.txt
1 A Sam
```

The Extraction Operation Operator '>>' does not consider white space characters
as part of strings (white space characters causes extraction to terminate).


# Unformatted IO

> **Single Character - Input**
> - `int get ();` Extracts a character from a stream and returns as int.
> - `istream & get (char & c);` Extracts a character from a stream, stores it in c and return the invoking istream reference.
> **Single Character - Output**
> `ostream & put (char c);` Inserts character c into the stream and return the invoking ostream reference.


