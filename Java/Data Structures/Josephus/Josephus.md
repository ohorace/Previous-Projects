```java
/**
 * Program to simulate Josephus problem
 * Input: Takes number of people and which position gets executed from the keyboard
 * Output: Prints the survivor as well as who gets executed
 * Data Structures 2108
 * 
 * @Olivia Horace
 * @February 22, 2015
 */
import java.io.*;
import java.util.*;
public class Josephus
{
    public static void main(String args[])
    {
        Scanner kbReader = new Scanner(System.in);
        System.out.print("Enter number of people in the circle: ");
        int circleCount = kbReader.nextInt();
        
        System.out.print("Enter which position gets executed: ");
        int exec = kbReader.nextInt();
        
        MyQueue myCircle = new MyQueue();
        for(int i = 1; i <= circleCount; i++)//adds the amount of people indicated by circleCount
        //starts counting at 1 so zero will not be first index and increments to the exact value of circleCount
        {
            myCircle.enqueue(i);
        }
        System.out.println("\n" + "Current circle: " + myCircle.toString() + "\n");
        
        while(myCircle.size() > 1)//while loop exeutes as long as the size is greater than 1
        {
            for(int j = 0; j < exec-1; j++)//for loop adds elements to the back of the queue until the value of exec-1 is reached
            {
                myCircle.enqueue(myCircle.dequeue());//adds to the end of queue the items removed
            }
            System.out.println(myCircle.dequeue() + " has been executed!!");//dequeues the element at the front (exec position) and prints the result
            System.out.println("Remaining survivors: " + myCircle.toString());//prints the remaining people in the queue
            System.out.println("");//blank line for readability
        }
        System.out.print("\n" + "THE SURVIVOR IS: " + myCircle.front().toString());//prints the last remaining value in queue
    }
}
```