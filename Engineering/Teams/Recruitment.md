# Recruitment

There are multiple methods for recruitment. Starting from solving a problem or asking for sample open source code or provide a problem statement before hand for the interview.

TOC
- [[#3year experience]]
	- [[#SCM]]
	- [[#Build System]]
	- [[#System Language - C]]
- [[#7 years experience]]
	- [[#Android]]
	

# ~3year experience

## SCM

- How to create a commit in Git?
- How do you rebase?
- Is git pull same as git rebase?

## Build System

- How to clean a particular package?
- How can I only fetch the package and extract?
- Where can I change the output package type?
- Where can I find the images for my board?
- Where can I find the extracted rootfs for inspection?

## System Language - C++

### Beginnner
- What do you understand from Polymorphism ? Why do we need it?
- What do you understand from Inheritance ? Why do we need it?
- What do you understand from Encapsulation ? Why do we need it?
- What do you understand from Abstraction ? Why do we need it?
- Can we have a recursice inline funtion?
- What is the return type of constructor?
- What is the memory layout of a C/C++ program?

### Intermediate
- What does a Static member in C++ mean?
- Why do you think they added std::move ?
- What are lambda functions? How are they different from inline functions?
- What is the use of virtual keyword?
- Explain the significance of vTable and vptr in C++ and how the compiler deals with them
- What is use of friend keyword?
- How is function overloading different from operator overloading?
- Is it possible to compile c++ program without main() method?
- What is the main difference between struct and class in C++?
- Explain Virtual Functions and the concept of Runtime Polymorphism in C++ with a code example
- Which tools would you use on linux for debugging ?

### Advanced
- What is a Copy Constructor? When is it called?
- Shallow copy & deep copy
- Open the link https://ideone.com/BgxmC6. There are 6 questions in it.
- Take a look at the following two code examples for printing a vector. Is there any advantage of using one over the other?
```cpp
Sample Code 1:

vector vec;
/* ... .. ... */
for (auto itr = vec.begin(); itr != vec.end(); itr++) {
 itr->print();
}

Sample Code 2:

vector vec;
/* ... .. ... */
for (auto itr = vec.begin(); itr != vec.end(); ++itr) {
 itr->print();
}
```
Post-increment is more expensive than pre-increment
- Program to print numbers from 1 to 10 using std::thread
- What is std::mutex?
- What is std::semaphore?
- What will be the output in the below code -
```cpp
#include <iostream>
using namespace std;

int main() {
    int val = 0;
	
	switch(val) {
	default:
		cout << "default" << endl;
		break;
	case 0:
		cout << "case 0" << endl;
		break;
	}
    return 0;
}
```

https://hackr.io/blog/cpp-interview-questions

- What is object slicing? https://www.geeksforgeeks.org/object-slicing-in-c/
- https://www.geeksforgeeks.org/simulating-final-class-in-c/?ref=lbp
- difference between a vector and a list?
# ~7 years experience

## Android

- Please explain the boot sequence for Android
- Where does init come up in the startup?
- What are native services?
- When was selinux introduced into Android? - 4.4
- What are the selinux policy modes?
- audit to allow