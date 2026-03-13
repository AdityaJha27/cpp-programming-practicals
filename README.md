---
## 💻 `# cpp-programming-practicals`
# Practical 1

## Question :- 
Write a program to compute the sum of the first n terms of the following series. The number of terms n is to be taken from the user through the command line. If the command line argument is not found then prompt the user to enter the value of n.

```cpp
#include <iostream>
using namespace std;

int main(int argc,char* argv[])
{
    int n,sum=0;

    if(argc>1)
        n=stoi(argv[1]);
    else
        cin>>n;

    for(int i=1;i<=n;i++)
        sum+=i;

    cout<<sum;
}  
```
# Practical 2

## Question :-
Write a program to remove the duplicates from an array.

```cpp
#include <iostream>
using namespace std;

int main()
{
    int n;
    cin>>n;

    int a[100];

    for(int i=0;i<n;i++)
        cin>>a[i];

    for(int i=0;i<n;i++)
    {
        for(int j=i+1;j<n;j++)
        {
            if(a[i]==a[j])
            {
                for(int k=j;k<n-1;k++)
                    a[k]=a[k+1];

                n--;
                j--;
            }
        }
    }

    for(int i=0;i<n;i++)
        cout<<a[i]<<" ";
}
```
# Practical 3

# Question :-
Write a program that prints a table indicating the number of occurrences of each alphabet in the text entered as command line arguments.

```cpp
#include <iostream>
#include <cctype>
using namespace std;

int main(int argc,char* argv[])
{
    int count[26]={0};

    for(int i=1;i<argc;i++)
    {
        string s=argv[i];


        for(char c:s)
        {
            if(isalpha(c))
            {
                c=tolower(c);
                count[c-'a']++;
            }
        }
    }

    for(int i=0;i<26;i++)
    {
        if(count[i]>0)
            cout<<(char)(i+'a')<<" "<<count[i]<<endl;
    }
}
```
# Practical 4

## Question :-
Write a menu driven program to perform string manipulation without using inbuilt string functions.

#### Operations:

- Show address of each character in string

- Concatenate two strings

- Compare two strings

- Calculate length of string using pointers

- Convert lowercase to uppercase

- Reverse string

- Insert a string at user specified position

```cpp
#include <iostream>
using namespace std;

int length(char *s)
{
    int i=0;
    while(*(s+i)!='\0')
        i++;
    return i;
}

void concat(char *a,char *b)
{
    int i=length(a);
    int j=0;

    while(*(b+j)!='\0')
    {
        *(a+i)=*(b+j);
        i++;
        j++;
    }

    *(a+i)='\0';
}

int compare(char *a,char *b)
{
    int i=0;

    while(*(a+i)!='\0' && *(b+i)!='\0')
    {
        if(*(a+i)!=*(b+i))
            return *(a+i)-*(b+i);
        i++;
    }

    return *(a+i)-*(b+i);
}

void upper(char *s)
{
    for(int i=0;*(s+i)!='\0';i++)
    {
        if(*(s+i)>='a' && *(s+i)<='z')
            *(s+i)=*(s+i)-32;
    }
}

void reverse(char *s)
{
    int l=length(s);

    for(int i=0;i<l/2;i++)
    {
        char t=*(s+i);
        *(s+i)=*(s+l-i-1);
        *(s+l-i-1)=t;
    }
}

int main()
{
    char a[100],b[100];

    cin>>a>>b;

    cout<<length(a)<<endl;

    concat(a,b);
    cout<<a<<endl;

    cout<<compare(a,b)<<endl;

    upper(a);
    cout<<a<<endl;

    reverse(a);
    cout<<a<<endl;
}
```
# Practical 5

## Question :-
Write a program to merge two ordered arrays to get a single ordered array.

```cpp
#include <iostream>
using namespace std;

int main()
{
    int n,m;
    cin>>n>>m;

    int a[100],b[100],c[200];

    for(int i=0;i<n;i++)
        cin>>a[i];

    for(int i=0;i<m;i++)
        cin>>b[i];

    int i=0,j=0,k=0;

    while(i<n && j<m)
    {
        if(a[i]<b[j])
            c[k++]=a[i++];
        else
            c[k++]=b[j++];
    }

    while(i<n)
        c[k++]=a[i++];

    while(j<m)
        c[k++]=b[j++];

    for(int i=0;i<n+m;i++)
        cout<<c[i]<<" ";
}
```
# Practical 6
## Question :-
Write a program to search a given element in a set of N numbers using Binary Search.

#### (a) With recursion

```cpp
#include <iostream>
using namespace std;

int binarySearch(int a[],int l,int r,int key)
{
    if(l>r)
        return -1;

    int mid=(l+r)/2;

    if(a[mid]==key)
        return mid;

    if(key<a[mid])
        return binarySearch(a,l,mid-1,key);

    return binarySearch(a,mid+1,r,key);
}

int main()
{
    int n,key;
    cin>>n;

    int a[100];

    for(int i=0;i<n;i++)
        cin>>a[i];

    cin>>key;

    cout<<binarySearch(a,0,n-1,key);
}
```
#### (b) Without recursion
```cpp
#include <iostream>
using namespace std;

int main()
{
    int n,key;
    cin>>n;

    int a[100];

    for(int i=0;i<n;i++)
        cin>>a[i];

    cin>>key;

    int l=0,r=n-1;

    while(l<=r)
    {
        int mid=(l+r)/2;

        if(a[mid]==key)
        {
            cout<<mid;
            return 0;
        }

        if(key<a[mid])
            r=mid-1;
        else
            l=mid+1;
    }

    cout<<-1;
}

```
# Practical 7

## Question :-

Write a program to calculate GCD of two numbers.

#### (a) With recursion
```cpp
#include <iostream>
using namespace std;

int gcd(int a,int b)
{
    if(b==0)
        return a;

    return gcd(b,a%b);
}

int main()
{
    int a,b;
    cin>>a>>b;

    cout<<gcd(a,b);
}
```
#### (b) Without recursion
```cpp
#include <iostream>
using namespace std;

int main()
{
    int a,b;
    cin>>a>>b;

    while(b!=0)
    {
        int t=b;
        b=a%b;
        a=t;
    }

    cout<<a;
}
```
# Practical 8
## Question :-

Create a Matrix class. Write a menu driven program to perform the following matrix operations:

- Sum

- Product

- Transpose

Exceptions should be thrown if matrices are incompatible.
```cpp
#include <iostream>
using namespace std;

class Matrix
{
public:
    int r,c,a[10][10];

    void input()
    {
        cin>>r>>c;

        for(int i=0;i<r;i++)
            for(int j=0;j<c;j++)
                cin>>a[i][j];
    }

    void display()
    {
        for(int i=0;i<r;i++)
        {
            for(int j=0;j<c;j++)
                cout<<a[i][j]<<" ";
            cout<<endl;
        }
    }

    Matrix add(Matrix m)
    {
        if(r!=m.r || c!=m.c)
            throw "Addition not possible";

        Matrix t;
        t.r=r;
        t.c=c;

        for(int i=0;i<r;i++)
            for(int j=0;j<c;j++)
                t.a[i][j]=a[i][j]+m.a[i][j];

        return t;
    }

    Matrix transpose()
    {
        Matrix t;

        t.r=c;
        t.c=r;

        for(int i=0;i<r;i++)
            for(int j=0;j<c;j++)
                t.a[j][i]=a[i][j];

        return t;
    }
};

int main()
{
    Matrix A,B,C;

    try
    {
        A.input();
        B.input();

        C=A.add(B);
        C.display();
    }
    catch(const char* msg)
    {
        cout<<msg;
    }
}
```
# Practical 9
##  Question :-

Define a class Person having name as data member.
Inherit two classes Student and Employee from Person.

- Student: course, marks, year

- Employee: department, salary

Write display() method in all classes and show runtime polymorphism.
```cpp
#include <iostream>
using namespace std;

class Person
{
public:
    string name;

    virtual void display()
    {
        cout<<name<<endl;
    }
};

class Student:public Person
{
public:
    string course;
    int marks,year;

    void display()
    {
        cout<<name<<" "<<course<<" "<<marks<<" "<<year<<endl;
    }
};

class Employee:public Person
{
public:
    string department;
    int salary;

    void display()
    {
        cout<<name<<" "<<department<<" "<<salary<<endl;
    }
};

int main()
{
    Person *p;

    Student s;
    Employee e;

    cin>>s.name>>s.course>>s.marks>>s.year;
    cin>>e.name>>e.department>>e.salary;

    p=&s;
    p->display();

    p=&e;
    p->display();
}
```
# Practical 10

##  Question :-

Create a Triangle class with exception handling to ensure:

- All sides > 0

- Sum of any two sides > third side

Provide overloaded functions to calculate:

- of right triangle

- Area using Heron's formula
```cpp
#include <iostream>
#include <cmath>
using namespace std;

class Triangle
{
public:
    double a,b,c;

    void input()
    {
        cin>>a>>b>>c;

        if(a<=0 || b<=0 || c<=0)
            throw "Invalid sides";

        if(a+b<=c || a+c<=b || b+c<=a)
            throw "Triangle not possible";
    }

    double area()
    {
        double s=(a+b+c)/2;
        return sqrt(s*(s-a)*(s-b)*(s-c));
    }

    double area(double base,double height)
    {
        return 0.5*base*height;
    }
};

int main()
{
    Triangle t;

    try
    {
        t.input();
        cout<<t.area();
    }
    catch(const char* msg)
    {
        cout<<msg;
    }
}
```
# Practical 11
## Question :-

Create a class Student containing:

- Roll No

- Name

- Class

- Year

- Total Marks

Store 5 objects in a file and retrieve them.
```cpp
#include <iostream>
#include <fstream>
using namespace std;

class Student
{
public:
    int roll,year,total;
    string name,cls;
};

int main()
{
    Student s[5];

    ofstream fout("student.txt");

    for(int i=0;i<5;i++)
        cin>>s[i].roll>>s[i].name>>s[i].cls>>s[i].year>>s[i].total;

    for(int i=0;i<5;i++)
        fout<<s[i].roll<<" "<<s[i].name<<" "<<s[i].cls<<" "<<s[i].year<<" "<<s[i].total<<endl;

    fout.close();

    ifstream fin("student.txt");

    for(int i=0;i<5;i++)
        fin>>s[i].roll>>s[i].name>>s[i].cls>>s[i].year>>s[i].total;

    for(int i=0;i<5;i++)
        cout<<s[i].roll<<" "<<s[i].name<<" "<<s[i].cls<<" "<<s[i].year<<" "<<s[i].total<<endl;

    fin.close();
}
```
# Practical 12
## Question :-

Copy the contents of one text file to another file after removing all whitespaces.
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main()
{
    ifstream fin("input.txt");
    ofstream fout("output.txt");

    char ch;

    while(fin.get(ch))
    {
        if(ch!=' ' && ch!='\n' && ch!='\t')
            fout<<ch;
    }

    fin.close();
    fout.close();
}
```
