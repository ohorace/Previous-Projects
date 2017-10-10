```java
/**
 * This class is used to create a Queue data structure with LinkedList implementation
 * Extends the LinkedList class
 * Implements the QueueInterface
 * 
 * @Olivia Horace
 * @February 20, 2015
 */
import java.io.*;
import java.util.*;
public class MyQueue<E> extends LinkedList<E> implements QueueInterface<E>
{
    //static variable, queue implemented as linked list
    private LinkedList<E> myQueue;
    /**
     * Constructor to intialize myQueue linkedlist
     */
    public MyQueue()
    {
        myQueue = new LinkedList<E>();
    }
       
    /**
     * Method to determine size of queue
     * @return size, number of elements in queue
     */
    public int size()
    {
        return myQueue.size();
    }
    
    /**
     * Method to determine if queue is empty
     * @return true if the queue is empty, false if it is not empty
     */
    public boolean isEmpty()
    {
        if(myQueue.size() == 0)
        {
            return true;
        }
        else
            return false;
    }
    
    /**
     * Method to get first element
     * @E, data that stores first element
     */
    public E front()
    {
        return myQueue.getFirst();
    }
    
    /**
     * Method to add element
     * @param E element, element to be added
     */
    public void enqueue(E element)
    {
        myQueue.addLast(element);
    }
    
    /**
     * Method to remove first element from queue
     * @return E, element at the beginning of queue
     */
    public E dequeue()
    {
        return myQueue.remove();
    }

    /**
     * Method to display elements in queue
     * @return String of queue elements
     */
    public String toString()
    {
        return "" + myQueue;
    }
}
```