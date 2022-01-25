# Week 1: Review of C++ Fundamentals

### Inputs and Outputs
`cout` and `cin` are used for displaying and taking the inputs
```
	#include <iostream>
	using namespace std;

	 int main() {
	     int i;

	     cout << "Enter an integer : ";
	     cin >> i;
	     cout << "You entered " << i << endl;
	 }

```

### Conditional Statements
if else if statements can be used to make them a bundle. In this case only one of the statements will work.
```
	int main()
	{
		int marks;

		cout << "Enter marks: ";
		cin >> marks;

		if (marks >= 90)
		{
			cout << "Your grade is A" << endl;
		}
		else if (marks >= 80)
		{
			cout << "Your grade is B" << endl;
		}
		else if (marks >= 70)
		{
			cout << "Your grade is C" << endl;
		}
		else if (marks >= 60)
		{
			cout << "Your grade is D" << endl;
		}
		else if (marks < 60)
		{
			cout << "Your grade is F" << endl;
		}

		return 0;
	}
```
Multiple conditions can be used in a conditional statement. If you want both the conditions to be true, use && operator.
```
	int main()
	{
		int number;

		cout << "Enter a number: ";
		cin >> number;

		if (number >= 1 && number <= 10)
		{
			cout << "Number is between 1 and 10" << endl;
		}
		else
		{
			cout << "Number is either less than 1 or greater than 10" << endl;
		}
	
		return 0;
	}
```
### While Loop: 
In order to iterate through statements, we can use a while loop.
```
	int main()
	{
		int i = 1;
		while (i <= 10)
		{
			cout << i << endl;
			i++;
		}

		return 0;
	}
```
Loops can be infinite
```
	int main()
	{
		while (true)
		{
			cout << "hello" << endl;
		}

		return 0;
	}	
```
You can break the loop by using `break` statement
```
	int main()
	{
		int number;

		while (true)
		{
			cout << "Enter a number (press -1 to quit): ";
			cin >> number;

			if (number == -1)
			{
				break;
			}
		}

		return 0;
	}
```
### For Loop:
```
	int main()
	{
		for (int i = 1; i <= 10; i++)
		{
			cout << i << endl;
		}	

		return 0;
	}
```
	
For loops can be infinite as well
```
	int main()
	{
		int number;
		for (; ; )
		{
			cout << "Enter a number: " ;
			cin >> number;

			if (number == -1)
			{
				break;
			}
		}

		return 0;
	}
```
### Functions:
Functions are used for reusability. Functions can be pre-defined or user-defined. It is recommended to keep your main method as simple as possible. If we want to reuse part of our code again, we can use functions.
```
	int main()
	{
		string userName, password;
		cout << "Enter User Name: ";
		cin >> userName;
		cout << "Enter Password: ";
		cin >> password;
		return 0;
	}
```
In order to keep main method clean and reuse part of the code, functions can be used.
```
	void login()
	{
		string userName, password;
		cout << "Enter User Name: ";
		cin >> userName;
		cout << "Enter Password: ";
		cin >> password;
	}

	int main()
	{
		login();
		return 0;
	}
```

The function header consists of:
* the function return type
* the function name
* the function parameter list
```
	void evenOdd(int number)
	{
		if (number %2 == 0)
		{
			cout << "Even" << endl;
		}
		else
		{
			cout << "Odd" << endl;
		}
	}

	int main()
	{
		int number;
		cout << "Enter a number: ";
		cin >> number;

		evenOdd(number);
		return 0;
	}
```

Functions are very handy when they return value.
```
	string EvenOdd(int number)
	{
		if (number % 2 == 0)
		{
			return "Even";
		}
		else
		{
			return "Odd";
		}
	}

	int main()
	{
		cout << EvenOdd(5);
		return	0;
	}
```
Any return value can be used for functions
```
	int add(int number1, int number2)
	{
		return number1 + number2;
	}

	int main()
	{
		cout << add(5, 6);
		return	0;
	}
```
### File Processing (Creating and Writing):
Memory storage is temporary. File storage is used for data retention.
* Creating and writing to a File
```
	#include <iostream>
	#include <string>
	#include <fstream>

	using namespace std;

	int main()
	{
	    string word;
	    cout << "Enter a word to file: ";
	    getline(cin, word);

	    ofstream file;
	    file.open("myfile.txt");
	    file << word;
	    file.close();
	    return 0;
	}
```
* Appending to a file.
```
	#include <iostream>
	#include <string>
	#include <fstream>

	using namespace std;

	int main()
	{
	    string word;
	    cout << "Enter a word to file: ";
	    getline(cin, word);

	    ofstream file;
	    file.open("myfile.txt", ios::app);
	    file << word;
	    file.close();
	    return 0;
	}
```
### File Processing (Reading):
Be Default, it will read only 1 word if there are spaces between the words.
```
	int main()
	{
	    string word;
	    ifstream file;
	    file.open("myFile.txt");
	    file >> word;
	    cout << word;
	    file.close();
	    return 0;
	}
```
In order to read the line, getline can be used.
```
	int main()
	{
	    string word;
	    ifstream file;
	    file.open("myFile.txt");
	    getline(file, word);
	    cout << word;
	    file.close();
	    return 0;
	}
```
Reading the whole file
```
	int main()
	{
	    string word;
	    ifstream file;
	    file.open("myFile.txt");

	    while (!file.eof())
	    {
	        getline(file, word);
	        cout << word<<endl;
	    }
    
    	file.close();
	return 0;
	}
```


### Arrays:
Arrays can be initialized as well as used in conditional statements
```
	#include <iostream>
	using namespace std;
	int main()
	{	
		int myArray[5] = {5, 10, 2, 25, 8};
		int max = 0;

		for (int i = 0; i < 5; i++)
		{
			if (myArray[i] > max)
			{
				max = myArray[i];
			}
		}

		cout << "Max. number in the array is: " << max << endl;

		return 0;
	}
```
Arrays can be passed to the functions
```
	#include <iostream>
	using namespace std;

	void displayArray(int numbers[], int size)
	{
	    for (int i = 0; i < size; i++)
	    {
        	cout << numbers[i] << "\t";
	    }
	}

	int main()
	{
	    const int SIZE = 5;
	    int numbers[5] = { 5, 2, 1, 6, 8 };
	    displayArray(numbers, SIZE);
	    return 0;
	}
```
### Pointers: 
Pointers can be used in arithematic expressions:
```
	#include <iostream>
	using namespace std;
	int main()
	{
		int number1 = 7;
		int number2 = 8;
		int* ptrNumber1 = &number1;
		int* ptrNumber2 = &number2;
 
		int result = (*ptrNumber1) + (*ptrNumber2);
	
		cout << "Sum of " << *ptrNumber1 << " and " << *ptrNumber2 << " is : "<< result<<endl;
		
		return 0;
	}
```
Pointers can be used in functions. Variables are passed to functions by value
```
	#include <iostream>
	using namespace std;
	void increment(int n)
	{
		n = n + 1;
	}
	int main()
	{
		int n = 7;
		increment(n);
		cout << "Result:" << n<<endl;
		return 0;
	}
```
Variables can be passed to functions by reference using pointers
```
	#include <iostream>
	using namespace std;

	void increment(int *ptr)
	{
	    *ptr = (*ptr) + 1;
	}

	int main() 
	{
	    int n = 7;
	    increment(&n);
	    cout << n << endl;
	    
	    return 0;
	}
```
To get the value of the array elements using pointer, we can use the ptr notation
```
	int main()
	{
		int myArray[5] = { 2, 1, 5, 3, 6 };
		int* ptr = &myArray[0];

		for (int i = 0; i < 5; i++)
		{
			cout << "myArray[" << i << "] = " << *(ptr + i) << endl;
			cout << "Address of myArray[" << i << "] = " << (ptr+i) << endl;
		}

		return 0;
	}
```
### Passing Arrays to functions
```
	#include <iostream>
	using namespace std;

	int sum_elements(int myArray[], int size)
	{
		int sum = 0;
		for (int i = 0; i < 5; i++)
		{
			sum = sum + myArray[i];
		}
		return sum;
	}

	int main()
	{
		int myArray[5] = { 2, 1, 5, 3, 6 };
		int* ptr = myArray;
		cout << sum_elements(myArray, 5);
		return 0;
	}
```
### Vectors
Vectors can serve as dynamic arrays
```
	#include <iostream>
	#include <vector>
	using namespace std;
	int main()
	{
		vector<int> v;
		int number;
		//add elements to a vector
		for (int i = 0; i < 5; i++)
		{
			cout << "Enter an integer element to add to a vector: ";
			cin >> number;
			v.push_back(number);
		}
		cout << "Size of the vector is: " << v.size() << endl;
		v.pop_back();
		cout << "Size of the vector after popping an element is: " << v.size() << endl;
		cout << "Status of the vector after popping an element from the vector:" << endl;
		for (int i = 0; i < v.size(); i++)
		{
			cout << v[i] << endl;
		}
		return 0;
	}
```
Vectors can be passed to a function as a parameter
```
	#include <iostream>
	#include <vector>

	using namespace std;

	void displayVector(vector<int> v)
	{
		for (int i = 0; i < v.size(); i++)
		{
			cout << "v[" << i << "]= " << v[i] << endl;
		}

	}

	int main()
	{
		vector<int> v;
		int number;
		while (true)
		{
			cout << "Enter a number: ";
			cin >> number;

			if (number == -1)
			{
				break;
			}
	
			v.push_back(number);
		}

		displayVector(v);
		return 0;
	}
```
Vectors can be passed by reference
```
	void displayVector(vector<int>& v)
	{
		for (int i = 0; i < v.size(); i++)
		{
			cout << "v[" << i << "]= " << v[i] << endl;
		}
	}

	int main()
	{
		vector<int> v;
		int number;
		while (true)
		{
			cout << "Enter a number: ";
			cin >> number;

			if (number == -1)
			{
				break;
			}

			v.push_back(number);
		}

		displayVector(v);

		return 0;
	}
```

Vectors can be returned from a function

```
	void displayVector(vector<int>& v)
	{
		for (int i = 0; i < v.size(); i++)
		{
			cout << "v[" << i << "]= " << v[i] << endl;
		}
	}

	vector<int> reverseVector(vector<int> v)
	{
		vector<int> newVector;
	
		for (int i = v.size() - 1; i >=0 ; i--)
		{
			newVector.push_back(v[i]);
		}
		return newVector;
	}

	int main()
	{
		vector<int> v;
		int number;
		while (true)
		{
			cout << "Enter a number: ";
			cin >> number;

			if (number == -1)
			{
				break;
			}

			v.push_back(number);
		}

		displayVector(v);
		v = reverseVector(v);
		cout << "reverse..." << endl;
		displayVector(v);

		return 0;
}
```