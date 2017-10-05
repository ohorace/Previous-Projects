```c#
//Olivia Horace 
//February 4, 2014
//EDITED: September 16, 2015 
//EDITS(9/16/15): Fixed algorithms to display users in diagnostic phase, declared same type variables in one line, condensed number of lines, created a user exit from diagnostics
//EDITS(10/6/15): Format columns to print users 
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace BloodBank
{
    public class Patients
    {
        public static List<string> Usernames, BloodType, Height, Physician;//declares the public static list for string inputs Username, BloodType, Height, and Physician 
        public static List<int> Ages, Weight;//delcares the static list for int inputs of Age and Weight

        public static string[] uName, uBT, uHeight, uPhysician;//declares static array to hold string inputs
        public static int[] uAge, uWeight;//declares static array to hold int inputs

        public static List<int> u18diagnosticPatientsAges, o18diagnosticPatientsAges, u100diagnosticPatientsWeights, o170diagnosticPatientsWeights;//declares static int list to store ages(over and under 18) and weight(under 100lbs and over 170lbs)

        public static List<string> u18diagnosticPatients, o18diagnosticPatients, u100diagnosticPatients, o170diagnosticPatients;//declares static string list to store name of patients over and under 18 and patients under 100lbs and over 170lbs

        static Patients()//constructor for the class Patients
        {
            Usernames = new List<string>();//initializes Usernames
            Ages = new List<int>();//initializes Ages
            BloodType = new List<string>();//initializes BloodType
            Height = new List<string>();//initializes Height
            Weight = new List<int>();//initializes Weight
            Physician = new List<string>();//initializes Physician
            uName = new string[1000];//initializes new string array for usernames
            uAge = new int[1000];//initializes new string array for age
            uBT = new string[1000];//initializes new string array for bloodtype
            uWeight = new int[1000];//initializes new string array for weight
            uHeight = new string[1000];//initializes new string array for height
            uPhysician = new string[1000];//initializes new string array for physician

            u18diagnosticPatientsAges = new List<int>();//initializes patient weights list
            o18diagnosticPatientsAges = new List<int>();//initializes patient ages list
            u100diagnosticPatientsWeights = new List<int>();//initializes patient ages list
            o170diagnosticPatientsWeights = new List<int>();//initializes patient ages list

            u18diagnosticPatients = new List<string>();//initializes patients list
            o18diagnosticPatients = new List<string>();//initializes patients list
            u100diagnosticPatients = new List<string>();//initializes patients list
            o170diagnosticPatients = new List<string>();//initializes patients list  
        }

        public static void getNames(string name)//public method with no return value that accepts the string 'name' from main 
        {
            Usernames.Add(name);//adds string 'name' to 'Usernames' list   
        }

        public static void getAges(int age)//public method with no return value that accepts the string 'age' from main
        {
            Ages.Add(age);//adds string 'age' to 'Ages' list
        }

        public static void getBT(string bloodType)//public method with no return value that accepts the string 'bloodType' from main 
        {
            BloodType.Add(bloodType);//adds string 'bloodType' to the 'BloodType' list
        }

        public static void getHeight(string height)//public method with no return value that accepts the string 'height' from main
        {
            Height.Add(height);//adds string 'height' to the 'Height' list
        }

        public static void getWeight(int weight)//public method with no return value that accepts the string 'weight' from main
        {
            Weight.Add(weight);//adds string 'weight' to the 'Weight' list
        }

        public static void getPhysician(string pcPhysician)//public method with no return value that accepts the string 'pcPhysician' from main
        {
            Physician.Add(pcPhysician);//adds string 'pcPhysician' to the 'Physician' list
        }

        public static string UppercaseWords(string value)//method to capitalize the first letter of words, taking a string input
        {
            char[] array = value.ToCharArray();//declares a character array by parsing the string to an array of characters
            if (array.Length >= 1)// Handle the first letter in the string.
            {
                if (char.IsLower(array[0]))//checks if the first character is lowercase
                {
                    array[0] = char.ToUpper(array[0]);//changes the first character to uppercase
                }
            }

            for (int i = 1; i < array.Length; i++)//scans through the rest of the array
            {
                if (array[i - 1] == ' ')//checks for spaces
                {
                    if (char.IsLower(array[i]))//checks if the character after the space is lowercase
                    {
                        array[i] = char.ToUpper(array[i]);//changes the character to uppercase
                    }
                }
            }
            return new string(array);//returns the new string from the array 
        }

        public static void Display()//method to print the list contents, accepts no parameters 
        {
            Console.WriteLine("");//prints blank line

            uName = Usernames.ToArray();//converts 'Usernames' list to a string array called uName (user name)
            uAge = Ages.ToArray();//converts 'Ages' list to a string array called uAge (user age)
            uBT = BloodType.ToArray();//converts 'BloodType' list to a string array called uBT (user blood type)
            uWeight = Weight.ToArray();//converts 'Weight' list to a string array called uWeight (user weight)
            uHeight = Height.ToArray();//converts 'Height' list to a string array called uHeight (user height)
            uPhysician = Physician.ToArray();//converts 'Physician' list to a string array called uPhysician (user physician) 

            int min = Math.Min(uName.Length, uAge.Length);//sets a integer named 'min' to be the determine the array with the least indices (they are equal) 
            min = Math.Min(min, uBT.Length);//also checks 'uBT' (all are equal)

            Console.ForegroundColor = ConsoleColor.Cyan;
            Console.Write("{0, -20} {1, -10} {2, -10} {3, -10} {4, -10} {5, -10}\n", "Name", "Age", "Blood", "Height", "Weight", "Physician");
            Console.ResetColor();

            Console.ForegroundColor = ConsoleColor.White;
            String s = "";
            for (int index = 0; index < min; index++)
                s += String.Format("{0, -20} {1, -10} {2, -10} {3, -10} {4, -10} {5, -10:N0}\n", uName[index], uAge[index], uBT[index], uHeight[index], uWeight[index], uPhysician[index]);

            Console.WriteLine(s);
            Console.ResetColor();
        }
    }
}
```