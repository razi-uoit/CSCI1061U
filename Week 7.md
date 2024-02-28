# Abstraction, Encapsulation, Inheritance and Polymorphism

1. Sometimes similar code is required to be used in multiple classes.
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
2. To avoid duplication of code, we can use inheritance by defining a parent class and making other classes as child classes
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
3. Access Modifier protected is used to access members in inherited classes
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
4. Multiple inheritance is the concept where a class can be inherited from multiple classes
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
5. Multi-Level Inheritance is where a chain of inheritance is followed
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
6. Function overriding is a concept where you'd like to override the behavior of a parent function. In this case the overridden function will be the one called by the child
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
7. Polymorphism is a concept where a parent can take a form of its children
```
	#include<iostream>
	using namespace std;

	class Vehicle
	{
		public:
		void drive()
		{
			cout <<"I can drive"<<endl;
		}
	};

	class Car: public Vehicle
	{
		public:
		void drive()
		{
			cout <<"I am Car and I can drive"<<endl;
		}
		void goToPicnic()
		{
			cout <<"Going to Picnic"<<endl;
		}
	};

	class Truck: public Vehicle
	{
		public:
		void drive()
		{
			cout <<"I am a Truck and I can drive"<<endl;
		}
		void carryGoods()
		{
			cout <<"Carrying Goods"<<endl;
		}
	};

	int main(int argc, char * argv[])
	{
		Car car;
		Truck truck;
		
		Vehicle *vehicles[2];
		vehicles[0] = &car;
		vehicles[1] = &truck;
		
		vehicles[0]->drive();
		vehicles[1]->drive();
		
		return 0;
	}
```

8. Above program can also be written for storing child objects in the heap memory
```

	int main(int argc, char * argv[])
	{
		
		Vehicle *vehicles[2];
		vehicles[0] = new Car();
		vehicles[1] = new Truck();
		
		vehicles[0]->drive();
		vehicles[1]->drive();
		
		delete vehicles[0];
		delete vehicles[1];
		
		return 0;
	}
```
9. Specific functions based on child objects can also be accessed using Polymorphism
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
10. We can use vectors instead of arrays to hold the parent pointer
```
	#include<iostream>
	#include<vector>
	using namespace std;

	class Employee
	{
		protected:
		double salary;
		
		public:
		Employee()
		{
			this->salary = 0.0;
		}
		double getSalary()
		{
			return this->salary;
		}
		void setSalary(double salary)
		{
			this->salary = salary;
		}
	};

	class FullTime : public Employee
	{
		public:
		FullTime()
		{
			salary = 5000.0;
		}
	};

	class PartTime : public Employee
	{
		public:
		PartTime()
		{
			salary = 2000.0;
		}
	};


	int main()
	{
		FullTime fullTime1;
		FullTime fullTime2;
		PartTime partTime1;
		PartTime partTime2;
		
		fullTime1.setSalary(6000.0);
		fullTime2.setSalary(8000.0);
		partTime1.setSalary(2000.0);
		partTime2.setSalary(3000.0);
		
		vector<Employee*> employees;
		employees.push_back(&fullTime1);
		employees.push_back(&fullTime2);
		employees.push_back(&partTime1);
		employees.push_back(&partTime2);
		
		double totalSalary = 0.0;
		
		for (int i=0; i<employees.size(); i++)
		{
			totalSalary = totalSalary + employees[i]->getSalary();
		}
		
		cout <<"Total Salary: "<<totalSalary<<endl;
		
		
		return 0;
	}
```
11. Even Odd exercise solution
```
#include <iostream>
#include <random>
using namespace std;

class Numbers
{
protected:
	int even_count;
	int odd_count;
public:
	Numbers()
	{
		even_count = 0;
		odd_count = 0;
	}
	void incrementEvenCount(int count)
	{
		this->even_count += count;
	}
	void incrementOddCount(int count)
	{
		this->odd_count+= count;
	}
};

class Even: public Numbers
{
public:
	Even()
	{

	}
	void showEvenCount()
	{
		cout << "Even count: " << even_count << endl;
	}

};

class Odd: public Numbers
{
public:
	Odd()
	{

	}
	void showOddCount()
	{
		cout << "Odd count: " << odd_count << endl;
	}
};


int generateRandomNumber()
{
	random_device rd;
	mt19937 gen(rd());

	uniform_int_distribution<> distrib(1, 100);

	return  distrib(gen);
}

int main()
{
	Numbers* numbers;
	Numbers* arr[10];

	int number, even_count = 0, odd_count = 0;
	for (int i = 0; i < 10; i++)
	{
		number = generateRandomNumber();
		cout << "Random Number generated: " << number << endl;
		if (number % 2 == 0)
		{
			even_count++;
			Even even;
			arr[i] = &even;
			arr[i]->incrementEvenCount(even_count);
			even.showEvenCount();
		}
		else
		{
			odd_count++;
			Odd odd;
			arr[i] = &odd;
			arr[i]->incrementOddCount(odd_count);
			odd.showOddCount();
		}
	}

	return 0;
}
```
