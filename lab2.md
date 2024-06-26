# Lab 2 Report

## Part 1

### Code for `ChatServer`:
```
import java.io.IOException;
import java.net.URI;
import java.net.URLDecoder;
import java.nio.charset.StandardCharsets;

interface URLHandler {
    String handleRequest(URI url);
}

class ChatHandler implements URLHandler {
    StringBuilder chatHistory = new StringBuilder();

    public String handleRequest(URI url) {
        if (url.getPath().equals("/add-message")) {
            String query = url.getQuery();
            String[] params = query.split("&");
            String messageParam = params[0].substring(2);  // s=<string>
            String userParam = params[1].substring(5);    // user=<string>

            // Decoding URL-encoded strings
            String message = URLDecoder.decode(messageParam, StandardCharsets.UTF_8);
            String user = URLDecoder.decode(userParam, StandardCharsets.UTF_8);

            // Append to chat history
            if (chatHistory.length() > 0) {
                chatHistory.append("\n");
            }
            chatHistory.append(user).append(": ").append(message);

            return chatHistory.toString();
        } else {
            return "404 Not Found!";
        }
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if (args.length == 0) {
            System.out.println("Missing port number");
            return;
        }

        int port = Integer.parseInt(args[0]);
        Server.start(port, new ChatHandler());
    }
}

class Server {
    public static void start(int port, URLHandler handler) throws IOException {
        java.net.ServerSocket server = new java.net.ServerSocket(port);
        System.out.println("Listening on port " + port);

        try {
            while (true) {
                java.net.Socket client = server.accept();
                java.io.BufferedReader in = new java.io.BufferedReader(new java.io.InputStreamReader(client.getInputStream()));
                java.io.BufferedWriter out = new java.io.BufferedWriter(new java.io.OutputStreamWriter(client.getOutputStream()));

                String line = in.readLine();
                if (line != null) {
                    String[] requestLine = line.split(" ");
                    String path = requestLine[1];
                    URI url = URI.create("http://localhost:" + port + path);

                    String response = handler.handleRequest(url);
                    out.write("HTTP/1.1 200 OK\r\n");
                    out.write("Content-Type: text/plain\r\n");
                    out.write("Connection: close\r\n");
                    out.write("\r\n");
                    out.write(response);
                    out.flush();
                }

                in.close();
                out.close();
                client.close();
            }
        } finally {
            server.close();
        }
    }
}
```


### Screenshots of using `/add-message`:

<img width="504" alt="Screenshot 2024-04-16 at 2 14 26 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/3b7ba858-a9d4-4eae-b973-651d31d61177">

**1. Which methods in your code are called?**

`Server.start` and `handleRequest` are called.

**2. What are the relevant arguments to those methods, and the values of any relevant fields of the class?**

- `Server.start(int port, URLHandler handler)`:

`port`: The port number on which the server is set to listen (from the main method's args array). 
`handler`: An instance of `ChatHandler` which processes incoming HTTP requests.

- `handleRequest(URI url)` in the `ChatHandler`:

`url`: The `URI` instance representing the URL accessed by the client. It includes the path `/add-message` and the query parameters `s=Hello&user=jpolitz`. 
`chatHistory`: This is a `StringBuilder` that holds the cumulative chat messages. Its state changes based on the request being processed.


**3. How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.**

Before the request, `chatHistory` would be an empty `StringBuilder`.
After processing the request `add-message?s=Hello&user=jpolitz`, the `chatHistory` updates to include the new message formatted as "jpolitz: Hello".
If the `chatHistory` were not initially empty, it would append the new message on a new line, hence the use of `chatHistory.append("\n")` to ensure each message starts on a new line.

---

<img width="596" alt="Screenshot 2024-04-16 at 2 14 36 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/90e3a924-9c70-4003-9fc2-4bf2a1575e8a">

**1. Which methods in your code are called?**

`Server.start` and `handleRequest` are called.

**2. What are the relevant arguments to those methods, and the values of any relevant fields of the class?**

`handleRequest(URI url)` in `ChatHandler`:

`url`: This `URI` object represents the incoming request URL and contains the path `/add-message` and the query string `s=How are you&user=yash`.
Inside the `handleRequest` method, the query is parsed to extract the `message` and `user` values from the parameters `s` and `user`.

Internal Variables within `handleRequest`:

`messageParam`: Extracted as "How are you" (the substring following "s=" in the query).
`userParam`: Extracted as "yash" (the substring following "user=" in the query).
`message`: The decoded message text "How are you".
`user`: The decoded user name "yash".

`chatHistory`:

A `StringBuilder` object that accumulates the chat history. Initially, it was either empty or contained previous messages.

**3. How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.**

`chatHistory` in `ChatHandler`:
Before the Request: It already contained earlier chat messages, such as "jpolitz: Hello" if this is not the first message sent during the session.
After Processing This Request: The `chatHistory` updates by appending the new message. It now includes the newly formatted message `"yash: How are you"`. If it wasn't the first message, it would be appended on a new line after the previous messages, preserving the chronological order of the chat.

---

## Part 2

1. <img width="954" alt="Screenshot 2024-04-16 at 2 35 12 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/7ec8fb05-ed7c-48a3-8238-c7bf480530ff">

2. <img width="934" alt="Screenshot 2024-04-16 at 2 35 47 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/6e05a563-7ffd-44b0-b1c1-249a304efdfc">

3. <img width="778" alt="Screenshot 2024-04-16 at 2 39 41 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/eeb3052f-1483-4aa7-869b-45ba2a4f245c">

---

## Part 3

Something I learned in week 2 or 3 was how to set up my own server. We learned how to set up a server locally and via the ieng6 server. I previously had very little experience using terminal and servers so being able to create my own and run commands on it was very interesting.
