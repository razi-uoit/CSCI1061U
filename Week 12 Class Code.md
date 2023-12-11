# Week 5 Class Code: Exception Handling and Modular Programming

1. The program below would break because of dividing by 0
```
	#include <iostream>
	using namespace std;

	int main()
	{
		int number1, number2;
	
		cout << "Enter number 1: ";
		cin >> number1;

		cout << "Enter number 2: ";
		cin >> number2;

		cout << "Result: " << number1 / number2;

		return 0;
	}
```
2. To fix the above program, we can use Exception Handling
```
	#include <iostream>
	using namespace std;

	int division(int numerator, int denominator)
	{
		return numerator / denominator;
	}

	int main()
	{
		int number1, number2;

		cout << "Enter number 1: ";
		cin >> number1;

		cout << "Enter number 2: ";
		cin >> number2;

		try
		{
			if (number2 == 0)
			{
				throw "Error";
			}
			else
			{
				int result = division(number1, number2);
				cout << "Result: " << endl;
			}
		
		}
		catch (const char * ex)
		{
			cout << "Cannot divide by zero" << endl;
		}
		return 0;
	}
```
	You can also throw an exception code as integer
```
	#include <iostream>
	using namespace std;

	int division(int numerator, int denominator)
	{
		return numerator / denominator;
	}

	int main()
	{
		int number1, number2;

		cout << "Enter number 1: ";
		cin >> number1;

		cout << "Enter number 2: ";
		cin >> number2;

		try
		{
			if (number2 == 0)
			{
				throw 1001;
			}
			else
			{
				int result = division(number1, number2);
				cout << "Result: " << endl;
			}
		
		}
		catch (const char * ex)
		{
			cout << "Cannot divide by zero" << endl;
		}
		catch (int ex)
		{
			cout << "Error Code: " << ex << endl;
		}
	
	return 0;
	}
```
3. You can catch exceptions in general as well
```
	#include <iostream>
	using namespace std;

	int division(int numerator, int denominator)
	{
		return numerator / denominator;
	}

	int main()
	{
		int number1, number2;

		cout << "Enter number 1: ";
		cin >> number1;

		cout << "Enter number 2: ";
		cin >> number2;

		try
		{
			if (number2 == 0)
			{
				throw 1001;
			}
			else
			{
				int result = division(number1, number2);
				cout << "Result: " << endl;
			}
		
		}
		catch (const char * ex)
		{
			cout << "Cannot divide by zero" << endl;
		}
		catch (int ex)
		{
			cout << "Error Code: " << ex << endl;
		}
		catch (...)
		{
			cout << "An exception occured" << endl;
		}

	
		return 0;
	}
```
3. Out of Range Exception

	The code below will crash the program by throwing an exception
```
	#include <iostream>
	#include <vector>
	using namespace std;

	int main()
	{
		vector<int> v = { 1, 2 };
		cout << v.at(2) << endl;

		return 0;
	}
```
	Above can be fixed in general using below code:
```
	#include <iostream>
	#include <vector>
	using namespace std;

	int main()
	{
		vector<int> v = { 1, 2 };

		try
		{
			cout << v.at(2) << endl;
		}
		catch (...)
		{
			cout << "Exception occurred" << endl;
		}

		return 0;
	}
```
4. Uptil now, we have been programming like below:
```
	#include <iostream>
	using namespace std;

	class Vehicle
	{
	private:
		string name;
		int kms;
	public:
		Vehicle()
		{
			name = "";
			kms = 0;
		}
		Vehicle(string name, int kms)
		{
			this->name = name;
			this->kms = kms;
		}
		string getName()
		{
			return this->name;
		}
		int getKms()
		{	
			return this->kms;
		}
		void display()
		{
			cout << "Name: " << this->name << ", KMs: " << this->kms << endl;
		}
	};

	int main()
	{
		Vehicle vehicle = Vehicle("Toyota Rav4", 1234);
		vehicle.display();
		return 0;
	}
```
	To use modular programming, we program modules.

	`Vehicle.h`
```
	#pragma once
	#include <iostream>
	using namespace std;
	class Vehicle
	{
	private:
		string name;
		int kms;
	public:
		Vehicle();
		Vehicle(string name, int kms);
		string getName();
		int getKms();
		void display();
	};
```
	`Vehicle.cpp`
```
	#include "Vehicle.h"

	Vehicle::Vehicle()
	{
		name = "";
		kms = 0;
	}
	Vehicle::Vehicle(string name, int kms)
	{
		this->name = name;
		this->kms = kms;
	}
	string Vehicle::getName()
	{
		return this->name;
	}
	int Vehicle::getKms()
	{
		return this->kms;
	}
	void Vehicle::display()
	{
		cout << "Name: " << this->name << ", KMs: " << this->kms << endl;
	}
```
	`main.cpp`
```
	#include "Vehicle.h"

	int main()
	{
		Vehicle vehicle = Vehicle("Toyota Rav4", 1234);
		vehicle.display();
		return 0;
	}

```
Converting above program from string to dynamic character array

	`Vehicle.h`
```
	#include<iostream>
	using namespace std;

	class Vehicle
	{
	    private:
	    char * name;
	    int kms;
    
    	public:
	    Vehicle(const char * name, int kms);
	    void display();
	    char * getName();
	    int getKMs();
	    ~Vehicle();
	};
```
	`Vehicle.cpp`
```
	#include "Vehicle.h"
	#include<cstring>

	Vehicle::Vehicle(const char * name, int kms)
	{	
	    int size = strlen(name);
	    this->name = new char[size + 1];
    
    	    for (int i=0; i<size; i++)
	    {
        	this->name[i] = name[i];
	    }
    
            this->kms = kms;
	}
	void Vehicle::display()
	{
	    cout <<"Name: "<<this->name<<endl;
	    cout <<"Kms: "<<this->kms<<endl;
	}
	char * Vehicle::getName()
	{
	    return this->name;
	}
	int Vehicle::getKMs()
	{
	    return this->kms;
	}
	Vehicle::~Vehicle()
	{
	    delete[] this->name;
	}
```
	`main.cpp`
```
	#include "Vehicle.h"

	int main()
	{
	    Vehicle vehicle = Vehicle("Toyota", 1234);
	    vehicle.display();
	   return 0;
	}
```
5. Modular Programming helps keeping global functions as well:

	`Vehicle.h`
```
	#include<iostream>
	using namespace std;

	class Vehicle
	{
	    private:
	    char * name;
	    int kms;
    
    	public:
	    Vehicle(const char * name, int kms);
	    void display();
	    char * getName();
	    int getKMs();
	    ~Vehicle();
	};

	void display(Vehicle *vehicles, int size);
```

	`Vehicle.cpp`
```
	#include "Vehicle.h"
	#include<cstring>

	Vehicle::Vehicle(const char * name, int kms)
	{
	    int size = strlen(name);
	    this->name = new char[size + 1];
    
	   strcpy(this->name, name);
    
    	this->kms = kms;
	}
	void Vehicle::display()
	{
	    cout <<"Name: "<<this->name<<endl;
	    cout <<"Kms: "<<this->kms<<endl;
	}
	char * Vehicle::getName()
	{
	    return this->name;
	}
	int Vehicle::getKMs()
	{
	    return this->kms;
	}
	Vehicle::~Vehicle()
	{
	    delete[] this->name;
	}

	void display(Vehicle *vehicles, int size)
	{   
	    for (int i=0; i<size; i++)
	    {
        	cout <<"Name: "<<vehicles[i].getName()<<endl;
	        cout <<"KMs: "<<vehicles[i].getKMs()<<endl;
        	cout <<"******************************"<<endl;
	    }
 
	}
```

	`main.cpp`
```
	#include "Vehicle.h"

	int main()
	{
	    Vehicle vehicles[5] = {
	        Vehicle("Toyota", 123),
	        Vehicle("Honda", 132),
	        Vehicle("Audi", 789),
        	Vehicle("BMW", 222),
	        Vehicle("Tesla", 777),
    
    	};
    
    	int size = sizeof(vehicles)/sizeof(vehicles[0]);
    
	    display(vehicles, size);
	    return 0;
	}
```
The above program can be modified to store vehicle array in the heap memory as follows:
```
	#include "Vehicle.h"

	int main()
	{
	    Vehicle *vehicles = new Vehicle[5]
	    {
		        Vehicle("Toyota", 123),
	        	Vehicle("Honda", 132),
		        Vehicle("Audi", 789),	
        		Vehicle("BMW", 222),
	        	Vehicle("Tesla", 777),
	    };
    
    	display(vehicles, 5);
    
    	delete[] vehicles;
	    return 0;
	}

```
6. Operator Overloading would work in a similar manner

	`Vehicle.h`
```
	#include<iostream>
	using namespace std;

	class Vehicle
	{
	    private:
	    char * name;
	    int kms;
    
    	public:
	    Vehicle(const char * name, int kms);
	    void display();
	    char * getName();
	    int getKMs();
	    ~Vehicle();
	};

	void display(Vehicle *vehicles, int size);
	ostream& operator<<(ostream& out, Vehicle &vehicle);
```
	`Vehicle.cpp`
```
	#include "Vehicle.h"
	#include<cstring>

	Vehicle::Vehicle(const char * name, int kms)
	{
	    int size = strlen(name);
	    this->name = new char[size + 1];
    
   	strcpy(this->name, name);
    
	    this->kms = kms;
	}
	void Vehicle::display()
	{
	    cout <<"Name: "<<this->name<<endl;
	    cout <<"Kms: "<<this->kms<<endl;
	}
	char * Vehicle::getName()
	{
	    return this->name;
	}
	int Vehicle::getKMs()
	{
	    return this->kms;
	}
	Vehicle::~Vehicle()
	{
	    delete[] this->name;
	}

	void display(Vehicle *vehicles, int size)
	{   
	    for (int i=0; i<size; i++)
	    {
	        cout <<"Name: "<<vehicles[i].getName()<<endl;
        	cout <<"KMs: "<<vehicles[i].getKMs()<<endl;
	        cout <<"******************************"<<endl;
	    }
    
	}

	ostream& operator<<(ostream& out, Vehicle &vehicle)
	{
	    cout <<"Name: "<<vehicle.getName()<<endl;
	    cout <<"Kms: "<<vehicle.getKMs()<<endl;
	    return out;
	}
```	

	`main.cpp`
```
	#include "Vehicle.h"

	int main()
	{
    
	 	Vehicle vehicle = Vehicle("Toyota", 123);
	    cout <<vehicle<<endl;
	    return 0;
	}
```

	Updating above program to use dynamic arrays of Vehicle with operator overloading

	`Vehicle.h`
```
	#include<iostream>
	using namespace std;

	class Vehicle
	{
	    private:
	    char * name;
	    int kms;
    
    	public:
	    Vehicle(const char * name, int kms);
	    void display();
	    char * getName();
	    int getKMs();
	    ~Vehicle();
	};

	void display(Vehicle *vehicles, int size);
	ostream& operator<<(ostream& out, Vehicle *vehicles);


	Vehicle.cpp

	#include "Vehicle.h"
	#include<cstring>

	Vehicle::Vehicle(const char * name, int kms)
	{
	    int size = strlen(name);
	    this->name = new char[size + 1];
    
	   strcpy(this->name, name);
    
	    this->kms = kms;
	}
	void Vehicle::display()
	{
	    cout <<"Name: "<<this->name<<endl;
	    cout <<"Kms: "<<this->kms<<endl;
	}
	char * Vehicle::getName()
	{
	    return this->name;
	}
	int Vehicle::getKMs()
	{
	    return this->kms;
	}
	Vehicle::~Vehicle()
	{
	    delete[] this->name;
	}

	void display(Vehicle *vehicles, int size)
	{   
	    for (int i=0; i<size; i++)
	    {
        	cout <<"Name: "<<vehicles[i].getName()<<endl;
	        cout <<"KMs: "<<vehicles[i].getKMs()<<endl;
        	cout <<"******************************"<<endl;
	    }
    
	}

	ostream& operator<<(ostream& out, Vehicle *vehicles)
	{
	    for (int i=0; i<5; i++)
	    {
	        out <<"Name: "<<vehicles[i].getName()<<endl;
        	out <<"KMs: "<<vehicles[i].getKMs()<<endl;
	        out <<"******************************"<<endl;
	    }
	    return out;
	}
```
	`main.cpp`
```
	#include "Vehicle.h"
	#include<cstring>

	Vehicle::Vehicle(const char * name, int kms)
	{
	    int size = strlen(name);
	    this->name = new char[size + 1];
    
	   strcpy(this->name, name);
    
	    this->kms = kms;
	}
	void Vehicle::display()
	{
	    cout <<"Name: "<<this->name<<endl;
	    cout <<"Kms: "<<this->kms<<endl;
	}
	char * Vehicle::getName()
	{
	    return this->name;
	}
	int Vehicle::getKMs()
	{
	    return this->kms;
	}
	Vehicle::~Vehicle()
	{
	    delete[] this->name;
	}

	void display(Vehicle *vehicles, int size)
	{   
	    for (int i=0; i<size; i++)
	    {
        	cout <<"Name: "<<vehicles[i].getName()<<endl;
	        cout <<"KMs: "<<vehicles[i].getKMs()<<endl;
        	cout <<"******************************"<<endl;
	    }
    
	}

	ostream& operator<<(ostream& out, Vehicle *vehicles)
	{
	    for (int i=0; i<5; i++)
	    {
	        out <<"Name: "<<vehicles[i].getName()<<endl;
        	out <<"KMs: "<<vehicles[i].getKMs()<<endl;
	        out <<"******************************"<<endl;
	    }
	    return out;
	}
```
7. Using operator overloading as member function

	`Vehicle.h`
```
	#include<iostream>
	using namespace std;

	class Vehicle
	{
	    private:
	    char * name;
	    int kms;
	    int passengers;
    
    	public:
	    Vehicle(const char * name, int kms, int passengers);
	    void display();
	    char * getName();
	    int getKMs();
	    int getPassengers();
	    Vehicle& operator+=(int);
	    ~Vehicle();
	};

	void display(Vehicle *vehicles, int size);
	ostream& operator<<(ostream& out, Vehicle *vehicles);
```
	`Vehicle.cpp`
```
	#include "Vehicle.h"
	#include<cstring>

	Vehicle::Vehicle(const char * name, int kms, int passengers)
	{
	    int size = strlen(name);
	    this->name = new char[size + 1];
    
	   strcpy(this->name, name);
    
    	this->kms = kms;
	    this->passengers = passengers;
	}
	void Vehicle::display()
	{
	    cout <<"Name: "<<this->name<<endl;
	    cout <<"Kms: "<<this->kms<<endl;
	}
	char * Vehicle::getName()
	{
	    return this->name;
	}
	int Vehicle::getKMs()
	{
	    return this->kms;
	}
	int Vehicle::getPassengers()
	{
	    return this->passengers;
	}
	Vehicle::~Vehicle()
	{
	    delete[] this->name;
	}
	Vehicle& Vehicle::operator+=(int i)
	{
	    this->passengers += i;
	    return *this;
	}

	void display(Vehicle *vehicles, int size)
	{   
	    for (int i=0; i<size; i++)
	    {
	        cout <<"Name: "<<vehicles[i].getName()<<endl;
        	cout <<"KMs: "<<vehicles[i].getKMs()<<endl;
	        cout <<"Passengers: "<<vehicles[i].getPassengers()<<endl;
        	cout <<"******************************"<<endl;
	    }   
	}

	ostream& operator<<(ostream& out, Vehicle *vehicles)
	{
	    for (int i=0; i<5; i++)
	    {
	        out <<"Name: "<<vehicles[i].getName()<<endl;
        	out <<"KMs: "<<vehicles[i].getKMs()<<endl;
	        cout <<"Passengers: "<<vehicles[i].getPassengers()<<endl;
        	out <<"******************************"<<endl;
	    }
	    return out;	
	}
```
	`main.cpp`
```
	#include "Vehicle.h"

	int main()
	{
	    Vehicle *vehicles = new Vehicle[5]
	    {
	        Vehicle("Toyota", 123, 1),
	        Vehicle("Honda", 132, 4),
	        Vehicle("Audi", 789, 5),
        	Vehicle("BMW", 222, 2),
	        Vehicle("Tesla", 777, 3),
	    };
    
    	cout <<vehicles<<endl;
    
	    for (int i=0; i<5; i++)
	    {
        	vehicles[i]+=2;
	    }
    
    	cout <<"After incrementing..."<<endl;
	    cout <<vehicles<<endl;
    
    	delete[] vehicles;
	
	    return 0;
	}
```
