# Week 10 Class Code: Function Templates, Lambda Functions and Function Pointers

Class templates help in writing classes for multiple data types. However, sometimes you dont want to write generic class but generic functions and hence can use function templates.
```
	#include <iostream>
	using namespace std;

	template<typename T>
	T sum(T x, T y)	
	{
		return x + y;
	}

	int main()
	{
		double x = 5.2, y = 7.4;
		cout << "Sum: " << sum<double>(x, y) << endl;
		return 0;
}
```
In most of the cases, compilers can infer the data type of function templates automatically.
```
	#include <iostream>
	using namespace std;

	template<typename T>
	T sum(T x, T y)
	{
		return x + y;
	}

	int main()
	{
		double x = 5.2, y = 7.4;
		cout << "Sum: " << sum(x, y) << endl;
		return 0;
	}
```
Function templates can accommodate different data types by using multiple datatypes in the definition of the template
```
	#include <iostream>
	using namespace std;

	template<typename T, typename U>
	T sum(T x, U y)
	{
		return x + y;
	}

	int main()
	{
		double x = 5.2;
		int y = 7;
		cout << "Sum: " << sum(x, y) << endl;
		return 0;
	}
```
`auto` can be used to allow c++ to infer the data type based on the initialization value;
```
	int main()
	{
		auto i = 5;
		cout << i << endl;	
		return 0;
	}

	You can use typeid to get the data type;

	#include <iostream>
	#include <typeinfo>
	using namespace std;

	int main()
	{
		auto i = 5;
		cout << i << endl;
		cout << typeid(i).name() << endl;

		return 0;
	}
```
Lambda expressions (or simply lambdas) enable you to define anonymous functions where they’re passed to a function.
```
	#include <iostream>
	using namespace std;

	int main()
	{
		auto helloWorld = []() {cout << "Hello World" << endl; };

		helloWorld();
		return 0;
	}
```
Lambda functions can be used with parameters
```
	int main()
	{
		auto sum = [](int x, int y) {return x + y; };
		cout <<sum(5, 7);
		return 0;
	}
```
`[]` in the lambda expression is a capture list where you can pass variables to be used inside the lambda expression
```
	int main()
	{
		int i = 6;
		auto sum= [i](int x, int y) {return x + y + i; };
		cout <<sum(5, 7);
		return 0;
	}
```
Captured variables are normally read only inside the lambda expression. Modifying them is not allowed. So, below is illegal:
```
	int main()
	{
		int i = 6;
		auto sum = [i](int x, int y) 
		{
			i = 8; // this line produces an error
			return x + y + i; 
		};
		cout <<sum(5, 7);
		return 0;
	}	
```
In order to modify the value of the captured variables, pass them by reference:
```
	int main()
	{
		int i = 6;
		auto sum = [&i](int x, int y) 
		{
			i = 8; // this is legal as the variable is passed by reference
			return x + y + i; 
		};
		cout <<sum(5, 7);
		return 0;
	}
```
Putting a `=` sign in the capture list will automatically allow the usage of local variables by value
```
	int main()
	{
		int i = 6;
		auto sum = [=](int x, int y)
		{
			return x + y + i; 
		};
		cout << sum(5, 7);
		return 0;
	}
```
Putting a `&` sign in the capture list will automatically allow the usage of local variable by reference
```
	int main()
	{
		int i = 6;
		auto sum = [&](int x, int y)
		{
			i = 2;
			return x + y + i; 
		};
		cout << sum(5, 7);
		return 0;
	}
```
Mix and match is possible for capture list as well. Below code passes everything by reference except j which is passed by value
```
	int main()
	{
		int i = 6;
		int j = 5;
		auto sum = [&, j](int x, int y)
		{
			i = 2;
			return x + y + i + j; 
		};
		cout << sum(5, 7);
		return 0;
	}
```
Using Lambda function with vectors.  

Finding sum of vector elements without using lambda function
```
	int sumElements(vector<int>& v)
	{
		int sum = 0;
		for (int i = 0; i < v.size(); i++)
		{
			sum += v[i];
		}
		return sum;
	}

	int main()
	{
		vector<int> v = { 1, 2, 3, 4, 5 };
		cout << "Sum: " << sumElements(v) << endl;

		return 0;
	}
```
Finding sum of vector elements using lambda function
```
	#include <iostream>
	#include <vector>
	#include <algorithm>
	using namespace std;

	int main()
	{
		int sum = 0;
		vector<int> v = { 1, 2, 3, 4, 5 };
		for_each(begin(v), end(v), [&sum](int x) {sum += x; });

		cout << "Sum: " << sum << endl;

		return 0;
	}
```
Sorting the vectors using Lambda functions
```
	#include <iostream>
	#include <vector>
	#include <algorithm>
	using namespace std;

	int main()
	{
	
		vector<int> v = { 8, 1, 5, 10, 6, 9, 12 };
	
		cout << "Unsorted Vector..." << endl;
		for_each(begin(v), end(v), [](int x) {cout << x << ' '; });

		sort(begin(v), end(v), [](int a, int b) {return a < b; });

		cout << "\nSorted Vector..." << endl;
		for_each(begin(v), end(v), [](int x) {cout << x << ' '; });
	
		return 0;
	}
```
Function Pointers are pointers, i.e. variables, which point to an address of a function.

The program below will show the address of a function
```
	void helloWorld()
	{
		cout << "Hello World" << endl;
	}

	int main()
	{
	
		cout <<helloWorld;
		return 0;
	}
```
A function pointer can make a pointer point to a function
```
	void helloWorld()
	{
		cout << "Hello World" << endl;
	}
	
	int main()
	{
		void(*ptr)() = helloWorld;
		ptr();
		return 0;
	}
```
Function pointers can point to function that return a datatype and take data types as parameters:
```
	int sum(int a, int b)
	{
		return a + b;
	}

	int main()
	{
		int(*sumPtr)(int, int) = sum;
		cout << sumPtr(5, 7);
	
		return 0;
	}
```
Function pointers can be very handy for optimizing the code
```
	int sum(int a, int b)
	{
		return a + b;
	}	
	int subtract(int a, int b)
	{
		return a - b;
	}
	int multiply(int a, int b)
	{
		return a * b;
	}

	int main()
	{
		int(*ptr[3])(int, int) = { sum, subtract, multiply };
		int choice;
		
		cout << "0. Add" << endl;
		cout << "1. Subtract" << endl;
		cout << "2. Multiply" << endl;
		cout << "Enter your choice: ";
		cin >> choice;

		cout << "Result: " << ptr[choice](5, 7) << endl;

		return 0;
	}
```