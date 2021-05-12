# Learning C

## Writing to the console
`printf` is used to write to the console
```c
printf("Hello World");
```

## Variables
A variable has a type, a name and a value and are defined like this
```c
int age = 24;
```
First we define that the variable is of the type `int` (number) then we define
the name (age in this case) and after a `=` the value

## Using variables in printf
To print out the value of a variable we have to use placeholders,
that are describing what type of value we want to print
```c
char name[] = "Marcel"
int age = 24

printf("%s", name);
printf("%d", age);
```
in this case `%s` stands for a string and `%d` for a digit

other format identifiers are:

- `%f` for a float
- `%c` for a character
- `%x` for a hex int
- `%p` for a pointer address

more can be found [here](https://www.cplusplus.com/reference/cstdio/printf/)

## Data Types
- `int`		=>	number without decimal places
- `double`	=>	number with decimal places
- `float`	=>	number with decima`
comment
*/
```

## Constants
Constants are like variable but they only can be defined **once**

The best practice is to name constants in upper-case letters 
so they can be identified as such e.g. `const float PI = 3.14`
```c
const float PI = 3.14;

[...]

PI = 5; //This will throw a error
```

## User Input
We can use `scanf` to get a input from the user via the console,
but this leads to issues with strings (`%s`) since it's just grabbing the
characters to the first space.

scanf is expecting the following paramters:

- format of the input (Data type)
- where to save it to (pointer to a variable)
```c
int age;
scanf("%d", &age);
```

To get around the issue with the strings we can use `fgets` 
which will read a whole line, however this function **cannot** convert the
input to a different data type than a string.
So the input read by this function is **always** a string!

A downside of `fgets` is that the newline character from pressing enter
to confirm the input will be included in the string.

fgets expects the following paramters:

- variable to store the input in (type char[])
- character input limit (int)
- where to get the input from (`stdin` for console input)

```c
char fullName[50];

//Limit to 50 since that how many characters our array can store
fgets(fullName, 50, stdin);
```

## Arrays
Arrays store multiple values of one type, you have to know how many values
you want to store in beforehand, since the program needs allocate the space
for the values in the memory.

If you assign the values at the time you are defining the array, you don't need
to define the size, in this case the size will be the amount of values you have
specified.
```c
//Size dont need to be specified here, size will be 3.
int numbers[] = {21,32,64};

//Size needs to be specified
int prices[10]; 
```

## Functions / Methods
Functions can have a return type (a value they give back when called), if it doesnt need to return something, the `void` keyword is used.

```c
void SayHello(){
    printf("Hello User");
}
```

Function also can have parameters, parameters are used to pass variables to a function. Parameters specified in the parentesis
```c
void SayHello(char name[]){
    printf("Hello %s", name);
}
```

The function in the following example returns the cube of the parameter `num` as a `double`. So if we specified a return value, `double` in this case we also **need** to return a double with the `return` keyword.
The `return` statement will immediatly return the specified value end exit out of the function.

Also we need to create the function **before** we use it or define a `prototype` before we use it
```c
//Prototype of the function
double GetCube(double num);

// Defined before usage
double GetSquare(double num){
    return num ^ 2.0;
}

int main(){
    //Usage of function
    prinf("%f",GetSquare(5));

    //Usage of function
    prinf("%f",GetCube(5)); 
}

//The function we declared a prototype for
double GetCube(double num){
    return num ^ 3.0;
}
```

## IF Statements
If statements are straight forward if this then that, if statements operate on boolean values (`true` or `false`). So the expression inside the parentesis have to return a boolean value.

But there are some operators we need to learn first:
- `==` Checks if the values of two operands are equal or not. If yes, then the condition becomes true.
- `!=` Checks if the values of two operands are equal or not. If the values are not equal, then the condition becomes true.
- `>` Checks if the value of left operand is greater than the value of right operand. If yes, then the condition becomes true.
- `<` Checks if the value of left operand is less than the value of right operand. If yes, then the condition becomes true.
- `>=` Checks if the value of left operand is greater than or equal to the value of right operand. If yes, then the condition becomes true.
- `<=` Checks if the value of left operand is less than or equal to the value of right operand. If yes, then the condition becomes true.
- `&&` Called Logical AND operator. If both the operands are non-zero, then the condition becomes true.
- `||` Called Logical OR Operator. If any of the two operands is non-zero, then the condition becomes true.

```c
if(value){
    //value is true
}
else{
    //value is false
}
```

so with the knowledge of the operators we can compare if 2 numbers are equal for example
```c
//Define 2 numbers
int fistNum = 1;
int secondNum = 2

//Use the '==' operator to check if both numbers are equal
if(firstNum == secondNum){
    printf("Numbers are equal");
}
else{
    printf("Numbers are not equal");
}
```
So in this case we would see `Numbers are not equal` in the terminal.

If we need serveral if condidtions in series we can chain them together
```c
if(age < 18){
    printf("You are allowed to pass");
} 
else if (age == 18){
    printf("Close call, but you are allowed to pass");
}
else{
    printf("Sorry, you are not allowed to pass");
}
```

## Switch Statements
Switch statements are similar to if statements but they just compare if a value is equal to something.
For example if u have a menu with different choices (e.g. 1-5), you can use a switch statement for that.

Imagine we have a tool that lets us do work on a database table, the menu logic would look like that
```c
char choice;

//Print our menu choices
printf("1. Create");
printf("2. Delete");
printf("3. Insert");
printf("4. Update");
printf("5. Quit");

//Get the choice from the user
scanf(" %c" &choice);

//Now the switch statement
switch(choice){
    case '1':
        printf("Creating entry");
        break;
    case '2':
        printf("Deleting entry");
        break;
    case '3':
        printf("Inserting entry");
        break;
    case '4':
        printf("Updating entry");
        break;
    case '5':
        printf("Exiting application");
        break;
    default:
        printf("Not a valid choice");
        break;
}
```
Our switch statement compares the value in the parentesis `choice` in our case with the defined values behind the `case`. If both values `match` the code inside the case will be executed.

If you haven't already noticed in every `case` statement there is `break`, this is needed if we want to exit after executing the case statement. If we dont't specify it the switch statement will `continue` to search for matches until it reaches the end.

Also there is a `defult` at the end that will be executed if nothing matches (or you dont put a break inside the case statement)