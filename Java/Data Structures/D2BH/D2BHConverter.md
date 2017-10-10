```java
/**
 * Class that contains conversion methods
 * D2B method converts a decimal number into a binary number
 * D2H method converts a decimal number into a hexadecimal number
 * Inputs cannot be negative
 * 
 * Data Structures 2108
 * @Olivia Horace 
 * @March 6, 2015
 */
import java.io.*;
import java.util.*;
public class D2BHConverter
{
    Stack<Integer> decimalHolder;
    Stack<String> stringHolder;
    ArrayList<Integer> tempList = new ArrayList<Integer>();//used only to reverse contents in stack

    /**
     * Constructor to instantiate the stack to hold integers
     */
    public D2BHConverter()
    {
        decimalHolder = new Stack<Integer>();
        stringHolder = new Stack<String>();
    }

    /**
     * Method to convert integer to a binary number
     * @param int input, number to be converted
     * @return Stack which contains the conversion
     * 
     * Number converted must have an inital value greater than or equal to 0
     */
    public Stack D2B(int input)
    {
        if(input > 0)
        {
            decimalHolder.push(input%2);//pushe remainder onto the stack
            return D2B(input/2);//runs the method again with the value of input divided by 2
        }
        else
            return decimalHolder;     
    }

    /**
     * Method to convert integer to a hexadecimal number
     * @param int input, number to be converted
     * @return Stack which contains the conversion
     * 
     * Number converted must have an inital value greater than or equal to 0
     */
    public Stack D2H(int input)
    {
        if (input > 0)
        {
            if(input%16 == 10)//adds letters to the stack if the remainder is 10-15
            {
                stringHolder.push("A");
                return D2H(input/16);
            }
            else if(input%16 == 11)
            {
                stringHolder.push("B");
                return D2H(input/16);
            }
            else if(input%16 == 12)
            {
                stringHolder.push("C");
                return D2H(input/16);
            }
            else if(input%16 == 13)
            {
                stringHolder.push("D");
                return D2H(input/16);
            }
            else if(input%16 == 14)
            {
                stringHolder.push("E");
                return D2H(input/16);
            }
            else if(input%16 == 15)
            {
                stringHolder.push("F");
                return D2H(input/16);
            }
            else//otherwise adds the remainder to the stack
            {
                int temp = input%16;
                stringHolder.push(String.valueOf(temp));
                return D2H(input/16);
            }
        }
        else
            return stringHolder;      
    }

    /**
     * Converts stack to arraylist so that it can be reversed
     * Numbers are added to stack in opposite order
     * @param Stack temp, input stack to be converted
     * @return Arraylist of reversed list
     * 
     * Method is used to reverse BINARY
     */
    public ArrayList convertToList(Stack<Integer> temp)
    {
        ArrayList<Integer> tempList = new ArrayList<Integer>();
        for(Integer i : temp)
        {
            tempList.add(i);
        }
        Collections.reverse(tempList);
        return tempList;
    }

    /**
     * Converts stack to arraylist so that it can be reversed
     * Numbers and letters are added to stack in opposite order
     * @param Stack temp, input stack to be converted
     * @return Arraylist of reversed list
     * 
     * Method is used to reverse HEXADECIMAL
     */
    public ArrayList convertToStringList(Stack<String> temp)
    {
        ArrayList<String> tempSList = new ArrayList<String>();
        for(String i : temp)
        {
            tempSList.add(i);
        }
        Collections.reverse(tempSList);
        return tempSList;
    }

    /**
     * ToString method to convert contents of stack to string
     * @return String of contents within stack
     */
    public String toString()
    {
        return tempList.toString();
    }
}
```