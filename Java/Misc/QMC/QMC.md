```Java
/**
 * Perform Grouping Operations for QMC
 * 
 * @Olivia Horace
 * @Spring 2015
 */
import java.io.*;
import java.util.*;
public class QMC
{
    public void enter2()
    {
        ArrayList<Integer> TwoInputsA = new ArrayList<Integer>();
        TwoInputsA.add(0);
        TwoInputsA.add(0);
        TwoInputsA.add(1);
        TwoInputsA.add(1);

        ArrayList<Integer> TwoInputsB = new ArrayList<Integer>();
        TwoInputsB.add(0);
        TwoInputsB.add(1);
        TwoInputsB.add(0);
        TwoInputsB.add(1);

        ArrayList<Integer> twoOutput= new ArrayList<Integer>();
        ArrayList<Integer> counter2 = new ArrayList<Integer>();

        Scanner kb2scan = new Scanner(System.in);
        for(int i = 0; i <4; i++)
        {
            System.out.print("Enter the value of the results row: ");
            int twoInR = kb2scan.nextInt();
            twoOutput.add(twoInR);
            counter2.add(i);
        }
        System.out.println("");
        System.out.printf("%1$-5s %2$-5s %3$-5s %4$-5s %n", "Row", "A", "B", "Output");
        for(int j = 0; j < TwoInputsA.size(); j++)
        {
            System.out.printf("%1$-5s %2$-5s %3$-5s %4$-5s %n", counter2.get(j), TwoInputsA.get(j), TwoInputsB.get(j),twoOutput.get(j));
        }  
        System.out.println("");

        for(int k = 0; k < TwoInputsA.size(); k++)
        {
            if(twoOutput.get(k) == 1)
            {
                continue;
            }
            else
            {
                twoOutput.remove(k);
                TwoInputsA.remove(k);
                TwoInputsB.remove(k);
                counter2.remove(k);
                k = k -1;
            }
        }

        System.out.println("All rows containing '1' as an output: ");
        System.out.printf("%1$-5s %2$-5s %3$-5s %4$-5s %n", "Row", "A", "B", "Output");
        for(int i = 0; i < TwoInputsA.size(); i++)
        {
            System.out.printf("%1$-5s %2$-5s %3$-5s %4$-5s %n", counter2.get(i), TwoInputsA.get(i), TwoInputsB.get(i), twoOutput.get(i));
        }  
        System.out.println("");

        ArrayList<Integer> group2 = new ArrayList<Integer>();
        int groupCounter = 0;
        int level0 = 0;
        int level1 = 1;
        int level2 = 2;
        for(int i = 0; i < TwoInputsA.size(); i++)
        {
            if((TwoInputsA.get(i) == 1) && (TwoInputsB.get(i) == 1))
            {          
                group2.add(level2);
            }
            else if((TwoInputsA.get(i) == 1) && (TwoInputsB.get(i) == 0) || (TwoInputsB.get(i) == 1) && (TwoInputsA.get(i) == 0))
            {
                group2.add(level1);
            }
            else
            {
                group2.add(level0);
            }
        }

        if(group2.get(0) != 0)
        {
            for(int i = 0; i < group2.size(); i++)
            {
                group2.set(i, (group2.get(i) - 1));
            }
        }

        System.out.println("Grouping of rows with same number of '1's as inputs: ");
        System.out.printf("%1$-8s %2$-5s %3$-5s %4$-5s %n", "Group", "Row", "A", "B");
        for(int i = 0; i < TwoInputsA.size(); i++)
        {
            System.out.printf("%1$-8s %2$-5s %3$-5s %4$-5s %n", group2.get(i), counter2.get(i), TwoInputsA.get(i), TwoInputsB.get(i));
        }  
        System.out.println("");   

        System.out.println(Comparison(TwoInputsA, TwoInputsB, group2, counter2));
    }

    public void enter3()
    {
        ArrayList<Integer> ThreeInputsA = new ArrayList<Integer>();
        ThreeInputsA.add(0);
        ThreeInputsA.add(0);
        ThreeInputsA.add(0);
        ThreeInputsA.add(0);
        ThreeInputsA.add(1);
        ThreeInputsA.add(1);
        ThreeInputsA.add(1);
        ThreeInputsA.add(1);

        ArrayList<Integer> ThreeInputsB = new ArrayList<Integer>();
        ThreeInputsB.add(0);
        ThreeInputsB.add(0);
        ThreeInputsB.add(1);
        ThreeInputsB.add(1);
        ThreeInputsB.add(0);
        ThreeInputsB.add(0);
        ThreeInputsB.add(1);
        ThreeInputsB.add(1);

        ArrayList<Integer> ThreeInputsC = new ArrayList<Integer>();
        ThreeInputsC.add(0);
        ThreeInputsC.add(1);
        ThreeInputsC.add(0);
        ThreeInputsC.add(1);
        ThreeInputsC.add(0);
        ThreeInputsC.add(1);
        ThreeInputsC.add(0);
        ThreeInputsC.add(1);

        ArrayList<Integer> ThreeInputsResults = new ArrayList<Integer>();
        int[] counter3 = new int[8];

        Scanner kb3scan = new Scanner(System.in);
        for(int i = 0; i <8; i++)
        {
            System.out.print("Enter the value of the results row: ");
            int threeInR = kb3scan.nextInt();
            ThreeInputsResults.add(threeInR);
            counter3[i] = i;
        }

        System.out.println("");
        System.out.printf("%1$-5s %2$-5s %3$-5s %4$-5s %5$-5s %n", "Row", "A", "B", "C", "Output");
        for(int i = 0; i < ThreeInputsA.size(); i++)
        {
            System.out.printf("%1$-5s %2$-5s %3$-5s %4$-5s %5$-5s %n", counter3[i], ThreeInputsA.get(i), ThreeInputsB.get(i), ThreeInputsC.get(i), ThreeInputsResults.get(i));
        }  
        System.out.println("");
    }

    public void enter4()
    {
        ArrayList<Integer> FourInputsA = new ArrayList<Integer>();
        FourInputsA.add(0);
        FourInputsA.add(0);
        FourInputsA.add(0);
        FourInputsA.add(0);
        FourInputsA.add(0);
        FourInputsA.add(0);
        FourInputsA.add(0);
        FourInputsA.add(0);
        FourInputsA.add(1);
        FourInputsA.add(1);
        FourInputsA.add(1);
        FourInputsA.add(1);
        FourInputsA.add(1);
        FourInputsA.add(1);
        FourInputsA.add(1);
        FourInputsA.add(1);

        ArrayList<Integer> FourInputsB = new ArrayList<Integer>();
        FourInputsB.add(0);
        FourInputsB.add(0);
        FourInputsB.add(0);
        FourInputsB.add(0);
        FourInputsB.add(1);
        FourInputsB.add(1);
        FourInputsB.add(1);
        FourInputsB.add(1);
        FourInputsB.add(0);
        FourInputsB.add(0);
        FourInputsB.add(0);
        FourInputsB.add(0);
        FourInputsB.add(1);
        FourInputsB.add(1);
        FourInputsB.add(1);
        FourInputsB.add(1);

        ArrayList<Integer> FourInputsC = new ArrayList<Integer>();
        FourInputsC.add(0);
        FourInputsC.add(0);
        FourInputsC.add(1);
        FourInputsC.add(1);
        FourInputsC.add(0);
        FourInputsC.add(0);
        FourInputsC.add(1);
        FourInputsC.add(1);
        FourInputsC.add(0);
        FourInputsC.add(0);
        FourInputsC.add(1);
        FourInputsC.add(1);
        FourInputsC.add(0);
        FourInputsC.add(0);
        FourInputsC.add(1);
        FourInputsC.add(1);

        ArrayList<Integer> FourInputsD = new ArrayList<Integer>();
        FourInputsD.add(0);
        FourInputsD.add(1);
        FourInputsD.add(0);
        FourInputsD.add(1);
        FourInputsD.add(0);
        FourInputsD.add(1);
        FourInputsD.add(0);
        FourInputsD.add(1);
        FourInputsD.add(0);
        FourInputsD.add(1);
        FourInputsD.add(0);
        FourInputsD.add(1);
        FourInputsD.add(0);
        FourInputsD.add(1);
        FourInputsD.add(0);
        FourInputsD.add(1);

        ArrayList<Integer> FourInputsResults = new ArrayList<Integer>();
        int[] counter4 = new int[16];

        Scanner kb4scan = new Scanner(System.in);
        for(int i = 0; i < 16; i++)
        {
            System.out.print("Enter the value of the results row: ");
            int fourInR = kb4scan.nextInt();
            FourInputsResults.add(fourInR);
            counter4[i] = i;
        }  

        System.out.println("");
        System.out.printf("%1$-5s %2$-5s %3$-5s %4$-5s %5$-5s %6$-5s %n", "Row", "A", "B", "C", "D", "Output");
        for(int i = 0; i < FourInputsA.size(); i++)
        {
            System.out.printf("%1$-5s %2$-5s %3$-5s %4$-5s %5$-5s %6$-5s %n", counter4[i], FourInputsA.get(i), FourInputsB.get(i), FourInputsC.get(i), FourInputsD.get(i), FourInputsResults.get(i));
        } 
        System.out.println("");
    }

    public ArrayList<String> Comparison (ArrayList<Integer> a, ArrayList<Integer> b, ArrayList<Integer> group, ArrayList<Integer> row)
    {
        int temp = group.get(0);
        int differenceCounter = 0;

        ArrayList<String> sorted = new ArrayList<String>();
        while(temp <= group.size())
        {
            for(int i = 0; i < a.size() -1 ; i++)
            {
                if(group.get(i) == temp)
                {
                    continue;
                }
                else
                {
                    if((a.get(i) != a.get(i+1)))
                    {
                        differenceCounter++;
                    }
                    else if(b.get(i) != b.get(i+1))
                    {
                        differenceCounter++;
                    }
                    else
                    {
                        break;
                    }

                    if(differenceCounter == 1)
                    {
                        if(a.get(i) == a.get(i+1))
                        {
                            sorted.add(String.valueOf(a.get(i)));
                        }
                        else
                        {
                            sorted.add("-");
                        }
                    }
                }
            }
            temp++;
        }
        return sorted;
    }
}
```java