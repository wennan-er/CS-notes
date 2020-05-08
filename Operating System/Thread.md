# Thread

## Thread Introduction
#### What is a thread?
* A sequential execution stream within process.   
  * Thread - Lightweight process. Multiple threads share one address space.    
  * Process - Heavyweight process. A process have their own address space.  

#### Thread Vs Process
| Process                                    | Threads                                         | 
| ------------------------------------------ | :---------------------------------------------  | 
| More security is desired (eg.Chrome browser: more process - more tabs )   | Leverage the power of a multi-core system       | 
| Running into synchronization primitives     | Want communication between the processes simplified      |  
| Don’t worry about race conditions     |  Want threads to be part of the same process  |
| One thread blocks in a task (say IO) then all threads block |   |