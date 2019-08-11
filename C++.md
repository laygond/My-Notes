# C++

# Compilatiion and Execution

[Udacity C++ Lesson 2 Compilation](https://classroom.udacity.com/courses/ud210/lessons/6b9a7102-460d-4f9f-9fb7-668df8e19fea/concepts/a2e09c86-3058-464a-9509-b95fc25d1693)

.cpp files are source files that most be compiled into an executable file, a.k.a binary file, in order to be run in a processor. There are many tools available to help you compile, rsuch as `g++` on Unix, to complex build systems that are integrated into IDEs like Visual Studio and Eclipse.

There is a high-level cross-platform build tool called **CMake** that does not compile code but sets the compilation configurations. It depends on a lower-level build tool called **Make** to *manage* compiling from source. And then Make depends on a compiler to do the actual compiling. 

source code →  COMPILE → (object file  → linking object files → executable)


- **Object File**: source code compiled and transformed into machine code but not executable yet. Among other things, object files describe their own public APIs (usually called symbols) as well as references that need to be resolved from other object files.
- **Linker**: during the linking process, the linker (the thing that does the linking) resolves symbolic references between object files and outputs a self-contained binary with all the machine code needed to execute.
    - **Dynamic Linking:** as an aside, linking is not required for all programs. Most operating systems allow **dynamic linking**, in which symbolic references point to libraries that are not compiled into the resulting binary. With dynamic linking, these references are resolved at runtime. An example of this is a program that depends on a system library. At runtime, the symbolic references of the program resolve to the symbols of the system library. There are pros and cons of dynamic linking. On the one hand, dynamically linked libraries are not linked within binaries, which keeps the overall file size down. However, if the library changes at any point, your code will automatically link to the new version. Like any changing dependency, difficult to fix and surprising bugs sometimes arise when versions change.

**Steps**

- To compile the program: g++ filename.cpp -o executableName
- To execute the program: ./executableName


# enum
    #include <iostream>
    using namespace std;
    
    int main()
    {
        //define MONTHS as having 12 possible values
        enum MONTHS {Jan, Feb, Mar, Apr,May,Jun,Jul,Aug,Sep,Oct,Nov,Dec};    
        //define bestMonth as a variable type MONTHS
        MONTHS bestMonth;
        //assign bestMonth one of the values of MONTHS
        bestMonth = Jan;
        //now we can check the value of bestMonths just 
        //like any other variable
        if(bestMonth == 0)
        {
            cout<<"I'm not so sure January is the best month\n" << Jan ;
        }
        return 0;
    }


# setw
    #include <iomanip>
    
    int main(){
      std::cout<<"\n\nThe text without any formating\n";
      std::cout<<"Ints"<<"Floats"<<"Doubles"<< "\n";
      std::cout<<"\nThe text with setw(15)\n";
      std::cout<<"Ints"<<std::setw(15)<<"Floats"<<std::setw(15)<<"Doubles"<< "\n";
      std::cout<<"\n\nThe text with tabs\n";
      std::cout<<"Ints\t"<<"Floats\t"<<"Doubles"<< "\n";  
      return 0;
    
    // The gap between Ints and floats has wider white space than the other because "Ints" has only 4 char and leaves 11 white spaces left in setw(15)
    }
# fstream

i = reading from
o = writing to


    /* Your assignment for this quiz
    **Change the contents of the file called input.txt
    **Change the ifstream and ofstream to fstream
    */
    #include <iostream>
    #include <fstream>
    #include <string>
    using namespace std;
    
    int main () {
    string line;
    //create an output stream to write to the file
    //append the new lines to the end of the file
    fstream myfileI ("input.txt", ios::app | ios::out); // /ofstream myfileI ("input.txt", ios::app);
    if (myfileI.is_open())
    {
    myfileI << "\nI am adding a liiiine.\n\n";
    myfileI << "I am adding another line.\n";
    myfileI.close();
    }
    else cout << "Unable to open file for writing";
    //create an input stream to write to the file
    fstream myfileO ("input.txt", ios::in); // ifstream myfileO ("input.txt")
    if (myfileO.is_open())
    {
        while ( getline (myfileO,line) )
        {
            cout << line << '\n';
        }
        myfileO.close();
    }
    
    else cout << "Unable to open file for reading";
    
    return 0;
    }


## Not using namespace then
    #include <iostream>
    #include <fstream>
    #include <string>
    //using namespace std;
    
    int main () {
        std::string line;
        //create an output stream to write to the file
        //append the new lines to the end of the file
        std::fstream myfileI ("input.txt", std::ios::app | std::ios::out);
        if (myfileI.is_open())
        {
            myfileI << "\nI am adding a liiiine.\n\n";
            myfileI << "I am adding another line.\n";
            myfileI.close();
        }
        else std::cout << "Unable to open file for writing";
      
        //create an input stream to write to the file
        std::fstream myfileO ("input.txt", std::ios::in);
        if (myfileO.is_open())
        {
            while ( getline (myfileO,line) )
            {
                std::cout << line << '\n';
            }
            myfileO.close();
        }
        
        else std::cout << "Unable to open file for reading";
        
        return 0;
    }


# cin getline

If a string has embedded spaces then cin would extract only the first word of the phrase or words given input, because space is treated as a separator or terminator for a value. Hence getline() would be better.

    #include <iostream>
    #include <string>
    
    int main(){
        std::string userName; 
        std::cout<<"Tell me your nickname?: ";
        std::getline(std::cin, userName);
        std::cout<<"Hello "<<userName<<"\n";
        return 0;
    }


# stringstream
    #include <iostream>
    #include <string>
    #include <sstream>
    
    int main (){
       std::string stringLength;
       float inches = 0;
       float yardage = 0;
       std::cout << "Enter number of inches: ";
       std::getline (std::cin,stringLength);
       std::stringstream(stringLength) >> inches;
       std::cout<<"You entered "<<inches<<"\n";
       yardage = inches/36;
       std::cout << "Yardage is " << yardage;
       return 0;
    }


# cmath

std is only used for functions not constants like M_PI

    #include <iostream>
    #include <cmath>
    
    int main() {    
        float cubeSide = 5.4;
        float sphereRadius = 2.33;
        float coneRadius = 7.65;
        float coneHeight = 14;
        float volCube, volSphere, volCone = 0;  
        volCube = std::pow(cubeSide,3);
        volSphere = (4.0/3.0) * M_PI * std::pow(sphereRadius,3);
        volCone = M_PI * coneRadius*coneRadius * (coneHeight/3.0);
        std::cout<< volCube <<std::endl;
        std::cout<< volSphere<<std::endl;
        std::cout<< volCone <<std::endl;
        return 0;
    }


# ++i & i++ PreFix and PostFix
    #include<iostream>
    using namespace std;
    
    int main() {
        int a, b = 0;
        int post, pre = 0;
        cout<<"Inital values: \t\t\tpost = "<<post<<" pre= "<<pre<<"\n";
        post = a++;
        pre = ++b;
        cout<<"After one postfix and prefix: \tpost = "<<post<<" pre= "<<pre<<"\n";
        post = a++;
        pre = ++b;
        cout<<"After two postfix and prefix: \tpost = "<<post<<" pre= "<<pre<<"\n";  
        return 0;
    }
# Pointers

char is special

    #include<iostream>
    #include<string>
    
    int main(){
        int givenInt;
        float givenFloat;
        double givenDouble ;
        char givenChar;
        std::string givenString;
        
        std::cin>> givenInt;
        std::cin>> givenFloat;
        std::cin>> givenDouble; 
        std::cin.ignore(); //gets rid of raimining in buffer (not really needed here)
        std::cin>> givenChar;
        std::cin.ignore(); // if omitted when printing givenString it shows blank
        std::getline(std::cin, givenString);
        
        std::cout<<givenInt<<"\t"<<&givenInt<<"\n";
        std::cout<<givenFloat<<"\t"<<&givenFloat<<"\n";
        std::cout<<givenDouble<<"\t"<<&givenDouble<<"\n";
        std::cout<<givenChar<<"\t"<<(void *)&givenChar<<"\n"; // char is special
        std::cout<<givenString<<"\t"<<&givenString<<"\n";
        return 0;
    }


# Read line of integers find Max and Min
    #include<iostream>
    #include<sstream>
    #include<string>
    
    int main(){
        std::string line;
        std::string num_s;
        int num;
        int maxNum = 0;
        int minNum = 100;
        int sum = 0; 
        char delim = ' ';
        
        std::getline(std::cin, line);       //you get a string
        std::stringstream lineNum(line);    //convert string into stream for next getline
        
        while (std::getline(lineNum, num_s, delim)){
            
            std::stringstream(num_s) >> num;//convert string into integer
            if (num>maxNum) maxNum= num;
            if (num<minNum) minNum= num;
            sum+=num;
        }
        std::cout<<maxNum<<std::endl;
        std::cout<<minNum<<std::endl;
        std::cout<<sum/15.0<<std::endl;
        
        return 0;
    }
    


# Arrays
    variableType arrayName [ ] = {//variables to be stored in the array};

or as:

    variableType arrayName[array size]

it supports multidimensional arrays

    typeOfVariable arrayName\[size of dim.1\][size of dim. 2] ...[size of dim. n];


    int array2Dimensions\[2\][3]; //Creates [2rowsx3columns] array of integers.
    int array2Dim\[2\][3] = {0,1,2,3,4,5}; // [0 1 2; 3 4 5]


## Sort

algorithm: guarantees that max is always pushed to the right of array, then push the second max to the left of first max and so on/

    #include <iostream>
    #include <stdio.h>
    
    int main() {
        int userInput[40];
        //Read and Print on the go
        for(int i = 0; i <40; ++i){
            std::cin >> userInput[i];
            std::cout << userInput[i]<<' ';
        }
        //Reverse Print
        std::cout << '\n';
        for(int i = 39; i >=0; --i) std::cout << userInput[i]<<' ';
        
        //Sorted Print
        std::cout << '\n';
        for(int i = 0; i < 40; i++){
            for(int j = 0; j < 39 - i; j++){ //no need to go all the way to the right
                if(userInput[j] > userInput[j + 1]){
                    int temp;
                    temp=userInput[j];
                    userInput[j]=userInput[j + 1];
                    userInput[j + 1]=temp;
                }
            }
        }
        //std::sort(userInput,userInput+40);
        for(int i = 0; i <40; ++i) std::cout << userInput[i]<<' ';
        
        return 0;
    }


## Find location of an input element in array

scanf  and printf 

https://www.geeksforgeeks.org/cincout-vs-scanfprintf/

     #include <iostream>
     #include <stdio.h>
    
     int main(){
         int searchKey = 0;
         int searchArray[10] = {324,4567,6789,5421345,7,65,8965,12,342,485};
         int location = 0;
    
         while(1){
             std::cout<<"Enter an integer ('-1' to quit): ";
             scanf("%d", &searchKey);
             std::cout<< searchKey<<"\n";
             if(searchKey == -1) break;
             int searchArrayLength = sizeof(searchArray)/sizeof(searchArray[0]);
             location = -1;
             for(size_t i=0; i<searchArrayLength; ++i){
                if(searchArray[i]==searchKey){
                  location = i;
                  break; 
                }
             }
    
             if(location != -1){
                 std::cout<<searchKey<<" is at location "<<location<<" in the array.\n";
             }
             else{
                 std::cout<<searchKey<<" is not in the array.\n";
             }
        }
         return 0;
     }


## Multiply arrays

std::cin skips empty spaces if there are any

    #include<iostream>
    int main(){
    
        //TODO: multiply a 4x4 array with vector of size 4. 
        //Print the resultant product vector
        int M\[4\][4];
        int x[4];
    
        //Read M
        for(size_t i=0; i<4; ++i)
            for(size_t j=0; j<4; ++j)
            {
                std::cin >> M\[i\][j];
            }
        //No need to read empty space cin skips that automatically
        
        //Read x
        for(size_t i=0; i<4; ++i)
        {
            std::cin >> x[i];
        }
    
        //Multiply y = Mx
        int cum_sum=0;
        int y[4];
        for(size_t i=0; i<4; ++i)
        {
            for(size_t j=0; j<4; ++j)
            {
                cum_sum += M\[i\][j]*x[j];
            }
            y[i] = cum_sum;
            cum_sum = 0;
        }
        
        //Print y
        for(size_t i=0; i<4; ++i)
        {
            std::cout << y[i] << std::endl;
        }
        
        return 0;
    }


# Functions

Function declarations  and definitions go in the header file: main.hpp

    #include "main.hpp"
    int main()
    {
        char operation = '/';
        float input1 = 9.8;
        float input2 = 2.3;
        float result;
    
        calculate(input1, input2, operation, result);
        printEquation(input1, input2, operation, result);
        return 0;
    }

The main.hpp file

    /*The header file for main.cpp*/
    #include<iostream>
    
    // Declarations
    void calculate(float in1, float in2, char op, float &ans);
    void printEquation(float input1,float input2, char operation, float result);
    
    //Definitions
    void calculate(float in1, float in2, char op, float &ans)
    {
        switch(op)
        {
            case '+': ans = in1 + in2;
                      break;
            case '-': ans = in1 - in2;
                      break;   
            case '*': ans = in1 * in2;
                      break;
            case '/': ans = in1 / in2;
                      break;
            default:  std::cout<<"Illegal operation\n";
        }
    }
    void printEquation(float input1,float input2, char operation, float result)
    {
        std::cout<<input1<<" "<<operation<<" "<<input2<<" = "<<result<<"\n";
    }


## By reference or Return Copy
    #include<iostream>
    void increment(int &input); //Note the addition of '&'
    
    int main(){
        int a = 34;
        std::cout<<"Before the function call a = "<<a<<"\n";
        increment(a);
        std::cout<<"After the function call a = "<<a<<"\n";
        return 0;
    }
    void increment(int &input)//Note the addition of '&'
    {
        input++; //**Note the LACK OF THE addition of '&'**
        std::cout<<"In the function call a = "<<input<<"\n";
    }


    #include<iostream>
    int increment(int input);
    int main(){
        int a = 34;
        std::cout<<"Before the function call a = "<<a<<"\n";
        a = increment(a);
        std::cout<<"After the function call a = "<<a<<"\n";
        return 0;
    }
    int increment(int input){
        input++;
        std::cout<<"In the function call a = "<<input<<"\n";
        return input;
    }
## Arrays as Function Parameters

C++ does not allow arrays to be passed to functions, but, as we have seen, it does allow pointers to be passed. 

There are three methods for passing an array by reference to a function:

- void functionName(variableType *arrayName)
- void functionName(variableType arrayName[length of array])
- void functionName(variableType arrayName[])


    /*Goal: Learn to pass arrays to functions*/
    #include<iostream>
    #include<iomanip>
    
    //Pass the array as a pointer
    void arrayAsPointer(int *array, int size);
    //Pass the array as a sized array
    void arraySized(int array[3], int size);
    //Pass the array as an unsized array
    void arrayUnSized(int array[], int size);
    
    int main()
    {
        const int size = 3;
        int array[size] = {33,66,99};
        //We are passing a pointer or reference to the array
        //so we will not know the size of the array
        //We have to pass the size to the function as well
        arrayAsPointer(array, size);
        arraySized(array, size);
        arrayUnSized(array, size);
        return 0;
    }
    
    void arrayAsPointer(int *array, int size)
    {
        std::cout<<std::setw(5);
        for(int i=0; i<size; i++) 
            std::cout<<array[i]<<" ";
        std::cout<<"\n";
    }
    
    void arraySized(int array[3], int size)
    {
        std::cout<<std::setw(5);
        for(int i=0; i<size; i++)
            std::cout<<array[i]<<" ";
        std::cout<<"\n";  
    }
    
    void arrayUnSized(int array[], int size)
    {
        std::cout<<std::setw(5);
        for(int i=0; i<size; i++)
            std::cout<<array[i]<<" ";
        std::cout<<"\n";  
    }
# Separate Header and Implementation Files

http://www.math.uaa.alaska.edu/~afkjm/csce211/handouts/SeparateCompilation.pdf

    /**
     * This is how the car works. No need to make any changes here.
     */
    
    #include "Car.h"
    
    #include <stdlib.h>
    #include <time.h>
    #include <iostream>
    
    // Constructor.
    Car::Car() {
      // initialize random seed for wearAndTear
      srand(time(NULL));
      // start off in working condition
      in_working_condition_ = true;
    }
    
    // Determine whether or not the car is still drivable after some wear and tear.
    void Car::wearAndTear() {
      // 50% chance that the car is still working after wear and tear
      int condition = rand() % 10;
      condition >= 5 ? in_working_condition_ = true : in_working_condition_ = false;
    }
    
    // Try to drive the car.
    bool Car::drive() {
      bool didDrive = false;
    
      if (in_working_condition_) {
        std::cout << "Driving!" << std::endl;
        wearAndTear();
        didDrive = true;
      } else {
        std::cout << "Broken down. Please fix." << std::endl;
        didDrive = false;
      }
    
      return didDrive;
    }
    
    
    // Fix the car.
    void Car::fix() {
      in_working_condition_ = true;
      std::cout << "Fixed!" << std::endl;
    }
    

the header is 

    #ifndef CAR_H
    #define CAR_H
    
    class Car {    
     public:
      Car();
      void wearAndTear();
      bool drive();
      void fix();
     private:
      bool in_working_condition_;
    };
    
    #endif  // CAR_H

