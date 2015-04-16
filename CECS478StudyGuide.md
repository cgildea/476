
###CHAPTER 1

1.1 Define computer security.
- The protection afforded to an automated information system in order to attain the applicable objectives of preserving the integrity, availability and confidentiality of information system resources (includes hardware, software, information, data...).

1.2 What is the OSI security architecture?
..* It defines a systematic approach for managers, describing a way of organizing the task of providing security.

1.3 What is the difference between passive and active security threats?
..* Passive attacks have to do with eavesdropping on, or monitoring transmissions. Email, file transfers, and client/server exchanges are examples of transmissions that can be monitored. 

..* Active attacks include the modification of transmitted data and attempts to gain unauthorized access to computer systems.

1.4 List and briefly define categories of passive and active network security attacks.
..*Passive: Unauthorized Disclosure

..*Active: 
---> Deception
---> Disruption
---> Usurpation (An event that results in control of system services of functions by an unauthorized entity)

1.5 List and briefly define categories of security services.
1. Authentication
2. Access Control
3. Data Confidentiality
4. Data Integrity
5. Non-repudiation (Prevents either sender or receiver from denying a transmitted message)
6. Availability

1.6 List and briefly define categories of security mechanisms.
1. Encipherment
2. Digital Signature
3. Access Control
4. Data Integrity
5. Authentication Exchange
6. Trusted Functionality
7. Event Detection
8. Security Audit Trail


--CIA--
**Confidentiality**:
..* **Data Confidentiality** -- Assures that private information is not made available or disclosed to unauthorized individuals.
..* **Privacy** -- Assures that individuals control or influence what information related to them may be collected and stored and by whom and to whom that information may be disclosed
**Integrity**
..* **Data integrity** -- Assures that information and programs are changed only in a specific and authorized manner.
..* **System integrity** -- Assurs that a system performs its intended function in an unimpaired manner, free from deliberate or inadvertent unauthorized manipulation of the system.
**Availability** -- Assures that systems work promptly and service is not denied to authorized users.

**Least privilege** -- means that every process and ever user of the system should operate using the least set of privileges necessary to perform the task.

**Attack Surfaces** -- consists of the reachable and exploitable vulnerabilities in a system. 


###CHAPTER 2

2.1 What are the essential ingredients of a symmetric cipher?
..* Plaintext
..* Encryption algorithm
..* Secret key
..* Ciphertext
..* Decryption algorithm

2.2 How many keys are required for two people to communicate via a symmetric cipher?
..* one - it's used for both encryption and decryption

2.3 What are the two principal requirements for the secure use of symmetric encryption?
..* A strong encryption algorithm. The opponent should be unable to decrypt ciphertext or discover the key even if he or she is in possession of a number of ciphertexts together with the plaintext that produced each ciphertext.

..* Sender and receiver must have obtained copies of the secret key in a secure fashion and must keep the key secure.

2.4 List three approaches to message authentication.
..* Using conventional encryption 
..* Using public-key encryption 
.** Using a secret value

2.5 What is a message authentication code?
..* A small block of data, that is appended to a message to assure that the sender is authentic and that the message is unaltered.

2.6 Briefly describe the three schemas illustrated in Figure 2.3.


2.7 What properties must a hash function have to be useful for message authentication?
1. H can be applied to a block of data of any size.
2. H produces a fixed-length output. 
3. H(x) is relatively easy to compute for any given x, making both hardware and software
implementations practical 
4. For any given value h, it is computationally infeasible to find x such that H(x) = h (one-way
property). 
5. For any given block x, it is computationally infeasible to find y ≠ x with H(y) = H(x) (weak collision resistant) 
6. It is computationally infeasible to find any pair (x, y) such that H(x) = H(y) (strong
collision resistant)

2.8 What are the principal ingredients of a public-key cryptosystem?
..* Plaintext
..* Encryption algorithm
..* Public and private keys
..* Ciphertext
..* Decryption algorithm

2.9 List and briefly define three uses of a public-key cryptosystem.
1. Encryption/decryption: The sender encrypts a message with the recipient's public key. 
2. Digital signature: The sender "signs" a message with its private key. 
3. Key exchange: Two sides cooperate to exchange as session key. Several different approaches are possible, involving the private key(s) of one or both parties

2.10 What is the difference between a private key and a secret key?
..* The key used in conventional encryption is typically referred to as a secret key. The two keys used for public-key encryption are referred to as the public key and the private key.

2.11 What is a digital signature?
..* A mechanism for authenticating a message. Bob uses a secure hash function, such as SHA-512, to generate a hash value for the message and then encrypts the hash code with his private key, creating a digital signature. Bob sends the message with the signature attached. When Alice receives the message she calculates a hash value for the message, decrypts the signature using Bob's public key and compares the calculated hash value to the decrypted hash value. If the two hash values match, Alice is assured that the message must have been signed by Bob. It is important to emphasize that the digital signature does not provide confidentiality.

2.12 What is a public-key certificate?
..* A certificate consists of a public key plus a user ID of the key owner, with the whole block signed by a trusted third party (= certificate authority CA). The user can then publish the certificate and anyone needing this user's public key can obtain the certificate and verify that it is valid by means of the attached signature.

2.13 How can public-key encryption be used to distribute a secret key for symmetric encryption?
Digital Envelope - Bob does the following: 
1. Prepare a message 
2. Generate a random symmetric key that will be used this time only. 
3. Encrypt that message using symmetric key encryption with the one-time key.Encrypt the one-time key using public-key encryption with Alice's public key. - Attach the encrypted one-time key to the encrypted message and send it to Alice.




###CHAPTER 3

Review Questions:

3.1 In general terms, what are four means of authenticating a user's identity?
1. **Something the individual knows**: Examples includes a password, a personal identification number (PIN), or answers to a prearranged set of questions. 

2. **Something the individual possesses**: Examples include electronic key-cards, smart cards, and physical keys. This type of authenticator is referred to as a token. 

3. **Something the individual is (static biometrics)**: Examples include recognition by fingerprint, retina, and face. 

4. **Something the individual does (dynamic biometrics)**: Examples include recognition by voice pattern, handwriting characteristics, and typing rhythm.

3.2 List and briefly describe the principal threats to the secrecy of passwords?
..* **Offline dictionary attack**: The attacker obtains the system password file and compares the password hashes against hashes of commonly used passwords. If a match is found, the attacker can gain access by that ID/password combination. 

..* **Specific account attack**: The attacker targets a specific account and submits password guesses until the correct password is discovered. 

..* **Popular password attack**: A variation of the preceding attack is to use a popular password and try it against a wide range of user Ids. 

..* **Password guessing against single user**: The attacker attempts to gain knowledge about the account holder and system password policies and uses that knowledge to guess the password. 

..* **Workstation hijacking**: The attacker waits until a logged-in workstation is unattended. 

..* **Exploiting user mistakes**: Strict polices force more complicated password and the user is more likely to write it down because it is difficult to remember. An attacker may trick the user or an account manager into revealing a password (also: preconfigured passwords for system administrators are a threat)

..* **Exploiting multiple password use Electronic monitoring**: If a password is communicated across a network to log on to a remote system, it is vulnerable to eavesdropping."

3.3 What are the two common techniques used to protect a password file?
1. Using a salt value. This salt is stored in plaintext with the hash from (salt + password). 
2. Password File Access Control. The hashed passwords are kept in a separate file from the user Ids referred to as shadow password file. Only privileged users have access to this file.

3.4 List and briefly describe four common techniques for selecting or assigning passwords.
1. **User education**

2. **Computer-generated passwords**

3. **Reactive password checking**: The system periodically runs its own password cracker and notifies the user if it was able to crack his or her password.

4. **Proactive password checking**: The user chooses his password based on rules given by thesystem (eg. at least eight characters long etc.)

3.5 Explain the difference between a simple memory card and a smart card.
..* Memory Card: Stores but does not process data. 

..* Smart Card: Has a microprocessor, different types memory, I/O ports etc. May also have a crypto coprocessor and an embedded antenna.

3.6 List and briefly describe the principal characteristics used for biometric identification.
..* Facial characteristics 

..* Fingerprints

..* Hand geometry

..* Retinal pattern

..* Iris

..* Signature

..* Voice

3.7 In the context of biometric user authentication, explain the terms, enrollment, verification, and identification.
..* **Enrollment**: Each individual who is to be included in the database of authorized users must first be enrolled in the system. 

..* **Verification**: The user enters a PIN and also uses a biometric sensor. Identification: The individual uses the biometric sensor but presents no additional information.

..* **Identification**: The individual uses the biometric sensor but presents no additional information. THe system compares the presented template to a stored one and determines a match.

3.8 Define the terms false match rate and false non-match rate, and explain the use of a threshold in relationship to these two rates.
..* False match rate: It measures the percent of invalid inputs which are incorrectly accepted. 

..* False non-match rate: It measures the percent of valid inputs which are incorrectly rejected.

By moving the threshold, the probabilities can be altered but note that a decrease in false match rate necessarily results in an increase in false non-match rate, and vice versa.

3.9 Describe the general concept of a challenge-response protocol.
..* The host generates a random number r and returns it to the user (=challenge). In addition, the host specifies two functions, a hash function h() and another function f() to be used in the response. The user calculates f(r', h(P')), where r' = r and P' is the user's password. When the response arrives, the host compares the incoming result to the calculated f(r, h(P)) and if it matches the user is authenticated. Advantages: Only the hashes of the passwords have to be stored and they do not have to be transmitted directly, so i cannot be captured during transmission.


###CHAPTER 4

Review Questions:

4.1 Briefly define the difference between DAC and MAC -- 
..* **Discretionary access control (DAC)** controls access based on the identity of the requestor and on access rules (authorization) stating what requestors are (or are not) allowed to do.
..* **Mandator access control (MAC)** controls access based on comparing security labels with security clearances.

4.2 How does RBAC relate to DAC and MAC -- 
..* **Role-based access controil** controls access based on the roles that users have within the system and on rules stating what accesses are allowed to users in given roles.
RBAC seems to be somewhat of a combination of DAC and MAC.

4.3 List and define three classes of subject in an access control system --
..* **Owner**: This may be the creator of a resource, such as a file. 
..* **Group**: In addition to the privileges assigned to an owner, a named group of users may also be the granted access rights.
..* **World**: The latest amount of access is granted to users who are able to access the system but are not included in the categories owner and group of this resource.

4.4 In the contect of AC, what is the diffence between a subject and object --
..* A subject is an entity capable of accessing objects (eg. user, application, process). 
An object is resource to which access is controlled. An object is an entity used to contain information (eg. records, files, directories, processors, communication ports)

4.5 What is an access right? --
..* An access right describes the way in which a subject may access an object. Eg. read, write, execute, delete.

4.6 What is the difference between an access control list and a capability ticket? --
..* In practice, an access matrix is usually sparse and is implemented by decomposition in one of two ways. 
The matrix may be decomposed by columns, yielding access control lists. 
For each object, an ACL lists users and their permitted access rights.
Decomposition by row yields capability tickets. A capability ticket specifies authorized objects and operations for a particular user.

4.7 What is a protection domain? --
..* A protection domain is a set of objects together with access rights to those objects. In terms of the access matrix, a row defines a protection domain. Although, in the protection domain model a user can spawn processes with a subset of access rights of the user. This is useful for servers to spawn processes for different classes of users and for not fully trusted processes to reduce their access rights to a safe subset.

4.8 Briefly define the four RBAC models of Figure 4.8a. --
..* **RBAC0**: contains the minimum functionality for an RBAC system. 
..* **RBAC1**: includes the RBAC0 functionality and adds role hierarchies, which enable one role to inherit permissions from another role. 
..* **RBAC2**: includes RBAC0 and adds constraints, which restrict the ways in which the components of a RBAC system may be configured. 
..* **RBAC3**: contains the functionality of all the other three models.

| Models        | Hierarchies           | Constraints  |
| :------------- |:-------------:| :-----:|
| RBAC0      | No | No |
| RBAC1     | Yes      |   No |
| RBAC2 | No     |    Yes |
| RBAC3 | Yes    |    Yes |

4.9 List and define the four types of entities in a base model RBAC system. --
1. **User**: An individual that has access to this computer system. Each individual has an associated user ID. 
2. **Role**: A named job function within the organization that controls this computer system. 
3. **Permission**: An approval of a particular mode of access to one or more objects.
4. **Session**: A mapping between a user and an activated subset of the set of roles to which the user is assigned.

4.10 Describe three types of role hierarchy constraints. --
1. **mutually exclusive roles**: These are roles such that a user can be assigned to only one role in the set. 
2. **cardinality**: This refers to a maximum number with respect to roles. One such constraint is to set a maximum number of users that can be assigned to a given role.
3. **prerequisite roles**: May dictate that a user can only be assigned to a particular role if it is already assigned to some other specified role.

4.11 In the NIST RBAC model, what is the difference between SSD and DSD? --
..* **Static Separation of Duty Relations**: SSD enables the definition of a set of mutually exclusive roles. SSD can place a cardinality constraint on a set of roles. 
..* **Dynamic Separation of Duty Relations**: DSD limit the availability of the permissions by placing constraints on the roles that can be activated within or across a user's session.


###CHAPTER 5

```
* Database managment systems
* Basic elements of a relational database system
* Define and explain SQL injection attacks
* Compare and contrast different approaches to database access control
* Explain how inference poses a security threat in database systems
* Encyption in a database system
* Overview of cloud computing concepts and security
```

####5.1 Need for Database Security

1. Effective database security requires a strategy based on a full understanding of the security vulnerabilities of SQL.

2. Typical organizations lack full-time database secuirty personnel.  

3. Most database environments consist of a heterogeneous mixture of database platforms, enterprise platforms, and OS platforms.  This creates an additional complexity hurtle for security personnel.

####5.2 Database Management Systems

**Database** -- Is a structured collection of data stored for use by one or more applications.

**Database Management System (DBMS)** -- Which is a suite of programs for constructing and maintaining the database and for offering ad hoc query facilities to multiple users and applications.

**Query Language** -- provides a uniform interface to the database for users and applications.

###5.3 Relational Databases

1. The drawback of using a single table is that some of the columns positions for a given row may be blank.  Also, any time a new sevice or new type of information is incorporated in the database, more columns must be added and the database and accompanying software must be redesigned and rebuilt.

**Tuple** -- Rows in a database.

**Attributes** -- Columns in a database.

**Primary Key** -- Is defined to be a ortion of a row used to uniquely identify a row in a table; the primary key consists of one or more column names.

**Foreign Key** -- The attributes that define the primary key of one table must appear as attributes in another table.

####5.4 SQL Injection Attacks

**SQLi** -- is an attack that exploits a security vulnerability occuring in the database layer of an application (such as queries).

SQLi Example:
```
Robert'; DROP TABLE STUDENTS; --
```
---
**__SQLi Attack Avenues__**

* **User Input** -- Attackers inject SQL commands by providing suitably crafted user inpute.

* **Server Variables** -- Server variables are a collection of variables that contain HTTP headers, network protocol headers, and environmental variables. 
..* If these variables are logged in a database without sanitation, this could create an SQL inject vulnerability becasue attackers could forge the values that are placed in HTTP and network headers, they can exploit the vulnerability by placing data directly into the headers.

* **Second-order Injection** -- Second-order injection occurs whne incomplete prevention mechanisms against SQL injection attacks are in place.  An attacker could use data already present in the system or database to trigger an SQL injection, i.e. an attack that does not come from the user but from within the server itself.

* **Cookies** -- When a client returns to a web application, cookies can be used to restore the client's state information.  An attacker could alter a cookie to have the application server build an SQL query based on the cookie's content.

* **Physical User Input** -- By supplying user input that constructs an attack outside the realm of web requests. i.e. barcodes, RFID tags, or even paper forms which are scanned using optical character recoggnition and passed to a database management system.
---

**__Attack Types__**

* **Tautology** -- This form of attack injects code in one or more conditional statements so that they always evaluate to true. Example:
```
SELECT info FROM users WHERE name = '__ ' OR 1=1 --__ AND pwpd = ' '
```
This injection effectively disables the password check and turns the WHERE clause into a tautology.  The query evaluates to true for each row in the table and returns all of them.

* **End-of-line Comment** -- After injecting code into a particular field, legetimate code that follows are nujllified through the usage of an end of line comment.

* **Piggybacked Queries** -- The attacker adds additional queries beyond the intended query.
---

**Inferance Attack** -- The attacker is able to reconstruct the information by sending particular requests and observing the results behavior of the Website/database server.
..* **Illegal/logically incorrect queries** -- The default error message is usally too descriptive or the fact that there is an error could reveal information about the database structure.
..* **Blind SQL Injection** -- The attacker asks the server ture/false questions.  If the statement is true, the site continues to function normally, if it is false, the page differs significantly from the normal functioning page.

###5.5 Database Access Control

**Centralized Administration** -- A small number of privileged users may grant and revoke access rights.

**Ownership-based Administation** -- The owner (creater) of a table may grant and revoke access rights to the table.

**Decentralized administration** -- The owner may grant and revoke authorization rights to other users, allowing them to grant and revoke access rights to the table.

**Cascading Authorization** -- The grant option enables an access right to cascade through a number of users.  

**Role-Based Access Control (RBAC)** 
..* **Application Owner** -- An end user owns database objects as part of an application.
..* **End user other than application owner** -- An end user who operates on database objects via a particular application but does not own any of the database objects.
..* **Administrator** -- User who has administration responsibility for part or all of the database.

###5.6 Inference

**Inference detection during database design** -- This approach removes an inference channel by altering the database structure or by changing the access control regime to prevent inference.  Examples include removing data dependencies by splitting a table into multiple tables or using more finegrained access control roles in an RBAC scheme. 

**Inference detection at query time** -- This approach seeks to eleiminate an inference channel violation during a query or series of queries.  If an inference channel is detected, the query is denied or altered.

###5.7 DataBase Encryption

Two disadvantages:
* **Key management** -- Authorized users must habe access to the decryption keys for the data which they have access to. This can be a complex task in large systems.
* **Inflexibility** -- When part or all of the database is encrypted, it becomes more cifficult to perform record searching.

###5.8 Cloud Computing

Three **service models**:
1. **Software as a service (SaaS)** -- Provides service to customers in the form of software, specifically application software, running on and accessible in the cloud. i.e. Gmail or Salesforce.com

2. **Platform as a service (PaaS)** -- Provides service to customers in the form of a platform on which the customer's applications can run. i.e. Google App Engine, Salesforce1 Platform

3. **Infrastructure as a service (IaaS)** -- Provides the customer access to the underlying cloud infrastructure. IaaS provides virtual machines and other abstracted hardware and operating systems. i.e. Amazon Elastic Computer Cloud (Amazon EC2) and Windows Azure.

NIST defines four **deplorment models**:

1. **Public cloud** -- The cloud is made available to the general public or a large industry group.
2. **Private cloud** -- The cloud is operated solely for an organization.
3. **Community cloud** -- The cloud is shared by several organizations and supports a specific community that has shared concerns.
4. **Hybrid cloud** -- The cloud is a composition of two or more of the above clouds.


###CHAPTER 20

20.1 What are the essential ingredients of a symmetric cipher?
..* Plaintext
..* Encryption algorithm
..* Secret key
..* Ciphertext
..* Decryption algorithm

20.2 What are the two basic functions used in encryption algorithms?
1. substitution: each element in the plaintext is (bit, letter, group of bits or letters) is mapped into another element 
2. transposition: elements in the plaintext are rearranged

20.3 How many keys are required for two people to communicate via a symmetric cipher?
..* Sender and receiver use the same key, so only one key is required.

20.4 What is the difference between a block cipher and a stream cipher?
..* A block cipher processes the input one block of elements at a time, producing an output block for each input block. A stream cipher processes the input elements continuously, producing output one element at a time, as it goes along.

20.5 What are the two general approaches to attacking a cipher?
1. **brute-force approach** = trying all possible keys 

2. **cryptanalysis** = statistical analysis of the ciphertext (attacker must have some general idea of the type of plaintext that is encrypted)

20.6 Why do some block cipher modes of operation only use encryption while others both encryption and decryption?
..* In some modes, the plaintext does not pass through the encryption function, but is XORed with the output of the encryption function. For decryption in these cases, the encryption function must also be used .

20.7 What is triple encryption?
..* A plaintext block is encrypted by passing it through an encryption algorithm , the result is then passed through the same encryption algorithm two more times.

20.8 Why is the middle portion of 3DES a decryption rather than an encryption?
..* There is no cryptographic significance to the use of decryption for the second stage. Its only advantage is that it allows users of 3DES to decrypt data encrypted by users of the older single DES by repeating the key.

20.9 What is the difference between link and end-to-end encryption?
..* There is a difference between link encryption and end-to-end encryption in that link encryption encrypts and decrypts all traffic at each end of a communication line whereas with end-to-end encryption the message is encrypted by the sender at the point of origin and only decrypted by the intended reader

20.10 List ways in which secret keys can be distributed to two communicating parties.
1. A key could be selected by A and physically delivered to B. 
2. A third party could select the key and physically deliver it to A and B. 
3. If A and B have previously and recently used a key, one party could transmit the new key to the other, encrypted using the old key.
4. If A and B each have an encrypted connection to a third party C, C could deliver a key on the encrypted links to A and B.

20.11 What is the difference between a session key and a master key?
..*A session key is a temporary encryption key 
used between two principals. 
..*A master key is a long-lasting key that is 
used between a key distribution centre and a 
principal for the purpose of encoding the 
transmission of session keys. 
Typically, the master keys are distributed by 
noncryptographic means.

20.12 What is a key distribution center?
..* A KDC determines which systems are allowed to communicate with each other. When permission is granted for the two systems to establish a connection, the key distribution center provides a one-time session key for that connection.


###CHAPTER 21

21.1 In the context of a hash function, what is a compression function?
..* A function for a single block of bits in a hash function is referred to as compression function.

21.2 What basic arithmetical and logical functions are used in SHA?
..* circular shifts, AND, OR, NOT and XOR

21.3 What changes in HMAC are required in order to replace one underlying hash function with another?
..* If it is desired to replace a given hash function, all that is required is to remove the existing hash function module and drop in the new module.

21.4 What is a one-way function?
..* This is a function that is easy to computer on every input, but hard to invert a given image of a random input. Here "easy" and "hard" are to be understood in the sense of computational complexity theory.

21.5 Briefly explain Diffie-Hellman key exchange.
..* The security relies on the fact that, while it is relatively easy to calculate exponentials modulo a prime number, it is infeasible for large prime numbers to calculate discrete logarithms. 
Steps:
1. q prime number, a a primitive root of q
2. User A selects a random integer XA < q and computes YA=aXA mod q
3. User B selects a random integer XB < q and computes YB=aXB mod q
4. Each side keeps X private and makes the Y value available publicly to the other side. 
5. User A computers the key as K = (YB)XA mod q
6. User B computers the key as K = (YA)XB mod q
These two calculations produce identical results -> A and B have exchanged a secret value.










