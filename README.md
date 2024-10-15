# AI for Java Developers

Welcome to the AI for Java Developers project! This repository demonstrates how to integrate AI capabilities into Java applications, from simple command-line scripts to more complex Java applications.

## Project Overview

This project showcases different approaches to working with AI, specifically focusing on integrating OpenAI's GPT models into Java applications. It provides examples ranging from basic curl commands to sophisticated Spring Boot implementations.

## Project Requirements

- Java Development Kit (JDK) 23 or later
- Maven for dependency management
- OpenAI API key

## Dependencies

The project uses the following main dependencies:

- Spring Boot 3.3.4
- Spring AI 1.0.0-M3 (for the Spring Boot example)

## Getting Started

To get started with this project, follow these steps:

1. Ensure you have JDK 23 or later installed on your system.
2. Clone this repository to your local machine.
3. Set up your OpenAI API key as an environment variable:
   ```
   export OPENAI_API_KEY=your_api_key_here
   ```

## How to Run the Application

### Curl Command Example

You can quickly test the OpenAI API using the provided curl command:

```bash
#!/bin/zsh
echo "Calling OpenAI..."
PROMPT="Tell me something interesting about Java"

curl https://api.openai.com/v1/chat/completions \
-H "Content-Type: application/json" \
-H "Authorization: Bearer $OPENAI_API_KEY" \
-d '{ "model": "gpt-4o", "messages": [{"role":"user", "content": "'"${PROMPT}"'"}] }'
```

### Java Application Example

To run the simple Java application:

1. Navigate to the root directory of the project.
2. Compile and run the `Application.java` file:

```bash
javac src/main/java/dev/danvega/Application.java
java src/main/java/dev/danvega/Application
```

### Spring Boot Application

To run the Spring Boot application:

1. Navigate to the root directory of the project.
2. Run the following Maven command:

```bash
mvn spring-boot:run
```

3. Once the application is running, you can access the book recommendation endpoint by visiting `http://localhost:8080` in your web browser or using a tool like curl:

```bash
curl http://localhost:8080
```

## Relevant Code Examples

### Simple Java HTTP Client

Here's an example of how to make a request to the OpenAI API using Java's built-in HTTP client:

```java
var apiKey = System.getenv("OPENAI_API_KEY");
var body = """
        {
            "model": "gpt-4o",
            "messages": [
                {
                    "role": "user",
                    "content": "Tell me an interesting fact about the Spring Framework"
                }
            ]
        }""";

var request = HttpRequest.newBuilder()
        .uri(URI.create("https://api.openai.com/v1/chat/completions"))
        .header("Content-Type", "application/json")
        .header("Authorization", "Bearer " + apiKey)
        .POST(HttpRequest.BodyPublishers.ofString(body))
        .build();

var client = HttpClient.newHttpClient();
var response = client.send(request, HttpResponse.BodyHandlers.ofString());
System.out.println(response.body());
```

### Spring Boot Controller

Here's an example of a Spring Boot controller that uses Spring AI to generate book recommendations:

```java
@RestController
public class BookController {

    private final ChatClient chatClient;

    public BookController(ChatClient.Builder builder) {
        this.chatClient = builder.build();
    }

    @GetMapping("/")
    public BookRecommendation home() {
        return chatClient.prompt()
                .user("Generate a book recommendation for a book on AI and coding. Please limit the summary to 100 words.")
                .call()
                .entity(BookRecommendation.class);
    }
}
```

## Conclusion

This project demonstrates the power and flexibility of integrating AI capabilities into Java applications. From simple scripts to more complex Spring Boot applications, you can leverage the OpenAI API to enhance your Java projects with AI-driven features.

We encourage you to explore the code, experiment with different prompts, and adapt the examples to your specific use cases. If you have any questions or suggestions, feel free to open an issue or submit a pull request.

Happy coding with AI and Java!