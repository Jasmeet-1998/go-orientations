> ## GO Basics

> Intro

- static typed & compiled
- imperative style programming paradigm, no pre-models/metadata for the solution, the written code inside function alone depicts the HOW to reach the actual solution.

- inspired from c performance & python syntax.

- multithreading, concurrent programming possible with scalability.

> Important points to keep in mind

- we write all code in go as package
- entry point to the program basically a function main.
- go run filename
- go build filename --> creates new .exe in the dir & exe file can run in any other OS even when that OS do not have go insatlled.

**Bonus (Cross compiling go code)**

- https://github.com/golang/go/wiki/WindowsCrossCompiling

            set GOOS=windows
            set GOARCH=386
            go build -o initiate.exe initiate.go

now initiate.exe can be run on any windows machine.

will generate a new executable that is linux OS specific

> ### Chapter-1

**Variable & Data Types**

- variable

            #syntax
            var valid_variableName1 type = "initialized value"

            #example

            var name string
            name = "Tim"
            name = "Bill"

- data types

1. Numbers

- Integers - Signed, Unsigned(no negatives)

a) unsigned integers

- uint8 / byte (0-255)
- uint16 (0-65535)
- uint32 (0-42949467295)
- uint64 (0 to 18446744073709551615)

b) signed integers

- int8 (-128 to 127)
- int16 (-32768 to 32767)
- int32/rune (-2147483648 to 2147483647)
- int64 (-9223372036854775808 to 9223372036854775808)

Note- we generally use max uint32 or int32

2. Machine Dependent Types (system automatically figures out how much space would be required on the basis of OS 32 or 64 bit)

- uint (32 or 64 bits)
- int (same size as uint)
- uintptr (unsigned integer to store uninterpreted bits of pointer value)

3. Floating Point Numbers

> floats

- float32 (IEEE 32 bit floating point number)
- float64 (IEEE 64 bit floating point number)

> complex(imaginary parts ioata)

- complex64 (float 32 real and imaginary part)
- complex128 (float 64 real and imaginary part)

4. Strings

- "hello world"

5. Booleans - true or false

> ### Chapter -2

**Assignment Expression & Implicit vs Explicit**

- explicit variable data type declaration

        var number uint16 = 260

- implicit variable data type declaration (go automatically handles types based on the value initialized)

        # number variable type is a number here
        var number = 260
        # number variable type is string now as the value is string
        var number = "yo"

- Expression assignment operator (:=)

        #syntax omit the var keyword, no need to use var here now
        name_ofVariable1 := initialValue

        #example
        number := 6

Note- Its not possible to change the type of already declared variable with a different value or redeclare that variable with same name that has already been instantiated.

        number := 6 // implicit as int
        number = "yo" // error not allowed

        number := "yo" // error not allowed

> Bonus & Important

        var number uint64
        fmt.Println(number) // will be -> 0 (default for uint64)

**All the variable with no initial value has a defualt value a/c to its data type**

        var bl bool
        fmt.Println(bl) // will be-> false

> ### Chapter -3

**Printing to console & fmt**

- Printf(formatter for consoling)

        # Printf act as formatters , like consoling the type of a variable with %T and value with %v
        fmt.Printf("%T %v",10, 20)

        # output
        int 20

- Sprintf (store the value in the variable)

        var x string = fmt.Sprintf("%T %v",10,20)
        fmt.Println(x)
        # output-> int 20

> IMPORTANT (fmt CHEATSHEET)

- General

1. %v (value in default format)
2. %T (Type)
3. %% (literal %) (to print a percent sign)

- Boolean

4. %t (true or false)

- Integer

5. %b (base 2)
6. %o (base 8)
7. %d (base 10)
8. %x (base 16)
9. %X (base 16 in capital letters)

- Floating Points

10. %e (scientific notations) (appends that e like in scientific calculator)
11. %f / %F (decimal no exponent) (omits the e of scientific notation)
12. %g (for large exponents)

- Strings

13. %s (default)
14. %q (double quoted string) (includes the "" of the string)

- Width, Precision & Padding

# syntax

width.precision.f

- %f (default width and precision)
- %9f (width 9 & default precision)
- %.2f (default width & precision 2)
- %9.2f (width 9 & precision 2)
- %9.f (width 9 & precision 0)

- %09d (pads digit to length 9 with preceeding 0's)
- %-4d (pads with spaces (width 4, left justified)) (number)
- %9q (pads with spaces (width 9, right justified )) (string)

> ### Chapter -4

**(Console input)Bufio scanner taking input from user and Type conversions(converting to numeric type)**

Aim- string--> integer or number or float taken from user

- Note- scanner of bufio automatically stores it as string by default , so if user is typing number we need to do string type conversions via **strconv**

> ### Chapter -5

**Arithmatic Operators & Math**

- add +
- sub -
- div /
- mul \*
- modul %
- () regular math to alter the exection a/c to BEDMAS

for doint sqrt, powers ,abs use math package

Note- the operands has to be in the same type to actually perform any operation on those operands.

> ### Chapter-6

**Boolean exp & conditions**

Note- the left & right expression should be of same type to compare them

- >
- <
- <=
- > =
- ==
- !=

> ### Chapter-7

**Chained Boolean exp & conditions**

Note- In case && and || appears together && is evaluated first though if we have bracket around || then the || expression evaluated first

- || (OR)
- && (AND)
- ! (NOT)

> ### Chapter-8

**if,elseif,else conditions**

                if condition {

                }else if condition {

                }else {

                }

> ### Chapter-8

**for & while loops**

                // style1
                x:=initialValue
                for terminationCondition{
                        //do magic
                        x++
                }

                // style2

                for x:=initValue; x<=termValue; inc/dec {
                        //do magic
                }

                // style3
                for _index, _value := range iterableName {
    	                //do magic
                }

> ### Chapter-8

**Switch**

                switch varToCheckTheValueOf{
                        case valueToCheckIComparisonTo:
                        default:
                }

> ## IMPORTANT How are array represented in golang?

                [0,3,6,9]
                0  1 2 3

- array in golang represented by 3 things

1. pointer(by default to 0 index of array)
2. length
3. capacity (equal to length always)

> ### Chapter-9 Arrays

- Note an array only have one type of values

                // an array with at most 5 elements name arrayName and contains string values only
                var arrayName [5]string

                // another way of declaring an array
                arr := [3]int{45,100,1}

> ### Chapter-10 Slices (Portions of array)

- helps to overcome outcomes with array like specifying the size of the array

                array - [0,3,6,9]
                a slice of above array - [3,6]

- how do slices are represented in golang

1.  [pointer] pointing to underlying array from which is sliced
2.  length - number of elements in slice
3.  capcaity - how many elements are possible in slice its length+1

                // if we dont specify the size then it is indeed a slice declaration
                var sliceName []int

                // means start from index 1 and go till 3 but do not include 3
                [1:3]

                // to find capacity
                fmt.println(cap(sliceName))

                // make a slice with keyword make of type slice and capacity 5
                a := make(type,capacity)
                a := make([]int,5)

> ### Chapter -12 Range in slices/array

                // i represent the index of the array or slice
                // element represetn the value on that i index
                for i,element := range a{
                }

> ### Chapter-13 Maps (store key: value pairs) (its uordered unlike array which are ordered)

                // creates a map with string as keys and pointing to values int
                var mp map[string]int

- Map should not be used if we are concerned about the order of data as map dont keep into account for the order of data inserted.

                // check wheather the key exist in the map if yes then grab that
                // ok will be set to true if key1 existon the map mp and store it value in val
                val, ok := mp["key1"]

- Updating, adding , searching in map are faster than array.

> #### NOTE- Only use array when order of the data matters if not just use maps they are faster and better

> ### Chapter-14 Functions (block of reusable code)

- labelled function returns

                func fun(x,y int)(l1,l2 int){
                        l1 = x+y
                        l2 = x-y
                        // automatically returns labeled return variables
                        return
                }

- defer (print or have something right before function is about to return)

> ### Chapter-15 Advanced function concept & functions closure

- function themselves act as datatype like int, float ,number

                        func fun {

                        }
                        func main{
                                // pass the function fun refference to x
                                x:=fun
                                // finally calling that function
                                x()
                        }

                        // pass a function to another function
                        func test2(myParamFunc func(int) int){
                                myFunc(7)
                        }

                        func main{
                                test2(fun)
                        }

> ### Chapter-15 Mutable & Immutable Data Types

> mutable data types are->

1. map (pointer replication)
2. slices (pointer replication)
3. array (no pointer replication)

- map & slices (pointer replication)

> both map and slices are mutable data types which observe a behaviour of pointer replication where on assigning value of existing map or slice variable to new variable will result in pointing of new and old variable to same map or slice address .

> pointer replication if now old variable change then new variable will change & vice-a-versa

> data types that has no pointer replication

- int (no pointer replication i.e no call by refference)
- strings (no pointer replication i.e no call by refference)
- float (no pointer replication i.e no call by refference)
- booleans (no pointer replication i.e no call by refference)
- arrays (pass a copy of the array to new variable so no pointer replication each variable will have its version of values)

> ## Chapter -16 Pointers and derefernece operator [& and *]

- & (pointer)
- [*] (derefernce)

Note- pointer can be used on both mutable & immutable data types to deref and update value via the pointer(&)

        // this means pass me the pointer of this variable i.e call be ref
        *string

        func main (){
                tochange := "hello"
                // *string means a string type pointer that stores address of toChange variable
                var pointer *string = &toChange
                fmt.Println(pointer)
        }

> ## Chapter -17 Structs & Custom types

- struct

        // syntax
        type Structname struct {
                //....
        }
        // the struct name by convention should have first letter in caps

- interface

        // syntax
        type I interface{
                //...
        }

- embeded structs

        type Point struct {
                x int32
                y int32
        }
        // syntax
        type Circle struct {
                radius float64
                // pointer point to the Point struct
                point *Point
        }

> ## Chapter -18 Structs methods

- methods are used to perform any operations on object inside struct

> ## Chapter -19 Interfaces

- interfaces is a set of related objects and types kinda blueprint that the variable name and types are for a particular object

- interface helps in data abstraction i.e hiding the actual implementation.

- interface will only give access to the method or objects that are actually implemented by the struct

- interfaces can be used as any types - variable type, return type, params type , in a map

- an object can implement multiple interfaces.

> ## Chapter-20 map,hashmap,hashtable

- ref: map_hashpam_hashtable.go

                        #syntax
                        map[keyType]valueType

                        #example
                        m := map[string]string{}

- note , by defaulta map is not ordered unless we use ordered map
