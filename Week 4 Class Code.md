# Week 4 Class Code: Operator Overloading and Friend Functions


Operator overloading is used to use an operator for performing many functions. For example, a '+' operators is used to add int and double

* Adding two integers
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
* Adding two doubles
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
* Concatenating two strings
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
Overloading `<<` operator to display objects on the console
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


Operators as member functions
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

	class Collections
	{
	public:	
		vector<Vehicle> v;

		void operator+=(Vehicle& vehicle)
		{
			v.push_back(vehicle);
		}
	};

	int main()
	{
		Vehicle car1 = Vehicle("Toyota RAV4", 1234);
		Vehicle car2 = Vehicle("Honda CRV", 234);
		Collections collections;

		collections += car1;
		collections += car2;

		return 0;
	}
```
Operators as Global functions
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

	class Collections
	{
	public:
		vector<Vehicle> v;

		void operator+=(Vehicle& vehicle)
		{
			v.push_back(vehicle);
		}
	};

	ostream& operator<<(ostream& output, Collections& collection)
	{
		for (int i = 0; i < collection.v.size(); i++)
		{
			output << collection.v[i].getName() << endl;
			output << collection.v[i].getKms() << endl;
		}
		return output;
	}

	int main()
	{
		Vehicle car1 = Vehicle("Toyota RAV4", 1234);
		Vehicle car2 = Vehicle("Honda CRV", 234);
		Collections collections;
	
		collections += car1;
		collections += car2;
		cout << collections;

		return 0;
	}
```
Overloading Binary Operators (+, - etc)
```
	#include<iostream>
	#include<string>

	using namespace std;

	class Point
	{
	private:	
		int x, y;
	public:
		Point()
		{
			x = 0;
			y = 0;
		}
		Point(int x, int y)
		{
			this->x = x;
			this->y = y;
		}
		int getX()
		{
			return x;
		}
		int getY()
		{
			return y;
		}
		void setX(int x)
		{
			this->x = x;
		}
		void setY(int y)
		{
			this->y = y;
		}

		Point operator+(Point& point)
		{
			Point temp;
			temp.x = this->x + point.x;
			temp.y = this->y + point.y;

			return temp;
		}

	};


	int main()
	{
		Point p1 = Point(4, 5);
		Point p2 = Point(6, 7);
	
		Point result = p1 + p2;
	
		cout << "(" << p1.getX() << "," << p1.getY() << ") + (" << p2.getX() << "," << p2.getY() << ")= (" << result.getX() << "," << 		result.getY() << ")" << endl;
	
		return 0;
	}
```
Friend functions are used to allow friends of the class to use its private and protected members.
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
