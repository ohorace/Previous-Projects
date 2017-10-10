```java
/**
 * Purpose: Tester method to test binary and hexidecimal conversions
 * Input: A decimal integer taken from the keyboard that must not be negative
 * Output: The binary and hexidecimal conversion of decimal input
 * Conditions: Numbers to be converted cannot be negative
 * 
 * Data Structures 2108
 * @Olivia Horace
 * @March 6, 2015
 */
import java.io.*;
import java.util.*;
public class D2BHTester
{
    public static void main(String args[])
    {
        int number;
        while(true)//while loop to make sure number entered is greater than or equal to 0
        {
            Scanner kbReader = new Scanner(System.in);
            System.out.print("Enter a non-negative number: ");
            number = kbReader.nextInt();
            if(number < 0)
            {
                System.out.println("Please enter a number that is not negative!");
            }
            else
                break;
        }
        D2BHConverter convert = new D2BHConverter();

        ////////////////////////////////////////////////////////////////////////////
        ///////////Prints answer without brackets, spaces, and commas////////////////
        //////////Creates a new stack with results of convert method////////////////

        Stack<Integer> testStack = convert.D2B(number);
        String newString = convert.convertToList(testStack).toString().replaceAll("\\[", "").replaceAll("\\]","").replaceAll(",","").replaceAll(" ","");
        System.out.print(number + " in binary: " + newString + "\n");

        Stack<String> testString = convert.D2H(number);
        String convertString = convert.convertToStringList(testString).toString().replaceAll("\\[", "").replaceAll("\\]","").replaceAll(",","").replaceAll(" ","");
        System.out.print(number + " in hexadecimal: " + convertString);
    }
}
```