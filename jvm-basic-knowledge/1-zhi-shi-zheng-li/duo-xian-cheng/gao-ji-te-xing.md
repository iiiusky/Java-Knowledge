# 高级特性

## ThreadLocal

* **Do what?**
  * 代表线程局部变量，为每个线程创建副本。
  * ThreadLocal是解决线程安全问题一个很好的思路，它通过为每个线程提供一个独立的变量副本解决了变量并发访问的冲突问题。在很多情况下，ThreadLocal比直接使用synchronized同步机制解决线程安全问题更简单，更方便，且结果程序拥有更高的并发性。
* **Scope**
  * 例如三辆长途汽车售票52人 ，分别售票

    ```java
            ThreadLocal<Integer> bus = new ThreadLocal(){
                @Override
                protected Object initialValue(){
                    return new Integer(52);
                }
            };
            TicketWindow w1 = new TicketWindow("A车")
            TicketWindow w1 = new TicketWindow("B车")
            TicketWindow w1 = new TicketWindow("C车")
    ```
* **How to do?**
  * **更新Thread本地变量**`ThreadLocalMap`**从而达到线程副本的目的。**
  * **实现原理**

    ```java
        private T setInitialValue() {
            T value = initialValue();
            Thread t = Thread.currentThread();
            ThreadLocalMap map = getMap(t);
            if (map != null)
                map.set(this, value);
            else
                createMap(t, value);
            return value;
        }
    ```

     

## Semaphore 信号量

* Do what?
* Scope
  * 12
  * `new Semaphore(5,true);`

## CountDownLatch

* **Do what?**
  * 这个类能够使一个线程等待其他线程完成各自的工作后再执行。例如，应用程序的主线程希望在负责启动框架服务的线程已经启动所有的框架服务之后再执行。
* **How to do?**

  ```java
  new CountDownLatch(3);
  CountDownLatch.await()
  ```

* **Scope**
  * **实现最大的并行性** 类似 Semaphore 信号量
  * **开始执行前等待n个线程完成各自任务**：例如应用程序启动类要确保在处理用户请求前，所有N个外部系统已经启动和运行了。
  * **死锁检测：**一个非常方便的使用场景是，你可以使用n个线程访问共享资源，在每次测试阶段的线程数目是不同的，并尝试产生死锁。

