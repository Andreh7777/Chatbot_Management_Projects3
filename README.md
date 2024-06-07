# Chat Service with FastAPI, Redis, and External API OpenAI Compatible Integration

This application aims to provide a chat service where users can send messages and receive responses.
It uses FastAPI for the web framework, Redis for efficient storage of chat histories and integrates 
with an external API for generating responses. The goal is to offer a straightforward and interactive 
chat experience for users while ensuring smooth management of chat data.

Here’s what it does:

Chat Service:
the application provides a chat service where users can send messages and receive responses.
Each chat session is identified by a `session_id`, allowing users to maintain a conversation over multiple interactions.

Configuration Management:
the application loads configuration settings from a `config.ini` file 
(you will have to modify the file with your own data). These settings include Redis connection details,
API endpoint, and authentication tokens.

Redis Cache:
the application uses Redis for caching chat histories. It initializes a Redis client with host,
port, and password parameters from the configuration file. Redis stores each user's chat history,
identified by their session ID.

Scheduler for Cache Cleanup:
the application employs `apscheduler` to schedule periodic cleanup of the 
Redis cache. A background job is set up to delete all messages in the Redis cache every hour 
(it can be changed to another desired value), ensuring efficient memory usage and preventing cache bloat.

External API Integration:
the application integrates with an external API to generate chat responses.
It sends the user's message history to the API, which returns a response generated by a language model
(you can also select another model, in this case I used “mistralai/Mistral-7B-Instruct-v0.2”). 
The API details and authentication are configured in the `config.ini` file.

Various libraries are imported in the code, and I've included a "requirements.txt" file to facilitate 
their installation. 

Simply run: pip install -r requirements.txt

Ensure that all necessary packages are installed and imported correctly before running the application.

Example of usage:
uvicorn main:app --reload
(change “main” to your python project name)

Example of request:
curl --location 'http://localhost:8000/chat/' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer #enter your token' \
--data '{
    "session_id": " YOUR_SESSION_ID",
    "message": " YOUR_MESSAGE_HERE"
  }'
  
1.	Replace 'http://localhost:8000/chat/' with the correct address of your server if it is different.
2.	Enter your token.
3.	Replace "YOUR_SESSION_ID" with the session ID you want to use. If you don’t provide a session_id, 
    a new one will be generated for you. During the first request you can simply avoid entering the 
	session id by deleting the "string" message keeping the quotes.
4.	Replace "YOUR_MESSAGE_HERE" with the message you want to send to the chatbot. 

These commands are for a bash shell, which is commonly used in Linux terminals (or alternatively, you can use 
Postman). If you’re using a different shell or operating system, you might need to adjust the syntax. 

Cheers,

@Andreh7777
