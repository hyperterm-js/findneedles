<!-- Confidential + Proprietary Google&#174;-->
<!-- Exercise #1 - findNeedles (required)-->
<!-- This exercise has two required parts:-->
<!--
1. Write an API reference document that explains
how to call this method. Your audience for this
document is an experienced Java programmer.
 
2. Assume you have a chance to send comments or
questions to the person who wrote the code.
Suggest ways to improve the code, for example,
to reduce memory usage or enhance features -->

# findNeedles() API <a name="top"/>

> **On this page:**
> 
> [Getting Started](#Overview)
- [findNeedles() example](#Example)
- [findNeedles() error messages](#Errors)
>
>[Use case example](#Uses)
>
>[Code references](#Code)
- [Method reference](#Method_ref)
- [Source code reference](#Source_code_ref)

## Getting Started <a name="Overview"/>

**findNeedles()** is a Java-based API called with two mandatory user input parameters:

- `String[] needles`: an array of **up to 5 elements**; referred to as *needles* or *needle*
- `String haystack`: a string of unrestricted length; referred to as *haystacks* or *haystack*

**findNeedles()** searches for *needles* in *haystack* and returns each *needle* with the number of times it occurred in *haystack*. 

> :memo: ***findNeedles() is case-sensitive and space-sensitive***
> <a name="case_sensitive"/>
> 
> Positive results are only returned if both the case of words and phrase spacing match exactly between your *needle* and the *haystack*.

> :memo: ***Leaving a parameter blank***
> 
> If you do not include `String[] needles` and `String haystack` parameters, the output will be null. 

[Back to ***On this page***](#top)

### findNeedles() example:<a name="Example"/>
	
	String haystack = "Heavy rain and heavy snow expected tomorrow.";
	String[] needles = {"Heavy", "rain", "snow", "expected", "Friday"};
	findNeedles(String haystack, String[] needles);
	
Returns:
	
	Heavy: 1
	rain: 1
	snow: 1 
	expected: 1
	Friday: 0
	
In this example, `Heavy` returns `1`, because it appears twice in *haystack* but only [once capitalized as in the *needle*](#case_sensitive). Both `rain` and `expected` return `1`, because they each appear once. `Friday` is returned as `0`, because it doesn't appear in *haystack*.

[Back to ***On this page***](#top)

### findNeedles() error messages:<a name="Errors"/>

> 🚨 ***"Too many words!" error message:***
> 
> The array within *String[] needles* can only take up to 5 elements. 

	String haystack = "Heavy rain and heavy snow expected tomorrow.";
	String[] needles = {"Heavy", "heavy", "rain", "snow", "expected", "Friday"};
	findNeedles(String haystack, String[] needles);
	
Returns:
	
	Too many words!


[Back to ***On this page***](#top)

## Use case example<a name="Uses"/>

The following is an example of a **findNeedles()** use case:

- SEO keyword indexing:
	- Given a keyword list as *needles* and your files as *haystacks*, 
	you can iterate over the files and compare your list of *needles* using each 
	file (converted to a string) as a *haystack*. Each *needle* is counted and 
	you can see the frequency your targets use the list of keywords.
	
[Back to ***On this page***](#top)

## Code references <a name="Code"/>

### Method reference <a name="Method_ref"/>

Method | findNeedles()      
------ | ------
Description | Java-based API that performs ***case-sensitive*** and ***space-sensitive*** searches for array elements in a string and returns the frequency for each element found
Parameters | Mandatory; `String haystack`: A string of unrestricted length. <br> Mandatory; `String[] needles`: An array of **up to 5 elements**.<br> 
Error messages | `Too many words!`: More than 5 elements were sent as part of `String[] needles`.

For usage, see [findNeedles() example](#Example).


[Back to ***On this page***](#top)

### Source code reference <a name="Source_code_ref"/>
```java
    public static void findNeedles(String haystack, String[] needles) {
       if (needles.length > 5) {
           System.err.println("Too many words!");
       } else {
           int[] countArray = new int[needles.length];
           for (int i = 0; i < needles.length; i++) {
               String[] words = haystack.split("[ \"\'\t\n\b\f\r]", 0);
               for (int j = 0; j < words.length; j++) {
                   if (words[j].compareTo(needles[i]) == 0) {
                       countArray[i]++;
                   }
               }
           }
           for (int j = 0; j < needles.length; j++) {
               System.out.println(needles[j] + ": " + countArray[j]);
           }
       }
   }
```
[Back to ***On this page***](#top)
