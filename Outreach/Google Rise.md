/*In this exercise we will be creating an Account class that allows us to deposit and withdraw money*/  
  
### Step One: ### First we must decide where to start and what things we will need. For our purposes, will we start by making the actual *Account* class first. What kind of properties do we need for a bank account? These will be our fields or instance variables.  
  
**Things to Remember:** Our instance variables should be private and our class name *Account* should start with a capital letter.  
  
**To get you started:**  
private String customerName; //this is the name of the account holder  
  
private __________ balance; //this is the amount of money we currently have in the account. What type of variable should “balance” be?  
  
### Step Two: ### Now in order to use our *Account* class and the methods we will later create, we will need objects. The class will make the objects and our constructor will be used to give these objects properties, either by a default constructor or a custom constructor.  

**Things to Remember:** Java will automatically create a default constructor but it is always best to create your own. A *default constructor* takes no parameters and will automatically assign every object created without parameters predetermined properties. A *custom constructor* takes parameters and will assign information passed in through these parameters as the object’s properties. 
Constructors **must** have the exact same name as your class.  
  
**To get you started:** First we will create the default constructor. What if someone wants to use our program but they don’t know while using it what the account holder’s name will be or how much their starting balance will be? This is the purpose of our default constructor.  

/**  
 *Default constructor to assign properties to an Account object  
**/  
public Account()//no parameters  
{  
customerName = “John Doe”;  
balance = 500.50  
}  
  
/**  
 *Custom constructor to assign properties to an Account object if we  
 *know beforehand what properties we want to assign them  
**/  
public Account(String newName, double newBalance)//parameters should be  variables that will be assigned to properties  
{  
____________________ = newName;  
  
____________________ = newBalance;  
}  
  
### Step Three: ### Now that we have our constructors we can create the heart of this class, our methods.  
We should consider the kind of methods that we will need. What do we need our Account class to be able to do?  
  
**Things to Remember:** Your AP exam will consist of mainly public methods. So for this class our methods will be public.  
  
**To get you started:** We will need accessor (get) methods as well as mutators or set methods. Our get methods will return a property and our set methods will assign a value to our properties.   
  
Set methods are **void!** They do not return anything. Our set methods will take parameters because we must know what values we are assigning.  
  
/**  
 *Set customerName  
**/  
public void setCustomerName(String newName)  
{  
this.customerName = newName;  
}  
  
Now we will need to do the same thing for balance:  

/**  
 *Set balance  
**/  
public void setBalance(                 )  
{  
____________________ = _____________;  
}  
  
Get methods must have a return type (i.e. they will **NOT** be void). The return type needs to be the same as the instance variable that we want to return. Our get methods will not take parameters and it will have to use the return keyword.  
  
/**  
 *Get customerName   
**/  
public String getCustomerName()  
{  
return this.CustomerName;  
}  
  
Now we will need to do the same thing for balance:  
  
/**  
 *Get balance  
**/  
public _________  getBalance()  
{  
_____________________________;  
}  
  
Now we can create the rest of our methods. What behaviors will our class need? Our Account class will need to be able to deposit money and withdraw money. So use the provided skeletons to construct these classes.  

**Things to Remember:** Our methods will still be public. For our program, these methods will not have a return type and they will need to take parameters.  
  
/**  
 *Deposit money method  
**/  
public void Deposit(double newAmount)  
{  
//how will we add the value of the parameter to the current  //balance and   store it  
}  
  
/**  
 *Withdraw money method  
**/  
public void Withdraw(double newAmount)  
{  
//how will we subtract the value of the parameter from the  
//current balance and store it  
}  
  
We also must create a toString method that will allow us to return the properties associated with an Account object  
  
**Things to Remember:** Java already has a toString method but to control the way things are displayed then it is good practice to always make your own toString method. The toString method returns a String that contains the values of our properties. The toString method does not take any parameters.   
/**  
 *To String method  
**/  
public String toString()  
{  
//how will we return a String of our properties   
}  

### Step Four: ### Now that we have constructed our Account class we need to make our AccountTester class. This class will contain our main method to run our program. In this class we need to create two Account objects; one will use our default constructer and the other will use our custom constructor. Then, we need to deposit and withdraw money from both accounts. Finally, we need to display the Customer Name and the Balance of both accounts. Complete the skeleton to form our tester class.  
  
public class AccountTester {  
public static void main (String args[]) {  
   
//Create two account objects  

_____________________________ = new _______________()//this should use our default constructor  
   
_____________________________ = new _______________(“                     “, _____ . ___)  
//this should use our custom constructor  

//Make deposits to both accounts, remember our deposit method is looking for a parameter   






//Make withdrawals from both accounts, remember our withdrawal method is looking for a parameter  






//Display the values of our account objects   





	}  
}  

These are the basic tools you will need to use each time you start a Java program. You must consider what types of properties you will need for instance variables, the kinds of behaviors class objects will have, and how to display the properties of objects. The tester class is used to execute the methods of your classes.   
