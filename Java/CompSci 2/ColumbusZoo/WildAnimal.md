```java
/**
 * wildAnimals class to manipulate objects created from wildAnimals class
 * Contains tempAnimals arrayList for search method
 * Extends the Animal superclass and overrides feed method
 * 
 * @Olivia Horace 
 * @November 26, 2014
 */
import java.util.*;
public class WildAnimal extends Animal implements Feedable
{
    ArrayList<WildAnimal> tempAnimals = new ArrayList<WildAnimal>();

    /**
     * default constructor 
     *creates default object from superclass
     */public WildAnimal()
    {
        super();
    }

    /**
     * Custom constructor 
     * @param String wSpecies, wild species
     * @param String wType, specific type of wild animal
     * @param int wWeight, weight of wild animal
     * 
     * uses superclass set methods
     */
    public WildAnimal(String wSpecies, String wType, int wWeight)
    {
        super.setSpecies(wSpecies);
        super.setType(wType);
        super.setWeight(wWeight);
    }

    /**
     * Feed method to feed wildAnimal OVERRIDES Animal feed method
     * Generates random number and feeds animal that amount of food
     * Subtracts that amount from foodBox variable in Animal class
     * If foodBox is less than or equal to 0, the foodBox is reset to 100
     * Uses superclass set method to change foodBox variable 
     */
    public void feed()
    {
        Random generator = new Random();
        int foodAmount = generator.nextInt(15);
        if(foodBox <= 0)
        {
            setFood(100);
        }
        setFood(foodBox - foodAmount);
    }
    
    /**
     * clearList method to remove all elements from temporary arrayList
     * Called after the search method is called
     */
    public void clearList()
    {
        tempAnimals.clear();
    }

    /**
     * Method doSomethingWhenFed to make the animal gain weight after being fed
     * uses Animal superclass set method change weight
     */
    public void doSomethingWhenFed()
    {
        setWeight(weight + 20);
    }

    /**
     * findWildSpecies method to search for specific species of wild animals
     * @param List<WildAnimals> array, array passed in of wildAnimals 
     * @param String species, species of animal to be searched for
     * @param int startingPoint, index where species will be searched for
     * 
     * @return ArrayList<WildAnimal>, arrayList made of matches to the species 
     * Method calls itself until the entire arrayList has been searched and if a match is found it is added to a temporary array
     */
    public ArrayList<WildAnimal> findWildSpecies(List<WildAnimal> array, String species, int startingPoint)
    {
        if(startingPoint > array.size() -1)
        {
            return tempAnimals;
        }

        else{
            if(array.get(startingPoint).getSpecies().equalsIgnoreCase(species))
            {
                tempAnimals.add(array.get(startingPoint));
                return findWildSpecies(array, species, ++startingPoint);
            }
            else
            {
                return findWildSpecies(array, species, ++startingPoint);
            }    
        }
    }
}
```