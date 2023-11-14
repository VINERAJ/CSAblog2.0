---
toc: True
comments: True
layout: post
title: Unit 6 Arrays
description: Lesson on the College Board Unit 6 Arrays.
courses: {'compsci': {'week': 9}}
type: hacks
---

## Intro into Arrays

- An **array** is a data structure used to implement a collection (list) of primitive or object reference data.

- An **element** is a single value in the **array**

- The __**index**__ of an **element** is the position of the element in the **array**

    - In java, the **first element** of an array is at **index 0**.

- The **length** of an **array** is the number of elements in the array.

    - **`length`** is a `public final` data member of an array

        - Since `length` is `public`, we can access it in **any class**!

        - Since `length` is `final` we cannot change an array's `length` after it has been created
    - In Java, the **last element** of an array named `list` is at **index** `list.length -1`

## A look into list Memory
`int [] listOne = new int[5];`

This will allocate a space in memory for 5 integers.

```
ARRAY: [0, 0, 0, 0, 0]
INDEX:  0  1  2  3  4
```

Using the keyword new uses the default values for the data type. The default values are as follows:

| Data Type | Default Value |
| --------- | ------------- |
| byte      | (byte) 0      |
| short     | (short) 0     |
| int       | 0             |
| double    | 0.0           |
| boolean   | false         |
| char      | '\u0000'      |

What do we do if we want to insert a value into the array?

`listOne[0] = 5;`

Gives us the following array:

```
ARRAY: [0, 0, 0, 0, 0]
INDEX:  0  1  2  3  4
```

What if we want to initialize our own values? We can use an initializer list!

`int [] listTwo = {1, 2, 3, 4, 5};`

Gives us the following array:

```
ARRAY: [1, 2, 3, 4, 5]
INDEX:  0  1  2  3  4
```

If we try to access an index outside of the range of existing indexes, we will get an error. But why? Remember the basis of all programming languages is memory. Because we are trying to access a location in memory that does not exist, java will throw an error (`ArrayIndexOutOfBoundsException`).

How do we print the array? Directly printing the array will not work, it just prints the value of the array in memory. We need to iterate through the array and print each value individually!


```java
/* lets take a look at the above */

int [] listOne = new int[5]; // Our list looks like [0, 0, 0, 0, 0]

listOne[2] = 33; // Our list looks like [0, 0, 33, 0, 0]
listOne[3] = listOne[2] * 3; // Our list looks like [0, 0, 33, 99, 0]

try {
    listOne[5] = 13; // This will return an error
} catch (Exception e) {
    System.out.println("Error at listOne[5] = 13");
    System.out.println("ArrayIndexOutOfBoundsException: We can't access a memory index that doesn't exist!");
}


System.out.println(listOne); // THIS DOES NOT PRINT THE LIST!! It prints the value in memory
System.out.println(listOne[4]); // This will actually print the vaules in the array
```

    Error at listOne[5] = 13
    ArrayIndexOutOfBoundsException: We can't access a memory index that doesn't exist!
    [I@7fbfce4e
    0


## Popcorn Hacks!

Write code to print out every element of listOne the following


```java
/* popcorn hacks go here */
int [] listOne = new int[5];
listOne[2] = 33; 
listOne[3] = listOne[2] * 3;
for (int i = 0; i<listOne.length; i++) {
    System.out.println(listOne[i]);
}
```

    0
    0
    33
    99
    0


## Reference elements

Lists can be made up of elements other than the default data types! We can make lists of objects, or even lists of lists! Lets say I have a class `Student` and I want to make a list of all students in the class. I can do this by creating a list of `Student` objects.

```
Student [] classList;
classList new Student [3];
```

Keep in mind, however, that the list won't be generated with any students in it. They are initialized to `null` by default, and We need to create the students and then add them to the list ourselves.

```
classList[0] = new Student("Bob", 12, 3.5);
classList[1] = new Student("John", 11, 4.0);
classList[2] = new Student("Steve", 10, 3.75);
```

## Popcorn hacks!

Use a class that you have already created and create a list of objects of that class. Then, iterate through the list and print out each object using:
 1) a for loop
 2) a while loop


```java
/* Popcorn hacks go here */
public class Book {
    private int pages;
    private String title;

    public Book (int pages, String title) {
        this.pages = pages;
        this.title = title;
    }

    public int getPages() {
        return this.pages;
    }

    public String getTitle() {
        return this.title;
    }

    public static void main(String[] args) {
        Book[] bookList = new Book[5];
        bookList[0] = new Book(200, "CSA");
        bookList[1] = new Book(105, "CSP");
        bookList[2] = new Book(50, "CSSE");
        bookList[3] = new Book(100, "AP Stats");
        bookList[4] = new Book(150, "AP Gov");
        for (int i=0; i<bookList.length; i++) {
            System.out.println("Book " + (i+1) + ": Title: " + bookList[i].getTitle() + ", Pages: " + bookList[i].getPages());
        }
        System.out.println("");
        int j = 1;
        while (j<=5) {
            System.out.println("Book " + (j) + ": Title: " + bookList[j-1].getTitle() + ", Pages: " + bookList[j-1].getPages());
            j++;
        }
    }
}
Book.main(null);
```

    Book 1: Title: CSA, Pages: 200
    Book 2: Title: CSP, Pages: 105
    Book 3: Title: CSSE, Pages: 50
    Book 4: Title: AP Stats, Pages: 100
    Book 5: Title: AP Gov, Pages: 150
    
    Book 1: Title: CSA, Pages: 200
    Book 2: Title: CSP, Pages: 105
    Book 3: Title: CSSE, Pages: 50
    Book 4: Title: AP Stats, Pages: 100
    Book 5: Title: AP Gov, Pages: 150


## Enhanced for loops

The enhanced `for` loop is also called a for-each loop. Unlike a "traditional" indexed `for` loop with three parts separated by semicolons, there are only two parts to the enhanced `for` loop header and they are separated by a colon.

The first half of an enhanced `for` loop signature is the type of name for the variable that is a copy of the value stored in the structure. Next a colon separates the variable section from the data structure being traversed with the loop.

Inside the body of the loop you are able to access the value stored in the variable. A key point to remember is that you are unable to assign into the variable defined in the header (the signature)

You also do not have access to the indices of the array or subscript notation when using the enhanced `for` loop.

These loops have a structure similar to the one shown below:

```js
for (type declaration : structure )
{
    // statement one;
    // statement two;
    // ...
}
```

## Popcorn Hacks!

Create an array, then use a enhanced for loop to print out each element of the array.


```java
/* Popcorn hacks go here */
int[] newArray = new int[3];
newArray[0] = 5;
newArray[1] = 4;
newArray[2] = 6;
for (int element: newArray) {
    System.out.println(element);
}
```

    5
    4
    6


## Min maxing

It is a common task to determine what the largest or smallest value stored is inside an array. in order to do this, we need a method that can ake a parameter of an array of primitive values (`int` or `double`) and return the item that is at the appropriate extreme.

Inside the method of a local variable is needed to store the current max of min value that will be compared against all the values in the array. you can assign the current value to be either the opposite extreme or the first item you would be looking at.

You can use either a standard `for` loop or an enhanced `for` loop to determine the max or min. Assign the temporary variable a starting value based on what extreme you are searching for.

Inside the `for` loop, compare the current value against the local variable, if the current value is better, assign it to the temporary variable. When the loop is over, the local variable will contain the approximate value and is still available and within scope and can be returned from the method.

## Popcorn Hacks!
Create two lists: one of ints and one of doubles. Use both a standard for loop and an enhanced for loop to find the max and min of each list.


```java
/* Popcorn hacks go here! */
public class minMax {
    public static int maxInt1(int[] intArray) {
        int max = -2147483647;
        for (int i = 0; i<intArray.length; i++) {
            if (intArray[i]>max) {
                max = intArray[i];
            }
        }
        return max;
    }

    public static int maxInt2(int[] intArray) {
        int max = -2147483647;
        for (int element: intArray) {
            if (element>max) {
                max = element;
            }
        }
        return max;
    }

    public static int minInt1(int[] intArray) {
        int min = 2147483647;
        for (int i = 0; i<intArray.length; i++) {
            if (intArray[i]<min) {
                min = intArray[i];
            }
        }
        return min;
    }

    public static int minInt2(int[] intArray) {
        int min = 2147483647;
        for (int element: intArray) {
            if (element<min) {
                min = element;
            }
        }
        return min;
    }

    public static double maxDouble1(double[] doubleArray) {
        double max = 2.2250738585072014E-308;
        for (int i = 0; i<doubleArray.length; i++) {
            if (doubleArray[i]>max) {
                max = doubleArray[i];
            }
        }
        return max;
    }

    public static double maxDouble2(double[] doubleArray) {
        double max = 2.2250738585072014E-308;
        for (double element: doubleArray) {
            if (element>max) {
                max = element;
            }
        }
        return max;
    }

    public static double minDouble1(double[] doubleArray) {
        double min = 1.79769313486231570e+308d;
        for (int i = 0; i<doubleArray.length; i++) {
            if (doubleArray[i]<min) {
                min = doubleArray[i];
            }
        }
        return min;
    }

    public static double minDouble2(double[] doubleArray) {
        double min = 1.79769313486231570e+308d;
        for (double element: doubleArray) {
            if (element<min) {
                min = element;
            }
        }
        return min;
    }

    public static void main(String[] args) {
        int[] intArray = new int[3];
        for (int j=0; j<=2; j++) {
            intArray[j] = j;
        }
        double[] doubleArray = new double[3];
        for (int h=0; h<=2; h++) {
            doubleArray[h] = 0.5+h;
        }
        System.out.println(maxInt1(intArray));
        System.out.println(maxInt2(intArray));
        System.out.println(minInt1(intArray));
        System.out.println(minInt2(intArray));
        System.out.println(maxDouble1(doubleArray));
        System.out.println(maxDouble2(doubleArray));
        System.out.println(minDouble1(doubleArray));
        System.out.println(minDouble2(doubleArray));
    }
}
minMax.main(null);
```

    2
    2
    0
    0
    2.5
    2.5
    0.5
    0.5


Hacks! (Due 10/22 11:59 PM)
Given an input of N integers, find A, the maximum, B, the minimum, and C the median.

Print the following in this order: A + B + C A - B - C (A + B) * C

Sample data:

I: 1 2 3 4 5
O: 9 1 18

I: 2 4 6 8 10 12 14 16
O: 28 6 180
For extra, create your own fun program using an array


```java
public class ArrayHacks {
    public int[] hacksArray(int[] array) {
        int[] hackArray = array;
        return hackArray;
    }
    
    public int findMax(int[] array) {
        int max = Integer.MIN_VALUE;
        for (int element:array) {
            if(element>max) {
                max = element;
            }
        }
        return max;
    }

    public int findMin(int[] array) {
        int min = Integer.MAX_VALUE;
        for (int element: array) {
            if(element<min) {
                min = element;
            }
        }
        return min;
    }

    public int findMedian(int[] array) {
        int median = 0;
        int size = array.length;
        if (size%2!=0) {
            median = array[(size/2)];
        }
        else {
            median = (array[size/2]+array[(size/2)-1])/2;
        }
        return median;
    }

    public String calculations(int max, int min, int median) {
        int equation1 = max+min+median;
        int equation2 = max-min-median;
        int equation3 = (max+min)*median;
        return equation1 + " " + equation2 + " " + equation3;
    }

    public static void main(String[] args) {
        ArrayHacks arrayHacks = new ArrayHacks();
        int[] hackArray = arrayHacks.hacksArray(new int[] {1, 2, 3, 4, 5}); 
        int max = arrayHacks.findMax(hackArray);
        int min = arrayHacks.findMin(hackArray);
        int median = arrayHacks.findMedian(hackArray);
        System.out.println(arrayHacks.calculations(max, min, median));

        int[] hackArray2 = arrayHacks.hacksArray(new int[] {2,4,6,8,10,12,14,16}); 
        int max2 = arrayHacks.findMax(hackArray2);
        int min2 = arrayHacks.findMin(hackArray2);
        int median2 = arrayHacks.findMedian(hackArray2);
        System.out.println(arrayHacks.calculations(max2, min2, median2));
        
    }
}
ArrayHacks.main(null);
```

    9 1 18
    27 5 162

