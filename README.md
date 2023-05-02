Download Link: https://assignmentchef.com/product/solved-comp6231-assignment-1-distributed-flight-reservation-system-dfrs-using-java-rmi
<br>
In the assignments and project, you are going to implement a simple Distributed Flight Reservation System (DFRS): a distributed system used by passengers and managers to make and manage flight reservations between different cities. Consider three cities: Montreal, Washington and New Delhi. Flights can be booked between these cities by passengers and the number of flights available between these cities is limited and can be controlled by the managers. There are different classes of flights such as economy class, business class and first class and the number of seats for each class from one city to other is fixed.




When a passenger books a flight, the passenger’s information is stored in a passenger record in the servers with following details: first name, last name, address, phone no., destination, class of flight, date of flight. These records are placed in several lists that are stored in a hash map according to the first letter of the last name indicated in the records. For example, all the records with the last name starting with “A” will belong to the same list and will be stored in a hash map (acting as the database) and the key will be “A”. Each server also maintains a log containing the history of all the operations that have been performed on that server. This should be an external text file (one per server) and shall provide as much information as possible about what operations are performed, at what time and who performed the operation.




The users of the system are the passengers who want to book the flights and the managers who will add and edit the flights. Managers can be identified by a unique <em>managerID</em>, which is constructed from the acronym of the city and a 4-digit number (e.g. MTL1111). Whenever a manager performs an operation, the system must identify the city that manager belongs to by looking at the <em>managerID </em>prefix and perform the operation on that server. A manager should also maintain a log (text file) of the actions he/she performed on the system and the response from the system when available. For example, if you have 10 managers using your system, you should have a folder containing 10 logs.




Whenever a passenger wants to book the flight, he/she has to invoke the following operation on the specific city’s server:

<ul>

 <li><em>bookFlight </em>(<em>firstName</em>, <em>lastName, address, phone, destination, date, class</em>) :</li>

</ul>

When a passenger invokes this method on the server for his/her departure city through a client program, the server attempts to create a passenger record<em>  </em>with the

<em>C</em> <em>OMP 6231 (Distributed System Design), Fall 2016 — Assignment 1                                        Page 2</em>

information provided, assigns a unique <em>RecordID </em>and inserts the record at the appropriate position in the hash map. The server returns information to the manager whether the operation was successful or not and both the server and the client store this information in their logs.

Managers may invoke the following operations:

<h2>•     getBookedFlightCount (recordType)</h2>

A manager invokes this method from his/her <em>ManagerClient </em>and the server associated with that manager concurrently finds out the number of records (i.e. number of flights booked) in all the cities/servers using UDP/IP sockets and returns the result to the manager. Note that only record counts (a number) are returned and not the records themselves. For example, if MTL has 6 records, Washington has 7 and New Delhi had 8, it should return the following: MTL 6, WST 7, NDL 8.

<h2>•     editFlightRecord (recordID, fieldName, newValue)</h2>

When invoked by a manager, the server associated with this manager (determined by the unique <em>managerID</em>) can change the information about the flights available on a particular date from a specified city tow a specified city. For example, the manager can change the information that flight going from Washington to New Delhi on September 24, 2016 at 1:00 p.m. has 55 economy seats, 20 business seats, and 15 fit class seats. He can even create a new flight at a specific date and delete the flight at a specific time.

<em> </em>

Thus, this application has a number of <em>Servers </em>(one per city) each implementing the above operations for that city, passengers and managers invoking the operations at the associated <em>Server </em>as necessary. When a <em>Server </em>is started, it registers its address and related/necessary information with a central repository. For each operation, the <em>ManagerClient </em>finds the required information about the associated <em>Server </em>from the central repository and invokes the corresponding operation.




In this assignment, you are going to develop this application using Java RMI. Specifically, do the following:

<ul>

 <li>Write the Java RMI interface definition for the <em>Server </em>with the specified operations.</li>

 <li>Implement the <em>Server</em>.</li>

 <li>Design and implement a <em>ManagerClient, </em>which invokes the server system to test the correct operation of the DFRS invoking multiple <em>Server </em>(each of the servers initially has a few records) and multiple managers.</li>

</ul>

You should design the <em>Server </em>maximizing concurrency. In other words, use proper synchronization that allows multiple passengers and managers to perform operations for the same or different records at the same time.

<strong> </strong>

<strong>Marking Scheme </strong>

<strong>[30%]</strong>  <em>Design Documentation</em>: Describe the techniques you use and your architecture, including the data structures. Design proper and sufficient test scenarios and explain what you want to test. Describe the most important/difficult part in this assignment. You can use UML and text description, but limit the document to 10

<em>C</em> <em>OMP 6231 (Distributed System Design), Fall 2016 — Assignment 1                                        Page 3</em>

pages. Submit the documentation and code by the due date; print the documentation and bring it to your demo.

<strong>[70%]</strong> <em>Demo in the Lab</em>: You have to register for a 5-minute demo. Please come to the lab session and choose your preferred demo time in advance. You cannot demo without registering, so if you did not register before the demo week, you will lose  40% of the marks. Your demo should focus on the following.

[50%] C<em>orrectness of code:</em> Demo your designed test scenarios to illustrate the correctness of your design. If your test scenarios do not cover all possible issues, you’ll lose part of mark up to 40%. You will also be evaluated on            the implementation of your design.

[20%] <em>Questions:</em> You need to answer some simple questions (like what we’ve discussed during lab tutorials) during the demo. They can be theoretical related directly to your implementation of the assignment.




<strong>Questions </strong>

If you are having difficulties understanding sections of this assignment, feel free to email the Teaching Assistant Mr. Harpreet Narula at <a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="ed858c9f9d9f888899838c9f98818cddddd8ad8a808c8481c38e8280c3">[email protected]</a> It is strongly recommended that you attend the tutorial sessions which will cover various aspects of the assignment.