# Distributed Computing Protocol V1.0 Specification : Discovery part


```
Author              : Olivier Liechti, HEIG-VD
Last revision date  : 21.03.2014

Modified by			: Simone Righitto , Anthony Roubaty
date				: 30.03.2014

Revision history
         27.03.2014 : added messages specification
         30.03.2014 : writing chapter 1,2,3 and 5
		 30.03.2014 : completed the message specification

```

## 1. Introduction

This specification is about the Discovery protocol used in the first step of the Distributed Computing Protocol. It is essential for a client to be able to know all computing engines before starting
speak with them. So we can say that the main goal of the discovery protocol is to let a client discovery all available Computing engines.

Just to introduce the general idea:
This protocol uses some defined messages and the broadcasting technique. 
The protocol is divided in 2 possible scenario :
	a) the client start up and need to discovery computing engines
	b) a computing engine start up and need to announce itself to already active clients

But before starting with technical details here a brief overview of covered Chapters:
```
2. Terminology 		   : glossary section
3. System Architecture : show the system architecture (components and interactions between components)
4. Protocol Details    : important details for developers who need to implements the protocol
5. Examples			   : some example 
6. References          : ;-)
```

## 2. Terminology

>This is a glossary section, where you define the important terms used in your specification. It is obviously critical to be clear, consistent and precise when writing a specification. Using the same terms throughout the document is therefore important.

**TERM_NAME**: definition

**TERM_NAME**: definition


## 3. Protocol Overview

>In this section, you should provide **all the information that is required for the readers to do a high-level design of the software components** that will use your protocol to interact with each other. The readers should have a clear picture of which components are involved, why they need to interact with each other and how they interact with each other.


### 3.1. System Architecture

>Insert at least one **component diagram** here, to show a high-level overview of the system. The diagram should show the different types of components, their interfaces and their high-level interactions.

<center><img width=520 src="images/04/componentDiagram.png"></center>

### 3.2. System Components

>In this paragraph, you should describe all components in your distributed system. In some protocols, it means that you will describe a client and a server. In other protocols, you will have more components, such as gateways or proxies. Sometimes, it is valuable to include users, or more precisely user roles, in the list.

>In the template, we have created a placeholder paragraph that describes one of the components (COMPONENT_NAME_1). You should have as many such paragraphs as there are components in your system (and in the components diagram that you have provided before).

#### 3.2.1. Component COMPONENT_NAME_1

>In this paragraph, the component COMPONENT_NAME_1 should be described. **What is its role** in the overall system architecture? What are the **important and interesting aspects** that the readers should be aware of? What is/are the interface(s) that are provided by the component? How do users interact with the component? Typically, it is possible to describe a component with a couple of paragraphs. This is not the place to provide all technical details yet.

### 3.3. Interactions Between Components

>Insert one or more **sequence diagrams** here, to show the high-level interactions between the components (request-replies, discovery, etc.). This is not the place to give all the details, but it should give the reader a general understanding of what is happening at runtime. For each sequence diagram, explain the reason for which the components are interacting with each other (i.e. state the purpose of the interaction).

<center><img width=520 src="images/04/sequenceDiagram.png"></center>



## 4. Protocol Details

>In this section, you should provide **all the information that is required for the readers to do a detailed design and an implementation of the software components** that will use your protocol to interact with each other. The readers should find a clear description of the communication patterns, the syntax and semantics of messages and of other rules defined by the protocol.

### 4.1. Transport Protocols and Connections

>In this paragraph, you should explain which protocols are used to transport application-level messages. You should define the standard port(s) (in the same way that HTTP defines 80 as the standard TCP port). You should also explain how the components start to interact with each other. If a connection is established, then how is it established and what is the procedure that needs to be implemented?

>The first step before a client can establish a connection with the server it must know his address. 
Computing engines are listening over UDP (port 5050) for DISCOVERY message from clients. When a client start up and need to connect to a computing engine it will send a DISCOVERY message on broadcast mode
over UDP (port 5050). The server receive the DISCOVERY call and send back an UDP datagram to the client containing his IP address and the TCP port where is listening for connection (TCP port 6060). This response message is called HERE_I_AM. 

>Now we can start a TCP connection.
The client send an HELLO message to the server.
The server 

### 4.2. State Management

>In this paragraph, you should explain whether your protocol is stageful or stateless. If it is stageful, then you should describe all the states in which an application session can be, what events can happen in each of these states and what are the possible transitions between the states and what happens during these transitions.

>Start by showing a state machine diagram, which will give an overview to the readers. Then provide a detailed description of each state.

<center><img width=320 src="images/04/stateMachineDiagram.png"></center>


#### 4.2.1. State NAME_OF_THE_STATE_1

> In this paragraph, you should describe one particular state that appears on the state machine diagram. You should explain what it means for the conversation to be in this state. You should also explain what events are expected to happen while the conversation is in this state and what messages can be accepted from the other component. You should describe what should happen when these events happen (transition to another state, emission of a message, etc).
> 
> Sometimes, you will specify timing constraints in this part of the document. For example, you could state that when the conversation enters a particular state, then a timer is started and emits a signal after a given time. This signal would be considered as a specific event, that might trigger a transition to another state and other side effects (closing of a connection, emission of a message, etc.).

### 4.3. Message Types, Syntax and Semantics

>In this section, you should describe in details what messages are exchanged by system components, how they are structured and encoded, when they should be sent and what should happen when they are received.

> It is a good idea to write one paragraph for each type of message. Very often, you will also want to document some decisions that are valid for all messages. For example, you could state that all messages are encoded in JSON or in XML. Or, if you are using a grammar in your specification, you could state what kind of grammar it is and document the high-level production rules. Also, many protocol define a common structure for several message types, often involving the separation between an envelope (with headers) and a payload. This structure and the role of the headers may then be specified in an additional section that would be added here.

#### 4.3.1. UDP messages

>The next messages are used for a first contact between a client and a computing engine 

##### 4.3.1.1 DISCOVERY
> message sent by a client who need the list of computing engines

##### 4.3.1.2 HERE_I_AM
> message sent by the computing engine to announce it selfe to the client

#### 4.3.2. TCP messages

>The next messages are used when the client know the server and wants to connect

##### 4.3.2.1 HELLO
> message sent by a client who wants to connect

##### 4.3.2.2 
> message sent by the computing engine to announce it selfe to the client

### 4.4. Miscellaneous Considerations

> Depending on the actual system and protocol, you will need to address additional issues and specify various elements. Typical topics that are covered in protocol specifications include reliability, caching, scalability, content negotiation, encoding formats and others. You will have to adapt this part of the template to describe what is relevant to your own situation. If you have many questions to answer, then you will most likely split this section into multiple sections.

### 4.5. Security Considerations

>In many protocol specifications, security aspects of the protocol are treated in a dedicated section. Sometimes, the authentication, authorization, confidentiality rules are specified in the main protocol specification. Very often, however, the main protocol specification defines a generic mechanism (e.g. it states that requests should contain an authentication header, without fully specifying what should be transmitted in the header). Other specification documents are then written to use this extension point and to specify one or more different ways to actually handle the authentication in a system implementation. The HTTP specification follows this approach, with authentication mechanisms specified in [RFC 2617](https://tools.ietf.org/html/rfc2617). 

## 5. Examples

>In this section, you should **give examples of interactions between the components** of the distributed system. In previous sections, you have specified detailed rules (messaging patterns, session states, message syntax and semantics, etc.). Developers will use these detailed specifications when they implement your protocol.

>But by providing examples in the document, **you will help them in two ways**. Firstly, it will be **easier for them to understand what your protocol does and how**. Analyzing at a concrete dialog between a client and a server is often easier than directly digging into a more abstract definition. Secondly, it will allow them to **confirm their understanding of the protocol specification**. After reading the different rules specified in the previous sections, they will have a way to check that they have understood them correctly.


## 6. References

>Very often, you will provide references to other protocol specifications and/or to other documents. This is something that you should do in a specific section of your document.
