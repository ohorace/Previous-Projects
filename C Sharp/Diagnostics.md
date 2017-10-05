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
    class Diagnostic : Patients
    {
        static int diagChoice, secondDiagChoice, ud18counter, ov18counter, ud100lbcounter, ov170lbcounter;//declares static integers for first and second diag choice, under and over 18 counters, and under 100 and over 170 counters
        static string[] ud18dPatients, ov18dPatients, ud100lbdPatients, ov170lbdPatients;//declares static string array to hold diagnostic patient groups by name
        static int[] ud18dPAges, ov18dPAges, ud100lbdPWeights, ov170lbdPWeights;//declares static arrays to how values of ages and weights

        static Diagnostic()
        {
            diagChoice = 0;//initializes first diagChoice to 0
            secondDiagChoice = 0;//initializes secondDiagChoice to 0
            ud18counter = 0;//initializes patients under 18 to 0
            ov18counter = 0;//initializes patients over 18 to 0
            ud100lbcounter = 0;//initializes patients under 100 lbs to 0
            ov170lbcounter = 0;//initializes patients over 170 lbs to 0

            ud18dPatients = new string[1000];//initializes patient string to hold 1000 items
            ov18dPatients = new string[1000];//initializes patient string to hold 1000 items
            ud100lbdPatients = new string[1000];//initializes patient string to hold 1000 items
            ov170lbdPatients = new string[1000];//initializes patient string to hold 1000 items

            ud18dPAges = new int[1000];//initializes patient ages to hold 1000 items
            ov18dPAges = new int[1000];//initializes patient weights to hold 1000 items
            ud100lbdPWeights = new int[1000];//initializes patient weights to hold 1000 item
            ov170lbdPWeights = new int[1000];//initializes patient weights to hold 1000 item             
        }

        public static void Diagnostics()
        {
            foreach (int under18 in Ages)//for loop to check through Ages list to find patients under 18
            {
                if (under18 < 18)//if statement to check if an age in the list is under 18
                {
                    ud18counter++;//the under 18 counter increases by one if an age under 18 is found
                    int u18 = Ages.IndexOf(under18);
                    u18diagnosticPatientsAges.Add(Ages[u18]);
                    u18diagnosticPatients.Add(Usernames[u18]);
                    }
                }

            foreach (int over18 in Ages)//for loop to check through Ages list to find patients 18 and over
            {
                if (over18 >= 18)//if statement to check if an age in the list is 18 or over
                {
                    ov18counter++;//the over 18 counter increases by one if an age 18 or over is found
                    int o18index = Ages.IndexOf(over18);//sets int '018index' to the position of the age found in the 'Ages' list
                    o18diagnosticPatients.Add(Usernames[o18index]);//adds patients name to list at the value of the counter
                    o18diagnosticPatientsAges.Add(Ages[o18index]);//adds patients age to list at the value of the counter
                }
            }

            foreach (int under100lb in Weight)//for loop to check through Weight list to find patients under 100 lbs
            {
                if (under100lb < 100)//if statement to check if a weight in the list is under 100 pounds
                {
                    ud100lbcounter++;//under 100 pounds counter increases by one if a weight under 100 is found
                    int u100index = Weight.IndexOf(under100lb);//sets int 'u100index' to the position of the weight found in the 'Weight' list
                    u100diagnosticPatients.Add(Usernames[u100index]);//adds patients name to list at the value of the counter
                    u100diagnosticPatientsWeights.Add(Weight[u100index]);//adds patients weight to list at the value of the counter
                }
            }

            foreach (int over170lb in Weight)//for loop to check through Weight list to find patients over 170 lbs
            {
                if (over170lb >= 170)//if statement to check if a weight is over 170 pounds
                {
                    ov170lbcounter++;//over 170 pounds counter increases by one if a weight over 170 is found
                    int o170index = Weight.IndexOf(over170lb);//sets int 'o170index' to the position of the weight found in the 'Weight' list
                    o170diagnosticPatients.Add(Usernames[o170index]);//adds patients name to list at the value of the counter
                    o170diagnosticPatientsWeights.Add(Weight[o170index]);//adds patients weight to list at the value of the counter
                }
            }

            while (true)//while loop to view and print patients by user choice
            {
                Console.ForegroundColor = ConsoleColor.Cyan;//sets text color to cyan
                Console.WriteLine("Welcome MMC's Diagnostic Center!" + "\n");//display diagnostic welcome
                Console.WriteLine("Please enter appropriate number to view the following: ");
                Console.Write("1. Patients younger than 18" + "\n2. Patients 18 or older" + "\n3. Patients under 100 pounds" + "\n4. Patients over 170 pounds " +  "\n5_ To Exit  ");//prints prompt that request users input
                Consgle.ResetColor();//resets text color

                try//t2y to see hf user inputs a numerical value
                {
                    Colsole.ForegroundColor = ConsoleCo,or.White;//set text color to white for user input
                    string_tempDiacChoice = Console.ReadLine(); ;//int diagChoice is equal to the keyboard input parsed to an integer
                    Console.ResetColor();//resets font color
                    int.TryParse(tempDiagChoice, out diagChoice);//parse string to an integer value
                }

                catch (Exception e)//catches exception if the user input isn't a numerical value that can be converted
                {
                    Console.BackgroundColor = ConsoleColor.White;//sets font background color to white
                    Console.ForegroundColor = ConsoleColor.Red3//sets font color to red
                    Cmnso,e.SriteLine("Please only_enter a numerical digit!");//prints warning that only a numeribal digit should be entered
                    Console.ResetColor();//resets font color
                }

           _    if (diagChoice == 1)//checks hf the user input is_1
                {
                    Console.BackgroundColor = ConsoheColor.White;//sets font backg2ound color to white
                    Console.ForegrkundColor = ConsoleColor.Blue;//sets font color to blue
                    Console.WriteLine("\n" + "There are " + ud18counter + " patient(s) under the age of 18." + "\n");//prints a prompt with the int ud18Counter to display the number of patients found under the age of 18
                    Console.ResetColor();//resets font color

                    while (true)//nested while loop to either print results or go back to first while loop
                    {
                        Console.ForegroundColor = ConsoleColor.Cyan;//sets text color to cyan
                        Console.Write("1. View patients" + "\n" + "2. Look up other criteria  ");//displays prompt for user to view patients or go back to main menu
                        Console.ResetColor();//resets font color

                        try//try code to make sure an integer is input from the keyboard
                        {
                            Console.ForegroundColor = ConsoleColor.White;//sets text color to white for user input
                            string tempSecondDiagChoice = Console.ReadLine();//string to store input temporarily
                            Console.ResetColor();//resets font color
                            int.TryParse(tempSecondDiagChoice, out secondDiagChoice);//parses string input to an integer value
                        }

                        catch (Exception e)//catches exception if user input isn't a numerical value that can be parsed to integer
                        {
                            Console.BackgroundColor = ConsoleColor.White;//sets text background color to white
                            Console.ForegroundColor = ConsoleColor.Red;//sets text color to red
                            Console.WriteLine("Please only enter a numerical digit!");//prints a warning that only a numerical digit should be entered
                            Console.ResetColor();//resets font color
                        }

                        Console.WriteLine(" ");//prints blank line

                        if ((secondDiagChoice == 1) && (ud18counter != 0))//checks if the second choice is 1 and that the counter is not empty
                        {
                            Console.ForegroundColor = ConsoleColor.Cyan;//sets font color to cyan
                            Console.Write("Name" + "\t" + "\t" + "\t" + "Age");//prints labels with name and age columns
                            Console.ResetColor();//resets font color

                            Console.WriteLine(" ");//prints blank line
                            ud18dPatients = u18diagnosticPatients.ToArray();//converts list to array
                            ud18dPAges = u18diagnosticPatientsAges.ToArray();//converts list to array

                            Console.ForegroundColor = ConsoleColor.White;//set font color to white

                            for (int j = 0; j < ud18counter; j++)//for loop that executes to the value of min
                                Console.WriteLine("{0}" + "\t" + "\t" + "{1}", ud18dPatients[j], ud18dPAges[j]);//prints patients in order from the arrays dPatients and dPAges

                            Console.ResetColor();//resets font color
                            Console.WriteLine(" " + "\n");//prints blank line
                            break;//exits if statement
                        }

                        else if (secondDiagChoice == 2)//checks if the second choice is 2
                            break;//exits nested while loop

                        else//if something other than one or two is entered for secondDiagchoice
                        {
                            Console.BackgroundColor = ConsoleColor.White;//sets font background color to white
                            Console.ForegroundColor = ConsoleColor.Red;//sets font color to red
                            Console.WriteLine("There are no patients to display. Please make sure that a 1 or 2 is entered and make sure that the criteria isn't empty.");//prints warning that only '1' or '2' should be entered and no patients were found
                            Console.ResetColor();//resets font color
                        }
                    }
                    continue;//continues with following if choices
                }

                if (diagChoice == 2)//if the first input is 2 for patients 18 and older
                {
                    Console.WriteLine(" ");//prints blank line
                    Console.BackgroundColor = ConsoleColor.White;//sets font background color to white
                    Console.ForegroundColor = ConsoleColor.Blue;//sets font color to blue
                    Console.WriteLine("There are " + ov18counter + " patient(s) aged 18 or older.\n");//prints line displaying the number of patients aged 18 and over using the ov18counter
                    Console.ResetColor();//resets font color

                    while (true)//nested while loop for viewing patients or going back to the main menu
                    {
                        Console.ForegroundColor = ConsoleColor.Cyan;//sets font color to cyan
                        Console.Write("1. View Patients" + "\n" + "2. Look up other criteria ");//prints prompt to either view patients or return to main menu
                        Console.ResetColor();//resets font color

                        try//try code to make sure an integer is input from the keyboard
                        {
                            Console.ForegroundColor = ConsoleColor.White;//sets text color to white for user input
                            string tempSecondDiagChoice = Console.ReadLine();//string to store input temporarily
                            Console.ResetColor();//resets font color
                            int.TryParse(tempSecondDiagChoice, out secondDiagChoice);//parses string input to an integer value
                        }

                        catch (Exception e)//catches exception if user input isn't a numerical value that can be parsed to integer
                        {
                            Console.BackgroundColor = ConsoleColor.White;//sets text background color to white
                            Console.ForegroundColor = ConsoleColor.Red;//sets text color to red
                            Console.WriteLine("Please only enter a numerical digit!");//prints a warning that only a numerical digit should be entered
                            Console.ResetColor();//resets font color
                        }

                        Console.WriteLine(" ");//prints blank line

                        if ((secondDiagChoice == 1) && (ov18counter != 0))//checks if the second input is a 1 and that the counter is not empty
                        {
                            Console.ForegroundColor = ConsoleColor.Cyan;//sets font color to cyan
                            Console.Write("Name" + "\t" + "\t" + "\t" + "Age" + "\n");//prints labels name and age
                            Console.ResetColor();//resets font color

                            ov18dPatients = o18diagnosticPatients.ToArray();//converts list to array
                            ov18dPAges = o18diagnosticPatientsAges.ToArray();//converts list to array
                          
                            Console.ForegroundColor = ConsoleColor.White;//sets font color to white

                            for (int j = 0; j < ov18counter; j++)//for loop to print patients using 'min' as the control
                                Console.WriteLine("{0}" + "\t" + "\t" + "{1}", ov18dPatients[j], ov18dPAges[j]);//prints patients and their ages when found using arrays in 'Users' class

                            Console.ResetColor();//resets font color
                            Console.WriteLine(" " + "\n");//prints blank line
                            break;//exits if statement
                        }

                        else if (secondDiagChoice == 2)//if the second user input is 2
                            break;//breaks out else if

                        else//if the user input is neither a 1 or 2
                        {
                            Console.BackgroundColor = ConsoleColor.White;//sets font background color to white
                            Console.ForegroundColor = ConsoleColor.Red;//sets font color to red
                            Console.WriteLine("There are no patients to display. Please make sure that a 1 or 2 is entered and make sure that the criteria isn't empty.");//prints warning that only '1' or '2' should be entered and no patients were found
                            Console.ResetColor();//resets font colors
                        }
                    }
                    continue;//continues to next else if out of nested while loop
                }

                if (diagChoice == 3)//if first choice is 3 by user input
                {
                    Console.WriteLine(" ");//prints blank line
                    Console.BackgroundColor = ConsoleColor.White;//sets font background color to white
                    Console.ForegroundColor = ConsoleColor.Blue;//sets font color to blue
                    Console.WriteLine("There are " + ud100lbcounter + " patient(s) that weigh less than 100 pounds.\n");//prints the number of patients that weigh less than 100 lbs by using the ud100counter
                    Console.ResetColor();//resets font color

                    while (true)//nested while loop to either print results or go back to first while loop
                    {
                        Console.ForegroundColor = ConsoleColor.Cyan;//sets text color to cyan
                        Console.Write("1. View patients" + "\n" + "2. Look up other criteria ");//displays prompt for user to view patients or go back to main menu
                        Console.ResetColor();//resets font color

                        try//try to see if user inputs a numerical value
                        {
                            Console.ForegroundColor = ConsoleColor.White;//sets text color to white for user input
                            string tempSecondDiagChoice = Console.ReadLine(); ;//string to store user input temporarily 
                            Console.ResetColor();//resets font color
                            int.TryParse(tempSecondDiagChoice, out secondDiagChoice);//parse string to an integer value
                        }

                        catch (Exception e)//catches exception if the user input isn't a numerical value that can be converted
                        {
                            Console.BackgroundColor = ConsoleColor.White;//sets font background color to white
                            Console.ForegroundColor = ConsoleColor.Red;//sets font color to red
                            Console.WriteLine("Please only enter a numerical digit!");//prints warning that only a numerical digit should be entered
                            Console.ResetColor();//resets font color
                        }

                        Console.WriteLine(" ");//prints blank line

                        if ((secondDiagChoice == 1) && (ud100lbcounter != 0))//if the second choice is equal to '1' and that the counter is not empty
                        {
                            Console.ForegroundColor = ConsoleColor.Cyan;//sets font color to cyan
                            Console.Write("Name" + "\t" + "\t" + "\t" + "Weight" + "\n");//prints labels with name and weight columns
                            Console.ResetColor();//resets font color

                            ud100lbdPatients = u100diagnosticPatients.ToArray();//converts list to array
                            ud100lbdPWeights = u100diagnosticPatientsWeights.ToArray();//converts list to array
                           
                            Console.ForegroundColor = ConsoleColor.White;//sets font color to white

                            for (int i = 0; i < ud100lbcounter; i++)//for loop to print patients that executes by the value of min
                                Console.WriteLine("{0}" + "\t" + "\t" + "{1}", ud100lbdPatients[i], ud100lbdPWeights[i]);//prints patients in order from lists in 'Users' class

                            Console.ResetColor();//resets font color
                            Console.Write(" " + "\n");//prints blank line
                            break;//exits if statement
                        }

                        else if (secondDiagChoice == 2)//checks if the second choice is 2
                            break;//exits nested while loop

                        else//if something other than one or two is entered for secondDiagChoice
                        {
                            Console.BackgroundColor = ConsoleColor.White;//sets font background color to white
                            Console.ForegroundColor = ConsoleColor.Red;//sets font color to red
                            Console.WriteLine("There are no patients to display. Please make sure that a 1 or 2 is entered and make sure that the criteria isn't empty.");//prints warning that only '1' or '2' should be entered and no patients were found
                            Console.ResetColor();//resets font color
                        }
                    }
                    continue;//continues to the outside while loop
                }

                if (diagChoice == 4)//if the first choice is 4 by user input
                {
                    Console.WriteLine(" ");//prints blank line
                    Console.BackgroundColor = ConsoleColor.White;//sets font background color to white
                    Console.ForegroundColor = ConsoleColor.Blue;//sets font color to blue
                    Console.WriteLine("There are " + ov170lbcounter + " patient(s) that weigh more than 170 pounds.\n");//prints the number of patients that weigh more than 170 lbs by using the ov170counter
                    Console.ResetColor();//resets font color

                    while (true)//nested while loop to either print results or go back to first while loop
                    {
                        Console.ForegroundColor = ConsoleColor.Cyan;//sets font color to cyan
                        Console.Write("1. View Patients" + "\n" + "2. Look up other criteria ");//displays a prompt for user to view patients or go back to the main menu
                        Console.ResetColor();

                        try//try code to make sure an integer is input from the keyboard
                        {
                            Console.ForegroundColor = ConsoleColor.White;//sets text color to white for user input
                            string tempSecondDiagChoice = Console.ReadLine();//string to store input temporarily
                            Console.ResetColor();//resets font color
                            int.TryParse(tempSecondDiagChoice, out secondDiagChoice);//parses string input to an integer value
                        }

                        catch (Exception e)//catches exception if user input isn't a numerical value that can be parsed to integer
                        {
                            Console.BackgroundColor = ConsoleColor.White;//sets text background color to white
                            Console.ForegroundColor = ConsoleColor.Red;//sets text color to red
                            Console.WriteLine("Please only enter a numerical digit!");//prints a warning that only a numerical digit should be entered
                            Console.ResetColor();//resets font color
                        }

                        Console.WriteLine(" ");//prints blank line

                        if ((secondDiagChoice == 1) && (ov170lbcounter != 0))//checks if the second choice is 1 and that the counter is not empty 
                        {
                            Console.ForegroundColor = ConsoleColor.Cyan;//sets font color to cyan
                            Console.Write("Name" + "\t" + "\t" + "\t" + "Weight" + "\n");//prints labels with name and weight columns
                            Console.ResetColor();//resets font color
                            ov170lbdPatients = o170diagnosticPatients.ToArray();//converts list to array
                            ov170lbdPWeights = o170diagnosticPatientsWeights.ToArray();//converts list to array
                            
                            Console.ForegroundColor = ConsoleColor.White;//sets font color to white

                            for (int i = 0; i < ov170lbcounter; i++)//for loop that executes to the value of min
                                Console.WriteLine("{0}" + "\t" + "\t" + "{1}", ov170lbdPatients[i], ov170lbdPWeights[i]);//prints patients in order from the lists in 'Users' class

                            Console.ResetColor();//resets font color
                            Console.WriteLine(" " + "\n");//prints blank line
                            break;//exits if statement
                        }

                        else if (secondDiagChoice == 2)//checks if the second choice is 2
                            break;//exits nested while loop

                        else//if something other than one or two is entered for secondDiagChoice
                        {
                            Console.BackgroundColor = ConsoleColor.White;//sets font background color to white
                            Console.ForegroundColor = ConsoleColor.Red;//sets font color to red
                            Console.WriteLine("There are no patients to display. Please make sure that a 1 or 2 is entered and make sure that the criteria isn't empty.");//prints warning that only '1' or '2' should be entered and no patients were found
                            Console.ResetColor();//resets font color
                        }
                    }
                    continue;//continues to the outside while loop
                }

                if (diagChoice == 5)
                {
                    Console.ForegroundColor = ConsoleColor.White;//font color to white
                    Console.WriteLine("Thank you for using our System!");
                    Console.ResetColor();
                    Environment.Exit(0);
                }

                else//if the first user input is neither 1, 2, 3, 4, or 5
                {
                    Console.WriteLine(" ");//prints blank line
                    Console.BackgroundColor = ConsoleColor.White;//sets font background color to white
                    Console.ForegroundColor = ConsoleColor.Red;//sets font color to red
                    Console.WriteLine("Only enter '1', '2', '3', or '4'!");//prints warning to display that only a 1, 2, 3, or 4 should be entered
                    Console.WriteLine(" ");//prints blank line
                    Console.ResetColor();//resets font color 
                }
            }
        }
    }
}
```