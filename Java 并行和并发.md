在 Java 和计算机科学中，并行（Parallelism） 和 并发（Concurrency） 是两个常见的概念，它们都与多任务处理相关，但有着显著的区别。

# 1. 概念区别

## 并行（Parallelism）
定义：指的是在同一时刻执行多个任务，通常依赖多核或多处理器硬件。
核心特征：真正的同时发生（Simultaneous Execution）。
场景：一个任务被拆分为多个子任务，这些子任务可以同时运行。
硬件依赖：需要多核 CPU 或多台计算机来实现。

## 并发（Concurrency）
定义：指的是在同一时间段内管理和执行多个任务，这些任务看起来像是同时进行，但实际上可能是交替执行。
核心特征：任务之间快速切换（Switching）。
场景：多个任务在逻辑上是同时进行的，但在底层实现中可能并不是同时运行，而是通过线程调度实现的。

# 2. 举例说明

## 并行（Parallelism）
例如：

有一台双核 CPU，同时处理两个任务。
如果任务 A 和任务 B 被拆分为子任务 A1、A2 和 B1、B2，可以在两个核心上分别执行 A1 和 B1。
程序代码示例：

```java

// 使用并行流进行计算（依赖多核 CPU）
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8);
numbers.parallelStream()
       .map(n -> n * 2)
       .forEach(System.out::println);
```

## 并发（Concurrency）
例如：

在一个单核 CPU 上运行两个任务，通过线程的快速切换来实现任务的交替执行。
一个线程处理任务 A 的一部分，切换到另一个线程处理任务 B 的一部分。
程序代码示例：

``` java
public class ConcurrencyExample {
    public static void main(String[] args) {
        Thread task1 = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                System.out.println("Task 1 - " + i);
            }
        });

        Thread task2 = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                System.out.println("Task 2 - " + i);
            }
        });

        task1.start();
        task2.start();
    }
}
运行结果中 Task 1 和 Task 2 的输出可能是交替的，取决于线程调度。
```
# 3. 并发和并行的核心区别

![Alt Text](https://github.com/yangdanfeng115/JavaStudy/blob/main/images/%E5%B9%B6%E5%8F%91%E4%B8%8E%E5%B9%B6%E8%A1%8C.png)

# 4. Java 中的并发与并行

Java 提供了多种工具和框架支持并发和并行编程：

## 并发工具（Concurrency）

线程：Java 的基础并发单元，通过 Thread 类或实现 Runnable 接口创建线程。
线程池：ExecutorService 提供了线程池管理功能，避免了频繁创建和销毁线程的开销。
并发包（java.util.concurrent）：提供线程安全的数据结构（如 ConcurrentHashMap）、同步工具（如 Semaphore）和高级并发任务管理（如 ForkJoinPool）。
示例：

```java

ExecutorService executor = Executors.newFixedThreadPool(2);
executor.submit(() -> System.out.println("Task 1"));
executor.submit(() -> System.out.println("Task 2"));
executor.shutdown();
```
## 并行工具（Parallelism）

### 并行流（Parallel Streams）：
Java 8 引入的流（Stream）框架，提供了简单的并行处理接口。

```java

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
numbers.parallelStream().forEach(System.out::println);
```
### Fork/Join 框架：
用于并行任务拆分，将一个任务分解为多个子任务，运行在不同线程上，最后合并结果。

```java

ForkJoinPool pool = new ForkJoinPool();
pool.invoke(new RecursiveTaskExample());
```
# 5. 关系与应用场景

## 并发是广义的，包含并行：

并发是“看起来像同时运行”，并行是“真正同时运行”。
所有并行程序都是并发的，但并发程序不一定是并行的。

## 应用场景：

并发：适合需要快速响应的任务，例如服务器处理多个客户端的请求。
并行：适合需要分解和计算的密集型任务，例如矩阵乘法、大数据处理。

# 总结
## 并发：主要关注如何处理多个任务的交替执行，逻辑上“同时”运行。
## 并行：主要关注如何拆分任务并同时在多个处理器或核上执行，物理上“同时”运行。

在 Java 中，选择并发还是并行，取决于任务的需求和硬件的能力。
