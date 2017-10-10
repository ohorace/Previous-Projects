```java
/**
 * Interface containing feed method to be used by animal and plant classes
 * Also contains doSomethingWhenFed Method to be used by animal and plant classes
 * 
 * @Olivia Horace
 * @December 3, 2014
 */
public interface Feedable
{
    /**
     * feed method declaration
     * Does not return a value
     * Takes no parameter
     */
    public void feed();
    public void doSomethingWhenFed();
}
```