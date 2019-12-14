# LEC 9

**Stack Smashing Defenses**

- Canaries
- DEP/NX
- ASLR

**Canaries**

When a buffer overflows, the canary is overwritten, and an exception is raised

**What are the types of Canaries?**

- Random Canaries
- XOR Canaries

**How to bypass canary protection?**

Structured Exception Handling exploit

**How to disable Canary protection?**

```bash
gcc ... -fno-stack-protector
```

**DEP/NX**

Makes important structures in memory as non-executable, and generates an exception if you try to execute them.

**How to disable NX protection?**

gcc ... -z execstack

**How to bypass NX Protection?**

 Return-to-lib-c exploit 

**Structured Exception Handling (SEH) exploit**

Overwrite the existing exception handler structure in the stack to point to your own code

 **Return-to-lib-c exploit** 

Return to a subroutine of the lib-C that is already present in the process' executable memory

**ASLR**

The OS will randomize the location where the standard libraries and other elements are storied in memory

**How does ASLR Effect lib-c subroutines?**

It makes it harder for the attacker to guess the address of a lib-c subroutine

**How to disable ASLR protection?**

```BASH
sysctl kernel.randomize_va_space=0
```

**How to Bypass ASLR PRotection?**

- Brute Force to guess ASLR offset
- Return-Oriented-Programming exploit

**Return-Oriented-Programming exploit**

Use instruction pieces of the existing program (called "gadgets") and chain them together to weave the exploit

**How to lower the risk of a program security flaw resulting from a bug?**

- Build better programs
- Build better operating systems

**Why are we still vulnerable to buffer overflows?**

Because C has primatives to manipulate memory directly

**Type-Safe Programs**

- Cannot corrupt their own memory
- Cannot access arbitrary memory addresses
- Do not crash

**Why are we still using unsafe programming languages?**

Because C and assembly are useful for high performance and hardware

**What are our approaches to writing better programing with unsafe programming languages?**

- Defensive Programming
- Proactive
- Formal

**What does the Defensive Programming approach entail?**

- Adopting good programming practices
- Being a security-aware programmer

**What does it mean to adopt good programming practices?**

- To practice Modularity
- To practice Encapsulation
- To practice Information Hiding

**Modularity**

Having separate modules for separate functionalities

Makes it easier to find security flaws when components are independent

**Encapsulation**

Limiting the interaction between components

Avoid wrong usage of components

**Information Hiding**

Hiding the implementation

However, the black box model does not improve security

**What does it mean to be a security aware programmer?**

- Validate all inputs
- Be "fault tolerant"
- Reusing widely used code

**What does the Proactive approach entail?**

- Using security libraries
- Penetration Testing

**What does it mean to use security libraries?**

- Use built in measures to counter stack smashing

**Penetration Testing**

- Testing functionalities
- Testing the security

**What does the Formal approach entail?**

- Using formal methods to verify a program
- Using formal methods to generate a program

**What does it mean to use formal methods to verify a program**

- Static Analysis

**How is Static Analysis used to verify a program?**

- It is analyzing code to detect security flaws

**Control Flow**

Analyzing the sequence of instruction

**Data Flow**

Analyzing how data is accessed

**What does it mean to use formal methods to generate a program**?

- Proof of correctness

**What does it mean to use Proof of Correctness to generate a program?**

- To first make a mathematical description of the program
- Prove the correctness of a solution
- And then implement the solution into code/hardware

**What are the pros of using formal methods?**

Nothing is better than a mathematical proof

**What are the cons of using formal methods?**

- Development is time, money and effort consuming
- Does not prevent from specification bugs

**Sandbox**

A tightly-controlled set of resources for untrusted programs to run in

**What do Intruction Detection/Prevention Systems do?**

They detect and prevent programs based on signatures and behaviours

How are Intruction Detection/Prevention Systems still vulnerable?



# LEC 10

**Action**

performs unsolicited operations on the system

**What are the types of Action?**

- Rabbit
- Backdoor
- Spyware
- Spamware
- Ransomware
- Adware

**Rabbit**

exhausts the hardware resources of a system until failure

**Backdoor**

allows an attacker to take control of the system bypassing authorization mechanisms

**Spyware**

Collects Information

**Spamware**

Uses the system to send spam

**Ransomware**

Restricts acess to system's data and resources and demands for a ransom

**Adware**

Renders unsolicited advertisement

**Dissimulation**

Avoid detection by anti-malware programs

**What are some types of Dissimulation?**

- Rootkit

**Rootkit**

Hides the existence of malicious activities

**Infection**

Penetrate a system and spreads to others

**What are some types of infections?**

- Replication
- Subterfuge

**Replication**

Copies itself to spread

**Subterfuge**

Based on user's credulity

**What are some types of Replication?**

- Virus
- Worm

**What are some types of Subterfuge?**

- Trojan Horse

**Virus**

Contaminates existing executable programs

**Worm**

Exploits a service's vulnerability

**Trojan Horse**

Tricks user into executing malicious code

**Control**

Activate the malicious code

**What are some types of Control?**

- Backdoor
- Logic Bomb

**Backdoor**

Communicates with command and controll servers, allowing an attacker to control the virus

**Logic Bomb**

Activates the malicious code when certain conditions are met on the system

**What is the Anatomy of a Virus?**

- Infection Vector
- Payload

**Payload**

What the virus does

**Infection Vector**

How the virus penetrates the system

**Non-resident Virus**

The virus becomes inactive as soon as the infected program terminates

**Resident Virus**

The Virus remains in memory even after the infected programs terminates

**What does the Virus Scanner focus on?**

Detection

**What does the Virus Removal Tools focus on?**

Sanitation

**What are some types of Virus Scanners?**

- Signature Based
- Behaviour Based

**Signature Based Virus Scanner**

Using a signature database of existing viruses

**Behavior Based Virus Scanner**

Looking for suspicious code patterns that can be used by viruses

**Virus Removal Tools**

Cleaning the memory and the filesystem of Viruses

**Polymorphic Virus**

Virus that mutates when replicating

**How does a Polymorphic Virus Mutate?**

- Cryptography
- Injecting Garbage Code
- Doing permutations with certain instructions or block of instructions
- Using code objuscation

**How do we detect a Polymorphic Virus?**

By detecting code patterns used for the self-modification

**Metamorphic Virus**

A virus that can reprogram itself

**How does a metamorphic virus reprogram itself?**

- Using different instructions
- Using different strategies to implement a functionality

**Macro Viruses**

A Virus written in a scripting language used by some office applications

**Are Macro Viruses Cross-Platform?**

Yes

**XSS Worm**

A worm that exploits a XSS vulernability within a website

**What was the era in the 70's for Viruses?**

The era of the first self-replicating programs

**What was the era in the 80's for Viruses?**

The era of maturity and first pandemics

**What was the era in the 90's for Viruses?**

The era of self-modifying virus and macros viruses

**What was the era in the 00's for Viruses?**

The era of Trojan Horses and Internet Worms

**What was the era in the 10's for Viruses?**

The era of Cyber-Warfare Malware, Ransomware, and IoT malware

**How to create a new malware?**

1. Create payload
2. Make it Undetectable
3. Spread it

**What does malware do?**

Usually put the computer under control of a Remote Administration Tool

**Remote Administration Tool (RAT)**

A program that has full control of another computer remotely

**What are some methods of obtaining a RAT?**

- DIY
- Buy one

**What are the pros of programming a RAT yourself?**

- Free
- Personalized

**What are the cons of programming a RAT yourself?**

- Time consuming
- Requires good expertise

**How do antiviruses detect malware?**

- Static Analysis
- Dynamic Analysis

**How do antiviruses detect malware with Static Analysis?**

- Scan program comparing it to a collection of signatures
- Bypassed by encryption and code obfuscation

**How do antiviruses detect malware with Dynamic Analysis?**

- Run program in a sandbox and infer from its behavior
- Bypassed by detecting the sandbox environment and employing trigger based behaviors

**What are the pros of making the code undetectable yourself?**

- Free
- Personalized

**What are the cons of making the code undetectable yourself?**

- Time consuming
- Requires good expertise

**How we spread malware using social engineering?**

Trick people into downloading and installing the malware

**What are the pros of spreading malware using social engineering?**

- Free

**What are the cons of spreading malware using social engineering?**

- Difficult to get cautious people infected
- Limited impact

**How do we spread malware through a webpage?**

Exploit a browser/plugin vulnerability to automatically download and install the malware

**What are the pros of spreading malware through a webpage?**

- Everyone with a vulnerable browser can be infected
- Can be used for massive infections and targeted ones

**What are the cons of spreading malware through a webpage?**

- Requires good expertise of the target browser, its vulnerabilities and how to exploit them

**How do we spread malware by buying installs?**

Use a spreading service called Pay-Per-Install (PPI)

**What are the pros of spreading malware by buying installs?**

- Easy
- Can be selective about the geolocation of the hosts

**What are the cons of spreading malware by buying installs?**

- Pricy

**Is there a cyber underground market for viruses?**

Yes

**What are the consequences of the state of viruses in this day and age?**

The anti-virus "is dead"

# LEC 11

**What is a web application?**

program running on the browser + program running on server

**Authentication**

Who are the authorized users?

**Authorization**

Who can access what and how?

**Recipe for user authentication:**

- Ask user for login and password
- verify login and password
- start a session
- grant access to resources

**The concept of a session**

- Tracked by a session id between browser and web app
- id should be unique and unforgeable
- session id is bind to key/value pairs data

**How to make the session id unique and unforgeable?**

make it a long random number or a hash

**Where is the session id stored?**

in the cookie and on server

**Where is the session id key/value pairs data stored?**

on the server and in cookie

**Can the user perform operations on the session id in the cookie?**

Yes

**Can the user perform operations on the session id on the server?**

No

**What is the easiest way to steal a user's credentials?**

steal the user's password or session ID

**What are the security concerns with authentication?**

eavesdropping and tampers on the network

**What does eavesdropping on the network violate for authentication?**

confidentiality

**What does tampering on the network violate for authentication?**

integrity

**Mixed Content**

- An HTTPS contains elements served with HTTP
- An HTTPS page transfers control to another HTTP page within the same domain

**Why is Mixed Content Dangerous?**

The Authentication cookie will be sent over HTTP

**Secure Cookie Flag**

The cookie will only be sent over HTTPS

**Should you exclusively use HTTPS in production?**

Yes

**Should I always have a valid signed certificate?**

Yes

**Should I use mixed content?**

No

**Should I always use the secure cookie flag with authentication cookie?**

Yes

**How to steal passwords from a client?**

- Social Engineering
- Keyloggers
- Data mining
- Hack client code

**How to steal passwords from the server?**

- Hack the server
- Hack the server code

**What are the Frontend Vulnerabilities?**

- Content Spoofing
- Cross-site Scripting
- Cross-site Request Forgery

**What are the Backend Vulernabilities?**

- Incompletely Mediation
- Information leakage
- SQL Injection

**Information Leakage**

Exposing sensitive data to the public

**Incomplete Mediation**

- Sensitive Operations are done on the Frontend
- Frontend data should never be trusted

**SQL Injection**

- Attacker Injects SQL/NoSQL code to do operations on DB

**Content Spoofing**

- Attacker injects HTML into the page to affect other visitors
- Can be solved by data validation

**Cross-Site Scripting (XSS)**

- Attacker does Javascript Code Injection to be executed by the browser

**What could an attacker to with Cross-Site Scripting?**

- Inject illegitimate Content
- Perform illegitimate HTTP requests
- Steal Session ID from cookie
- Steal user's login/pass

**What are some Variations of XSS Attacks?**

- Reflected XSS
- Stored XSS
- DOM-based Attack

**Reflected XSS**

Malicious data sent to the backend is sent back to frontend to be inserted into the DOM

**Stored XSS**

Malicious data sent to backend DB to be sent back to frontend, inserted into the DOM

**DOM-based attack**

Malicious data is manipulated in the frontend and inserted into the DOM

**How to curb XSS attacks?**

Data inserted in the DOM must be validated

**HttpOnly cookie flag**

Makes the cookie not readable/writable from frontend

Prevents authentication from being leaked from XSS

**Cross-Site Request Forgery**

An attacker executes unwanted actions on webapp

either by cross origin requests with ajax requests

or injecting malicious urls into the page

**Same Origin Policy**

Forces resources to come from the same domain (protocol, host, port)

Only effects Ajax requests and Form actions

**Ajax requests across domains**

Attacker causes cross domain ajax request

Only HTTP response is blocked, but request goes through

**How to prevent Cross-Site Request Forgery?**

- CSRF Tokens
- SameSite cookie flag

**CSRF Tokens**

Protects legitimate requests with a CSRF token

**SameSite cookie Flag**

The cookie will not be sent over cross-site requests

**Can we trust Client side code?**

No

# LEC 12

**Social Engineering**

The act of manipulating people into performing actions or divulging confidential information

**Information Diving**

Recovering technical data from discarded material

**Phishing**

Attempting to acquire secrets by posing as a trustworthy entity

