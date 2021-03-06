# Thread Pool

## CachedThreadPool

* 默认 最大 `Interger. MAX_VALUE` 线程数的线程池
* `ExecutorService service = Executors.newCachedThreadPool()`

## FixedThreadPool

* 定长线程池，最优数量：`Runtime.getRuntime().availableProcessors()`
* 不会释放线程
*  `ExecutorService service Executors.newFixedThreadPool(10);`

## SingleThreadPool

* 同时只有一个线程运行，可以按照指定顺序\(FIFO, LIFO, 优先级\)执行
*  `ExecutorService service = Executors.newSingleThreadExecutor();`  

## ScheduleThreadPool

* 定时执行线程池
* `ExecutorService service = Executors.newScheduledThreadPool(10);` 

## WorkStealingPool

* Fork/Join

  ```java
      public static void main(String[] args) throws IOException {
          // 根据cpu是几核来开启几个线程
          ExecutorService service = Executors.newWorkStealingPool();
          // 查看当前计算机是几核
          System.out.println(Runtime.getRuntime().availableProcessors());
          service.execute(new R(1000));
          service.execute(new R(2000));
          service.execute(new R(3000));
          service.execute(new R(1000));
          service.execute(new R(2000));

          // WorkStealing是精灵线程(守护线程、后台线程)，主线程不阻塞，看不到输出。
          // 虚拟机不停止，守护线程不停止
          System.in.read();
      }

      static class R implements Runnable {
          int time;

          public R(int time) {
              this.time = time;
          }

          @Override
          public void run() {
              try {
                  TimeUnit.MILLISECONDS.sleep(time);
              } catch (InterruptedException e) {
                  e.printStackTrace();
              }
              System.out.println(time + ":" + Thread.currentThread().getName());
          }
      }
  1000:ForkJoinPool-1-worker-1
  1000:ForkJoinPool-1-worker-4
  2000:ForkJoinPool-1-worker-2
  2000:ForkJoinPool-1-worker-5
  3000:ForkJoinPool-1-worker-3
  ```

