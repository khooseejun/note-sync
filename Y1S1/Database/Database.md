# Chap 1

1) Main use of DBMS in organizations
	- Enterprise applications
	- enterprise resource planning system
	- data warehousing implementation
	- big data analytics

2) database characteristics
	- persistent
	- lasts a long time
	- lasts longer than  the execution of a computer program

	- inter-related
		- stores entities and relationships among the entities
		- the relationship, connection among entities
	- shared
		- multiple users, hundreds to thousands of data entry screens and reports
		- multiple users, many people simultaneously use a database

3) application of database ( the range of database applications)
	- personal databases
	- two-tier client/server databases
	- multiple client / server databases

4) Define DBMS and SQL
	- DBMS
		- The database management system is a software suite that creates, processes, and administers databases.
	- SQL
		- The structured query language is an internationally recognized standard database language that is used by all commercial DBMSs.

5) Data and Information
	- Data
		- Raw facts, raw data that not yet been processed to reveal the meaning
		- building blocks of information
		- Data management such as generation, storage, and retrieval of data
	- Information
		- produced by processing data
		- reveals the meaning of data
		- enables knowledge creation

6) If ask different between data and information : 
	- The main difference between data and information is that data refers to raw facts or raw data that have not yet been processed to reveal their meaning. Data serves as the building blocks of information and involves management activities such as the generation, storage, and retrieval of data.

	- information is produced by processing data, and it reveals the meaning of the data. Information is meaningful and useful as it enables knowledge creation for better understanding and decision-making.
# Chap 2

1) DBMS VS file-based system (three different)
	- In a file-based system, the same data may be stored in multiple files,which causes redundancy In contrast,

	- A DBMS integrates data into a single logical repository, reducing redundancy and maintaining consistency

	- In a file-based system, any change in the file structure requires corresponding changes in all related application programs.

	- In a DBMS, data is independent from application programs due to the abstraction provided by the system, allowing greater flexibility.

	- In a file-based system,generating new reports or queries requires extensive programming in 3GL, which is time-consuming

	- In a DBMS, users can issue and queries using a query language such as SQL, making data retrieval faster, easier, and more efficient.

2) Types of database
	- single-user
	- supports only one user at a time
- Desktop
	- single 
		- user database running on a personal computer
	- Multi-user
		- supports multiple concurrent users at the same time
	- work-group
		- Multi-user database that supports a small group of users or a single department
	- enterprise
		- multi-user database that supports a large group of users or an entire organization

3) Why database design is important
	- defines the database’s expected use
	- avoid redundant data
	- Different approach needed for different types of databases

4) Define data redundancy
	- Data redundancy results in data inconsistency
	- Different and conflicting versions of the same data appear in different places
	- Data anomalies develop when required changes in redundant data are not made successfully

5) Define anomalies and three types of anomalies
	- Modification anomalies
	    - Occur when changes must be made to existing records
	- deletion anomalies
    	- occur when deleting records
	- insertion anomalies
    	- occur when entering new records

6) The database system environment
	- Hardware
	- software
	- people
	- procedures
	- data

7) DBMS function
	- data dictionary management
	- data storage management
	- security management
	- backup and recovery management

# Chap 3

1) Define data model
	- Data model is a representation, usually graphical, of a real-word data structure.

2) Define business rules
	- A business rule is a brief, precise, and unambiguous description of a policy, procedure, or principle within a specific organization.

3) Examples of business rules (FInd on question give )

4) Importance of business rules
	- They standardize the company’s view of data.
	- They serve as a communication tool between users and database designers
	- They allow database designers to understand the nature, role, and scope of data
	- They help designers to understand business processes.

5) Data model components
	- Data model components are entities, attributes, relationships, and constraints
	- A noun in a business rule will translate into an entity in data model

6) Entity relationship diagram/model ( ERD )
	- ERD advantages
		- visual representation
		- effective communication tool
	- ERD disadvantages
		- limited constraint representation
		- limited relationship representation
		- loss of information content
		- no data manipulation language
# Chap 5

1) Key
    1) Primary key
		- Primary key is an attribute that is uniquely identifies a row in a table 
		- A primary key is a candidate key selected as the primary means of identifying rows in a relation. 

	2) Foreign key
		- Foreign key is an attribute that establishes the relationship between database tables
		- A foreign key is the primary key of one relation that is placed in another relation to from a link between the relations

	3) Composite key
		-  composite key is a key that consists of two or more columns

	4) Candidate key
		- A candidate key is a key that determines all of the other columns in a relation.

2) Denormalisation
	- insert problems
	- update problems
	- delete problems

3) Define normalisation
	- Process for evaluating and correcting table structures to minimize data redundancies.

4) Work a series of stages normal from (three NF)
	- First normal from (1NF)
	- Second normal from (2NF)
	- Third normal from (3NF)
# Chap 7
1) Difference between data administration and database administration
	- Data administration is a high-level function responsible for the overall management of data resources in an organization, including maintaining corporate-wide definitions and standards
	- Database administration is a technical function that focuses on the physical design of the database and handles technical issues such as security enforcement, database performance, backup and recovery.

  2) Data administration function/rules
	- develop information architecture
	- resolve data conflicts
	- manage the data repository

3) Database administration function/rules
    - analyzing and designing databases
	- selecting DBMS and related software tools
    - Tuning database performance

4) Database backup and recovery ( four basic facilities)
	- backup facilities
	    - save copies of the database regularly so it can be restored if damaged

	- journalizing facilities
		- keep logs of all changes and transactions to track what happened.

	- checkpoint facilities
	    - Pause, finish all current work, and update logs so recovery is faster

	- recovery manager
		- The recovery manager uses the transaction log and the database change to restore the database.