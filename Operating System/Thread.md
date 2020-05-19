# Thread

## Thread Introduction
#### What is a thread?
* A sequential execution stream within process.   
  * Thread - Lightweight process. Multiple threads in one process share one address space.      
  * Process - Heavyweight process. A process have their own address space.  

#### Thread Vs Process
| Process                                    | Threads                                         | 
| ------------------------------------------ | :---------------------------------------------  | 
| More security is desired (eg.Chrome browser: more process - more tabs )   | Leverage the power of a multi-core system       | 
| Running into synchronization primitives     | Want communication simplified and cheaper      |  
| Don’t worry about race conditions     |  Switching between threads is cheaper than process  |
| One thread blocks in a task (say IO) then all threads block |   |

#### Thread State  

<div align=center>
<img src="./pic/Thread/thread1.png" width="15%" height="30%"/>  
</div>

* State shared by all threads in addr space  
  * Content of memory(global variables, heap).  
  * I/O state: file descriptors, network connnections, etc.  

* State "private" to each thread (all kept in TCB = Thread Control Block)    
  * CPU registers(program counter).  
  * Execution stack pointer.  

#### Multithread Programs
* Network Servers  
  * Concurrent requests from network: File Server, Web Server.  

## Pthread Functions

```c
int pthread_create(pthread_t *thread, const pthread_attr_t *attr,void *(*start_routine) (void *), void *arg);  
```
* Goal: Create a new thread to run func(args).  
  * First - pointer to a variable hold the id of the newly created thread.  
  * Second - pointer to attributes some of the advanced features of pthreads.  
  * Third - pointer to a function we want to run.  
  * Fourth - pointer given to our function.  

```c
int pthread_yield(void);
```
* Goal: Relinquish processor voluntarily. The thread is placed at the end of the run queue, and another thread is scheduled to run.    

```c
int pthread_join(pthread_t thread, void **retval);  
```
* Goal: Parent waits for the child thread to finish, clean up thread resources.      
  * Retval store exit status thread.    

```c
void pthread_exit(void *retval);
```
* Goal: Quit thread and clean up, wake up joiner if any.    
  * Always success.  

####     