# Disk Representation 

## DBMS Architecture
client: SQL.  
server: Database Management System.  

#### Database Management System Modules
(1)Query Parsing & Oprators: Parse, check and verify SQL legal. Translate into an efficient relational query plan.  
(2)Relational Operators: There are individual algorithms put together to execute a dataflow.  
(3)Files and Index Management: Organiza tables and Records as groups of pages in a logical file.  
(4)Buffer Management: Map disk block to system memory(RAM).  
(5)Disk Space Management: Map pages to locations on disk. (read/write a page, allocate/de-allocate logical pages)    

![](./pic/dbms1.png)
## Disks
NOTE: There is **no pointer dereference**. Instead using an API:  
READ: transfer "page" of data from disk to RAM.   
WRITE: transfer "page" of data from RAM to disk.  

#### Components of a disk
* Only one head reads/writes at any one time.  
* Block = Unit of transfer for disk read/write. Block/page size is a multiple of (fixed) sector size.  

#### Accessing a Disk page
(1)seek time: movine arms to position disk head on track.  
(2)rotational delay: waiting for block to rotate under head.  
(3)transfer time: actually moving data to/from disk surface.  
Note: key to I/O cost: reduce seek/rotational delays.  

