# Lab Report 2
## Part 1
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String [] list = new String[0];

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            String everything = "";
            for(String item: list){
                everything = (everything + "%n " + item);
            }
            return String.format(everything);
        } else{
            if (url.getPath().equals("/add-message")){
                String[] parameters = url.getQuery().split("&");
                String[] front = parameters[0].split("=");
                String[] back = parameters[1].split("=");
                if (front[0].equals("s") && back[0].equals("user")){
                    int length = list.length;
                    String [] temp = new String[length + 1];
                    for(int i = 0; i < length; i++){
                        temp[i] = list[i];
                    }
                    list = temp;
                    String store = back[1] + ": " + front[1];
                    list[length] = store;
                    String everything = "";
                    for(String item: list){
                        everything = (everything + "%n " + item);
                    }
                    return String.format(everything);
                }
            }
            
        }
        return "404 Not Found!";

    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```

![Image](https://github.com/efang5/cse15l-lab-reports/blob/main/Screenshot%202024-01-26%20at%2012.36.04%20PM.png?raw=true)
Which methods in your code are called?
What are the relevant arguments to those methods, and the values of any relevant fields of the class?
How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
![Image](https://github.com/efang5/cse15l-lab-reports/blob/main/Screenshot%202024-01-26%20at%2012.36.29%20PM.png?raw=true)
Which methods in your code are called?
What are the relevant arguments to those methods, and the values of any relevant fields of the class?
How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.

## Part 2
Private Key
![Image](https://github.com/efang5/cse15l-lab-reports/blob/main/Screenshot%202024-01-26%20at%2012.34.02%20PM.png?raw=true)
Public Key
![Image](https://github.com/efang5/cse15l-lab-reports/blob/main/Screenshot%202024-01-26%20at%2012.50.52%20PM.png?raw=true)
Login Without Password
![Image](https://github.com/efang5/cse15l-lab-reports/blob/main/Screenshot%202024-01-26%20at%2012.40.36%20PM.png?raw=true)

## Part 3
In a couple of sentences, describe something you learned from lab in week 2 or 3 that you didn't know before.


