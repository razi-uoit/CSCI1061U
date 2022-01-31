# Week 3 Class Code : Dynamic Memory

### Static Memory is held at the load time

	#include <iostream>
	using namespace std;

	string even(int number)
	{
		string flag = "Not Even";

		if (number % 2 == 0)
		{
			flag = "even";
		}

		return flag;
	}

	string odd(int number)
	{
		string flag = "Not odd";

		if (number % 2 != 0)
		{
			flag = "odd";
		}

		return flag;
	}

	int main()
	{
		int number;
		cout << "Enter a number: ";
		cin >> number;

		string result = even(number);
		cout << "Result: " << result<<endl;
		result = odd(number);
		cout << "Result: " << result << endl;
		return 0;
	}

#### Dynamic Memory

	int main()
	{

		// variable created in stack
		int number = 7;
		cout << "Number in stack: " << number << endl;	

		// variable created in heap
		int* ptr = new int;
		*ptr = 7;
		cout << "Number in heap: " << *ptr << endl;

		return 0;
	}

#### Dynamic Memory for Arrays

	int main()
	{
		// arrays created in stack
		int numbers[5] = {5, 7, 8, 33, 44};

		// arays created in heap
		int* ptr = new int[5];
		ptr[0] = 13;
		ptr[1] = 14;
		ptr[2] = 15;
		ptr[3] = 16;
		ptr[4] = 17;

		return 0;
	}

#### Dynamic Memory for Dynamic Arrays

	#include <iostream>
	using namespace std;

	int main()
	{
		int size;
		cout << "Enter the size of the Array: ";
		cin >> size;

		int* numbersPtr = new int[size];
		int number;
		for (int i = 0; i < size; i++)
		{
			cout << "Enter element " << i << ": ";
			cin>>number;
			*(numbersPtr + i) = number;
		}
		cout << "Values entered... " << endl;
		for (int i = 0; i < size; i++)
		{
			cout << "numbersPtr[" << i << "] = " << *(numbersPtr + i) << endl;
		}
		return 0;
	}

#### Dynamic Memory for Objects

	#include <iostream>
	using namespace std;

	class Vehicle
	{
	private:
		string name, make, color;
	public:
		Vehicle(string name, string make, string color)
		{
			this->name = name;
			this->make = make;
			this->color = color;
		}
		void display()
		{
			cout << "Make is " << make << ", Color is " << color << ", Name is " << name << endl;
		}
	};

	int main()
	{
		Vehicle corolla = Vehicle("Corolla", "Toyota", "White");
		corolla.display();
	
		Vehicle* ptrVehicle = new Vehicle("Corolla", "Toyota", "White");
		(*ptrVehicle).display();

		return 0;
	}

#### Memory Leak

	int main()
	{
		int* ptr = new int;
		*ptr = 7;
		cout << "Ptr: " << *ptr << endl;
		cout << "Ptr Address: " << ptr << endl;
		ptr = new int;
		*ptr = 10;

		cout << "Ptr: " << *ptr << endl;
		cout << "Ptr Address: " << ptr << endl;

		return 0;
	}

#### Memory Deallocation

	int main()
	{
		int* ptr = new int;
		*ptr = 7;
		cout << "Ptr: " << *ptr << endl;
		cout << "Ptr Address: " << ptr << endl;

		delete ptr;
		ptr = new int;
		*ptr = 10;

		cout << "Ptr: " << *ptr << endl;
		cout << "Ptr Address: " << ptr << endl;

		return 0;
	}
	
#### Memory Deallocation with Arrays

	int main()
	{
		int* ptr = new int[5];
		ptr[0] = 2;
		ptr[1] = 4;
		ptr[2] = 6;
		ptr[3] = 8;
		ptr[4] = 10;

		delete[] ptr;

		for (int i = 0; i < 5; i++)
		{
			cout << "ptr[" << i << "] = " << *(ptr + i) << endl;
		}

		return 0;
	}

#### Memory Leaks in Functions

	void someFunction()
	{
		int* ptr = new int(10);
	}
	int main()
	{
		someFunction();
		return 0;
	}
