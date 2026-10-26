

### Lecture  - 1

**1. What is Data?**
• Raw, unorganized facts without inherent meaning (text, numbers, symbols, etc.).
• Data is measured in bits and bytes, and recorded without inherent significance until processed.

**2. Types of Data**
• **Quantitative**: Numerical data (e.g., weight, volume, cost).
• **Qualitative**: Descriptive, non-numerical data (e.g., name, gender, color).

**3. What is Information?**
• Organized and processed data that provides context, aids decision-making, and makes data meaningful.
• Example: Analyzing data of residents to determine senior citizens, sex ratio, etc.

**4. Data vs Information**
• **Data**: Raw facts, lacks context, unorganized, doesn’t drive decisions alone.
• **Information**: Organized, processed data with context, used for decision-making.
• Information depends on data, whereas data can exist independently.

**5. What is a Database?**
• A structured electronic system for storing, accessing, managing, and updating data.
• Requires a Database Management System (DBMS) for efficient use.

**6. What is DBMS?**
• A set of programs to manage data storage, retrieval, and operations (addition, access, update, deletion).
• Example: Ensures convenient, efficient management of relevant data for an enterprise.

**7. DBMS vs File System**
• **File System Limitations**: Data redundancy, inconsistency, difficult access, data isolation, integrity, atomicity, concurrent access, security issues.
• **DBMS Advantages**: Resolves file system limitations by offering secure, consistent, and accessible data management.


### Lecture - 2

**1. View of Data (Three Schema Architecture)**
• **Goal**: Provides an abstract view of data to simplify user interaction by hiding data storage details.
• **Levels**:
	• **Physical/Internal Level**: Lowest level, describes data storage structures, data compression, encryption.
	• **Logical/Conceptual Level**: Middle level, focuses on data relationships, used by DBAs for database design.
	• **View/External Level**: Highest level, shows personalized views to users, improves security by restricting access.

**2. Instances and Schemas**
• **Instance**: Data in DB at a specific moment.
• **Schema**: Database structure design, infrequently changes; types include Physical, Logical, and View schemas.
• **Physical Data Independence**: Changes in physical schema do not affect logical schema or applications.

**3. Data Models**
• Provides tools to describe the logical design of DB, e.g., ER model, Relational Model, Object-oriented Model.

**4. Database Languages**
• **DDL (Data Definition Language)**: Specifies DB schema, applies consistency constraints.
• **DML (Data Manipulation Language)**: For querying and modifying DB data, includes retrieval, insertion, deletion, updates.
• **Example**: SQL contains both DDL and DML.

**5. Database Access from Applications**
• Applications (written in C/C++, Java, etc.) interact with DB using APIs like ODBC (for C) and JDBC (for Java).

**6. Database Administrator (DBA)**
• **Role**: Manages schema, storage, authorization, and maintenance.
• **Responsibilities**: Schema definition, backups, security updates, system upgrades.

**7. DBMS Application Architectures**
• **T1 Architecture**: Client, server, and DB on the same machine.
• **T2 Architecture**: Client and server on different machines; API standards like ODBC/JDBC enable interactions.
• **T3 Architecture**: Client, App server, and DB separated; app server handles business logic and enhances security, scalability, and data integrity.


