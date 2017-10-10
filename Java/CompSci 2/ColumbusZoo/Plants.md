```java
/**
 * Plant class to manipulate plant objects
 * Contains tempPlants for search method and instance variables, location, plantType, and height
 * Contains get and set methods, feed method, doSomethingWhenFed method, and toString method
 * 
 * @Olivia Horace
 * @November 26, 2014
 */
import java.util.*;
public class Plants implements Feedable
{
    ArrayList<Plants> tempPlants = new ArrayList<Plants>();
    String location;
    String plantType;
    int height;

    /**
     * Default constructor 
     * Creates generic plant object
     */
    public Plants()
    {
        location = "Room 1";
        plantType = "Flower";
        height = 4;
    }

    /**
     * Custom constructor 
     * @param String newLocation, location of plant
     * @param String newPType, specific plant type
     * @param int height, height of plant
     * 
     * uses self-contain set methods
     */
    public Plants(String newLocation, String newPType, int height)
    {
        setLocation(newLocation);
        setPlantType(newPType);
        setHeight(height);
    }

    /**
     * setLocation method
     * @param String nLocation, new location
     * 
     * Assigns parameter to instance variable location
     */
    public void setLocation(String nLocation)
    {
        location = nLocation;
    }

    /**
     * setPlantType method
     * @param String nPType, new plant type
     * 
     * Assigns parameter to instance variable plantType
     */
    public void setPlantType(String nPType)
    {
        plantType = nPType;
    }

    /**
     * setHeight method
     * @param int nHeight
     * 
     * Assigns parameter to instance variable height
     */
    public void setHeight(int nHeight)
    {
        height = nHeight;
    }

    /**
     * getLocation method
     * @return location
     * Returns location variable
     */
    public String getLocation()
    {
        return location;
    }

    /**
     * getPlantType method
     * @return plantType
     * Returns plantType variable
     */
    public String getPlantType()
    {
        return plantType;
    }

    /**
     * getHeight
     * @return height
     * Returns height variable 
     */
    public int getHeight()
    {
        return height;
    }

    /**
     * feed method
     * Generates a random number to feed the animal
     * Uses Animal class to access foodBox variable 
     * Uses Animal setFood method to assign new value of foodBox
     * If foodBox is less than or equal to 0, foodBox is reset to 100
     */
    public void feed()
    {
        Random generator = new Random();
        int foodAmount = generator.nextInt(10);
        if(Animal.foodBox <= 0)
        {
            Animal.setFood(100);
        }
        Animal.setFood(Animal.foodBox - foodAmount);
    }

    /**
     * doSomethingWhenFed method 
     * Method invoked after feed method to increase plant height by 1
     * Uses self-contained setHeight method
     */
    public void doSomethingWhenFed()
    {
        setHeight(height + 1);
    }
    
    /**
     * clearList method to remove all elements from temporary arrayList
     * Called after the search method is called
     */
    public void clearList()
    {
        tempPlants.clear();
    }

    /**
     * findPlantLocation method to search plants arrayList
     * @param List<Plants> array, arrayList of plants to be searched
     * @param String room, location for which method is searching
     * @param int startingPoint, index where room is searched for 
     * @return ArrayList<Plants>, returns arrayList 'tempPlants' 
     * 
     * Method calls itself to search for a match of locations (regardless of case) and adds it to temporary arrayList
     */
    public ArrayList<Plants> findPlantLocation(List<Plants> array, String room, int startingPoint)
    {
        if(startingPoint > array.size() - 1)
        {
            return tempPlants;
        }

        else{
            if(array.get(startingPoint).getLocation().equalsIgnoreCase(room))
            {
                tempPlants.add(array.get(startingPoint));
                startingPoint = startingPoint + 1;
                return findPlantLocation(array, room, startingPoint);
            }
            else
            {
                startingPoint = startingPoint + 1;
                return findPlantLocation(array, room, startingPoint);
            }    
        }
    }

    /**
     * toString method
     * @returns String of plant location, plant type, and plant height
     */
    public String toString()
    {
        return "Plant Location: " + location + "\nPlant Type: " + plantType + "\nPlant Height: " + height + "\n";
    }
}
```