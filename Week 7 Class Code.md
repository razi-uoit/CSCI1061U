# Week 7 Class Code: Abstraction, Encapsulation, Inheritance and Polymorphism

Sometimes similar code is required to be used in multiple classes.
```
	class Car
	{
	public:
		void drive()
		{
			cout << "I can drive" << endl;
		}
		void engineStart()
		{
			cout << "Engine started" << endl;
		}
		void engineStop()
		{
			cout << "Engine Stopped" << endl;
		}
		void goToPicnic()
		{
			cout << "Going to Picnic" << endl;
		}
	};

	class Truck
	{
	public:
		void drive()
		{
			cout << "I can drive" << endl;
		}
		void engineStart()
		{
			cout << "Engine started" << endl;
		}
		void engineStop()
		{
			cout << "Engine Stopped" << endl;
		}
		void carryGoods()
		{
			cout << "Carrying Goods" << endl;
		}
	};

	int main()
	{
		Car car;
		Truck truck;
	
		cout << "Car Object..." << endl;
		car.drive();
		car.engineStart();
		car.engineStop();
		car.goToPicnic();

		cout << "Truck Object..." << endl;
		truck.drive();
		truck.engineStart();
		truck.engineStop();
		truck.carryGoods();
		return 0;
	}
```
To avoid duplication of code, we can use inheritance by defining a parent class and making other classes as child classes
```
	#include <iostream>

	using namespace std;

	class Vehicle
	{
	public:
		void drive()
		{
			cout << "I can drive" << endl;
		}
		void engineStart()
		{
			cout << "Engine started" << endl;
		}
		void engineStop()
		{
			cout << "Engine Stopped" << endl;
		}	
	};

	class Car: public Vehicle
	{
	public:
	
		void goToPicnic()
		{
			cout << "Going to Picnic" << endl;
		}
	};

	class Truck: public Vehicle
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

		cout << "Car Object..." << endl;
		car.drive();
		car.engineStart();
		car.engineStop();
		car.goToPicnic();

		cout << "Truck Object..." << endl;
		truck.drive();
		truck.engineStart();
		truck.engineStop();
		truck.carryGoods();
		return 0;
	}
```

Access Modifier protected is used to access members in inherited classes
```
	#include <iostream>

	using namespace std;

	class Vehicle
	{
	private:
		int secret = 0;
	protected:
		int someVariable = 7;
	public:
		void drive()
		{
			cout << "I can drive" << endl;
		}
		void engineStart()
		{
			cout << "Engine started" << endl;
		}
		void engineStop()
		{
			cout << "Engine Stopped" << endl;
		}
	};

	class Car: public Vehicle
	{
	public:	
	
		int getSomeVariable()
		{
			return someVariable;
		}
	
		void goToPicnic()
		{
			cout << "Going to Picnic" << endl;
		}
	};

	class Truck: public Vehicle
	{
	public:	
		void carryGoods()
		{
			cout << "Carrying Goods" << endl;
		}

	};
	
	int main()
	{
		Vehicle vehicle;
		
		Car car;
		Truck truck;

		cout << "Car Object..." << endl;
		car.drive();
		car.engineStart();
		car.engineStop();
		car.goToPicnic();
		cout << car.getSomeVariable()<<endl;

		cout << "Truck Object..." << endl;
		truck.drive();
		truck.engineStart();
		truck.engineStop();
		truck.carryGoods();
		return 0;
	}
```

Multiple inheritance is the concept where a class can be inherited from multiple classes
```
	#include <iostream>

	using namespace std;

	class Phone
	{
	public:
		void makeCalls()
		{
			cout << "I can make calls" << endl;
		}
	};

	class SmartPhone
	{
	public:
		void browseInternet()
		{
			cout << "I can browse Internet" << endl;
		}

	};

	class Android: public Phone, public SmartPhone
	{
	public:	
		void IAmAndroid()
		{
			cout << "I am Android" << endl;
		}
	};

	int main()
	{
		Android android;
		android.IAmAndroid();
		android.makeCalls();
		android.browseInternet();
		return 0;
	}
```
Multi-Level Inheritance is where a chain of inheritance is followed
```
	#include <iostream>

	using namespace std;

	class Phone
	{
	public:
		void makeCalls()
		{
			cout << "I can make calls" << endl;
		}
	};

	class SmartPhone: public Phone
	{
	public:
		void browseInternet()
		{
			cout << "I can browse Internet" << endl;
		}

	};

	class Android: public SmartPhone
	{
	public:
		void IAmAndroid()
		{
			cout << "I am Android" << endl;
		}
	};

	int main()
	{
		Android android;
		android.IAmAndroid();
		android.makeCalls();
		android.browseInternet();
		return 0;
	}
```
Function overriding is a concept where you'd like to override the behavior of a parent function. In this case the overridden function will be the one called by the child
```
	#include <iostream>

	using namespace std;

	class Phone
	{
	public:
		void makeCalls()
		{
			cout << "I can make calls" << endl;
		}
	};

	class SmartPhone: public Phone
	{
	public:	
		void browseInternet()
		{
			cout << "I can browse Internet" << endl;
		}

	};

	class Android: public SmartPhone
	{
	public:
		void IAmAndroid()
		{
			cout << "I am Android" << endl;
		}

		void makeCalls()
		{
			cout << "I can make calls from Android" << endl;
		}
	};

	int main()
	{
		Android android;
		android.IAmAndroid();
		android.makeCalls();
		android.browseInternet();
		return 0;
	}
```
Polymorphism is a concept where a parent can take a form of its children
```
	#include <iostream>

	using namespace std;


	class Vehicle
	{
	protected:
		int kms = 0;
	public:
	
		void drive()
		{
			cout << "I can drive" << endl;
		}
		void engineStart()
		{
			cout << "Engine started" << endl;
		}
		void engineStop()
		{
			cout << "Engine Stopped" << endl;
		}
		void setKMs(int kms)
		{
			this->kms = kms;
		}
	};
	
	class Car: public Vehicle
	{
	public:
	
		void goToPicnic()
		{
			cout << "Going to Picnic" << endl;
		}
		void showKMs()
		{
			cout << "I am a Car and I drove: " << kms << " kms" << endl;
		}
	};

	class Truck: public Vehicle
	{
	public:
	
		void carryGoods()
		{
			cout << "Carrying Goods" << endl;
		}
		void showKMs()
		{
			cout << "I am a Truck and I drove: " << kms << " kms" << endl;
		}
	};

	int main()
	{
		Car car;
		Truck truck;

		Vehicle* vehicle = &car;
		vehicle->setKMs(2000);
	
		car.showKMs();
		truck.showKMs();
		return 0;
    }
```