
工厂模式

---
> 定义：
>>  工厂方法(Factory Method)模式的意义是定义一个创建产品对象的工厂接口，将实际创建工作推迟到子类当中。核心工厂类不再负责产品的创建，这样核心类成为一个抽象工厂角色，仅负责具体工厂子类必须实现的接口，这样进一步抽象化的好处是使得工厂方法模式可以使系统在不修改具体工厂角色的情况下引进新的产品。



说明：
定义一个创建对象的接口，让其子类自行决定实现哪个工厂类，工厂模式使其创建过程延申到子类进行；

应用实例
- hibernate切换数据库，只需切换驱动和方言即可；
- 


`工厂模式简单代码示例`
1. 产品的接口
```
public interface IProduct{
    public void method();
}

```
2. 两个具体的产品
```
public class ProductA implements IProduct{

    public void method() {
        System.out.println("产品A方法");
    }

}

```

```
public class ProductB implements IProduct{

    public void method() {
        System.out.println("产品B方法");
    }

}

```

3. 工厂类
```
public class Creator {

    private Creator(){}
    
    public static IProduct createProduct(String productName){
        if (productName == null) {
            return null;
        }
        if (productName.equals("A")) {
            return new ProductA();
        }else if (productName.equals("B")) {
            return new ProductB();
        }else {
            return null;
        }
    }
}

```

4. 测试类
```
public class Client {

    public static void main(String[] args) {
        IProduct product1 = Creator.createProduct("A");
        product1.method();
        
        IProduct product2 = Creator.createProduct("B");
        product2.method();
    }
}

```



`常用的工厂模式是静态工厂，利用static方法，一般情况工厂类不需要实例化；`

```


interface food{}

class A implements food{}
class B implements food{}
class C implements food{}

public class StaticFactory {

    private StaticFactory(){}
    
    public static food getA(){  return new A(); }
    public static food getB(){  return new B(); }
    public static food getC(){  return new C(); }
}

class Client{
    //客户端代码只需要将相应的参数传入即可得到对象
    //用户不需要了解工厂类内部的逻辑。
    public void get(String name){
        food x = null ;
        if ( name.equals("A")) {
            x = StaticFactory.getA();
        }else if ( name.equals("B")){
            x = StaticFactory.getB();
        }else {
            x = StaticFactory.getC();
        }
    }
}


```



