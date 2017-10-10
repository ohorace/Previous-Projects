```java
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */

/**
 *
 * @author Vladimir
 */
public interface QueueInterface<E> { 
  
  /** 
   * Returns the number of elements in the queue.
   * @return number of elements in the queue.
   */
  public abstract int size(); 
  
  /** 
   * Returns whether the queue is empty.
   * @return true if the queue is empty, false otherwise.
   */
   public abstract boolean isEmpty(); 
 
   /**
   * Inspects the element at the front of the queue.
   * @return element at the front of the queue.
   */
    public abstract E front(); 
  
    /** 
   * Inserts an element at the rear of the queue.
   * @param element new element to be inserted.
   */
    public abstract void enqueue (E element); 
  
   /** 
   * Removes the element at the front of the queue.
   * @return element removed.
   */
  public abstract E dequeue();
  
  abstract String toString();
  
 } 
```