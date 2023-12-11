# Command Line arguments and MakeFile

`X.h`
```
class X
{
    private:
    int x;
    
    public:
    X(int x);
    int getX();
};
```
`X.cpp`
```
#include "X.h"

X::X(int x)
{
    this->x = x;
}
int X::getX()
{
    return this->x;
}
```

`Y.h`
```
class Y
{
    private:
    int y;
    
    public:
    Y(int y);
    int getY();
};
```
`Y.cpp`
```
#include "Y.h"

Y::Y(int y)
{
    this->y = y;
}
int Y::getY()
{
    return this->y;
}
```

`main.cpp`
```
#include<iostream>
#include "X.h"
#include "Y.h"
using namespace std;

int main()
{
    X x = X(5);
    Y y = Y(6);
    
    int result = x.getX() + y.getY();
    
    cout <<"Result: "<<result<<endl;
    return 0;
}
```

### Makefile
```
all:
	g++ main.cpp X.cpp Y.cpp -o main.o
```

Make Files can do many other things as splitting the code into multiple targetes

Makefile
```
all: output

output: main.o X.o Y.o
	g++ main.o X.o Y.o -o ouptut.o

main.o: main.cpp
	g++ -c main.cpp

X.o: X.cpp
	g++ -c X.cpp

Y.o: Y.cpp
	g++ -c Y.cpp
```

It is a good idea to remove all the intermediary files once done. So, clean target can help in that

```
all: output

output: main.o X.o Y.o
	g++ main.o X.o Y.o -o ouptut.o

main.o: main.cpp
	g++ -c main.cpp

X.o: X.cpp
	g++ -c X.cpp

Y.o: Y.cpp
	g++ -c Y.cpp

clean:
	rm -rf *.o
```
Variables can be introduced in the make files as well
```
CC=g++

all: output

output: main.o X.o Y.o
	$(CC) main.o X.o Y.o -o ouptut.o

main.o: main.cpp
	$(CC) -c main.cpp

X.o: X.cpp
	$(CC) -c X.cpp

Y.o: Y.cpp
	$(CC) -c Y.cpp

clean:
	rm -rf *.o
```

Flags can be provided as well
```
CC=g++
CFLAGS=-c

all: output

output: main.o X.o Y.o
	$(CC) main.o X.o Y.o -o ouptut.o

main.o: main.cpp
	$(CC) $(CFLAGS) main.cpp

X.o: X.cpp
	$(CC) $(CFLAGS) X.cpp

Y.o: Y.cpp
	$(CC) $(CFLAGS) Y.cpp

clean:
	rm -rf *.o
```

Command Line Arguments can be used to get data to feed to your program. Argc is used to count the number of arguments
```
#include<iostream>
#include "X.h"
#include "Y.h"
using namespace std;

int main(int argc, char *argv[])
{
    cout <<"Argc: "<<args<<endl;
	
    int i = 5, j = 6;
	
    X x = X(i);
    Y y = Y(j);
    
    int result = x.getX() + y.getY();
    
    cout <<"Result: "<<result<<endl;
    return 0;
}
```

Argv depicts an array of pointers to the characters and contains all the arguments including the output file name
```
#include<iostream>
#include "X.h"
#include "Y.h"
using namespace std;

int main(int argc, char *argv[])
{
	cout <<"Argc: "<<argc<<endl;
	
	for (int i=0; i<argc; i++)
	{
		cout <<"Argv: "<<argv[i]<<endl;
	}
	
	int i = 5, j = 6;
	
    X x = X(i);
    Y y = Y(j);
    
    int result = x.getX() + y.getY();
    
    cout <<"Result: "<<result<<endl;
    return 0;
}
```
Command line arguments need to be converted to int as they are normally arrays
```
#include<iostream>
#include "X.h"
#include "Y.h"
using namespace std;

int main(int args, char *argv[])
{
	int i = atoi(argv[1]);
	int j = atoi(argv[2]);
    X x = X(i);
    Y y = Y(j);
    
    int result = x.getX() + y.getY();
    
    cout <<"Result: "<<result<<endl;
    return 0;
}
```
