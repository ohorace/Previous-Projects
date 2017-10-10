```c#
//Olivia Horace
//February 4, 2014
//EDITED: September 16, 2015
//EDITS(9/16/15): Fixed algorithms to display users in diagnostic phase, declared same type variables in one line, condensed number of lines, created a user exit from diagnostics
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace BloodBank
{
    class Program : Patients//program class inherits patients class
    {
        static void Main(string[] args)
        {
            string name;//declares string 'name'
            while (true)//while loop to continue entering in patients
            {
                while (true)//nested while loop to check names
                {
                    Console.ForegroundColor = ConsoleColor.Cyan;//sets font color of magenta for opening prompt
                    Console.Write("Welcome to MMC'S Blood Bank System: " + "\n" + "Please enter patient's first and last name: ");//prompt that asks for the patients name
                    Console.ResetColor();//resets the color

                    Console.ForegroundColor = ConsoleColor.White;//sets font color to white for user input
                    string tempName = Console.ReadLine();//stores a temporary name from input
                    name = tempName.ToLower();//converts name to all lowercase and stores it in string 'name'
                    Console.ResetColor();//resets color

                    if (Usernames.Any(str => (str.Equals(name, StringComparison.InvariantCultureIgnoreCase)) || (str.Contains(name))))//checks if the list of usernames contains the name entered
                    { 
                        Console.BackgroundColor = ConsoleColor.White;//sets font background to white
                        Console.ForegroundColor = ConsoleColor.Red;//sets font color to red
                        Console.WriteLine("This name has been entered!");//Warning displayed and loop restarts if name exists
                        Console.ResetColor();//resets font color
                        Console.WriteLine(" ");//prints blank line 
                    }

                    else
                        break;//breaks out of inside loop and continues with code
                }

                if (name != "admin")//if the name entered is not 'admin' the name is added to the list
                {
                    name = Patients.UppercaseWords(name);//capitalizes patients name to traditional capitalization
                    Patients.getNames(name);//adds the capitalized name to list of names using method 'getNames'
                }

                if (name == "admin")//if the name entered is 'admin' it will display any patient information that has been entered
                {
                    Console.WriteLine("");//prints blank line
                    Patients.Display();//prints all patients information
                    Console.WriteLine("");//prints blank line
                }

                else
                {
                    Console.ForegroundColor = ConsoleColor.Cyan;//sets font color to cyan
                    Console.Write("Please enter age: ");//prompt that requests patient age
                    Console.ResetColor();//resets font color

                    Console.ForegroundColor = ConsoleColor.White;//sets font color to white
                    string tempAge = Console.ReadLine();//stores the input in the string 'tempAge'
                    Console.ResetColor();//resets font color

                    int age = int.Parse(tempAge);//parses string input to an integer
                    Patients.getAges(age);//adds this string to the list of ages using the method 'getAges'

                    while (true)
                    {
                        Console.ForegroundColor = ConsoleColor.Cyan;//sets font color to cyan
                        Console.Write("Please enter blood type: ");//prompt that requests patient blood type
                        Console.ResetColor();//resets color

                        Console.ForegroundColor = ConsoleColor.White;//sets font color white
                        string bloodInput = Console.ReadLine();//stores input in the string 'bloodInput'
                        Console.ResetColor();//resets color

                        string bloodType = bloodInput.ToUpper();//declares and initializes string 'bloodType' to equal 'bloodInput' in uppercase

                        if ((bloodType.Equals("A", StringComparison.InvariantCultureIgnoreCase)) || (bloodType.Equals("B", StringComparison.InvariantCultureIgnoreCase) || (bloodType.Equals("AB", StringComparison.InvariantCultureIgnoreCase) || (bloodType.Equals("O", StringComparison.InvariantCultureIgnoreCase)))))//only stores the value if it is a, b, ab, or o
                        {
                            Patients.getBT(bloodType);//adds this string to the list of bloodtypes using the method 'getBT'
                        }
                        if ((bloodType.Equals("A", StringComparison.InvariantCultureIgnoreCase)) || (bloodType.Equals("B", StringComparison.InvariantCultureIgnoreCase) || (bloodType.Equals("AB", StringComparison.InvariantCultureIgnoreCase) || (bloodType.Equals("O", StringComparison.InvariantCultureIgnoreCase)))))//checks blood types regardless of case
                        {
                            break;//inside while loop will exit and main loop will be continued if an appropriate blood type is entered
                        }
                        else
                        {
                            Console.BackgroundColor = ConsoleColor.White;//sets font background color to white
                            Console.ForegroundColor = ConsoleColor.Red;//sets warning color for the following message to red
                            Console.WriteLine("Please only enter 'A', 'B', 'AB', or 'O'!");//if the entry is not an appropriate blood type, the nested loop starts again
                            Console.ResetColor();//resets color from red
                            Console.WriteLine(" ");//prints blank line
                        }
                    }

                    Console.ForegroundColor = ConsoleColor.Cyan;//sets font color to cyan
                    Console.Write("Please enter height (in inches): ");//prompt that requests patient height
                    Console.ResetColor();//resets color

                    Console.ForegroundColor = ConsoleColor.White;//sets font color to white
                    string height = Console.ReadLine();//stores input in the string 'height'
                    Console.ResetColor();//resets color
                    Patients.getHeight(height);//adds this string to the list of heights using the method 'getHeight'

                    Console.ForegroundColor = ConsoleColor.Cyan;//sets font color to cyan
                    Console.Write("Please enter weight (in pounds): ");//prompt that requests patient weight
                    Console.ResetColor();//resets color

                    Console.ForegroundColor = ConsoleColor.White;//sets font color to white
                    string tempWeight = Console.ReadLine();//stores input in the string 'weight'
                    Console.ResetColor();//resets color

                    int weight = int.Parse(tempWeight);//initializes int 'weight' to store temp weight input as an integer
                    Patients.getWeight(weight);//adds this string to the list of weights using the method 'getWeight'

                    Console.ForegroundColor = ConsoleColor.Cyan;//sets font color to cyan
                    Console.Write("Please enter primary care physician: ");//prompt that requests patient physician
                    Console.ResetColor();//resets color

                    Console.ForegroundColor = ConsoleColor.White;//sets font color to White 
                    string pcPhysician = Console.ReadLine();//stores input in the string 'pcPhysician'

                    Patients.getPhysician(UppercaseWords(pcPhysician));//adds this string to the list of physicians using the method 'getPhysician
                    Console.ResetColor();//resets font color 

                    Console.Write("\n");//prints a blank line
                    Console.ForegroundColor = ConsoleColor.Cyan;//set font color to cyan for prompt
                    Console.Write("Would you like to enter another patient?: ");//asks if the user wants to add another patient
                    Console.ResetColor();//resets font color

                    Console.ForegroundColor = ConsoleColor.White;//set font color to white for input
                    string contProg = Console.ReadLine();//stores their input in the string 'contProg' (control program)
                    Console.ResetColor();//resets color

                    if ((contProg.Equals("no", StringComparison.InvariantCultureIgnoreCase)) || (contProg.Equals("n", StringComparison.InvariantCultureIgnoreCase)))//accepts any form of 'no' regardless of case
                    {
                        Patients.Display();//prints all patients information
                        Console.WriteLine("");//prints blank line
                        Console.ForegroundColor = ConsoleColor.White;//sets font color white
                        DateTime myValue = DateTime.Now;//declares new datetime variable 
                        Console.WriteLine("This report was generated on: " + myValue.ToString());//prints a line displaying the time the report was generated
                        Console.ResetColor();//resets font color
                        Console.WriteLine(" ");//prints blank line
                        Diagnostic.Diagnostics();//calls diagnostic method
                        break;//exits the program
                    }

                    else { Console.WriteLine(" "); }//if the user doesn't enter no, a blank line is printed and the program loops again
                }
            }
        }
    }
}
```


