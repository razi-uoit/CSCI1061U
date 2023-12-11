# Week 3 Class Code : Dynamic Memory

1. Static Memory is held at the load time
```
	#include<iostream>

	using namespace std;

	int main()
	{
	    int number = 7;
	    cout <<"Number: "<<number<<endl;
	    return 0;
	}
```
2. Dynamic Memory is held in the heap memory
```
	int main()
	{

		// variable created in stack
		int number = 7;
		cout << "Number in stack: " << number << endl;	

		// variable created in heap
		int* ptr = new int;
		*ptr = 7;
		cout << "Number in heap: " << *ptr << endl;

		return 0;
	}
```
3. Dynamic Memory for Arrays
```
	int main()
	{
		// arrays created in stack
		int numbers[5] = {5, 7, 8, 33, 44};

		// arays created in heap
		int* ptr = new int[5];
		ptr[0] = 13;
		ptr[1] = 14;
		ptr[2] = 15;
		ptr[3] = 16;
		ptr[4] = 17;

		for (int i =0; i<5; i++)
    		{
		        cout <<ptr[i]<<"\t";
		}

		return 0;
	}
```
	Below program would result in error in some of the modern compilers
```
	#include<iostream>

	using namespace std;

	int main()
	{
	    int size;
	    cout <<"Enter the size of the array: ";
	    cin >>size;
	    int myArray[size] = {5, 6, 7, 8, 9};
        
    	    for (int i =0; i<5; i++)
	    {
        	cout <<myArray[i]<<"\t";
	    }
	    return 0;
	}
```
	For g++ below command can be used to generate an error based on C++ standards

	`g++ -pedantic-errors source.cpp -o source.o`

4. Dynamic Memory for Dynamic Arrays
```
	#include <iostream>
	using namespace std;

	int main()
	{
		int size;
		cout << "Enter the size of the Array: ";
		cin >> size;

		int* numbersPtr = new int[size];
		int number;
		for (int i = 0; i < size; i++)
		{
			cout << "Enter element " << i << ": ";
			cin>>number;
			*(numbersPtr + i) = number;
		}
		cout << "Values entered... " << endl;
		for (int i = 0; i < size; i++)
		{
			cout << "numbersPtr[" << i << "] = " << *(numbersPtr + i) << endl;
		}
		return 0;
	}

```
5. Dynamic arrays can be part of classes as well
```
	#include<iostream>

	using namespace std;

	class Numbers
	{
	    private:
		    int *ptr;
		    int size;
    
    	    public:
	    Numbers(int size)
	    {
        	this->size = size;
	        ptr = new int[size];
	    }
	
	    void enterNumbers()
	    {
        	for (int i =0; i<size; i++)
	        {
        	    cout <<"Enter element at "<<i<<": ";
	            cin >>ptr[i];
	        }
	    }
	    void showEven()
    	    {
	        for (int i =0; i<size; i++)
	        {
        	    if (ptr[i]%2 == 0)
	            {
        	        cout <<ptr[i]<<"\t";
	            }
        	}
	        cout <<endl;
	    }
	};

	int main()
	{
	    int size;
	    cout <<"Enter the size of the array: ";
	    cin >>size;

	    Numbers numbers = Numbers(size);
	    numbers.enterNumbers();
	    numbers.showEven();

    
	    return 0;
	}
```
6. Working with Character arrays
```
	#include<iostream>

	using namespace std;

	class Vehicle
	{
	    private:
	    const char *name;
	    int kms;
    
    	public:
	    Vehicle(const char * name, int kms)
	    {
        	this->name = name;
	        this->kms = kms;
	    }
	    void display()
	    {
        	cout <<"Name: "<<this->name<<endl;
	        cout <<"KMs: "<<this->kms<<endl;
	    }
	};

	int main()
	{
	    Vehicle vehicle = Vehicle("Toyota Rav 4", 1234);
	    vehicle.display();
    
	    return 0;
	}
```
	In this code, the character array is created in the stack memory. To create in the heap memory we do the following:
```
	#include<iostream>

	using namespace std;

	class Vehicle
	{
	    private:
	    const char *name;
	    int kms;
    
    	public:
	    Vehicle(const char * name, int kms)
	    {
        	this->name = new char[13];
	        this->name = name;
        	this->kms = kms;
	    }
	    void display()
	    {
        	cout <<"Name: "<<this->name<<endl;
	        cout <<"KMs: "<<this->kms<<endl;
	    }
	};

	int main()
	{
	    Vehicle vehicle = Vehicle("Toyota Rav 4", 1234);
	    vehicle.display();

	    return 0;
	}
```
	The right way to write the above program is below:
```
	#include<iostream>
	#include<cstring>

	using namespace std;

	class Vehicle
	{
	    private:
	    char *name;
	    int kms;
    
    	public:
	    Vehicle(const char * name, int kms)
	    {
        	this->name = new char[13];
	        strcpy(this->name, name);
        	this->kms = kms;
	    }
	    void display()
	    {
        	cout <<"Name: "<<this->name<<endl;
	        cout <<"KMs: "<<this->kms<<endl;
	    }
	};

	int main()
	{
	    Vehicle vehicle = Vehicle("Toyota Rav 477999", 1234);
	    vehicle.display();

	    return 0;
	}
```
	Even better approach is to get the size using strlen() function from cstring library
```
	#include<iostream>
	#include<cstring>

	using namespace std;

	class Vehicle
	{
	    private:
	    char *name;
	    int kms;
    
    	public:
	    Vehicle(const char * name, int kms)
	    {
        	int size = strlen(name);
	        this->name = new char[size];
        	strcpy(this->name, name);
	        this->kms = kms;
	    }
	    void display()
	    {
        	cout <<"Name: "<<this->name<<endl;
	        cout <<"KMs: "<<this->kms<<endl;
	    }
	};

	int main()
	{
	    Vehicle vehicle = Vehicle("Toyota Rav 477999", 1234);
	    vehicle.display();

	    return 0;
	}
```
5. Dynamic Memory for Objects
```
	#include <iostream>
	using namespace std;

	class Vehicle
	{
	private:
		string name, make, color;
	public:
		Vehicle(string name, string make, string color)
		{
			this->name = name;
			this->make = make;
			this->color = color;
		}
		void display()
		{
			cout << "Make is " << make << ", Color is " << color << ", Name is " << name << endl;
		}
	};

	int main()
	{
		Vehicle corolla = Vehicle("Corolla", "Toyota", "White");
		corolla.display();
	
		Vehicle* ptrVehicle = new Vehicle("Corolla", "Toyota", "White");
		(*ptrVehicle).display();

		return 0;
	}
```
6. Memory Leak
```
	int main()
	{
		int* ptr = new int;
		*ptr = 7;
		cout << "Ptr: " << *ptr << endl;
		cout << "Ptr Address: " << ptr << endl;
		ptr = new int;
		*ptr = 10;

		cout << "Ptr: " << *ptr << endl;
		cout << "Ptr Address: " << ptr << endl;

		return 0;
	}
```
7. Memory Deallocation
```
	int main()
	{
		int* ptr = new int;
		*ptr = 7;
		cout << "Ptr: " << *ptr << endl;
		cout << "Ptr Address: " << ptr << endl;

		delete ptr;
		ptr = new int;
		*ptr = 10;

		cout << "Ptr: " << *ptr << endl;
		cout << "Ptr Address: " << ptr << endl;

		return 0;
	}
```	
8. Memory Deallocation with Arrays
```
	int main()
	{
		int* ptr = new int[5];
		ptr[0] = 2;
		ptr[1] = 4;
		ptr[2] = 6;
		ptr[3] = 8;
		ptr[4] = 10;

		delete[] ptr;

		for (int i = 0; i < 5; i++)
		{
			cout << "ptr[" << i << "] = " << *(ptr + i) << endl;
		}

		return 0;
	}
```
9. Memory Leaks in Functions
```
	void someFunction()
	{
		int* ptr = new int(10);
	}
	int main()
	{
		someFunction();
		return 0;
	}
```
