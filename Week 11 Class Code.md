# Week 12 Class Code: Shallow and Deep Copy

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
