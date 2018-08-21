单例模式


双重检查（double-check）

终极版
```
//懒汉式终极版
public static Singleton(){
//一个静态实例
private static volatile Singleton singleton;
//一个私有的构造函数
private Singleton(){}
//公有的静态方法，返回静态实例
public static Singleton getInstance(){
  if(singleton==null){
    Synchronized(Singleton.class){
        if(singleton==null){
            singleton = new Singleton();
        }
    }
  }

}
  return singleton;
}


```
