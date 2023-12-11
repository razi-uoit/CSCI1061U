# Week 4 Class Code: Operator Overloading and Friend Functions

1. Operator overloading is used to use an operator for performing many functions. For example, a '+' operators is used to add int and double

	adding two integers
```
	#include<iostream>
	#include<string>
	using namespace std;

	int main()
	{
		int number1 = 7, number2 = 10;

		int result = number1 + number2;

		cout <<"Result: "<<result<<endl; 
		return 0;
	}
```
	adding two doubles
```
	#include<iostream>
	#include<string>
	using namespace std;

	int main()
	{
		double number1 = 7.5, number2 = 10.3;

		double result = number1 + number2;

		cout <<"Result: "<<result<<endl; 
		return 0;
	}
```
2. '+' operator is also overloaded with an additional functionality of concatenating two strings
```
	#include<iostream>
	#include<string>
	using namespace std;

	int main()
	{
		string string1 = "Ontario ", string2 = "Tech";

		cout << "String 1: " << string1 << endl;
		cout << "String 2: " << string2 << endl;

		string result = string1 + string2;
		cout << "Result: " << result << endl;

		return 0;
	}
```
3. Overloading << operator to display objects on the console
```
	class Vehicle
	{
	private: 
		string name;
		int kms;
	public:
		Vehicle(string name, int kms)
		{
			this->name = name;
			this->kms = kms;
		}
		string getName()
		{
			return name;
		}
		int getKms()
		{
			return kms;
		}
	};

	ostream& operator<<(ostream& output, Vehicle& vehicle)
	{
		output << "Name: " << vehicle.getName() << endl;
		output << "Kms: " << vehicle.getKms() << endl;
		return output;
	}
	int main()
	{
		Vehicle car1 = Vehicle("Toyota RAV4", 1234);
		Vehicle car2 = Vehicle("Honda CRV", 5678);
		cout << car1<<car2;

		return 0;
	}

```
4. Overloading == operator for objects
```
	#include <iostream>
	using namespace std;

	class Vehicle
	{
	    private:
	    string name;
	    int kms;
    
    	public:
	    Vehicle(string name, int kms)
	    {
        	this->name = name;
	        this->kms = kms;
	    }
	    string getName()
	    {
        	return this->name;
	    }
	    int getKMs()
	    {
        	return this->kms;
	    }
	    void display()
	    {
        	cout <<"Name: "<<this->name<<endl;
	        cout <<"KMs: "<<this->kms<<endl;
	    }
	};

	bool operator==(Vehicle &v1, Vehicle &v2)
	{
	    if (v1.getName() == v2.getName() && v1.getKMs() == v2.getKMs())
	    {
        	return true;
	    }
	    return false;
	}

	int main()
	{
	    Vehicle v1 = Vehicle("Toyota RAV4", 1234);
	    Vehicle v2 = Vehicle("Honda CRV", 7890);
    
	    if (v1 == v1)
	    {
        	cout <<"Same Objects"<<endl;
	    }
	    else
	    {
        	cout <<"Different Objects"<<endl;
	    }
    
	    return 0;
	}
```

5. Operator as member functions
```
	#include <iostream>
	using namespace std;

	class Vehicle
	{
	    private:
	    string name;
	    int kms;
    
    	public:
	    Vehicle(string name, int kms)
	    {
        	this->name = name;
	        this->kms = kms;
	    }
	    string getName()
	    {
        	return this->name;
	    }
	    int getKMs()
	    {
        	return this->kms;
	    }
	    void display()
	    {
        	cout <<"Name: "<<this->name<<endl;
	        cout <<"KMs: "<<this->kms<<endl;
	    }
	    bool operator==(Vehicle &v2)
	    {
        	if (this->name == v2.name && this->kms == v2.kms)
	        {
        	    return true;
	        }
        	return false;
	    }
	};

	int main()
	{
	    Vehicle v1 = Vehicle("Toyota RAV4", 1234);
	    Vehicle v2 = Vehicle("Honda CRV", 7890);
    
	    if (v1 == v2)
	    {
        	cout <<"Same Objects"<<endl;
	    }
	    else
	    {
        	cout <<"Different Objects"<<endl;
	    }
    
    	return 0;
	}
```
6. Overloading += as a member function
```
	#include <iostream>
	using namespace std;

	class Vehicle
	{
	    private:
	    string name;
	    int kms;
	    int passengers;
    
    	public:
	    Vehicle(string name, int kms, int passengers)
	    {
        	this->name = name;
	        this->kms = kms;
        	this->passengers = passengers;
	    }
	    string getName()
	    {
        	return this->name;
	    }
	    int getKMs()
	    {
        	return this->kms;
	    }
	    int getPassengers()
	    {
        	return this->passengers;
	    }
	    void display()
	    {
        	cout <<"Name: "<<this->name<<endl;
	        cout <<"KMs: "<<this->kms<<endl;
	    }
	    bool operator==(Vehicle &v2)
	    {
        	if (this->name == v2.name && this->kms == v2.kms)
	        {
        	    return true;
	        }
	        return false;
	    }
	    Vehicle& operator+=(int i)
	    {
        	this->passengers = this->passengers + i;
	        return *this;
        
	    }
	};

	ostream& operator<<(ostream& out, Vehicle& vehicle)
	{
	    out <<"Name: "<<vehicle.getName()<<endl;
	    out <<"KMs: "<<vehicle.getKMs()<<endl;
	    out <<"Passengers: "<<vehicle.getPassengers()<<endl;
	    return out;
	}

	int main()
	{
	    Vehicle v1 = Vehicle("Toyota RAV4", 1234, 5);
	    cout <<v1<<endl;
	    v1+=2;
	    cout <<v1<<endl;
    
	    return 0;
	}
```

7. In order to make ostream& operator<< as a member function, you need to use an indirect method as ostream& operator<< cannot write to ostream object.
```
	#include<iostream>

	using namespace std;

	class Vehicle
	{
	    private:
	    string name;
	    int kms;
	    int passengers;
    
    	public:
	    Vehicle(string name, int kms, int passengers)
	    {
	        this->name = name;
        	this->kms = kms;
	        this->passengers = passengers;
	    }

   	string getName()
	{
	        return this->name;
	}
	int getKMs()
    	{
        	return this->kms;
	}
    	int getPassengers()
    	{
        	return this->passengers;
    	}
    	bool operator==(Vehicle& v2)
    	{
        	if (this->name == v2.name && this->kms == v2.kms)
        	{
	           return true;
        	}
        	return false;
    	}
    	Vehicle& operator+=(int i)
    	{
        	this->passengers = this->passengers + i;
        	return *this;
    	}
    	ostream& display(ostream& out)
    	{
        	out <<"Name: "<<this->name<<endl;
        	out <<"KMs: "<<this->kms<<endl;
        	out <<"Passengers: "<<this->passengers<<endl;
        	return out;
    	}
	};

	ostream& operator<<(ostream& out, Vehicle& v)
	{   
    		return v.display(out);
	}

	int main()
	{
    		Vehicle v1 = Vehicle("Toyota RAV4", 1234, 5);
    
    		cout <<v1;
    	        return 0;
	}

```
7. Overloading Binary Operators (+, - etc)
```
	#include <iostream>

	using namespace std;

	class Numbers
	{
	    private:
	    int * numbers;
	    int size;
    
    	public:
	    Numbers(int *arr, int size)
	    {
        	this->size = size;
	        this->numbers = new int[this->size];
        
        	for(int i=0; i<this->size; i++)
	        {
        	    this->numbers[i] = arr[i];
	        }
	    }
	    ~Numbers()
	    {
        	delete[] this->numbers;
	    }
	    void display()
	    {
        	for (int i=0; i<this->size;i++)
	        {
        	    cout <<this->numbers[i]<<"\t";
	        }
	        cout<<endl;
	    }
	    void operator+(Numbers& n)
	    {
        	int *temp = new int[this->size];
	        for (int i=0; i<this->size;i++)
        	{
	            temp[i] = this->numbers[i] + n.numbers[i];
        	}
	        for (int i=0; i<this->size;i++)
        	{
	            cout <<temp[i]<<"\t";
        	}
	        delete[] temp;
	    }
	};

	int main()
	{
	    int arr[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    
	    int size = sizeof(arr)/sizeof(arr[0]);
    
	    Numbers n1 = Numbers(arr, size);
	    Numbers n2 = Numbers(arr, size);
    
            n1.display();
	    
	    n2.display();
    
	    n1 + n2;
    
	    return 0;
	}
```

8. Friend functions are used to allow friends of the class to use its private and protected members.
```
	class Vehicle
	{
	private:
		string name;
		int kms;
		int OBU;
	public:
		Vehicle(string name, int kms, int OBU)
		{
			this->name = name;
			this->kms = kms;
			this->OBU = OBU;
		}
		string getName()
		{
			return name;
		}
		int getKms()
		{
			return kms;
		}
	
		friend int getOBU(Vehicle vehicle);

	};

	int getOBU(Vehicle vehicle)
	{
		return vehicle.OBU;
	}

	int main()
	{
		Vehicle car1 = Vehicle("Toyota RAV4", 1234, 12);
		Vehicle car2 = Vehicle("Honda CRV", 234, 12);


		cout << "OBU: " << getOBU(car1) << endl;

		return 0;
	}
```
9. Friend Functions can be handy with operator overloading
```
	class Vehicle
	{
	private:
		string name;
		int kms;
		int OBU;
	public:
		Vehicle(string name, int kms, int OBU)
		{
			this->name = name;
			this->kms = kms;
			this->OBU = OBU;
		}
		string getName()
		{
			return name;
		}
		int getKms()
		{
			return kms;
		}
		friend ostream& operator<<(ostream& output, Vehicle& vehicle);
	};

	ostream& operator<<(ostream& output, Vehicle& vehicle)
	{
		output << "Name: " << vehicle.getName() << endl;
		output << "Kms: " << vehicle.getKms() << endl;
		output << "OBU: " << vehicle.OBU << endl;
		return output;
	}
	int main()
	{
		Vehicle car1 = Vehicle("Toyota RAV4", 1234, 12);
		Vehicle car2 = Vehicle("Honda CRV", 5678, 34);
		cout << car1 << car2;
	
		return 0;
	}

```
