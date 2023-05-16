# JUC 常识  

## 基本概念  

* JUC：java.util.concurrent  
  * java.util.concurrent.atomic  
  * java.util.concurrent.locks    
* 线程  
  * Thread  
  * Runable  
  * Callable  
    * call 方法返回值  

## 锁的原理  

* Lock VS synchronized  
  * synchronized 原理  
    * monitor作为计数器，
    * monitor -> mutex -> atomic_long -> CAS(compare and set, 指令集CMPXCHG)

* 锁的应用
  * CurrentHashMap
    * 分段加锁，提高可用性
