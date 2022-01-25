# Week 2: Classes and Objects in C++

### Classes are used to create objects
```
	#include<iostream>
	using namespace std;

	class Vehicle
	{
	public: 
		string make, name;

		void carDetails()
		{
			cout << "Make: " << make << endl;
			cout << "Name: " << name << endl;
		}

		void drive()
		{
			cout << "I can drive" << endl;
		}
	};

	int main()
	{
		Vehicle car1;
		car1.name = "A8";
		car1.make = "Audi";
		car1.carDetails();
		car1.drive();

		Vehicle car2;
		car2.name = "Series 7";
		car2.make = "BMW";
		car2.carDetails();
		car2.drive();

		return 0;
	}
```
### Constructor
A constructor is called automatically when an object of a class is created
```
	#include<iostream>
	using namespace std;

	class Vehicle
	{
	public: 
		string make, name;

		Vehicle()
		{
			make = "Audi";
			name = "A8";
		}

		void carDetails()
		{
			cout << "Make: " << make << endl;
			cout << "Name: " << name << endl;
		}

		void drive()
		{
			cout << "I can drive" << endl;
		}
	};

	int main()
	{
		Vehicle car1;
		car1.carDetails();
		car1.drive();
		return 0;
	}
```
Public instance variables can be access directly as well
```
	#include<iostream>
	using namespace std;

	class Vehicle
	{
	public: 
		string make, name;

		Vehicle()
		{
			make = "Audi";
			name = "A8";
		}

		void drive()
		{
			cout << "I can drive" << endl;
		}
	};

	int main()
	{
		Vehicle car1;
		cout << car1.make << endl;
		cout << car1.name << endl;
		car1.drive();
		return 0;
	}
```
### Constructor with parameters
```
	#include<iostream>
	using namespace std;

	class Vehicle
	{
	public: 
		string make, name;

		Vehicle()
		{
			make = "Audi";
			name = "A8";
		}
		Vehicle(string newName, string newMake)
		{
			make = newMake;
			name = newName;
		}

		void drive()
		{
			cout << "I can drive" << endl;
		}
	};

	int main()
	{	
		Vehicle car1 = Vehicle("A8", "Audi");
		cout << car1.make << endl;
		cout << car1.name << endl;

		car1.drive();
		return 0;
	}
```
### Putting classes in separate files
Vehicle.h
```
	#include<iostream>
	using namespace std;
	class Vehicle
	{
	public:
		string make, name;

		Vehicle()
		{
			make = "Audi";
			name = "A8";
		}
		Vehicle(string newName, string newMake)
		{
			make = newMake;
			name = newName;
		}

		void drive()
		{
			cout << "I can drive" << endl;
		}
	};
```
Source.cpp
```
	#include<iostream>
	#include "Vehicle.h"
	using namespace std;

	int main()
	{
		Vehicle car1 = Vehicle("A8", "Audi");
		cout << car1.make << endl;
		cout << car1.name << endl;

		car1.drive();
		return 0;
	}
```
Constructors can be used to create objects from class
```
	#include<iostream>

	using namespace std;

	class Vehicle 
	{
	public: 
		string name, type, color;

		Vehicle()
		{

		}
	
		Vehicle(string newName, string newType, string newColor)
		{
			name = newName;
			type = newType;
			color = newColor;
		}

		void showDetails()
		{
			cout << "Name: " << name << endl;
			cout << "Type: " << type << endl;
			cout << "Color: " << color << endl;
		}
	};

	int main()
	{
		Vehicle car1 = Vehicle("Audi", "Sedan", "White");

		car1.showDetails();
		return 0;
	}
```

Classes are by default private
```
	class Vehicle 
	{
	private:
		string name, type, color;

	public:

		Vehicle(string newName, string newType, string newColor)
		{
			name = newName;
			type = newType;
			color = newColor;
		}

		void showDetails()
		{
			cout << "Name: " << name << endl;
			cout << "Type: " << type << endl;
			cout << "Color: " << color << endl;
		}
	};

	int main()
	{
		Vehicle car1 = Vehicle("Audi", "Sedan", "White");
		car1.showDetails();
		return 0;
	}
```
### Getters and Setters
```

	class Vehicle 
	{
	private:
		string name, type, color;

	public:

		Vehicle(string newName, string newType, string newColor)
		{
			name = newName;
			type = newType;
			color = newColor;
		}

		string getName()
		{
			return name;
		}
		string getType()
		{	
			return type;
		}
		string getColor()
		{
			return color;
		}

		void setName(string sName)
		{
			name = sName;
		}

		void setType(string sType)
		{
			type = sType;
		}
	
		void setColor(string sColor)
		{
			color = sColor;
		}
		void showDetails()
		{
			cout << "Name: " << name << endl;
			cout << "Type: " << type << endl;
			cout << "Color: " << color << endl;
		}
	};

	int main()
	{
		Vehicle car1 = Vehicle("Audi", "Sedan", "White");
		car1.showDetails();
		cout << car1.getColor();
		car1.setColor("Black");
		car1.showDetails();
		return 0;
	}
```

### Arithematics using Objects
```
	#include<iostream>

	using namespace std;

	class X
	{
	private:
		int a;

	public:
		int getA()
		{
			return a;
		}

		void setA(int newA)
		{
			a = newA;
		}
	};

	class Y
	{
	private:
		int b;

	public:
		int getB()
		{
			return b;
		}

		void setB(int newB)
		{
			b = newB;
		}
	};

	int main()
	{
		X obj1 = X();
		obj1.setA(5);

		Y obj2 = Y();
		obj2.setB(6);

		int a = obj1.getA();
		int b = obj2.getB();

		cout << "a: " << a << endl;
		cout << "b: " << b << endl;

		int result = a + b;
		cout << "Result: " << result << endl;
		return 0;
	}

```
Above can also be done directly
```
	int main()
	{
		X obj1 = X();
		obj1.setA(5);

		Y obj2 = Y();
		obj2.setB(6);

		int result = obj1.getA() + obj2.getB();
		cout << "Result: " << result << endl;
		return 0;
	}
```
### Passing objects to the functions
```
	void addObjects(X obj1, Y obj2)
	{
		obj1.setA(5);
		obj2.setB(6);

		int result = obj1.getA() + obj2.getB();
		cout << "Result: " << result << endl;
	}

	int main()
	{
		X obj1 = X();
		Y obj2 = Y();

		addObjects(obj1, obj2);

		return 0;
	}
```