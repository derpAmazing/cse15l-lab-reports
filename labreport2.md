# Part 1 - ChatServer
## The Code of ChatServer
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    String chat = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format(chat);
        } else {
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("&");
                // s=<string>, user=<string>
                String message = parameters[0].split("=")[1];
                String username = parameters[1].split("=")[1];
                chat += (username + ": " + message + "\n");
                return chat;
            }
            return "404 Not Found!";
        }
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
## First Add Message
![Image](firstAddMessage.png)
Methods called: The ```getPath```,```contains```, ```getQuery```, and ```split``` method are called.
Relevant arguments:
- To the contains method, we pass in "/add-message", which is our only path (aside from the default "/" that I've left in)
- To the getPath method, we just pass in "/" to check whether it's the default path or the only other path which is "/add-message"
- To getQuery, we don't pass in any arguments as it just retrieves everything after ?
- To split, we pass in "&" or "=" depending on what how we need to split the queries/query pieces to obtain the username or message. Here I use "&" first to split the query into the message part and the user part.
Fields:
- The chat field is updated here with the username and message obtained from using split to split the query into pieces and formatted in the required format. Here it is updated with ```"jeremy: hi\n"```
- As the chat field was empty before, the chat field now becomes the same as what we added which is "jeremy: hi\n".
## Second Add Message
![Image](secondAddMessage.png)
Methods called: The ```contains```, ```getQuery```, and ```split``` method are called.
Relevant arguments:
- To the contains method, again we pass in "/add-message"
- To the getPath method, we just pass in "/" to check whether it's the default path or the only other path which is "/add-message"
- To getQuery, we don't pass in any arguments as it just retrieves everything after ?
- To split, we pass in "&" or "=" depending on what how we need to split the queries/query pieces to obtain the username or message. Here I use "&" first to split the query into the message part and the user part.
Fields:
- The Handler class only has one field which is ```chat`` - the chat so far.
- The chat field is updated here with the username and message obtained from using split to split the query into pieces and formatted in the required format. Here it is updated with ```"another guy: hi how are you doing!\n"```
- The chat field is now updated and the formatted string before is added on top, becoming: ```"jeremy: hi\n another guy: hi how are you doing!\n"```

# Part 2
## The absolute path to the private key for your SSH key for logging into ieng6
![Image](privateKeyPath.png)
The Absolute Path: ```C:\Users\jerem\.ssh\id_rsa```
## The absolute path to the public key for your SSH key for logging into ieng6
![Image](publicKeyPath.png)
The Absolute Path: ```C:\Users\jerem\.ssh\id_rsa.pub```
## Logging in without a password
![Image](noPassword.png)

# Part 3
The most interesting thing I've learned by far in these weeks is how URLs are formatted and how websites process these URLs into paths, queries, and even parts of a query in order to process a great number of different things. I've noticed now how google searches happen through the same format that our simplistic programs run on, where you have a path then a query that is split and processed. In google's case, it's search?q=SEARCHTERM&SOMEOTHERSTUFF. 
