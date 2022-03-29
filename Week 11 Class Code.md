# Week 11 Class Code: Recursion, Shallow and Deep Copy

A recursive function is a function that calls itself, either directly, or indirectly (through another function).

`Factorial without recursion`
```
	#include <iostream>
	using namespace std;
 
	int factorial(int number)
	{
		int result = 1;
		for (int i = number; i > 1; i--)
		{
			result = result * i;
		}
		return result;
	}
	int main()
	{
		int number;
		cout << "Enter a number to find its factorial: ";
		cin >> number;
 
		cout << "Factorial of " << number << " is: " << factorial(number) << endl;
		return 0;
	}
```
`Factorial with recursion`
```
	#include <iostream>
	using namespace std;

	int factorial(int number)
	{
		if (number <= 1)
		{
			return 1;
		}
		else
		{
			return number * factorial(number - 1);
		}
	}

	int main()
	{
		int number;
		cout << "Enter a number: ";
		cin >> number;

		cout << "Factorial: " << factorial(number) << endl;
		return 0;
	}
```
Power function with and without recursion

`Power without recursion`
```
	#include <iostream>
	using namespace std;

	int power(int base, int exponent)
	{
		int result = 1;

		for (int i =1; i<=exponent; i++)
		{ 
			result = result * base;
		}

		return result;
	}

	int main()
	{
		int base, exponent;
		cout << "Enter Base: ";
		cin >> base;
	
		cout << "Enter Exponent: ";
		cin >> exponent;

		cout << "Result: " << power(base, exponent) << endl;
		return 0;
	}
```
`Power with recursion`
```
	#include <iostream>
	using namespace std;

	int power(int base, int exponent)
	{
		if (exponent < 1)
		{
			return 1;
		}
		else
		{
			return base * power(base, exponent - 1);
		}
	}

	int main()
	{
		int base, exponent;
		cout << "Enter Base: ";
		cin >> base;

		cout << "Enter Exponent: ";
		cin >> exponent;

		cout << "Result: " << power(base, exponent) << endl;
		return 0;
	}
```
Fibonnaci Series using Recursion
```
	#include <iostream>
	using namespace std;

	int fib(int number)
	{
		if (number == 0 || number == 1)
		{
			return number;
		}
		else
		{
			return fib(number - 1) + fib(number - 2);
		}
	}
	int main()
	{
		int number;

		cout << "How many fibonacci numbers you want to generate: ";
		cin >> number;

		for (int i = number; i >= 1; i--)
		{
			cout << fib(i) << " ";
		}

		return 0;
	}
```
Shallow Copy works great if heap memory is not included for any of the instance variable.
```
	#include <iostream>
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
		void setValues(int x, int y)
		{
			this->x = x;
			this->y = y;
		}
		void setX(int x)
		{
			this->x = x;
		}
		void display()
		{
			cout << "X : " << x << ", Y: " << y << endl;
		}
	};

	int main()
	{
		Point p1;
	
		p1.setValues(5, 7);

		cout << "Point 1... " << endl;
		p1.display();

		Point p2 = p1;
		p2.setValues(6, 8);

		p1.setX(10);

		cout << "Point 2... " << endl;
		p2.display();
	
		return 0;
	}
```
Introducing a variable in the heap to see how Shallow Copy works
```
	#include <iostream>
	using namespace std;

	class Point
	{
	private:
		int x, y;
		int* z;
	public:
		Point()
		{
			x = 0;
			y = 0;
			z = new int;
		}
		void setValues(int x, int y, int z)
		{
			this->x = x;
			this->y = y;
			*this->z = z;
		}
		void setZ(int z)
		{
			*this->z = z;
		}
		void display()
		{
			cout << "X : " << x << ", Y: " << y <<", *Z: "<<*z <<endl;
		}
	};

	int main()
	{
		Point p1;

		p1.setValues(5, 7, 10);

		cout << "Point 1... " << endl;
		p1.display();

		Point p2 = p1;
		p2.setValues(6, 8, 11);

		p1.setZ(100);

		cout << "Point 2... " << endl;
		p2.display();

		return 0;
	}
```
Deep Copy helps in copying the heap memory as well using Copy Constructor
```
	#include <iostream>
	using namespace std;

	class Point
	{
	private:
		int x, y;
		int* z;
	public:
		Point()
		{
			x = 0;
			y = 0;
			z = new int;
		}
		Point(Point& p)
		{
			this->x = p.x;
			this->y = p.y;
			z = new int;
			*this->z = *(p.z);
		}
		void setValues(int x, int y, int z)
		{
			this->x = x;
			this->y = y;
			*this->z = z;
		}
		void setZ(int z)
		{
			*this->z = z;
		}
		void display()
		{
			cout << "X : " << x << ", Y: " << y <<", *Z: "<<*z <<endl;
		}
	};


	int main()
	{
		Point p1;
	
		p1.setValues(5, 7, 10);

		cout << "Point 1... " << endl;
		p1.display();

		Point p2 = p1;
		p2.setValues(6, 8, 11);
		p1.setZ(100);

		cout << "Point 2... " << endl;
		p2.display();

		return 0;
	}
```
