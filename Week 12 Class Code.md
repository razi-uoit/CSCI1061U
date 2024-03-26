# Week 12 : Deep and Shallow Copy

1. Provided the following code will produce an error as name pointer would try to delete memory location already deallocated by the compiler:
```
#include <iostream>
#include <cstring>

using namespace std;
class Vehicle
{
    private:
    const char * name;
    
    public:
    Vehicle(const char * name)
    {
        int size = strlen(name);
        this->name = new char[size + 1];
        this->name = name;
    }
    ~Vehicle()
    {
        delete[] this->name;
    }
    void display()
    {
        cout <<"Name: "<<this->name<<endl;
    }
};

int main()
{
    Vehicle v = Vehicle("Toyota");
    v.display();
    return 0;
}
```

2. This problem can be solved by copying the elements one by one manually
```
#include <iostream>
#include <cstring>

using namespace std;


class Vehicle
{
    private:
    char * name;
    
    public:
    Vehicle(const char * name)
    {
        int size = strlen(name);
        this->name = new char[size + 1];
        for (int i=0; i<size; i++)
        {
            this->name[i] = name[i];
        }
        this->name[size] = '\0';
    }
    ~Vehicle()
    {
        delete[] this->name;
    }
    void display()
    {
        cout <<"Name: "<<this->name<<endl;
    }
};

int main()
{
    Vehicle v = Vehicle("Toyota");
    v.display();
    return 0;
}
```
3. strcpy is another way of doing the copy which would avoid such errors
```
#include <iostream>
#include <cstring>

using namespace std;


class Vehicle
{
    private:
    char * name;
    
    public:
    Vehicle(const char * name)
    {
        int size = strlen(name);
        this->name = new char[size + 1];
        strcpy(this->name, name);
    }
    ~Vehicle()
    {
        delete[] this->name;
    }
    void display()
    {
        cout <<"Name: "<<this->name<<endl;
    }
};

int main()
{
    Vehicle v = Vehicle("Toyota");
    v.display();
    return 0;
}
```
4. Copying an object through a pointer would mean you are making that pointer point to that object is the memory and hence changing anything through that pointer would result in changing that particular object. Code below will throw an error:
```
#include <iostream>
#include <cstring>

using namespace std;


class Vehicle
{
    private:
    char * name;
    
    public:
    Vehicle(const char * name)
    {
        int size = strlen(name);
        this->name = new char[size + 1];
        strcpy(this->name, name);
    }
    ~Vehicle()
    {
        delete[] this->name;
    }
    void display()
    {
        cout <<"Name: "<<this->name<<endl;
    }
};

int main()
{
    Vehicle v = Vehicle("Toyota");
    v.display();
    
    Vehicle copy = v;
    copy.display();
    return 0;
}
```
5. Using copy constructor would help coyping the values properly
```
#include <iostream>
#include <cstring>

using namespace std;


class Vehicle
{
    private:
    char * name;
    
    public:
    Vehicle(const char * name)
    {
        int size = strlen(name);
        this->name = new char[size + 1];
        strcpy(this->name, name);
    }
    Vehicle(const Vehicle& other)
    {
        int size = strlen(other.name);
        this->name = new char[size + 1];
        strcpy(this->name, other.name);
    }
    ~Vehicle()
    {
        delete[] this->name;
    }
    void display()
    {
        cout <<"Name: "<<this->name<<endl;
    }
};

int main()
{
    Vehicle v = Vehicle("Toyota");
    v.display();
    
    Vehicle copy = v;
    copy.display();
    return 0;
}
```
6. We can also have these two object hold completely different values for name
```
#include <iostream>
#include <cstring>

using namespace std;


class Vehicle
{
    private:
    char * name;
    
    public:
    Vehicle(const char * name)
    {
        int size = strlen(name);
        this->name = new char[size + 1];
        strcpy(this->name, name);
    }
    Vehicle(const Vehicle& other)
    {
        int size = strlen(other.name);
        this->name = new char[size + 1];
        strcpy(this->name, other.name);
    }
    ~Vehicle()
    {
        delete[] this->name;
    }
    void setName(const char * name)
    {
        delete[] this->name;

        int size = strlen(name);
        this->name = new char[size + 1];

        strcpy(this->name, name);
    }
    void display()
    {
        cout <<"Name: "<<this->name<<endl;
    }
};

int main()
{
    Vehicle v = Vehicle("Toyota");
    v.display();
    
    Vehicle copy = v;
    copy.setName("Honda");
    copy.display();
    
    v.display();
    return 0;
}
```
7. Lets now create a copy object using parameterized constructor and then copy the object to display. Below will produce an error:
```
#include <iostream>
#include <cstring>

using namespace std;


class Vehicle
{
    private:
    char * name;
    
    public:
    Vehicle(const char * name)
    {
        int size = strlen(name);
        this->name = new char[size + 1];
        strcpy(this->name, name);
    }
    Vehicle(const Vehicle& other)
    {
        int size = strlen(other.name);
        this->name = new char[size + 1];
        strcpy(this->name, other.name);
    }
    ~Vehicle()
    {
        delete[] this->name;
    }
    void setName(const char * name)
    {
        delete[] this->name;

        int size = strlen(name);
        this->name = new char[size + 1];

        strcpy(this->name, name);
    }
    void display()
    {
        cout <<"Name: "<<this->name<<endl;
    }
};

int main()
{
    Vehicle v = Vehicle("Toyota");
    v.display();
    
    Vehicle copy = Vehicle("Honda");
    copy = v;
    copy.display();
    
    v.display();
    return 0;
}
```
8. In order to solve the above problem, we have to overload assignment operator to do the required operation of allocating the new memory
```
#include <iostream>
#include <cstring>

using namespace std;


class Vehicle
{
    private:
    char * name;
    
    public:
    Vehicle(const char * name)
    {
        int size = strlen(name);
        this->name = new char[size + 1];
        strcpy(this->name, name);
    }
    Vehicle(const Vehicle& other)
    {
        int size = strlen(other.name);
        this->name = new char[size + 1];
        strcpy(this->name, other.name);
    }
    Vehicle& operator=(const Vehicle& other)
    {
        if (this != &other)
        {
            delete[] this->name;
            
            int size = strlen(other.name);
            this->name = new char[size + 1];
            strcpy(this->name, other.name);
        }
        return *this;
    }
    ~Vehicle()
    {
        delete[] this->name;
    }
    void setName(const char * name)
    {
        delete[] this->name;

        int size = strlen(name);
        this->name = new char[size + 1];

        strcpy(this->name, name);
    }
    void display()
    {
        cout <<"Name: "<<this->name<<endl;
    }
};

int main()
{
    Vehicle v = Vehicle("Toyota");
    v.display();
    
    Vehicle copy = Vehicle("Honda");
    copy = v;
    copy.display();
    
    v.display();
    return 0;
}
```
9. This is called Rule of 3:

The rule states that if a class defines one (or more) of the following three special member functions, it should explicitly define all three:

- `Destructor`: Responsible for releasing resources acquired by an object. If a class dynamically allocates memory, it should have a destructor to deallocate that memory to prevent memory leaks.

- `Copy Constructor`: Responsible for creating a new object that is a copy of an existing object. If a class dynamically allocates memory, a copy constructor is necessary to perform a deep copy of the dynamically allocated resources.

- `Copy Assignment Operator`: Responsible for assigning one object to another of the same type. If a class dynamically allocates memory, the default assignment operator performs a shallow copy, which may lead to memory leaks or double deletion. Hence, a custom copy assignment operator is needed to ensure proper resource management.
	
10. Lets now see how Deep and Shallow copy work with Inheritance. Below code should work fine without errors and memory leaks.
```
#include <iostream>
#include <cstring>

using namespace std;
class Vehicle
{
    protected:
    char * name;
    
    public:
    Vehicle(const char * name)
    {
        int size = strlen(name);
        this->name = new char[size + 1];
        strcpy(this->name, name);
    }
    Vehicle(const Vehicle& other)
    {
        int size = strlen(other.name);
        this->name = new char[size + 1];
        strcpy(this->name, other.name);
    }
    Vehicle& operator=(const Vehicle& other)
    {
        if (this != &other)
        {
            delete[] this->name;
            
            int size = strlen(other.name);
            this->name = new char[size + 1];
            strcpy(this->name, other.name);
        }
        return *this;
    }
    ~Vehicle()
    {
        delete[] this->name;
    }
    void setName(const char * name)
    {
        delete[] this->name;

        int size = strlen(name);
        this->name = new char[size + 1];

        strcpy(this->name, name);
    }
    void display()
    {
        cout <<"Name: "<<this->name<<endl;
    }
};

class Car: public Vehicle
{
    private:
    char * type;
    public:
    Car(const char * name, const char * type): Vehicle(name)
    {
        int size = strlen(type);
        this->type = new char[size + 1];
        strcpy(this->type, type);
    }
    ~Car()
    {
        delete[] this->type;
    }
    void display()
    {
        Vehicle::display();
        cout <<"Type: "<<this->type<<endl;
    }
};

int main()
{
    Car car = Car("Toyota", "Sedan");
    car.display();
    return 0;
}
```
11. When we try to copy objects of a child, we start getting errors because of the same reason as we had errors without inheritance and vehicle object was copied:
```
#include <iostream>
#include <cstring>

using namespace std;


class Vehicle
{
    protected:
    char * name;
    
    public:
    Vehicle(const char * name)
    {
        int size = strlen(name);
        this->name = new char[size + 1];
        strcpy(this->name, name);
    }
    Vehicle(const Vehicle& other)
    {
        int size = strlen(other.name);
        this->name = new char[size + 1];
        strcpy(this->name, other.name);
    }
    Vehicle& operator=(const Vehicle& other)
    {
        if (this != &other)
        {
            delete[] this->name;
            
            int size = strlen(other.name);
            this->name = new char[size + 1];
            strcpy(this->name, other.name);
        }
        return *this;
    }
    ~Vehicle()
    {
        delete[] this->name;
    }
    void setName(const char * name)
    {
        delete[] this->name;

        int size = strlen(name);
        this->name = new char[size + 1];

        strcpy(this->name, name);
    }
    void display()
    {
        cout <<"Name: "<<this->name<<endl;
    }
};

class Car: public Vehicle
{
    private:
    char * type;
    public:
    Car(const char * name, const char * type): Vehicle(name)
    {
        int size = strlen(type);
        this->type = new char[size + 1];
        strcpy(this->type, type);
    }
    ~Car()
    {
        delete[] this->type;
    }
    void display()
    {
        Vehicle::display();
        cout <<"Type: "<<this->type<<endl;
    }
};

int main()
{
    Car car = Car("Toyota", "Sedan");
    car.display();
    
    Car copy = car;
    copy.display();
    return 0;
}
```
12. In order to solve this problem, we have to introduce copy constructor in the child class as well:
```
#include <iostream>
#include <cstring>

using namespace std;


class Vehicle
{
    protected:
    char * name;
    
    public:
    Vehicle(const char * name)
    {
        int size = strlen(name);
        this->name = new char[size + 1];
        strcpy(this->name, name);
    }
    Vehicle(const Vehicle& other)
    {
        int size = strlen(other.name);
        this->name = new char[size + 1];
        strcpy(this->name, other.name);
    }
    Vehicle& operator=(const Vehicle& other)
    {
        if (this != &other)
        {
            delete[] this->name;
            
            int size = strlen(other.name);
            this->name = new char[size + 1];
            strcpy(this->name, other.name);
        }
        return *this;
    }
    ~Vehicle()
    {
        delete[] this->name;
    }
    void setName(const char * name)
    {
        delete[] this->name;

        int size = strlen(name);
        this->name = new char[size + 1];

        strcpy(this->name, name);
    }
    void display()
    {
        cout <<"Name: "<<this->name<<endl;
    }
};

class Car: public Vehicle
{
    private:
    char * type;
    public:
    Car(const char * name, const char * type): Vehicle(name)
    {
        int size = strlen(type);
        this->type = new char[size + 1];
        strcpy(this->type, type);
    }
    Car(const Car& other): Vehicle(other)
    {
        int size = strlen(other.type);
        this->type = new char[size + 1];
        strcpy(this->type, other.type);
    }
    
    ~Car()
    {
        delete[] this->type;
    }
    void display()
    {
        Vehicle::display();
        cout <<"Type: "<<this->type<<endl;
    }
};

int main()
{
    Car car = Car("Toyota", "Sedan");
    car.display();
    
    Car copy = car;
    copy.display();
    return 0;
}
```
13. What if we create an object of child class using its parameterized constructor and then copy objects. Below will produce an error:
```
#include <iostream>
#include <cstring>

using namespace std;


class Vehicle
{
    protected:
    char * name;
    
    public:
    Vehicle(const char * name)
    {
        int size = strlen(name);
        this->name = new char[size + 1];
        strcpy(this->name, name);
    }
    Vehicle(const Vehicle& other)
    {
        int size = strlen(other.name);
        this->name = new char[size + 1];
        strcpy(this->name, other.name);
    }
    Vehicle& operator=(const Vehicle& other)
    {
        if (this != &other)
        {
            delete[] this->name;
            
            int size = strlen(other.name);
            this->name = new char[size + 1];
            strcpy(this->name, other.name);
        }
        return *this;
    }
    ~Vehicle()
    {
        delete[] this->name;
    }
    void setName(const char * name)
    {
        delete[] this->name;

        int size = strlen(name);
        this->name = new char[size + 1];

        strcpy(this->name, name);
    }
    void display()
    {
        cout <<"Name: "<<this->name<<endl;
    }
};

class Car: public Vehicle
{
    private:
    char * type;
    public:
    Car(const char * name, const char * type): Vehicle(name)
    {
        int size = strlen(type);
        this->type = new char[size + 1];
        strcpy(this->type, type);
    }
    Car(const Car& other): Vehicle(other)
    {
        int size = strlen(other.type);
        this->type = new char[size + 1];
        strcpy(this->type, other.type);
    }
    
    ~Car()
    {
        delete[] this->type;
    }
    void display()
    {
        Vehicle::display();
        cout <<"Type: "<<this->type<<endl;
    }
};

int main()
{
    Car car = Car("Toyota", "Sedan");
    car.display();
    
    Car copy = Car("Honda", "SUV");
    copy = car;
    copy.display();
    
    car.display();
    return 0;
}
```
14. In order to overcome this error, we introduce assignment operator overloading:
```
#include <iostream>
#include <cstring>

using namespace std;


class Vehicle
{
    protected:
    char * name;
    
    public:
    Vehicle(const char * name)
    {
        int size = strlen(name);
        this->name = new char[size + 1];
        strcpy(this->name, name);
    }
    Vehicle(const Vehicle& other)
    {
        int size = strlen(other.name);
        this->name = new char[size + 1];
        strcpy(this->name, other.name);
    }
    Vehicle& operator=(const Vehicle& other)
    {
        if (this != &other)
        {
            delete[] this->name;
            
            int size = strlen(other.name);
            this->name = new char[size + 1];
            strcpy(this->name, other.name);
        }
        return *this;
    }
    ~Vehicle()
    {
        delete[] this->name;
    }
    void setName(const char * name)
    {
        delete[] this->name;

        int size = strlen(name);
        this->name = new char[size + 1];

        strcpy(this->name, name);
    }
    void display()
    {
        cout <<"Name: "<<this->name<<endl;
    }
};

class Car: public Vehicle
{
    private:
    char * type;
    public:
    Car(const char * name, const char * type): Vehicle(name)
    {
        int size = strlen(type);
        this->type = new char[size + 1];
        strcpy(this->type, type);
    }
    Car(const Car& other): Vehicle(other)
    {
        int size = strlen(other.type);
        this->type = new char[size + 1];
        strcpy(this->type, other.type);
    }
    Car& operator=(const Car& other)
    {
        if (this != &other)
        {
            Vehicle::operator=(other);
            delete[] this->type;
            
            int size = strlen(other.type);
            this->type = new char[size + 1];
            strcpy(this->type, other.type);
        }
        return *this;
    }
    
    ~Car()
    {
        delete[] this->type;
    }
    void display()
    {
        Vehicle::display();
        cout <<"Type: "<<this->type<<endl;
    }
};

int main()
{
    Car car = Car("Toyota", "Sedan");
    car.display();
    
    Car copy = Car("Honda", "SUV");
    copy = car;
    copy.display();
    
    car.display();
    return 0;
}
```
15. Virtual destructors are handy when it comes to calling the destructors in order. Below code will have a memory leak because Car destructor is never called:
```
#include <iostream>
#include <cstring>

using namespace std;


class Vehicle
{
    private:
    char * name;
    
    public:
    Vehicle(const char * name)
    {
        int size = strlen(name);
        this->name = new char[size + 1];
        strcpy(this->name, name);
    }
    Vehicle(const Vehicle& other)
    {
        int size = strlen(other.name);
        this->name = new char[size + 1];
        strcpy(this->name, other.name);
    }
    Vehicle& operator=(const Vehicle& other)
    {
        if (this != &other)
        {
            delete[] this->name;
            
            int size = strlen(other.name);
            this->name = new char[size + 1];
            strcpy(this->name, other.name);
        }
        return *this;
    }
    ~Vehicle()
    {
        cout <<"Vehicle destructor"<<endl;
        delete[] this->name;
    }
    void setName(const char * name)
    {
        delete[] this->name;

        int size = strlen(name);
        this->name = new char[size + 1];

        strcpy(this->name, name);
    }
    virtual void display()
    {
        cout <<"Name: "<<this->name<<endl;
    }
};

class Car: public Vehicle
{
    private:
    char * type;
    public:
    Car(const char * name, const char * type): Vehicle(name)
    {
        int size = strlen(type);
        this->type = new char[size + 1];
        strcpy(this->type, type);
    }
    Car(const Car& other): Vehicle(other)
    {
        int size = strlen(other.type);
        this->type = new char[size + 1];
        strcpy(this->type, other.type);
    }
    Car& operator=(const Car& other)
    {
        if (this != &other)
        {
            Vehicle::operator=(other);
            delete[] this->type;
            
            int size = strlen(other.type);
            this->type = new char[size + 1];
            strcpy(this->type, other.type);
        }
        return *this;
    }
    
    ~Car()
    {
        cout <<"Car destructor"<<endl;
        delete[] this->type;
    }
    void display()
    {
        Vehicle::display();
        cout <<"Type: "<<this->type<<endl;
    }
};

int main()
{
    Vehicle *v = new Car("Toyota", "Sedan");
    v->display();
    
    delete v;
    return 0;
}
```
16. In order to avoid having such memory leaks, it is important to call destructors in order. Once way to do it is to make Parent destructor virtual.
```
#include <iostream>
#include <cstring>

using namespace std;


class Vehicle
{
    private:
    char * name;
    
    public:
    Vehicle(const char * name)
    {
        int size = strlen(name);
        this->name = new char[size + 1];
        strcpy(this->name, name);
    }
    Vehicle(const Vehicle& other)
    {
        int size = strlen(other.name);
        this->name = new char[size + 1];
        strcpy(this->name, other.name);
    }
    Vehicle& operator=(const Vehicle& other)
    {
        if (this != &other)
        {
            delete[] this->name;
            
            int size = strlen(other.name);
            this->name = new char[size + 1];
            strcpy(this->name, other.name);
        }
        return *this;
    }
    virtual ~Vehicle()
    {
        cout <<"Vehicle destructor"<<endl;
        delete[] this->name;
    }
    void setName(const char * name)
    {
        delete[] this->name;

        int size = strlen(name);
        this->name = new char[size + 1];

        strcpy(this->name, name);
    }
    virtual void display()
    {
        cout <<"Name: "<<this->name<<endl;
    }
};

class Car: public Vehicle
{
    private:
    char * type;
    public:
    Car(const char * name, const char * type): Vehicle(name)
    {
        int size = strlen(type);
        this->type = new char[size + 1];
        strcpy(this->type, type);
    }
    Car(const Car& other): Vehicle(other)
    {
        int size = strlen(other.type);
        this->type = new char[size + 1];
        strcpy(this->type, other.type);
    }
    Car& operator=(const Car& other)
    {
        if (this != &other)
        {
            Vehicle::operator=(other);
            delete[] this->type;
            
            int size = strlen(other.type);
            this->type = new char[size + 1];
            strcpy(this->type, other.type);
        }
        return *this;
    }
    
    ~Car()
    {
        cout <<"Car destructor"<<endl;
        delete[] this->type;
    }
    void display()
    {
        Vehicle::display();
        cout <<"Type: "<<this->type<<endl;
    }
};

int main()
{
    Vehicle *v = new Car("Toyota", "Sedan");
    v->display();
    
    delete v;
    return 0;
}
```
