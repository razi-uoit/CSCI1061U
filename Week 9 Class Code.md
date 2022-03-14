# Week 8 Class Code: Namespaces, Templates and STLs
A namespace is a declarative region that provides a scope to the identifiers (the names of types, functions, variables, etc) inside it. 

Vehicle.h
```
	#include <iostream>
	using namespace std;

	namespace space1 {
		class Vehicle
		{	
		private:
			string name;
			int kms;

		public:
			void drive()
			{
				cout << "I can drive" << endl;
			}
		};
	}
```

AnotherVehicle.h
```
	
	#include <iostream>
	using namespace std;

	namespace space2
	{
		class Vehicle
		{
		private:
			string name;
			int kms;

		public:
			void startEngine()
			{
				cout << "Engine Started" << endl;
			}
		};
	}
```
Source.cpp
```
	#include "Vehicle.h"
	#include "AnotherVehicle.h"

	int main()
	{
		space1::Vehicle v1;
		v1.drive();
	
		space2::Vehicle v2;
		v2.startEngine();

		return 0;
	}
```
Identifiers outside the namespace can access the members by using the fully qualified name for each identifier

Vehicle.h
```
	#include <iostream>
	using namespace std;

	namespace space1 {
		class Vehicle
		{
		private:
			string name;
			int kms;

		public:
			void drive()
			{
				cout << "I can drive" << endl;
			}
		};
		void vehicleGlobalFunction()
		{
			cout << "This is vehicle global function" << endl;
		}
	}
```
AnotherVehicle.h
```
	#include <iostream>
	using namespace std;

	namespace space2
	{
		class Vehicle
		{
		private:
			string name;
			int kms;	

		public:
			void startEngine()
			{
				cout << "Engine Started" << endl;
			}
		};

		void anotherVehicleGlobalFunction()
		{
			cout << "This is another vehicle global function" << endl;
		}
	}
```
Source.cpp
```
	#include "Vehicle.h"
	#include "AnotherVehicle.h"

	int main()
	{
		space1::Vehicle v1;
		v1.drive();
		space1::vehicleGlobalFunction();

		space2::Vehicle v2;
		v2.startEngine();
		space2::anotherVehicleGlobalFunction();

		return 0;
	}
```

Class templates help in writing classes for multiple data types.

The problem here is that it would work for int but not for double or float. To make them work we have to create separate classes for double and float.
```
	#include <iostream>
	using namespace std;

	class X
	{
	private:
		int x;
	public:
		X()
		{
			x = 0;
		}
		X(int x)
		{
			this->x = x;
		}
		int getX()
		{
			return this->x;
		}
	};

	class Y
	{
	private:	
		int y;
	public:
		Y()
		{
			y = 0;
		}
		Y(int y)
		{
			this->y = y;
		}
		int getY()
		{
			return this->y;
		}
	};

	double sum(X obj1, Y obj2)
	{
		return obj1.getX() + obj2.getY();
	}
	
	int main()
	{
		X obj1 = X(5);
		Y obj2 = Y(7);
		cout << "X + Y = " << sum(obj1, obj2) << endl;

		X obj3 = X(5.6);
		Y obj4 = Y(7.8);
		cout << "X + Y = " << sum(obj3, obj4) << endl;
		return 0;
	}
```
Above problem can be solved using templates
```
	#include <iostream>
	using namespace std;

	template <class T>
	class X
	{
	private:
		T x;
	public:
		X()
		{
			x = 0;
		}
		X(T x)
		{
			this->x = x;
		}
		T getX()
		{
			return this->x;
		}
	};

	template <class T>
	class Y
	{
	private:
		T y;
	public:
		Y()
		{
			y = 0;
		}
		Y(T y)
		{
			this->y = y;
		}
		T getY()
		{
			return this->y;
		}
	};	

	int sum(X<int> obj1, Y<int> obj2)
	{
		return obj1.getX() + obj2.getY();
	}
	double sum(X<double> obj1, Y<double> obj2)
	{
		return obj1.getX() + obj2.getY();
	}

	int main()
	{
		X<int> obj1 = X<int>(5);
		Y<int> obj2 = Y<int>(7);
		cout << "X + Y = " << sum(obj1, obj2) << endl;
	
		X<double> obj3 = X<double>(5.6);
		Y<double> obj4 = Y<double>(7.8);
		cout << "X + Y = " << sum(obj3, obj4) << endl;
		return 0;
	}
```	
Creating a vector class with and without templates

Without templates:
```
	#include <iostream>
	using namespace std;

	class Vector
	{
	private:
		int* numbers;
		int size;
	public:
	
		Vector(int size)
		{
			this->size = size;
			this->numbers = new int[size];
		}
		void addElements()
		{
			cout << "Enter " << size << " elements..." << endl;

			for (int i = 0; i < size; i++)
			{
				cout << "numbers[" << i<<"] = ";
				cin >> numbers[i];
			}
		}
		int sumElements()
		{	
			int sum = 0;
			for (int i = 0; i < size; i++)
			{
				sum += numbers[i];
			}
			return sum;
		}
	};

	int main()
	{
		Vector v1(5);
		v1.addElements();
		cout << "Sum: " << v1.sumElements();
		return 0;
	}
```
With templates:
```
	#include <iostream>
	using namespace std;

	template<class T>
	class Vector
	{
	private:
		T* numbers;
		int size;
	public:
	
		Vector(int size)
		{
			this->size = size;
			this->numbers = new T[size];
		}
		void addElements()
		{
			cout << "Enter " << size << " elements..." << endl;
	
			for (int i = 0; i < size; i++)
			{
				cout << "numbers[" << i<<"] = ";
				cin >> numbers[i];
			}
		}
		T sumElements()
		{
			T sum = 0;
			for (int i = 0; i < size; i++)
			{
				sum += numbers[i];
			}
			return sum;
		}
	};

	int main()
	{
		Vector<float> v1(5);
		v1.addElements();
		cout << "Sum: " << v1.sumElements();

		return 0;
	}
```
Implementing a Stack using Templates
```
	#include <iostream>
	#include<vector>
	using namespace std;

	template<class T>
	class Stack
	{
	private:
		vector<T> stack;
	public:
		void pushToStack(T element)
		{
			stack.push_back(element);
		}
		void popFromStack()
		{
			stack.pop_back();
		}
		void display()
		{
			cout << "Elements of stack from top to bottom:"<<endl;
			for (int i = stack.size()-1; i >= 0; i--)
			{
				cout << "Element[" << i << "] = " << stack[i] << endl;
			}

		}
	};

	int main()
	{
		Stack<float> stack;
		float number = 0;
		for (int i = 0; i < 5; i++)
		{
			cout << "Enter Element " << i << ": ";
			cin >> number;
	
			stack.pushToStack(number);
		}
		stack.display();

		stack.popFromStack();
	
		stack.display();
		return 0;
	}
```

Stack in STL
```
	#include <iostream>
	#include<stack>
	using namespace std;

	int main()
	{
		stack<int> s1;
	
		int number;

		for (int i = 0; i < 5; i++)
		{
			cout << "Enter a number: ";
			cin >> number;
			s1.push(number);
		}
		cout << "Elements of the stack..." << endl;
	
		while (!s1.empty())
		{

			cout << s1.top()<<endl;
			s1.pop();	
		}
	
		return 0;
	}

```
Array in STL
```
	#include <iostream>
	#include<array>
	using namespace std;

	int main()
	{
		array<int, 5> arr;

		int number = 0;
		for (int i = 0; i < arr.size(); i++)
		{
			cout << "Enter element : "<<i<<": ";
			cin >> number;
			arr[i] = number;
		}

		for (int i = 0; i < arr.size(); i++)
		{
			cout << "arr[" << i << "] = " << arr[i] << endl;
		}
	return 0;
	}
```