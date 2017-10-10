```java
/**
 * Class that manipulates DomesticAnimal objects
 * Extends the Animal class and overrides the feed method
 * Contains tempAnimals arrayList for search method
 * 
 * @Olivia Horace
 * @November 26, 2014
 */
import java.util.*;
public class DomesticAnimal extends Animal implements Feedable
{
    ArrayList<DomesticAnimal> tempAnimals = new ArrayList<DomesticAnimal>();
    /**
     * Default constructor 
     */
    public DomesticAnimal()
    {
        super();
    }

    /**
     * Custom constructor 
     * @param String dSpecies, domestic species
     * @param String dType, specific type of domestic animal
     * @param int dWeight, weight of domestic animal
     * 
     * Uses superclass set methods
     */
    public DomesticAnimal(String dSpecies, String dType, int dWeight)
    {
        super.setSpecies(dSpecies);
        super.setType(dType);
        super.setWeight(dWeight);
    }

    /**
     * feed method OVERRIDES superclass feed method
     * Generates a random number and then subtracts that number from static foodBox variable in Animal class
     * If the foodBox amount is equal to or less than 0, the foodBox is refilled to 100
     * Uses superclass setFood method to change amount in foodBox
     */
    public void feed()
    {
        Random generator = new Random();
        int foodAmount = generator.nextInt(10);
        if(foodBox <= 0)
        {
            setFood(100);
        }
        setFood(foodBox - foodAmount);
    }

    /**
     * doSomethingWhenFed Method to do something when a domestic animal is fed
     * uses superclass set method to change the weight of the object that uses the method 
     */
    public void doSomethingWhenFed()
    {
        setWeight(weight + 5);
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
     * findDomSpecies method used to search for a specfic species in the ArrayList 
     * @param List<domAnimals> array, array list passed in of domAnimals
     * @param String species, specific species that is being search for
     * @param int startingPoint, index that will be examined
     * 
     * @return ArrayList<domAnimals>, an arrayList of domAnimals
     * Method calls itself to search for matches (regardless of case) to the species and adds it to the temporary array
     */
    public ArrayList<DomesticAnimal> findDomSpecies(List<DomesticAnimal> array, String species, int startingPoint)
    {
        if(startingPoint > array.size() -1)
        {
            return tempAnimals;
        }

        else
        {if(array.get(startingPoint).getSpecies().equalsIgnoreCase(species))
            {
                tempAnimals.add(array.get(startingPoint));
                return findDomSpecies(array, species, ++startingPoint);
            }
            else
            {
                return findDomSpecies(array, species, ++startingPoint);
            }    
        }
    }
}
```