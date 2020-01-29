---
title: java_sychronized
date: 2019-08-16 21:47:24
tags: java
---
# sychronized 基本使用
## 1. 修饰普通方法
```java
class Main {
    public synchronized void method1() {
        System.out.println("Method 1 start");
        try {
            System.out.println("Method 1 execute");
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("Method 1 end");
    }

    public synchronized void method2(){
        System.out.println("Method 2 start");
        try {
            System.out.println("Method 2 execute");
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("Method 2 end");
    }

    public static void main(String[] args) {
        final Main test = new Main();
        new Thread(() -> test.method1()).start();
        new Thread(() -> test.method2()).start();
    }
}
```
#### 结果
method1执行并退出后才执行method2
#### 说明
通过同一个对象去调用上了同步锁的不同方法时,这些方法会竞争同一个对象上的锁,造成互斥,故只能顺序执行

## 2. 修饰静态方法
同一个类的不同实例调用上了同步锁的不同*静态*方法

## 3. 修饰代码块
在执行的代码块前加上*sychronize(this)*, 同修饰普通方法

也可以sychronize(object) 锁住其它对象, 这是修饰代码块与修饰方法的一大不同
