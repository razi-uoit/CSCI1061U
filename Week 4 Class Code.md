# Week 4 Class Code: Operator Overloading and Friend Functions

1. Operator overloading is used to use an operator for performing many functions. For example, a '+' operators is used to add int and double

	`adding two integers`
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
	`adding two doubles`
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
2. `+` operator is also overloaded with an additional functionality of concatenating two strings
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
3. Overloading `<<` operator to display objects on the console
```
	class Vehicle
	{
    		private:
    		char * name;
    		int kms;
    
   		public:
		Vehicle(const char * n, int k)
		{
		        name = new char[strlen(n) + 1];
		        strcpy(name, n);
		        kms = k;
		}
		char * getName()
		{
		        return name;
		}
		int getKMs()
		{
		        return kms;
		}
		~Vehicle()
		{
		        delete[] name;
		}
	};


	ostream& operator<<(ostream& out, Vehicle& vehicle)
	{
		out <<"Name: "<<vehicle.getName()<<endl;
		out <<"KMs: "<<vehicle.getKMs()<<endl;
		return out;
	}

	int main()
	{
	    Vehicle v1 = Vehicle("Toyota RAV 4", 1234);
	    
	    cout <<v1<<endl;

	    return 0;
	}
```
4. Overloading `==` operator for objects
```
	bool operator==(Vehicle &v1, Vehicle &v2)
	{
	    return (strcmp(v1.getName(), v2.getName()) == 0 && v1.getKMs() == v2.getKMs());
	}

	int main()
	{
	    Vehicle v1 = Vehicle("Toyota RAV 4", 1234);
	    Vehicle v2 = Vehicle("Toyota RAV 4", 1235);
    
    	    cout <<v1<<endl;
	    cout <<v2<<endl;
    
	    if (v1==v2)
	    {
        	cout <<"Objects are similar"<<endl;
	    }
	    else
	    {
        	cout <<"Objects are different"<<endl;
	    }
            
	    return 0;
	}
```

5. We can overload operators like `+=` as well
```
	#include <iostream>
	#include <cstring>

	using namespace std;

	class Vehicle
	{
	    private:
	    char * name;
	    int kms;
	    int passengers;
    
    	    public:
	    Vehicle(const char * n, int k, int p)
	    {
        	name = new char[strlen(n) + 1];
	        strcpy(name, n);
        	kms = k;
	        passengers = p;
	    }
	    char * getName()
	    {
        	return name;
	    }
	    int getKMs()
	    {
        	return kms;
	    }
	    int getPassengers()
	    {
        	return passengers;
	    }
	    void setPassengers(int p)
	    {	
	        passengers = p;
	    }
	    ~Vehicle()
	    {
        	delete[] name;
	    }
	};

	ostream& operator<<(ostream& out, Vehicle& vehicle)
	{
	    out <<"Name: "<<vehicle.getName()<<endl;
	    out <<"KMs: "<<vehicle.getKMs()<<endl;
	    return out;
	}

	bool operator==(Vehicle &v1, Vehicle &v2)
	{
	    return (strcmp(v1.getName(), v2.getName()) == 0 && v1.getKMs() == v2.getKMs());
	}

	Vehicle& operator+=(Vehicle &v1, int p)
	{
	    int temp = v1.getPassengers() + p;
	    v1.setPassengers(temp);
	    return v1;
	}

	int main()
	{
	    Vehicle v1 = Vehicle("Toyota RAV 4", 1234, 4);
	    cout <<"Passengers before increment: "<<v1.getPassengers()<<endl;
	    v1+=1;
    
	    cout <<"Passengers after increment: "<<v1.getPassengers()<<endl;
    
	    return 0;
	}
```
6. Overloading Binary Operators (`+`, `-` etc)
```
	#include <iostream>
	#include <cstring>

	using namespace std;

	class Numbers
	{
	    private:
	    int *numbers;
	    int size;
    
    	public:
	    Numbers(int * n, int s)
	    {
        	size = s;
	        numbers = new int[size];
        	for (int i=0; i<size; i++)
	        {
        	    numbers[i] = n[i];
	        }
	    }
	    ~Numbers()
	    {
        	delete[] numbers;
	    }
	    int getSize()
	    {
        	return size;
	    }
	    int * getNumbers()
	    {
        	return numbers;
	    }
	    void setNumbers(int n)
	    {
        	for (int i=0; i<size; i++)
	        {
        	    numbers[i] = numbers[i] + n;
	        }
	    }
	};

	ostream& operator<<(ostream& out, Numbers &n)
	{
	    for (int i=0; i<n.getSize(); i++)
	    {
        	out <<n.getNumbers()[i]<<"\t";
	    }
	    return out;
	}

	Numbers& operator+=(Numbers& n, int i)
	{
	    n.setNumbers(i);
	    return n;
	}

	int * operator+(Numbers& n1, Numbers& n2)
	{
	    int *obj = new int[n1.getSize()];
	    int temp = 0;
	    for (int i=0; i<n1.getSize(); i++)
	    {
        	temp = n1.getNumbers()[i] + n2.getNumbers()[i];
	        obj[i] = temp;
	    }
	    return obj;
    
	}

	int main()
	{
	    int arr1[5] = {2, 4, 6, 8, 10};
	    int arr2[5] = {1, 2, 3, 4, 5};
    
	    int size1 = sizeof(arr1)/sizeof(arr1[0]);
	    int size2 = sizeof(arr2)/sizeof(arr2[0]);
    
	    Numbers numbers1 = Numbers(arr1, size1);
	    Numbers numbers2 = Numbers(arr2, size2);
        
	    cout <<"Array 1: "<<numbers1<<endl;
	    cout <<"Array 2: "<<numbers2<<endl;
    
	    int * obj = numbers1+numbers2;
    
	    cout <<"\nSum of arrays: "<<endl;
    
	    for (int i=0; i<size1; i++)
	    {
        	cout <<obj[i]<<"\t";
	    }
    
	    cout <<endl;
    
	    delete[] obj;
    
	    cout <<"Testing += operator..."<<endl;
    
	    numbers1+=2;
    
    	    cout <<"\nModified Array 1: "<<numbers1<<endl;
    
            return 0;
	}
```
7. Operator as member functions
```
	#include <iostream>
	#include <cstring>

	using namespace std;

	class Vehicle
	{
	    private:
	    char * name;
	    int kms;
	    int passengers;
    
    	public:
	    Vehicle(const char * n, int k, int p)
	    {
        	name = new char[strlen(n) + 1];
	        strcpy(name, n);
        	kms = k;
	        passengers = p;
	    }
	    char * getName()
	    {
        	return name;
	    }
	    int getKMs()
	    {
        	return kms;
	    }
	    int getPassengers()
	    {
        	return passengers;
	    }
	    void setPassengers(int p)
	    {	
	        passengers = p;
	    }
	    ~Vehicle()
	    {
        	delete[] name;
	    }
            bool operator==(Vehicle &v)
	    {
          	  return (strcmp(name, v.name) == 0 && kms == v.kms && passengers == v.passengers);
            }
	};

	int main()
	{
	    Vehicle v1 = Vehicle("Toyota RAV4", 1234, 4);
	    Vehicle v2 = Vehicle("Toyota RAV4", 1234, 4);
    
    	    if (v1==v2)
	    {
        	cout <<"Similar"<<endl;
	    }
	    else
	    {
        	cout <<"Not Similar"<<endl;
	    }
    
    	    return 0;
	}
```
8. Overloading `+=` as a member function
```
	#include <iostream>
	#include <cstring>

	using namespace std;

	class Vehicle
	{
	    private:
	    char * name;
	    int kms;
	    int passengers;
    
    	public:
	    Vehicle(const char * n, int k, int p)
	    {
        	name = new char[strlen(n) + 1];
	        strcpy(name, n);
        	kms = k;
	        passengers = p;
	    }
	    char * getName()
	    {
        	return name;
	    }
	    int getKMs()
	    {
        	return kms;
	    }
	    int getPassengers()
	    {
        	return passengers;
	    }
	    void setPassengers(int p)
	    {	
	        passengers = p;
	    }
	    ~Vehicle()
	    {
        	delete[] name;
	    }
            bool operator==(Vehicle &v)
            {
    	        return (strcmp(name, v.name) == 0 && kms == v.kms && passengers == v.passengers);
            }
            Vehicle& operator+=(int i)
            {
    	        passengers = passengers + i;
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
	    Vehicle v1 = Vehicle("Toyota RAV4", 1234, 4);
	    v1+=2;
    
	    cout <<v1<<endl;

	    return 0;
	}
```

9. In order to make `ostream& operator<<` as a member function, you need to use an indirect method as ostream& operator<< cannot write to ostream object.
```
	#include <iostream>
	#include <cstring>

	using namespace std;

	class Vehicle
	{
	    private:
	    char * name;
	    int kms;
	    int passengers;
    
    	public:
	    Vehicle(const char * n, int k, int p)
	    {
        	name = new char[strlen(n) + 1];
	        strcpy(name, n);
        	kms = k;
	        passengers = p;
	    }
	    char * getName()
	    {
        	return name;
	    }
	    int getKMs()
	    {
        	return kms;
	    }
	    int getPassengers()
	    {
        	return passengers;
	    }
	    void setPassengers(int p)
	    {	
	        passengers = p;
	    }
	    ~Vehicle()
	    {
        	delete[] name;
	    }
            bool operator==(Vehicle &v)
            {
            	return (strcmp(name, v.name) == 0 && kms == v.kms && passengers == v.passengers);
            }
            Vehicle& operator+=(int i)
            {
           	passengers = passengers + i;
            	return *this;
            }
            ostream& display(ostream& out)
            {
                out <<"Name: "<<name<<endl;
                out <<"KMs: "<<kms<<endl;
                out <<"Passengers: "<<passengers<<endl;
                return out;
            }
	};

        ostream& operator<<(ostream& out, Vehicle& vehicle)
        {
       		return vehicle.display(out);
	}

	int main()
	{
	    Vehicle v1 = Vehicle("Toyota RAV4", 1234, 4);
   
	    cout <<v1<<endl;

            return 0;
	}
```

10. Friend functions are used to allow friends of the class to use its private and protected members.
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
11. Friend Functions can be handy with operator overloading
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
```
