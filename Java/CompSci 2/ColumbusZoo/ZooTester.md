```java
/**
 * Program that creates a database for animals and plants at the Columbus Zoo.
 * Reads wild animals, domestic animals, and plants from 3 separate texts files and adds them to three separate ArrayLists
 * Allows the manager to add new animals or plants, remove animals or plants, search for animals by species, search for plants by location, feed animals or plants, or print current inventory to text file
 * 
 * @Olivia Horace
 * @November 26, 2014
 */
import java.io.*;
import java.util.*;
public class ZooTester
{
    public static void main(String[] args) throws FileNotFoundException //in the event no file is found
    {
        //ArrayLists for Domestic animals, Wild animals, and plants
        ArrayList<DomesticAnimal> domestAnimals = new ArrayList<DomesticAnimal>();
        ArrayList<WildAnimal> wildAnimals = new ArrayList<WildAnimal>();
        ArrayList<Plants> plants = new ArrayList<Plants>();

        //"Dummy" objects created to use class methods
        WildAnimal testWA = new WildAnimal();
        DomesticAnimal testDA = new DomesticAnimal();
        Plants testPlant = new Plants();

        //file where Domestic animals are located with scanner
        File myDomesticatedAnimalsFile = new File("domesticatedAnimals.txt");
        Scanner scanDomAnimals = new Scanner(myDomesticatedAnimalsFile);

        //While loop to scan over Domestic Animals file and add information to ArrayList 'domestAnimals'
        while(scanDomAnimals.hasNext())
        {
            String domSpecies = scanDomAnimals.nextLine();
            if(domSpecies.equals("***"))
            {
                break;
            }
            else
            {
                String domType = scanDomAnimals.nextLine();
                int domWeight = Integer.parseInt(scanDomAnimals.nextLine());

                domestAnimals.add(new DomesticAnimal(domSpecies, domType, domWeight));
            }
        }

        //Prints Domestic Animals ArrayList from the file to the screen
        System.out.println("\t \t \t DOMESTICATED ANIMALS");
        System.out.printf("%1$-20s %2$-25s %3$-20s %n", "ANIMAL SPECIES", "ANIMAL TYPE", "ANIMAL WEIGHT");
        for(int i = 0; i < domestAnimals.size(); i++)
        {
            System.out.printf("%1$-20s %2$-25s %3$-20s %n", domestAnimals.get(i).getSpecies(), domestAnimals.get(i).getType(), domestAnimals.get(i).getWeight());
        }

        //file where Wild Animals are located with scanner
        File myWildAnimalsFile = new File("wildAnimals.txt");
        Scanner scanWildAnimals = new Scanner(myWildAnimalsFile);

        //while loop to scan over Wild Animals file and add information to ArrayList 'wildAnimals'
        while(scanWildAnimals.hasNext())
        { 
            String wildSpecies = scanWildAnimals.nextLine();
            if(wildSpecies.equals("***"))
            {
                break;   
            }
            else
            {
                String wildType = scanWildAnimals.nextLine();
                int wildWeight = Integer.parseInt(scanWildAnimals.nextLine());

                wildAnimals.add(new WildAnimal(wildSpecies, wildType, wildWeight));  
            }
        }

        //prints Wild Animals ArrayList from the file to the screen
        System.out.println("\n \t \t \tWILD ANIMALS");
        System.out.printf("%1$-20s %2$-25s %3$-20s %n", "ANIMAL SPECIES", "ANIMAL TYPE", "ANIMAL WEIGHT");
        for(int j = 0; j < wildAnimals.size();j++)
        {
            System.out.printf("%1$-20s %2$-25s %3$-20s %n", wildAnimals.get(j).getSpecies(), wildAnimals.get(j).getType(), wildAnimals.get(j).getWeight());
        }

        //file where Plants are located with scanner
        File myPlantFile = new File("plants.txt");
        Scanner scanPlants = new Scanner(myPlantFile);
        //while loop to scan over Plants file and add information to ArrayList 'plants'
        while(scanPlants.hasNext())
        {
            String plantLocation = scanPlants.nextLine();
            if(plantLocation.equals("***"))
            {
                break;
            }
            else
            {
                String plantType = scanPlants.nextLine();
                int plantHeight = Integer.parseInt(scanPlants.nextLine());

                plants.add(new Plants(plantLocation, plantType, plantHeight));
            }
        }

        //prints plant ArrayList from file to the screen
        System.out.println("\n \t \t \tPLANTS");
        System.out.printf("%1$-20s %2$-25s %3$-20s %n", "LOCATION", "PLANT TYPE", "PLANT HEIGHT");
        for(int k = 0; k < plants.size();k++)
        {
            System.out.printf("%1$-20s %2$-25s %3$-20s %n", plants.get(k).getLocation(), plants.get(k).getPlantType(), plants.get(k).getHeight());
        }

        ////////////////////////////////////////////////////////////////////////
        ///////////////////////////Contains Menu!!!/////////////////////////////
        /////'int cont' used to determine if do-while loop will start again/////
        ////////////////////'cont' = continue//////////////////////////////////
        int cont;
        do
        {
            //////////////////////////////////////////////////////////////////
            ////////////Print statements for current ArrayLists///////////////
            //////////////////////////////////////////////////////////////////
            System.out.println("\t \t \t DOMESTICATED ANIMALS");
            System.out.printf("%1$-20s %2$-25s %3$-20s %n", "ANIMAL SPECIES", "ANIMAL TYPE", "ANIMAL WEIGHT");
            for(int i = 0; i < domestAnimals.size(); i++)
            {
                System.out.printf("%1$-20s %2$-25s %3$-20s %n", domestAnimals.get(i).getSpecies(), domestAnimals.get(i).getType(), domestAnimals.get(i).getWeight());
            }
            System.out.println("\n \t \t \tWILD ANIMALS");
            System.out.printf("%1$-20s %2$-25s %3$-20s %n", "ANIMAL SPECIES", "ANIMAL TYPE", "ANIMAL WEIGHT");
            for(int j = 0; j < wildAnimals.size();j++)
            {
                System.out.printf("%1$-20s %2$-25s %3$-20s %n", wildAnimals.get(j).getSpecies(), wildAnimals.get(j).getType(), wildAnimals.get(j).getWeight());
            }
            System.out.println("\n \t \t \tPLANTS");
            System.out.printf("%1$-20s %2$-25s %3$-20s %n", "LOCATION", "PLANT TYPE", "PLANT HEIGHT");
            for(int k = 0; k < plants.size();k++)
            {
                System.out.printf("%1$-20s %2$-25s %3$-20s %n", plants.get(k).getLocation(), plants.get(k).getPlantType(), plants.get(k).getHeight());
            }

            /////////////////////////////////////////////////////////////////////////
            ///////////////////Prompts user to chose a menu item////////////////////
            ///////////////////////////////////////////////////////////////////////
            Scanner contReader = new Scanner(System.in);
            System.out.println("Menu: \n" + "\t0) Exit\n" + "\t1) Add plant or animal" + "\n\t2) Remove plant or animal" + "\n\t3) Search animal species" + "\n\t4) Search plant locations" + "\n\t5) Feed plant or animal" + "\n\t6) Save current inventory");
            cont = Integer.parseInt(contReader.nextLine());

            /////////////////////////////////////////////////////////////////////////////
            ///////////////////Switch statement for 'cont' variable//////////////////////
            ///////////////////Loop exited if cont = 0///////////////////////////////////
            switch(cont)
            {
                case 0: 
                break;
                case 1: //if user input is one to add a new plant or animal
                {
                    Scanner addItem = new Scanner(System.in);
                    System.out.println("1. Plant" + "\n2. Wild animal" + "\n3. Domesticated animal");
                    int itemAdded = Integer.parseInt(addItem.nextLine());
                    if(itemAdded == 1)
                    {
                        System.out.print("Enter a room location: ");
                        String tempPlantLoc = addItem.nextLine();
                        System.out.print("Enter plant type: ");
                        String tempPlantType = addItem.nextLine();
                        System.out.print("Enter plant height: ");
                        int tempPlantHeight = Integer.parseInt(addItem.nextLine());

                        plants.add(new Plants(tempPlantLoc, tempPlantType, tempPlantHeight));
                    }
                    else if(itemAdded == 2)
                    {
                        System.out.print("Enter an animal species(Mammal, Reptile, Bird, Amphibian, or Fish): ");
                        String tempWildSpecies = addItem.nextLine();
                        System.out.print("Enter animal type: ");
                        String tempWildType = addItem.nextLine();
                        System.out.print("Enter animal weight: ");
                        int tempWildWeight = Integer.parseInt(addItem.nextLine());

                        wildAnimals.add(new WildAnimal(tempWildSpecies, tempWildType, tempWildWeight));
                    }
                    else
                    {
                        System.out.print("Enter an animal species: ");
                        String tempDomSpecies = addItem.nextLine();
                        System.out.print("Enter animal type: ");
                        String tempDomType = addItem.nextLine();
                        System.out.print("Enter animal weight: ");
                        int tempDomWeight = Integer.parseInt(addItem.nextLine());

                        domestAnimals.add(new DomesticAnimal(tempDomSpecies, tempDomType, tempDomWeight));
                    }
                    break;
                }
                case 2://if user input is 2 to remove a plant or animal
                {
                    Scanner removeItem = new Scanner(System.in);
                    System.out.println("From which database would you like to remove: " + "\n1. Plants" + "\n2. Wild Animals" + "\n3. Domesticated Animals");
                    int itemRemoved = Integer.parseInt(removeItem.nextLine());
                    if(itemRemoved ==1)
                    {
                        System.out.println("PLANTS");
                        for(int k = 0; k < plants.size();k++)
                        {
                            System.out.println(k + "\t" + plants.get(k).toString());
                        }

                        System.out.print("Please enter the number to the LEFT of the item you would like to remove: ");
                        int plantRemoved = Integer.parseInt(removeItem.nextLine());

                        plants.remove(plantRemoved);

                        System.out.println("PLANTS");
                        for(int k = 0; k < plants.size();k++)
                        {
                            System.out.println(k + "\t" + plants.get(k).toString());
                        }
                    }
                    else if (itemRemoved == 2)
                    {
                        System.out.println("WILD ANIMALS");
                        for(int j = 0; j < wildAnimals.size();j++)
                        {
                            System.out.println(j + "\t" + wildAnimals.get(j).toString());
                        }

                        int wildRemoved = Integer.parseInt(removeItem.nextLine());
                        wildAnimals.remove(wildRemoved);

                        System.out.println("WILD ANIMALS");
                        for(int j = 0; j < wildAnimals.size();j++)
                        {
                            System.out.println(j + "\t" + wildAnimals.get(j).toString());
                        }
                    }
                    else
                    {
                        System.out.println("DOMESTICATED ANIMALS");
                        for(int i = 0; i < domestAnimals.size(); i++)
                        {
                            System.out.println(i + "\t" + domestAnimals.get(i).toString());
                        }

                        int domestRemoved = Integer.parseInt(removeItem.nextLine());
                        domestAnimals.remove(domestRemoved);

                        System.out.println("DOMESTICATED ANIMALS");
                        for(int i = 0; i < domestAnimals.size(); i++)
                        {
                            System.out.println(i + "\t" + domestAnimals.get(i).toString());
                        }
                    }
                    break;
                }
                case 3://if user input is 3 to search for animal by species
                {
                    Scanner searchAnimal = new Scanner(System.in);

                    System.out.print("Please enter which species of animals for which you would like to search: ");
                    String searchItem = searchAnimal.nextLine();

                    System.out.println(testWA.findWildSpecies(wildAnimals, searchItem, 0));
                    System.out.println(testDA.findDomSpecies(domestAnimals, searchItem, 0));

                    testWA.clearList();
                    testDA.clearList();
                    break;
                }
                case 4://if user input is 4 to search plants by location
                {
                    Scanner searchPlant = new Scanner(System.in);

                    System.out.print("Please enter a room location for which you would like to search\n ex. room 1: ");
                    String plantSearchItem = searchPlant.nextLine();

                    System.out.println(testPlant.findPlantLocation(plants, plantSearchItem, 0));

                    testPlant.clearList();
                    break;
                }
                case 5://if user input is 5 to feed a plant or animal
                {
                    Scanner feed = new Scanner(System.in);
                    System.out.println("From which would you like to feed: " + "\n1. Plants" + "\n2. Wild Animals" + "\n3. Domesticated Animals");
                    int itemToFeed = Integer.parseInt(feed.nextLine());
                    if(itemToFeed ==1)
                    {
                        System.out.println("PLANTS");
                        for(int k = 0; k < plants.size();k++)
                        {
                            System.out.println(k + "\t" + plants.get(k).toString());
                        }

                        System.out.print("Please enter the number to the LEFT of the item you would like to feed: ");
                        int plantFed = Integer.parseInt(feed.nextLine());

                        plants.get(plantFed).feed();
                        plants.get(plantFed).doSomethingWhenFed();

                        System.out.println("PLANTS");
                        for(int k = 0; k < plants.size();k++)
                        {
                            System.out.println(k + "\t" + plants.get(k).toString());
                        }
                    }
                    else if (itemToFeed == 2)
                    {
                        System.out.println("WILD ANIMALS");
                        for(int j = 0; j < wildAnimals.size();j++)
                        {
                            System.out.println(j + "\t" + wildAnimals.get(j).toString());
                        }

                        System.out.print("Please enter the number to the LEFT of the item you would like to feed: ");
                        int wildFed = Integer.parseInt(feed.nextLine());
                        wildAnimals.get(wildFed).feed();
                        wildAnimals.get(wildFed).doSomethingWhenFed();

                        System.out.println("WILD ANIMALS");
                        for(int j = 0; j < wildAnimals.size();j++)
                        {
                            System.out.println(j + "\t" + wildAnimals.get(j).toString());
                        }
                    }
                    else
                    {
                        System.out.println("DOMESTICATED ANIMALS");
                        for(int i = 0; i < domestAnimals.size(); i++)
                        {
                            System.out.println(i + "\t" + domestAnimals.get(i).toString());
                        }
                        System.out.print("Please enter the number to the LEFT of the item you would like to feed: ");

                        int domestFed = Integer.parseInt(feed.nextLine());
                        domestAnimals.get(domestFed).feed();
                        domestAnimals.get(domestFed).doSomethingWhenFed();

                        System.out.println("DOMESTICATED ANIMALS");
                        for(int i = 0; i < domestAnimals.size(); i++)
                        {
                            System.out.println(i + "\t" + domestAnimals.get(i).toString());
                        }
                    }
                    break;
                }
                case 6://if user input is 6 to write the current Zoo inventory to a text file
                {
                    PrintWriter domesticOut = new PrintWriter("domesticatedAnimals.txt");

                    System.out.println("...Now adding domestic animals to file...");
                    for(int i = 0; i < domestAnimals.size(); i++)
                    {
                        domesticOut.println(domestAnimals.get(i).getSpecies());
                        domesticOut.println(domestAnimals.get(i).getType());
                        domesticOut.println(domestAnimals.get(i).getWeight());
                    }                    
                    System.out.println("...Now adding food box to file...");
                    domesticOut.println("***");
                    domesticOut.println("Amount of food left in food box: " + Animal.foodBox);
                    domesticOut.close();

                    PrintWriter wildOut = new PrintWriter("wildAnimals.txt");
                    System.out.println("...Now adding wild animals to file...");
                    for(int j = 0; j < wildAnimals.size();j++)
                    {
                        wildOut.println(wildAnimals.get(j).getSpecies());
                        wildOut.println(wildAnimals.get(j).getType());
                        wildOut.println(wildAnimals.get(j).getWeight());
                    }
                    System.out.println("...Now adding food box to file...");
                    wildOut.println("***");
                    wildOut.println("Amount of food left in food box: " + Animal.foodBox);
                    wildOut.close();

                    PrintWriter plantsOut = new PrintWriter("plants.txt");
                    System.out.println("...Now adding plants to file...");
                    for(int k = 0; k < plants.size();k++)
                    {
                        plantsOut.println(plants.get(k).getLocation());
                        plantsOut.println(plants.get(k).getPlantType());
                        plantsOut.println(plants.get(k).getHeight());
                    }
                    System.out.println("...Now adding food box to file...");
                    plantsOut.println("***");
                    plantsOut.println("Amount of food left in food box: " + Animal.foodBox);
                    plantsOut.close();
                    break;
                }
                default://if user doesn't enter an integer 0-6
                {
                    System.out.println("We didn't quite catch that!");
                    break;
                }
            }
        }
        while (cont != 0);//while loop continues to iterate as long as cont variable does not equal 0
    }
}
```