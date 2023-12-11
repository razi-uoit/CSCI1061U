# Week 9 Class Code: Virtual Functions and Abstract Classes

1. In order to avoid including libraries multiple times, we can use #ifndef

`Vehicle.h`
```
#ifndef VEHICLE_H
#define VEHICLE_H

#include <iostream>
using namespace std;

class Vehicle
{
protected:
	string name;
	int kms;
public:
	Vehicle();
	Vehicle(string name, int kms);
	string getName();
	int getKms();
	void display();

};
#endif
```

`Vehicle.cpp`

```
#include "Vehicle.h"

Vehicle::Vehicle()
{
	this->name = "";
	this->kms = 0;
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
	cout << "Name: " << this->name << endl;
	cout << "Kms: " << this->kms << endl;
}
```
`Car.h`
```
#ifndef CAR_H
#define CAR_H
#include "Vehicle.h"

class Car : public Vehicle
{
public:
	Car();
	Car(string name, int kms);
	void display();
};

#endif
```
`Car.cpp`
```
#include "Car.h"

Car::Car()
{

}
Car::Car(string name, int kms) : Vehicle(name, kms)
{
	this->name = name;
	this->kms = kms;
}
void Car::display()
{
	Vehicle::display();
}
```

`Truck.h`
```
#ifndef TRUCK_H
#define TRUCK_H

#include "Vehicle.h"

class Truck : public Vehicle
{
public:
	Truck();
	Truck(string name, int kms);
	void display();
};

#endif
```
`Truck.cpp`
```
#include "Truck.h"

Truck::Truck()
{

}
Truck::Truck(string name, int kms) : Vehicle(name, kms)
{
	this->name = name;
	this->kms = kms;
}
void Truck::display()
{
	Vehicle::display();
}
```
`main.cpp`
```
#include "Car.h"
#include "Truck.h"

int main()
{
	Car car = Car("Toyota", 1234);
	car.display();

	Truck truck = Truck("Hino", 6789);
	truck.display();
	return 0;
}
```
2. Instead of ifndef, we can also use #pragma once but with limited effect.

`Vehicle.h`
```
#pragma once
#include <iostream>
using namespace std;

class Vehicle
{
protected:
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
`Car.h`
```
#pragma once
#include "Vehicle.h"

class Car : public Vehicle
{
public:
	Car();
	Car(string name, int kms);
	void display();
};
```
`Truck.h`
```
#pragma once
#include "Vehicle.h"

class Truck : public Vehicle
{
public:
	Truck();
	Truck(string name, int kms);
	void display();
};
```

3. Constructors in Single Inheritance

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
4. Destructors are called in opposite direction in inheritance
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
5. Constructors in Multiple Inheritance

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
6. Parent pointer can hold the address of child objects even inside the functions
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
			cout << "I can drive" << endl;
		}
		void display()
		{
			cout << "Name: " << name << ", KMs: " << kms << endl;
		}
	};

	class Car :public Vehicle
	{
	public:
		Car(string name, int kms) : Vehicle(name, kms)
		{
			this->name = name;
			this->kms = kms;
		}
		void goToPicnic()
		{
			cout << "Going to Picnic" << endl;
		}
	};

	class Truck :public Vehicle
	{
	public:	
		Truck(string name, int kms) : Vehicle(name, kms)
		{
			this->name = name;
			this->kms = kms;
		}
		void carryGoods()
		{
			cout << "Carrying goods" << endl;
		}
	};

	void show(Vehicle& vehicle)
	{
		vehicle.display();
	}

	int main()
	{
		Vehicle vehicle = Vehicle("General Vehicle", 0000);
		Car car = Car("Toyota Rav4", 1234);
		Truck truck = Truck("Hino", 5678);

		show(vehicle);
		show(car);
		show(truck);

		return 0;
	}
```


7. Virtual functions are used to make calls to the child's overridden function
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
If child has no overridden function then virtual function would call itself through parent.

8. Abstract classes are the classes from which you never intend to instantiate any objects.

The code below will produce an error since abstract class requires all of its virtual functions to be implemented in child classes
```
	#include <iostream>
	using namespace std;

	class Vehicle
	{
	public:
		virtual void drive()=0;
		
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
