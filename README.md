# JavaFX   
## CallBack   
•  **CallBack interface**,  bir işlemin tamamlanmasının ardından belirli bir kodun çalıştırılmasını sağlar. Belirli bir girdiyi alıp belirli bir çıktıyı döndüren fonksiyonel arayüzdür.
```java
public interface Calback<InputType, OutputType>{
  OutputType call(InputType param);
}   
```  
•  **call()**, her hücre için bir Cell nesnesi oluşturur ve geri döndürür.  public ListCell<String> call(ListView<String> listView) böümünde her hücre için ListCell<String> nesnesi oluşturur ve döndürür.     
•  **Synchronous Callback**;ana işlem tamamlanana kadar bekler sonra callback fonksiyonunu çağırır.CallBack fonksiyonu çağırılana kadar ana işleme devam edilmez ve işlem sırası bloklanır.    
•  **Asynchronous Callback**; ana işlem devam ederken başlatılır ve callback fonksiyonu işlemin tamamlanmasından sonra çağrılır. Ana işlem callback fonksiyonunun tamamlanmasını beklemez.   
•  **SetCellFactory()**, liste, tablo veya ağaç veri yapılarında hücrelerin nasıl görüntüleneceğini ve davranacağını özelliştirmek için kullanılır. ListView, TableColumn vs. öğesinin hjücrelerini özelleştirmek için setCellFactory, Callback interface'ini kullanır. Bötylece her ListCell, TableCell ... nesnesinin  nasıl oluşturulacağını ve güncelleneceğini tanımlar.
```java
listView.setCellFactory(new Callback<ListView<String>, ListCell<String>>(){
  @Override
  public ListCell<String> call(ListView<String> listView){
    return new ListCell<String>(){
      @Override
      protected void updateItem(String item, boolean empty){//Hücre içeriği burada güncellenir. item hücre içeriği, empty hücrenin boş olup olmadığını belirten boolean değer
        super.updateItem(item,empty);
        if(item!=null){
        ...
        } else {
        ...
        }
      }
    }
});
```
 
•  **ChangeListener**, bir ObservableValue içerisindeki değişiklikleri dinlemek ve bu değişikliklere tepki vermek için kullanılır. ObservableValue'aki değişikliği dinler ve changed metodunu uygular. Changed metodu dinlenen değerde bir değişiklik olduğunda otomatik olarak çağırılır.    
•  **BooleanProperty**, JavaFX kütüphanesindeki bir abstract classtır. Boolean tipinde bir değeri temsil eder ve binding, dinleyici eklem gibi özellikleri vardır. Abstract bir class olduğu için doğrudan kullanılamaz. Bunun yerine impleBooleanProperty gibi somut classları(concrete class) kullanır. 

•  **SimpleBooleanProperty**, JavaFX kütüphanesinde yer alan bir boolean değerini temsil eden ve yönetmek için kullanılan bir sınıftır. Bir checkbox'ın etkinlik durumunu , bir textfieldın içeriğinin boş olup olmadığını, bir ilerleme çubuğunun ilerleme durumunu takip etmek için ve veri bağlamak için(bind) kullanılabilir. Değer değişikliklerini dinleyen bir dinleyiciye sahiptir.    
```java
addListener(ChangeListener <? super Boolean> listener)
```
Dinleyiciyi kaldırmak için;  
```java
removeListener(ChangeListener <? super Boolean> listener)
``` 
Veri bağlamak için;   
```java
bind(Binding <? super Boolean> observable)
``` 
•  **Concrete Class(Somut Sınıf)**, doğrudan örneklenebilen yani new anahtar kelimesi kullanılarak bir instance'ının yani objesinin oluşturulabileceği anlamına gelir.  Bir obje yaratmak için constructor'a sahip olan ve doğrudan kullanılabilen bir sınıftır.   
•  **Abstract Class (Soyut Sınıf)**, doğrudan örneklenemezler yani new anahtar kelimesi ile bir obje oluşturulamaz. Bu sınıflar başka sınıflar tarafından genişletilebilir(extends edebilir) ve örneklenebilir.   
•  **Interface**, doğrudan örneklenemezler, bir arayüzü kullanabilmek için bir classın bu interface'i implement etmesi gerekir. Bir sınıf arayüzü implement ettiğinde arayüzde tanımlanan tüm metodları gerçekleştirmek zorundadır. Genellikle metod imzalarını içerirler ve metodların gerçekleştirilmesini somut classlara bırakırlar.  
```java
public interface Vehicle(){
  void startEngine();
}
public class Car implements Vehicle{
  @Override
  public void startEngine(){
    System.out.println("Engine started");
  }
}
public class Main(){
  public static void main(String[] args){
    Vehicle myCar=new Car();
    myCar.startEngine();
  }
}
```
•  **Inheritance**, nesne yönelimli programlamada bir sınıfın başka bir sınıfın özelliklerini ve davranışlarını devralmasıdır. Bu yeni bir class oluştururken mevcut bir sınıfın işlevselliğini yeniden kullanmayı ve genişletmeyi sağlar. Bu işlem **extends** anahtar kelimesi ile yapılır.
```java
public abstract class Animal {
  public abstract void makeSound();//abstract metod
  public void sleep(){//tamamlanmış metod
    System.out.println("Zzz...");
  }
}
public class Dog extends Animal{
  @Override
  public void makeSound(){//abstract metod gerçekleştiriyor
    System.out.println("Bark");
  }
}
public class Main(){
  public static void main(String[] args){
    Animal myDog = new Dog();
    myDog.makeSound();
    myDog.sleep();
  }
}
```
