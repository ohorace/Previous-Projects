```Java
/**
 * Project to optimize expressions using Quinne-McCluskey
 * 
 * @Olivia Horace
 * @Spring 2015
 */
import java.io.*;
import java.util.*;
public class Tester
{
    public static void main(String[] args)
    {            
        Scanner scan = new Scanner(System.in);
        while(true)
        {
        System.out.print("Enter number of inputs (0 to quit): ");
        int inputs = scan.nextInt();
        
        QMC test = new QMC();
        if(inputs == 2)
        {
            test.enter2();
        }
        else if (inputs == 3)
        {
            test.enter3();
        }
        else if(inputs == 4)
        {
            test.enter4();
        }
        else if(inputs == 0)
        {
            break;
        }
        else
        {
            System.out.println("Please enter 2,3, or 4!");
        }
    }
}
}
```