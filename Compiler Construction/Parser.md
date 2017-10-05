```Java
/**
 * Parser class to hand the left and right lists
 * 
 * @Olivia Horace
 * @version (a version number or a date)
 */
import java.util.*;
public class Parser
{
    private String optr;

    private ArrayList<String> left = new ArrayList<String>();
    private ArrayList<String> right = new ArrayList<String>();
    public Parser(String optChar){
        this.optr = optChar;
    }
    
    public String getOp(){
    return optr;
    }

    public void setLeft(ArrayList<String> arr){
        for(int i = 0; i < arr.size(); i++){
            left.add(arr.get(i));
        }
    }

    public void setRight(ArrayList<String> arr){
        for(int i = 0; i < arr.size(); i++){
            right.add(arr.get(i));
        }
    }

    public boolean isOperator(String op){
        if(op.equals("-") || op.equals("+") || op.equals("/") || op.equals("*"))
        {
            return true;
        }
        else {
            return false;
        }
    }

    public double calcLeft(){
        String opt = "";
        double calc = 0;
        for(int i = 0; i < left.size(); i++){
            if(isOperator(left.get(i))){
                opt = left.get(i);
            }
        }

        for(int i = 0; i < left.size(); i++){
            if(!(isOperator(left.get(i)))){
                switch(opt){
                    case "+":
                    calc = calc + Double.parseDouble(left.get(i));
                    break;

                    case "-":
                    calc = calc - Double.parseDouble(left.get(i));
                    break;

                    case "/":
                    calc = calc / Double.parseDouble(left.get(i));
                    break;

                    case "*":
                    calc = calc * Double.parseDouble(left.get(i));
                    break;

                    default:
                    break;
                }
            }
        }
        return calc;
    }

    public double calcRight(){
        String opt = "";
        double calc = 0;
       for(int i = 0; i < right.size(); i++){
            if(isOperator(right.get(i))){
                opt = right.get(i);
            }
        }

        for(int i = 0; i < right.size(); i++){
            if(!(isOperator(right.get(i)))){
                switch(opt){
                    case "+":
                    calc = calc + Double.parseDouble(right.get(i));
                    break;

                    case "-":
                    calc = calc - Double.parseDouble(right.get(i));
                    break;

                    case "/":
                    calc = calc / Double.parseDouble(right.get(i));
                    break;

                    case "*":
                    calc = calc * Double.parseDouble(right.get(i));
                    break;

                    default:
                    break;
                }
            }
        }
        return calc;
    }
    
    public double finalCalc(double opr1, double opr2){
        if(optr.equals("+")){
            return opr1 + opr2;
        }
        else if(optr.equals("-")){
            return opr1 - opr2;
        }
        else if(optr.equals("/")){
            return opr1 / opr2;
        }
        else if(optr.equals("*")){
            return opr1 * opr2;
        }
        else{
            System.out.println("Expression cannot be performed");
            return -1;
        }
    }
}
```