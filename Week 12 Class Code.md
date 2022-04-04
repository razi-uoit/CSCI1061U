# Week 12 Class Code: Exception Handling and Modular Programming

The program below would break because of dividing by 0
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
To fix the above program, we can use Exception Handling
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
You can catch exceptions in general as well
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
Out of Range Exception: The code below will crash the program by throwing an exception
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
Uptil now, we have been programming like below:
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
Inheritance would work in the same fashion

`Vehicle.h`
```
	#pragma once
	#include <iostream>
	class Vehicle
	{
	private:
		std::string name;
		int kms;
	public:
		Vehicle();
		Vehicle(std::string name, int kms);
		std::string getName();
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
	Vehicle::Vehicle(std::string name, int kms)
	{
		this->name = name;
		this->kms = kms;
	}
	std::string Vehicle::getName()
	{
		return this->name;
	}
	int Vehicle::getKms()
	{
		return this->kms;
	}
	void Vehicle::display()
	{
		std::cout << "Name: " << this->name << ", KMs: " << this->kms << std::endl;
	}
```
`Car.h`
```
	#include "Vehicle.h"

	class Car : public Vehicle
	{
	private:
		std::string color;
	public:
		Car(std::string name, int kms, std::string color);
		void goToPicnic();
	};
```
`Car.cpp`
```
	#include "Car.h"

	Car::Car(std::string name, int kms, std::string color) : Vehicle(name, kms)
	{
		this->color = color;
	}
	void Car::goToPicnic()
	{
		std::cout << "Going to Picnic" << std::endl;
	}

	main.cpp

	#include "Car.h"

	int main()
	{
		Vehicle vehicle = Vehicle("Toyota Rav4", 1234);
		vehicle.display();

		Car car = Car("Honda CRV", 4567, "Red");
		car.display();
		return 0;
	}	
```
Operator Overloading would work in a similar manner

`Vehicle.h`
```
	#pragma once
	#include <iostream>
	class Vehicle
	{
	protected:
		std::string name;
		int kms;
	public:
		Vehicle();
		Vehicle(std::string name, int kms);
		std::string getName();
		int getKms();
		void setKms(int kms);
		void display();
	};

	Vehicle& operator+=(Vehicle& v, int value);

	Vehicle.cpp

	#include "Vehicle.h"

	Vehicle::Vehicle()
	{
		name = "";
		kms = 0;
	}
	Vehicle::Vehicle(std::string name, int kms)
	{
		this->name = name;
		this->kms = kms;
	}
	std::string Vehicle::getName()
	{
		return this->name;
	}
	int Vehicle::getKms()
	{
		return this->kms;
	}
	void Vehicle::display()
	{
		std::cout << "Name: " << this->name << ", KMs: " << this->kms << std::endl;
	}
	void Vehicle::setKms(int kms)
	{
		this->kms = kms;
	}

	Vehicle& operator+=(Vehicle& V, int value)
	{
		V.setKms(V.getKms() + value);
		return V;

	}
```
No change in Car.h and Car.cpp

`main.cpp`
```
	#include "Car.h"

	int main()
	{
		Vehicle vehicle = Vehicle("Toyota Rav4", 1234);
		vehicle.display();

		Car car = Car("Honda CRV", 4567, "Red");
		car.display();

		vehicle += 1;
		vehicle.display();
		return 0;
	}
```
Namespaces are used in a similar manner

`Vehicle.h`
```
	#pragma once
	#include <iostream>

	namespace ontariotech
	{
		class Vehicle
		{
		protected:
			std::string name;
			int kms;
		public:
			Vehicle();
			Vehicle(std::string name, int kms);
			std::string getName();
			int getKms();
			void setKms(int kms);
			void display();
		};

		Vehicle& operator+=(Vehicle& v, int value);
	}
```
`Vehicle.cpp`
```
	#include "Vehicle.h"

	namespace ontariotech
	{
		Vehicle::Vehicle()
		{
			name = "";
			kms = 0;
		}
		Vehicle::Vehicle(std::string name, int kms)
		{
			this->name = name;
			this->kms = kms;
		}
		std::string Vehicle::getName()
		{
			return this->name;
		}
		int Vehicle::getKms()
		{
			return this->kms;
		}
		void Vehicle::display()
		{
			std::cout << "Name: " << this->name << ", KMs: " << this->kms << std::endl;
		}
		void Vehicle::setKms(int kms)
		{
			this->kms = kms;
		}

		Vehicle& operator+=(Vehicle& V, int value)
		{
			V.setKms(V.getKms() + value);
			return V;
	
		}
	}
```
`Car.h`
```
	#include "Vehicle.h"

	namespace ontariotech
	{
		class Car : public Vehicle
		{
		private:
			std::string color;
		public:
			Car(std::string name, int kms, std::string color);
			void goToPicnic();
		};
	}
```
`Car.cpp`
```
	#include "Car.h"

	namespace ontariotech
	{
		Car::Car(std::string name, int kms, std::string color) : Vehicle(name, kms)
		{
			this->color = color;
		}
		void Car::goToPicnic()
		{
			std::cout << "Going to Picnic" << std::endl;
		}
	}
```
`main.cpp`
```
	#include "Car.h"
	using namespace ontariotech;
	int main()
	{
		Vehicle vehicle = Vehicle("Toyota Rav4", 1234);
		vehicle.display();

		Car car = Car("Honda CRV", 4567, "Red");
		car.display();

		vehicle += 1;
		vehicle.display();
		return 0;
	}	
```




	
