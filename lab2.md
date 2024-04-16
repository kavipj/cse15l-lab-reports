# Lab 2 Report

## Part 1
Code for `ChatServer`:
```
import java.io.IOException;
import java.net.URI;
import java.net.URLDecoder;
import java.nio.charset.StandardCharsets;

interface URLHandler {
    String handleRequest(URI url);
}

class ChatHandler implements URLHandler {
    // This stores all chat messages
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
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);
        Server.start(port, new ChatHandler());
    }
}

// You will need a simple HTTP server framework like this one
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

                    // Handle request and send response
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

Screenshots of using `/add-message`:
<img width="596" alt="Screenshot 2024-04-16 at 2 14 36 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/90e3a924-9c70-4003-9fc2-4bf2a1575e8a">
<img width="504" alt="Screenshot 2024-04-16 at 2 14 26 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/3b7ba858-a9d4-4eae-b973-651d31d61177">

---

## Part 2

---

## Part 3
