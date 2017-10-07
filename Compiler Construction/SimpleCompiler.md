```Java
import java.io.*;
import java.util.*;

public class SimpleCompiler2 {
    public static void main(String[] args) throws IOException{
        //variables to store two numbers and the operation to be performed
        double oper1 = 0;
        String optr = "";
        double oper2 = 0;

        int opCount = 0;
        String root = "";
        //stack will be used to push data from the text file into 

        ArrayList<String> operands = new ArrayList<String>();
        try{
            //creates a file reader and a streamtokenizer
            Scanner scan = new Scanner(new BufferedReader(new FileReader("computations.txt")));
            String temp = "";
            while(scan.hasNext()){
                temp = scan.next();
                operands.add(temp);
            }
        }
        catch(IOException e){
            System.out.println("Please check your text file and try again");
        }

        parse(operands);
    }

    /**
     * Parse operands creates two arraylist based on where the expression is split
     * The left arraylist is the expression to the left of the main operator
     * The right arraylist is the expression to the right of the main operator
     * The parse method creates the Tree and calls the method to calcuate the final answer
     */
    public static void parse(ArrayList<String> arr){
        //create left and right lists
        //call evaluation function using these trees
        ArrayList<String> left = new ArrayList<String>();
        ArrayList<String> right = new ArrayList<String>();
        int counter = 0;

        //first checks to first see if there are parenthesis (if not then this is handled as a simple calculation)
        if((arr.contains("(") || arr.contains(")")) && parenChecker(arr)){
            //outer for loops goes through entire array list
            //counter is incremeted each time a parentheis is found
            //when counter = 1 every item encountered is added to the left tree until a closing parenthesis is found
            //when counter = 3, third parenthesis which is the second opening parenthesis, every item encountered is added to the right tree until a closing parenthesis is found
            for(int i = 0; i < arr.size(); i++){
                if(arr.get(i).equals("(")){
                    counter = counter + 1;
                }
                if(counter == 1){
                    for(int j = i+1; j < arr.size(); j++){
                        if(!(arr.get(j).equals(")"))){
                            left.add(arr.get(j));
                        }
                        else{
                            counter++;
                            break;
                        }
                    }
                }
                else if (counter == 3){
                    for(int j = i+1; j < arr.size(); j++){
                        if(!(arr.get(j).equals(")"))){
                            right.add(arr.get(j));
                        }
                        else{
                            counter++;
                            break;
                        }
                    }
                }
            }

            //creates tree to perform calculation
            Compute comp = new Compute(getMiddleOp(arr));
            comp.setLeft(left);
            comp.setRight(right);

            //System.out.println("\nLeft " + myTree.calcLeft());
            //System.out.println("\nRight " + myTree.calcRight());
            System.out.println(comp.finalCalc(comp.calcLeft(), comp.calcRight()));
        }

        //executes if expression does not contain any parenthesis or if they don't match up **WILL FIX ERROR HANDLING HERE**
        else{
            System.out.println(calcSimple(arr));
        }

    }

    /**
     * Returns the value of the main operator, the one in the middle outside of any parenthesis 
     */
    public static String getMiddleOp(ArrayList<String> arr){
        int opCounter = 0;
        String opt = "";
        for(int i = 0; i < arr.size(); i++){
            if(arr.get(i).equals("+") || arr.get(i).equals("-") || arr.get(i).equals("/") || arr.get(i).equals("*")){
                opCounter++;
                if(opCounter == 2){
                    opt = arr.get(i);
                }
            }
        }
        return opt;
    }

    /**
     * Returns the answer to an equation without parenthesis
     * Converts arraylist to stack and solves sequentially
     */
    public static double calcSimple(ArrayList<String> arr){
        double oper1 = 0;
        String optr = "";
        double oper2 = 0;

        double answer = 0;
        Stack<String> tempStack = new Stack<String>();
        for(int i = arr.size() - 1; i >= 0; i--){
            tempStack.push(arr.get(i));
        }

        try{
            do{
                oper1 = Double.parseDouble(tempStack.pop());
                optr = tempStack.pop();
                oper2 = Double.parseDouble(tempStack.pop());
            }while(!(tempStack.empty()));
        }
        //catches an exception if something is attempted to be popped into oper1 or oper2 that
        //cannot be converted to a double
        catch (NumberFormatException e) {
            System.out.println("Cannot be converted to a double");
        }
        //catches an exception if one of the lines in the do while loop cannot be executed because 
        //the stack is empty
        catch (EmptyStackException e) {
            System.out.println("This stack is empty");
        }

        //selects operation based on the value of the operation 
        switch(optr){
            case "+":
            answer = oper1 + oper2;
            break;

            case "-":
            answer = oper2 - oper1;
            break;

            case "*":
            answer = oper1 * oper2;
            break;

            case "/":
            //doesn't allow  division by 0
            if(oper2 != 0){
                answer  = oper2 / oper1;
            }
            else{
                System.out.println("You cannot divide by 0");
            }

            default:
            break;

        }
        return answer;
    }

    /**
     * Checks parenthesis in array lists and counts them
     */
    public static boolean parenChecker(ArrayList<String> arr){
        int open = 0;
        int close = 0;
        for(int i = 0; i < arr.size(); i++){
            if(arr.get(i).equals("(")){
                open++;
            }
            else if(arr.get(i).equals(")")){
                close++;
            }
        }

        //returns false if there aren't the same number of opening and closing parenthesis 
        //returns true otherwise
        if(open != close){
            return false;
        }
        else{
            return true;
        }
    }
}
```
