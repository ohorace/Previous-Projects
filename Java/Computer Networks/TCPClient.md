```java

import java.io.*;
import java.net.*;
import java.util.Scanner;
import java.io.File;
import java.io.InputStream;
import java.io.OutputStream;
/**
 * Olivia Horace
 * CPSC 5157U
 */
public class TCPClient {
    public static void main(String argv[]) throws Exception {
        String sentence;
        String modifiedSentence;

        long startTime = 0;//start time of counter
        long endTime = 0;//endtime of counter
        float totalTime = 0;//total time elapsed from start to finish

        Scanner in = new Scanner(System.in);
        BufferedReader inFromUser = new BufferedReader(new InputStreamReader(System.in));
        Socket clientSocket = new Socket("localhost", 6789);

        DataOutputStream outToServer = new DataOutputStream(clientSocket.getOutputStream());
        BufferedReader inFromServer = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));

        //text file and buffer
        FileInputStream inFile = new FileInputStream("sample1.txt");
        BufferedReader fileReader = new BufferedReader(new InputStreamReader(inFile));

        System.out.println("Continue or not (Y/N)");
        String s = in.next();

        int count = 0;//number of lines in the text file
        String textCount;//variable used to store line from text file for the while loop
        try{
            while((textCount = fileReader.readLine()) != null){
                count++;//increment line counter
            }
        }
        catch (FileNotFoundException c){
            System.out.println("File not found");
        }
        //sends to the server the number of lines in the text file
        //it is only sent one time before the main loop begins
        outToServer.writeBytes(count + "\n");
        //reinstantiates text file and buffer to start reading from the beginning
        inFile = new FileInputStream("sample1.txt");
        fileReader = new BufferedReader(new InputStreamReader(inFile));

        while (s.equals("Y") || s.equals("y")) {
            //resets transmission time to 0
            totalTime = 0;
            try {
                //for loop transmits file 100 times
                for (int i = 1; i <= 100; i++) {
                    //String to store text from text file
                    String textLine;
                    //start timer
                    startTime = System.currentTimeMillis();
                    while ((textLine = fileReader.readLine()) != null) {
                        //as long as the line is not null, send the data from the text file to the server
                        outToServer.writeBytes(textLine + "\n");               
                    }
                    //stop timer
                    endTime = System.currentTimeMillis();
                    //reinstantiate text file and buffer to begin reading from the top again on next transmission
                    inFile = new FileInputStream("sample1.txt");
                    fileReader = new BufferedReader(new InputStreamReader(inFile));
                }

                //compute the total time by subtracting the end time from the start time
                //add to total time
                totalTime += (endTime - startTime);
            } 
            //catch file not found exception
            catch (FileNotFoundException e) {
                System.out.println("File Not Found");
            }

            //find average transmission time
            totalTime = totalTime / 100;
            System.out.println("Average transmission time: " + totalTime + "ms");
            System.out.println("Continue or not (Y/N)");
            s = in.next();
        }

        clientSocket.close();
        System.out.println("I am done now!");
        inFile.close();
    }
}
```