```java
/**
 * Animal superclass with species, type, and weight instance variables and static foodBox variable
 * Contains set and get methods for instances variables
 * Contains feed method which is overridden in subclasses
 * Contains toString method
 * 
 * @Olivia Horace
 * @November 26, 2014
 */
import java.util.*;
public class Animal implements Feedable
{
    String species;
    String animalType;
    int weight;
    static int foodBox = 100;
    /**
     * Default constructor 
     * Creates generic animal object
     */
    public Animal()
    {
        setSpecies("Generic");
        setType("House pet");
        setWeight(100);
    }

    /**
     * Custom constructor 
     * @param String newSpecies, species of animal
     * @param String newType, specific type of animal
     * @param int newWeight, weight of animal
     * 
     * Uses set methods to assign paramaters to instance variables
     */
    public Animal(String newSpecies, String newType, int newWeight)
    {
        setSpecies(newSpecies);
        setType(newType);
        setWeight(newWeight);
    }

    /**
     * setSpecies method 
     * @param String nSpecies, new species
     * Assigns parameter to species variable
     */
    public void setSpecies(String nSpecies)
    {
        species = nSpecies;
    }

    /**
     * setType method
     * @param String nType, new type
     * Assigns parameter to animalType variable
     */
    public void setType(String nType)
    {
        animalType = nType;
    }

    /**
     * setWeight method
     * @param int nWeight, new weight
     * Assigns parameter to weight variable
     */
    public void setWeight(int nWeight)
    {
        weight = nWeight;
    }

    /**
     * setFood method
     * @param int nFood, new food
     * the parameter to static variable foodBox
     */
    public static void setFood(int nFood)
    {
        foodBox = nFood;
    }

    /**
     * getSpecies method
     * @return species
     * Returns species variable
     */
    public String getSpecies()
    {
        return species;
    }

    /**
     * getType method
     * @return animalType
     * Returns animalType variable
     */
    public String getType()
    {
        return animalType;
    }

    /**
     * getWeight method
     * @return weight
     * Returns weight variable
     */
    public int getWeight()
    {
        return weight;
    }

    /**
     * getFood method
     * @return foodBox
     * Returns foodBox variable
     */
    public static int getFood()
    {
        return foodBox;
    }

    /**
     * feed method to feed Animal object
     * Subtracts 1 from foodBox 
     * Reassigns the value of foodBox by using the setFood method
     * If the foodBox has a value of 0 or less, the foodBox is reset to 100
     */
    public void feed()
    {
        if(foodBox <= 0)
        {
            setFood(100);
        }
        setFood(foodBox -1);
    }

    /**
     * doSomethingWhenFed method to increase the weight of object after being fed
     * Weight variable is increased by 1
     */

    public void doSomethingWhenFed()
    {
        weight += 1;
    }

    /**
     * toString method to print objects of Animal class
     * @return String containing animal species, animal type, and weight
     */
    public String toString()
    {
        return "Animal Species: " + species + "\nAnimal Type: " + animalType + "\nAnimal Weight (lbs): " + weight + "\n \n";
    }

}
```