# Multi-threaded File Compression System

## Overview

This project is a TCP-based client/server application developed using C# and Windows Forms.

The system allows multiple clients to connect to a server and send files for compression.  
The server receives the file, compresses it using GZip compression, then sends the compressed version back to the client.

The project demonstrates:

- TCP socket programming
- Multi-threading
- File streaming
- NetworkStream usage
- Sending and receiving files using sockets
- Windows Forms GUI development

---

# Technologies Used

- C#
- .NET Framework
- Windows Forms
- TCP Sockets
- NetworkStream
- GZipStream

---

# Project Structure

## Server

The server application:

- Waits for client connections
- Creates a separate thread for every connected client
- Receives file size first
- Receives file bytes
- Compresses the file
- Sends compressed file size
- Sends compressed file bytes

## Client

The client application provides a graphical interface that allows the user to:

- Select a file
- Connect to the server
- Send the file
- Receive the compressed version
- Save the compressed file locally

---

# Communication Protocol

The communication process is implemented as follows:

## Client → Server

1. Send file size
2. Send file bytes

## Server → Client

1. Send compressed file size
2. Send compressed file bytes

---

# Important Concepts Used

## TCP Connection

The connection is established using:

```csharp
Socket client = new Socket(
    AddressFamily.InterNetwork,
    SocketType.Stream,
    ProtocolType.Tcp);
```

---

## File Transfer Using Bytes

Files are transferred as byte arrays:

```csharp
byte[] fileBytes = File.ReadAllBytes(path);
```

---

## Receiving Data Using Loops

The application uses loops while receiving data because TCP data may arrive in multiple packets.

```csharp
while(totalReceived < fileSize)
{
    int received = ns.Read(
        buffer,
        totalReceived,
        fileSize - totalReceived);

    totalReceived += received;
}
```

---

# How To Run

## Server

1. Open the server project
2. Run the application
3. The server starts listening on port 9050

## Client

1. Open the client project
2. Run the application
3. Select a file using the Browse button
4. Click Send
5. The compressed file will be received and saved

---

# Notes

- The server supports multiple clients using threads.
- NetworkStream is used for sending and receiving file data.
- StreamReader and StreamWriter are used only for text messages.
- Binary files such as images, PDFs, and compressed files are transferred using byte arrays.

---

# Author

Abdullah Ahmed