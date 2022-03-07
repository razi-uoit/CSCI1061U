# Week 8 Class Code: Virtual Functions and Abstract Classes

A class’s Destructor is called implicitly when an object is destroyed
```
	#include <iostream>
	using namespace std;

	class Vehicle
	{
	private:
		int* sensors;
	public:
		Vehicle()
		{
			sensors = new int[25];
			cout << "Default Constructor called" << endl;
		}
		void drive()
		{
			cout << "Vehicle can drive  "<< endl;
		}
		~Vehicle()
		{
			delete[] sensors;
			sensors = nullptr;
			cout << "Destructor called" << endl;
		}
	};

	int main()
	{
		Vehicle vehicle;
		vehicle.drive();
		return 0;
	}
```
Constructors in Single Inheritance.  
The code below would result in an error as Car constructor is trying to implicitly call the default vehicle constructor.
```
	#include <iostream>
	using namespace std;

	class Vehicle
	{
	protected:
		string name;
		int kms;

	public:
		Vehicle(string name, int kms)
		{
			this->name = name;
			this->kms = kms;
		}
		void drive()
		{
			cout << "Vehicle is driving" << endl;
		}
	};

	class Car: public Vehicle
	{
	public:	
		Car(string name, int kms)
		{
			this->name = name;
			this->kms = kms;
		}
		void drive()
		{
			cout << "Car is driving" << endl;
		}
		void goToPicnic()
		{
			cout << "Going to picnic" << endl;
		}
	};

	int main()
	{
		Car car("Toyota", 123);
		car.drive();
		return 0;
	}
```
In order to fix the above code, one way is to create a default constructor for the Vehicle class
```
	#include <iostream>
	using namespace std;

	class Vehicle
	{
	protected:
		string name;
		int kms;

	public:
		Vehicle()
		{
			this->name = "";
			this->kms = 0;
			cout << "Default Vehicle Constructor called..." << endl;
		}
		Vehicle(string name, int kms)
		{
			this->name = name;
			this->kms = kms;
		}
		void drive()
		{
			cout << "Vehicle is driving" << endl;
		}
	};	

	class Car : public Vehicle
	{
	public:	
		Car()
		{
			cout << "Car Default Constructor called..." << endl;
		}
		Car(string name, int kms)
		{
			this->name = name;
			this->kms = kms;
			cout << "Car Parameterized Constructor called..." << endl;
		}
		void drive()
		{
			cout << "Car is driving" << endl;
		}
		void goToPicnic()
		{
			cout << "Going to picnic" << endl;
		}
	};	

	int main()
	{
		Car car1 = Car("Toyota", 123);
		Car car2 = Car();

		car1.drive();
		car2.drive();
		return 0;
	}
```
Destructors are called in opposite order in inheritance
```
	#include <iostream>
	using namespace std;

	class Vehicle
	{
	protected:
		string name;
		int kms;

	public:
		Vehicle()
		{
			this->name = "";
			this->kms = 0;
			cout << "Default Vehicle Constructor called..." << endl;
		}
		Vehicle(string name, int kms)
		{
			this->name = name;
			this->kms = kms;
		}
		void drive()
		{
			cout << "Vehicle is driving" << endl;
		}
		~Vehicle()
		{
			cout << "Vehicle Destructor called..." << endl;
		}
	};	

	class Car : public Vehicle
	{
	public:	
		Car()
		{
			cout << "Car Default Constructor called..." << endl;
		}
		Car(string name, int kms)
		{
			this->name = name;
			this->kms = kms;
			cout << "Car Parameterized Constructor called..." << endl;
		}
		void drive()
		{
			cout << "Car is driving" << endl;
		}
		void goToPicnic()
		{
			cout << "Going to picnic" << endl;
		}
		~Car()
		{
			cout << "Car Destructor called..." << endl;
		}
	};

	int main()
	{
		Car car1 = Car("Toyota", 123);
		car1.drive();
	
		return 0;
	}
```
Explicitly calling the constructor
```
	#include <iostream>
	using namespace std;

	class Vehicle
	{
	protected:
		string name;
		int kms;

	public:
		Vehicle()
		{
			this->name = "";
			this->kms = 0;
			cout << "Vehicle Default Constructor called" << endl;
		}
		Vehicle(string name, int kms)
		{
			this->name = name;
			this->kms = kms;
			cout << "Vehicle Parameterized Constructor called" << endl;
		}
		void drive()
		{
			cout << "Vehicle is driving" << endl;
		}
	};

	class Car: public Vehicle
	{
	public:
		Car(string name, int kms): Vehicle(name, kms)
		{
			this->name = name;
			this->kms = kms;
			cout << "Car Constructor called" << endl;
		}
		void drive()
		{
			cout << "Car is driving" << endl;
		}
		void goToPicnic()
		{
			cout << "Going to picnic" << endl;
		}
	};

	int main()
	{
		Car car("Toyota", 123);
		car.drive();
		return 0;
	}
```
Constructors in Multiple Inheritance.  
In multiple inheritance, constructors are called based on their order of inheritance
```
	#include <iostream>
	using namespace std;

	class Phone
	{
	protected:
		int speed;
	public:
		Phone()
		{
			speed = 0;
			cout << "Phone constructor called" << endl;
		}
		Phone(int speed)
		{
			this->speed = speed;
			cout << "Phone Parameterized constructor called" << endl;
		}
		void makeCalls()
		{
			cout << "I can make calls with speed: "<<speed << endl;
		}
	};		

	class SmartPhone
	{
	protected:
		int wiFi;
	public:
		SmartPhone()
		{
			wiFi = 0;
			cout << "Smart Phone constructor called" << endl;
		}
		SmartPhone(int wiFi)
		{	
			this->wiFi = wiFi;
			cout << "Smart Phone Parameterized constructor called" << endl;
		}
		void browseInternet()
		{
			cout << "I can browse Internet with WiFi speed: "<<wiFi << endl;
		}	
	};

	class Android: public Phone, public SmartPhone
	{
	public:	
		Android(int speed, int wiFi): Phone(speed), SmartPhone(wiFi)
		{
			cout << "Android Parameterized constructor called" << endl;
			this->speed = speed;
			this->wiFi = wiFi;
		}	
		Android()
		{
			cout << "Android constructor called" << endl;
		}
		void iAmAndroid()
		{
			cout << "I am Android" << endl;
		}
	};
	int main()
	{
		Android android1;
		android1.iAmAndroid();
		android1.makeCalls();
		android1.browseInternet();
	
		Android android2 = Android(24000, 5);
		android2.iAmAndroid();
		android2.makeCalls();
		android2.browseInternet();

		return 0;
	}
```
Virtual functions are used to make calls to the child's overridden function
```
	#include <iostream>
	using namespace std;

	class Vehicle
	{
	public:
		virtual void drive()
		{
			cout << "Vehicle can drive" << endl;
		}
	};

	class Car : public Vehicle
	{
	public:
		void goToPicnic()
		{
			cout << "Going to Picnic" << endl;
		}
		void drive()
		{
			cout << "Car can drive" << endl;
		}
	};

	class Truck : public Vehicle
	{
	public:
		void carryGoods()
		{
			cout << "Carrying Goods" << endl;
		}
	};
	int main()
	{
		Car car;
		Truck truck;
	
		Vehicle* vehicle[2];
		vehicle[0] = &car;
		vehicle[1] = &truck;
	
		vehicle[0]->drive();
		vehicle[1]->drive();
	
		return 0;
	}	
```
`If child has no overridden function then virtual function would call itself through parent.`

Abstract classes are the classes from which you never intend to instantiate any objects.

`The code below will produce an error since abstract class requires all of its virtual functions to be implemented in child classes`
```
	#include <iostream>
	using namespace std;

	class Vehicle
	{
	public:
		virtual void drive() = 0
		{
			cout << "Vehicle can drive" << endl;
		}
	};

	class Car : public Vehicle
	{
	public:	
		void goToPicnic()
		{
			cout << "Going to Picnic" << endl;
		}
		void drive()
		{
			cout << "Car can drive" << endl;
		}
	};

	class Truck : public Vehicle
	{
	public:	
		void carryGoods()
		{
			cout << "Carrying Goods" << endl;
		}
	
	};
	int main()
	{
		Car car;
		Truck truck;

		Vehicle* vehicle[2];
		vehicle[0] = &car;
		vehicle[1] = &truck;

		vehicle[0]->drive();
		vehicle[1]->drive();

		return 0;
	}
```
Abstract Classes can be non-virtual or non-pure-virtual functions
```
	class Vehicle
	{
	public:
		virtual void drive() = 0
		{
			cout << "Vehicle can drive" << endl;
		}
		void startEngine()
		{
			cout << "Engine started" << endl;
		}
	};

	int main()
	{
		Car car;
		Truck truck;

		Vehicle* vehicle[2];
		vehicle[0] = &car;
		vehicle[1] = &truck;
	
		vehicle[0]->drive();
		vehicle[1]->drive();

		// This is valid
		vehicle[0]->startEngine();
		
		return 0;
	}
```