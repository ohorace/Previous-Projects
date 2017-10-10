```java
/**
 * Program to check if brackets in an HTML file are balanced
 * Displays Balanced or Unbalanced when run
 * 
 * @Olivia Horace
 * @Feburary 13, 2015
 */
import java.io.*;
import java.util.*;
public class ParenChecker
{
    public static void main(String[] args) throws FileNotFoundException
    {
        File myHTML = new File("ohoraceSample.html");
        Scanner checker = new Scanner(myHTML);

        Stack<Character> charStack = new Stack<Character>();
        boolean result = true; //status of result determines where balanced or unbalanced is printed
        String temp;//used to hold line of text file
        char ch;//used to store characters in the line 
        while(checker.hasNext() && (result = true))//if there are still lines and the result has not been set to false
        {
             temp = checker.nextLine();
             for(int i = 0; i < temp.length(); i++)//scans over the letters/charaters in the line
             {
                 ch = temp.charAt(i);
                 if(ch == '<')//if an open bracket is found it gets pushed onto the stack
                 {
                     charStack.push(ch);
                    }
                    else if(ch == '>')//checks for closing bracket character
                    {
                        if (charStack.isEmpty())//checks if the stack is empty so the program won't attempt to pop an empty stack
                        {
                            result = false;//returns false and the line is unbalanced because there is nothing on the stack to match the closing bracket
                            break;
                        }
                        if(charStack.pop() != '<')//if the character that has been popped doesn't equal an open then it is unbalanced
                        {
                            result = false;
                        }
                    }
                }
        }
        if ((result = false) || (!charStack.isEmpty()))//if the stack is not empty there was an unequal amount of brackets so it is unbalanced OR if an unbalanced criteria was met in the loop
        {
            System.out.print("UNBALANCED");
        }
        else//if the result boolean is still true then html text file is balanced
        {
            System.out.print("BALANCED");
        }
}
}
```