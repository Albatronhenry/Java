### [sleep()、wait()、yield()、join()方法 解析](http://blog.csdn.net/yangyan19870319/article/details/6205312)
*   1.sleep()方法

　　在指定时间内让当前正在执行的线程暂停执行，但不会释放“锁标志”。不推荐使用。
  
　　sleep()使当前线程进入阻塞状态，在指定时间内不会执行。
  
*   2.wait()方法
  
　　在其他线程调用对象的notify或notifyAll方法前，导致当前线程等待。线程会释放掉它所占有的“锁标志”，从而使别的线程有机会抢占该锁。
  
　　当前线程必须拥有当前对象锁。如果当前线程不是此锁的拥有者，会抛出IllegalMonitorStateException异常。
  
　　唤醒当前对象锁的等待线程使用notify或notifyAll方法，也必须拥有相同的对象锁，否则也会抛出IllegalMonitorStateException异常。
  
　　waite()和notify()必须在synchronized函数或synchronized　block中进行调用。如果在non-synchronized函数或non-synchronized　block中进行调用，
  虽然能编译通       过，但在运行时会发生IllegalMonitorStateException的异常。

  
*   3.yield方法
  
　　暂停当前正在执行的线程对象。
  
　　yield()只是使当前线程重新回到可执行状态，所以执行yield()的线程有可能在进入到可执行状态后马上又被执行。
  
　　yield()只能使同优先级或更高优先级的线程有执行的机会。
  
*   4.join方法
  
　　等待该线程终止。
  
　　等待调用join方法的线程结束，再继续执行。如：t.join();//主要用于等待t线程运行结束，若无此句，main则会执行完毕，导致结果不可预测。

   比较重要的几点需要注意：
   
         1 sleep和yield的区别在于, sleep可以使优先级低的线程得到执行的机会,  而yield只能使同优先级的线程有执行的机会.
         
         2 interrupt方法不会中断一个正在运行的线程.就是指线程如果正在运行的过程中, 去调用此方法是没有任何反应的. 为什么呢, 因为这个方法只是提供给 
被阻塞的线程, 即当线程调用了.Object.wait, Thread.join, Thread.sleep三种方法之一的时候, 再调用interrupt方法, 才可以中断刚才的阻塞而继续去执行线程.

         3 join()  当join(0)时等待一个线程执行直到它死亡返回主线程,  当join(1000)时主线程等待一个线程1000纳秒,后回到主线程继续执行.

         4 waite()和notify()必须在synchronized函数或synchronized　block中进行调用。如果在non-synchronized函数或non-synchronized　block中进行调用，
虽然能编译通过，但在运行时会发生IllegalMonitorStateException的异常。

------------

notify&notify补充
------------

当一个线程进入wait之后，就必须等其他线程notify/notifyall,使用notifyall，可以唤醒

所有处于wait状态的线程，使其重新进入锁的争夺队列中，而notify只能唤醒一个。注意,任何时候只有一个线程可以获得锁，也就是说只有一个线程可以运行

synchronized 中的代码，notifyall只是让处于wait的线程重新拥有锁的争夺权，但是只会有一个获得锁并执行。

#### [notify只会通知一个在等待的对象，而notifyAll会通知所有在等待的对象，并且所有对象都会继续运行](http://www.jb51.net/article/92473.htm)

#### ]notify用得不好容易导致死锁,大部分情况还是是用notifyall](http://www.jb51.net/article/36657.htm)
