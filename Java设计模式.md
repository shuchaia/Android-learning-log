## Java设计模式

## 单例模式

### 饿汉式单例模式

这种方式在类加载时就完成了实例化，避免了线程同步的问题。

```java
public class Singleton {
    private static Singleton instance = new Singleton();
    
    private Singleton() {}
    
    public static Singleton getInstance() {  
        return instance;  
    }
}
```



### 懒汉式单例模式

这种方式是在第一次调用`getInstance()`方法时才创建实例，**可能会有线程安全**的问题。

```java
public class Singleton {  
    private static Singleton instance;  
  
    private Singleton() {}  
  
    public static synchronized Singleton getInstance() {  
        if (instance == null) {  
            instance = new Singleton();  
        }  
        return instance;  
    }  
}
```



### 双检锁单例模式

这种方式通过在懒汉式单例模式的基础上，添加了双重检查，确保线程安全，并且提高了效率。

```java
public class Singleton {  
    private volatile static Singleton instance;  
  
    private Singleton() {}  
  
    public static Singleton getInstance() {  
        if (instance == null) {  
            synchronized (Singleton.class) {  
                if (instance == null) {  
                    instance = new Singleton();  
                }  
            }  
        }  
        return instance;  
    }  
}
```



### 静态内部类单例模式

这种方式利用了静态内部类的特性，在第一次加载Singleton类时不会初始化instance，而是在第一次调用`getInstance()`方法时才会加载`SingletonInstance`类，并初始化instance。

```java
public class Singleton {  
    private Singleton() {}  
  
    private static class SingletonInstance {  
        private static final Singleton INSTANCE = new Singleton();  
    }  
  
    public static Singleton getInstance() {  
        return SingletonInstance.INSTANCE;  
    }  
}
```



### 枚举单例模式

这种方式利用了枚举的特性，在第一次加载Singleton类时就会初始化instance，并且天然是线程安全的。

```java
public enum Singleton {  
    INSTANCE;  
}
```

