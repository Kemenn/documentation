# Kemenn

This is the technical documentation for the server and client fonctionnement.

- [DESCRIPTION](#description)
- [SERVER](#server)
- [CLIENT](#client)
- [MESSAGES](#message)



## Description :


### Deployement diagram
![The deployement diagram](./french_deployment_diagram.png)


### Client :

The client is made in 4 parts :

 - There is a service that **manages the connection** to the alert server. It works in parallel in a completely autonomous way.

 - There is the **shortcut detector**. It listens to the keyboard to detect the double press of the F12 key (by default). When the key has been pressed twice in a row, an alert is sent.

 - There is the **message manager**. As soon as a message is received, it processes it (answer to the server, display a window with a message, send an alert).

 - There is the **displayer**. It is responsible for displaying a window in a non-blocking way.
 
#### Client use case diagram
![The use case diagram](./french_use_case_diagram_client.png)


### Server :

The server is made in 3 parts:

 * **The configuration manager** : it is in charge of reading the configuration and looking for the necessary information to send messages to the clients.

 * **The message handler** : it processes incoming messages and replies to them.

 * **The session manager** : it keeps an updated list of the current sessions of the rds servers. It also keeps the list of correspondence between mac address and username of all clients (thin client or thick client).

 * **The web interface** : is managed by apache.


#### Server use case diagram
![The use case diagram](./french_use_case_diagram_server.png)



## Server

### Files

When kemenn server is started, fonctionnement files are stored in /tmp/kemenn.

| Filename | Fonction |
| :------: | :------- |
| kemenn_started | Contain the PID of main processus of kemenn server |
| command  | * You can write command interpretate by kemenn server |
| out.log  | The standard logs |
| err.log  | The error logs |

*: This file is edited by "kemenn" command ([read doc](#https://github.com/Kemenn/srv-kemenn#command-interface)). But you can use it at the hand with the best syntax.

The configurations files are stored in */etc/kemenn*. The .ini files is configure by [web interface](https://github.com/Kemenn/srv-kemenn#web-interface). "*kemenn*" file need [configure at the hand](https://github.com/Kemenn/srv-kemenn#configuration), and need restart of kemenn service.

The installations files are stored in /usr/share/kemenn.

#### Logs

There is 2 files for logs :
*/tmp/kemenn/out.log* for the standard output, and */tmp/kemenn/err.log* for the errors output.

**Syntax of outgoing messages :**

`r[] '' → messages received (Read)`

`s[] '' → sent message (Send)`

`m[] '' → Information message from the server`

`a[] '' → message sent for Action`



## Message

This part describe the input/output message on server. The input messages come from a client, and output is for client ;)

![sequence diagram to come...](./sequence_diagram.png)