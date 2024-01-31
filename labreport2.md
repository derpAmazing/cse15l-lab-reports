# Part 1 - ChatServer
## The Code of ChatServer
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
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

![Image](firstAddMessage.png)
