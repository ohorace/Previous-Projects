```java 
import java.io.*;
import java.net.*;
//import org.apache.commons.io.FileUtils;

/**
 * Olivia Horace
 * CPSC 5157U
 */

public class TCPServer {
    public static void main(String argv[]) throws Exception
    {
        String clientSentence;
        String capitalizedSentence;
        Socket connectionSocket;
        BufferedReader inFromClient;
        DataOutputStream outToClient;

        ServerSocket welcomeSocket = new ServerSocket(6789);
        System.out.println("I am waiting for a connection from Client Side...");
        connectionSocket = welcomeSocket.accept();
        inFromClient = new BufferedReader(new InputStreamReader(connectionSocket.getInputStream()));
        outToClient = new DataOutputStream(connectionSocket.getOutputStream());

        //text file stored on the client sidee and buffer reader
        FileInputStream inFile = new FileInputStream("sample1.txt");
        BufferedReader fileReader = new BufferedReader(new InputStreamReader(inFile));

        int i=0;
        int errorCount = 0;//count the number of errors in transmission
        int serverCount = 0;//this count is used to keep track of when the end of the text file is reached; acts as a line counter on the server side
        int count = Integer.parseInt(inFromClient.readLine());//this is number of lines in the text file sent from the client side
        //the count variable is one read once on the server side and is only send once from the client side
        System.out.println("I am starting now...");
        while(true){
            i++;
            clientSentence = inFromClient.readLine();
            if(clientSentence == null) {      
                break;
            }
            //else statement handles all text from the text file
            //end of the text file has not been reached
            else{
                //if the serverCount (which is incremented on the server side) is equal to count (number of lines in the client's text file, sent by client)
                //then the end of the text file has been reached 
                //reinstantiate the buffer to read the server side text file from the beginning
                if(serverCount == count){
                    serverCount = 0;//reset the serverCount to 0 
                    inFile = new FileInputStream("sample1.txt");
                    fileReader = new BufferedReader(new InputStreamReader(inFile));
                }

                //checks to see if the line from the client side is NOT equal to the line from the text file stored at the server
                if(!clientSentence.equals(fileReader.readLine())){
                    //if it's not equal the errorCounter is incremented by 1
                    errorCount += 1;
                }
                System.out.println("I have received: "+ clientSentence + "   "+ i + "th times");
                
                //the serverCounter is incremented by 1
                serverCount += 1;
            }
        }

        System.out.println("Number of errors: " + errorCount);//prints the number of errors
        System.out.println("I am done now");
        welcomeSocket.close();
    }
}
```