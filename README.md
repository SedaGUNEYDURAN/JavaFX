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
      protected void updateItem(String item, boolean empty){//Hücre içeriği burada güncellenir.
                                                            //item hücre içeriği, empty hücrenin boş olup
                                                            //olmadığını belirten boolean değer
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
•  **Abstract Class (Soyut Sınıf)**, doğrudan örneklenemezler yani new anahtar kelimesi ile bir obje oluşturulamaz. Bu sınıflar başka sınıflar tarafından genişletilebilir(extends edebilir) ve örneklenebilir. Bir class'a sadece bir abstract inherit edilebilir. Static metodlar abstract olarak tanımlanamaz.  
•  **Interface**, doğrudan örneklenemezler, bir arayüzü kullanabilmek için bir classın bu interface'i implement etmesi gerekir. Bir sınıf arayüzü implement ettiğinde arayüzde tanımlanan ve  kullanılacak olan tüm metodları gerçekleştirmek zorundadır yani gereksinimlerine göre metodu doldurmalıdır. Genellikle metod imzalarını içerirler ve metodların gerçekleştirilmesini somut classlara bırakırlar.  Java 8 ile birlikte, interfacelerde default metodlar ve static metodlar tanıtıldı.Bu metodlar, interfacelerin metodları nasıl gerçekleştireceğine dair bilgi verir. 
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
>Metod İmzası: 3 bileşeni içerir; metod adı, dönüş tipi, parametre listesi.
>```java
>public class Example{
>  //bu metodun imzası: void greet(String name)
>  public void greet(String name){
>    System.out.println("Hello,"+name);
>}
>```
      •  Interface'ler classların implement etmesi gereken method signaturlarını ve canstant değerlerini tanımalmak için kullanlır. 
      Yani interfacedeki değişpkenler her zaman "public static final" olarak tanımlanır ve başka türde değişkenler kullanılamaz.   
```java   
      public interface MyInterface{
      int value1=5; //kısaca yazmak istersek bu şekilde yazabiliriz ancak public static final int value1=5 olarak kabul edilir
      public static final int value2=10; // iki versiyonda aynı anlama gelir ce derleyici tarafından aynı şekilde işlenir. 
      }
 ```
>public, değişkenlerin interface'i implement eden tüm sınıflar tarafından erişilebilir olduğu anlamına gelir.
>static, değişkenlerin classın bir instance'ına bağlı olmadığını, dolayısıyla interface'in kendisine ait olduğunu ifade ederler.
>final, değişkenin değerinin sadece bir kez atanabileceğini ve sonra değiştirilemeyeceğini ifade eder.   

     •  Bir class'a birden fazla interface implement edilebilir.
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
•  **super()**, bir classın subclassında(alt classından) constructorında, superclassının(üst classının) constructorını çağırmak için kullanılır.
```java
class Animal{
  Animal(){
    System.out.println("Animal constructor called");
  }
}
class Dog extends Animal(){
  Dog(){
    super();
    System.out.println("Dog constructor called");
  }
}
public class Main(){
  public static void main(String[] args){
    Dog dog=new Dog();
  }
}
```
>Çıktı;   
>Animal constructor called   
>Dog constructor called


•  **Software Development Life Cycle(SDLC)**: Yazılım projelerinin yönetimi ve geliştirilmesi için kullanılan, yapılandırılmış ve sistematik bir süreçtir.Temel aşamaları; planlama,gereksinim analizi, tasarım, geliştirme, test, dağıtım, bakım. Farklı projeler ve farklı gereksinimler için farklı SDLC modelleri bulunur;
>**Waterfall(Şelale) Modeli**; aşamaların sırasıyla ve birbirini takip ederek ilerlediği, geri dönüşün zor oldu modeldir.  
>**Agile(Çevik) Modeli**; esnek ve iteraktif bir yaklaşımla, sürekli geri bildirim ve iyileştirme sağlayan modeldir.  
>**Spiral Modeli**; risk analizi ve protiplemeye odaklanan, iteraktif ve döngüsel bir yaklaşımdır.  
>**V modeli**; test faaliyetlerinin geliştirme faaliyetleriyle paralel olarak yürütüldüğü modeldir.

•  **Plastik Software Configuration Management**, bir yazılım konfigürasyon yönetim aracıdır(Git, SVN gibi düşün ). Dağıtık(distributed) ve merkezi(centralized) sürüm kontrol sistemlerinin avantajlarını birleştirerek yüksek performanslı ve ölçeklenebilir bir çözüm sunar.Conflictleri tespit eder ve çözer.   
•  **Asana**, ekiplerin projelerini ve görevlerini planmasına, izlemesine ve yönetmesine yardımcı olan bir proje yönetim yazılımıdır(Jira gibi).  
•  **DOORS(Dynamic Object-Oriented Requirements System)**, gereksinim yönetimi için güçlü ve kapsamlı bir çözümdür. Gereksinimlerin toplanması, izlenmesi, değişiklik yönetimi ve işbirliği gibi kritik süreçlerde etkinlik sağlar.   
•  Neden veri yapıları kullanırız? Veri yapıları bilgisayar bilimlerinin temellerini oluşturur. Verinin etkin bir şekilde yönetilmesini, işlenmesini ve analiz edilmesi için önemlidir. Yazılım geliştiriciler doğru veri yapılarını kullanrak uygulamaların performansını ve verimliliğini arttırabilir.    
•  **Stack**, LIFO(Last In, First Out) prensibi ile çalışır.Dizi ve linked list mantığın ile oluşturulabilirler.Stack işlemleri;     
 > Push: stack'e eleman ekleme işlemi yapar, yeni eklenen eleman top olur.  
 > Pop: stack'ten eleman çıkarır, top elemanı çıkarır.  
 > Peek: kullanıcıya veri ödndürür, top elemanını döndürür.

•  **Queues**, FIFO(First In, First Out) prensibi ile çalışır. poll() metodu kuyruktaki en alttaki öğeyi yani en önce giren ögeyi döndürür ve sile. Kuyruk boş olduğunda bir exception fırlatmaz, null değeri döndürür.    
•  **HashMap**, Key-Value çiftlerini hızlıca aramak için kullanılır. Her key'e karşılık gelen bir değer bulunur. Anahtar unique'tir, bir değer birden fazla olabilir. Elemanları ekleme sorasına göre depolamaz. 
•  **Linked HashMap**, gönderilen değerler ekleme sırasına göre eklenir.   
•  **TreeMap**, gönderilen değerler keylerine göre küçükten büyüğe doğru sıralanarak depolanır.   
•  **Concurrent HashMap**, birden fazla thread herhangi bir bir komplikasyon olmadan tek bir nesne üzerinde çalışabilir. Bir anahtar veya değer olarak boş nesneler eklemek mümkün değildir. ConcurrentHashMap nesnesini kitlemeden bir okuma işlemi için herhangi bir sayıda thread uygulanabilir. Ancak obje güncellemek için thread'in, thread'in çalışmak istediği belirli segmenti kitlemesi gerekir. Bu tür locking mekanizmasına "segment lockig"  or "bucket locking" denir. ConcurrentHashMap nesnesi, concurrency levela göre bir dizi segmente bölünür. Varsayılan concurrency level'ı 16'dır. Bu nedenle bir seferde 16 update işlemi threadler tarafından gerçekleştirilir. 
>Concurrency Level; eşzamanlı olarak mapi güncelleyen thread sayısı.  

•  **Binary Search Tree(İkili Arama Ağacı)**, ilk önce kök düğüm oluşturulur. Sadece sağ ve sol çocuklar eklenir. Sol çocuklar daima parenttan küçük olmalıdır. Sağ çocuklar parent'tan büyük olmalıdır. Her eklenen düğüm leaf durumundadır(leaflerin çocuğu olmaz). Arama yapıldığında karşılaştırılmaya roottan başlanır. Karmaşıklığı Big O(logn). Delete ve insert işlemlerinin maaliyetleri yüksektir. Denge sorunu vardır.     
•  **Heap**, binary tree üzerine kuruludur. Full complete tree doldurma yapmaktır amaç(yukarıdan aşağıya, soldan sağa doldurma işlemi yapılır.). İki türü vardır;
>Max heap: parent düğümü child düğümünden büyük ya da eşit olmalıdır.   
>Min heap ; parent düğümü child düğümünden küçük ya da eşit olmalıdır.
 
•  **Linked List**, Saklanan veriler kendisinden sonra gelen veriyi işaret etmek zorundadır. Her düğüm 2 değer tutar: içinde tutacağı değer ve sonraki düğümü gösteren pointer-referans değer. Dinamik bir yapısı vardır, istediğimiz kadar eleman ekleyebiliriz. Eleman ekleme ve silme işlemleri kolaydır. Random erişim yoktur, baştan başlamak zorundayız.Array List ile karşılaştırdığımızda eleman eklemek istediğimizde Array List'in performansı Linked List'e göre kötüdür çünkü elemanlarının hepsi yer değiştirmek zorunda kalır(2. indexle 3. index, 3.indexle 4. index gibi ..). Linked List eleman eklemek istediğimizde sadece iki tane objenin yerini değiştiririz.Hafıza bakımından karşılaştırdığımızda Linked List daha fazla yer kaplar;pointer tuttuğu için ekstra hafıza tutar. Üç çeşittir:
> Tek yönlü bağlı listeler(singly linked list): Son düğümün pointerı NULL.  
> Dairesel bağlı liste(Circular linked list): son düğüm ilk düğümün pointerını tutar.  
> Çift yönlü bağlı listeler(Doubly linked list ): Sonraki ve önceki elemanın olmak üzere iki pointer tutar.

•  Bir queue'yu sadece stack yapısı kullanarak nasıl çalıştırabiliriz? İki stack ile bunu sağlayabiliriz. Birinci stack eklemek için ikinci stack çıkarmak için kullanılır.  
 ```java
public class QueueUsingStacks<T>{
  private Stack<T> stack1;
  private Stack<T> stack2;
  public QueueUsingStacks(){
    stack1=new Stack<>();
    stack2=new Stack<>();
  }
  public void enqueue(T item){
    stack1.push(item);
  }
  public T dequeue(){
    if(stack2.isEmpty()){
      if(stack1.isEmpty()){
        throw new RuntimeException("Queue is empty");
      }
      while(!stack1.isEmpty()){
        stack2.push(stack1.pop());
      }
    }
    return stack2.pop();
  }
  public boolean isEmpty(){
    return stack1.isEmpty()&&stack2.isEmpty(); 
  }
  public T peek(){
    if(stack2.isEmpty()){
      if(stack1.isEmpty()){
        throw new RuntimeException("Queue is empty");
      }
      while(!stack1.isEmpty()){
        stack2.push(stack1.pop());
      }
    }
    return stack2.peek();
  }
}
```
•  **Algoritma Complexity**: Bir algoritmanın performansını, ölçmek için kullanılan kavramdır. Algoritmanın performansı ne kadar hızlı çalıştığına, ne kadar kaynak yani bellek, zaman tükettiğine bakılarak hesaplanır.Asimptotik olarak Big-O notasyonu ile ifade edilir.

      •  O(1): sabit zamanlıdır. Giriş verisinin büyüklüğünden bağımsızdır.  
         O(n): doğrusal zamanlıdır. Giriş verisinin büyüklüğü ile doğru orantılıdır.   
         O(n^2): kare zamanlıdır.Giriş verisinin büyüklüğünün karesi ile orantılıdır.  
         O(logn): logaritmik zamanlıdır. Giriş verisinin büyüklüğünün logaritması ile orantılıdır.   
      •  İki türü vardır;  
      
           •  Time Complexity: algoritmanın çalışmasını tamamlamak için ihtiyaç duyduğu süredir.    
           •  Space Coplexity: algortimanın çalışması sırasında ihtiyaç duyduğu bellek miktarıdır.     
•  **Process**; word, excel veya herhangi başka bir uygulama henüz çalışmıyorken bir programdır. Programlar çalıştırıldığında process olarak nitelendirilir. Process'ler hayatlarına tek bir thread ile başlarve bu thread'e main thread denilir. Diğer threadler ise programın çalışma esnasında sistem fonksiyonları tarafından yaratılmaktadır.  
•  **Heap**; Java projeleri processe dönüştükleri zaman kendi memory space'ini yani heapini oluşturur.  
•  **Multitasking**; bilgisayarın bir çok processi aynı anda çalıştırmasıdır.Örneğin web browser'ı çalıştırırken aynı anda spotifyın da açık olması.     
•  **Thread**; bir processin birden fazla işi aynı anda yapmasını sağlayan yapılara thread denir. Bir process bünyesinde bir ya da birden fazla thread barındırabilir.    Thread'ler aynı anda sadece tek bir işi yapabilir. Threadler processin içinde oluştuğu için processlerin olşturduğu bellek alanına direkt olarak erişim sağlayabilirler ve her threadin sadece kendisiniğn erişebileceği bir tane "thread stack"i bulunur.Threadler,in çalışma sırası jvm ve işletim sistemine bağlıdır.
> "Synchronized" anahtar kelimesini yazdığımızda o obje üstünden, o class üzerinden sadece tek bir anahtara(lock) sahip oluruz. Threatler anahtarla metoda giriyor gibi düşün ve anahtara da lock de. İki tane anahtar oluşturmak istediğinde
 ```java
public synchronized void metod1(){
  metod içeriği
}
 ```
yerine 
 ```java
public void metod1(){
 synchronized(lock1){
    metod içeriği
}
  
}
 ```
•  **Paralel programlama**; threadlerin çok çekirdekli işlemcilerde farklı çekirdeklerde eşzamanlı olarak çalıştırılmasıdır.    
•  **Multithread**;bir process içinde bir çok thread oluşturup bir çok işi bir arada yapmaktadır.Wordde yazı yazarken aynı anda kelimelerin sayılması gibi   
•  **Concurency(eşzamanlılık)**; bir çok işimizi threadler yardımıyla paralel olarak yapabiliriz. Threadlerin paralel olarak çalışmasına concurency denir.  
•  **Deadlock**; iki ya da daha fazla processin devam etmek için birbirlerinin bitmesini beklemesi ve sonuçta ikisinin de devam edememesi durumudur.   
•  **Semafor**;Birden fazla processin eş zamanlı çalışması durumunda birbirleri için risk teşkil ettikleri kritik zamanlarda birbirlerini beklemesini sağlayan mekanizmadır.  
•  **Mutex**;  
•  **Cache**;  
•  **Memory Leak**;  
•  **Polimorfizm**;  
•  **  
•  Library nedir?  
•  UML Dokümantasyonu;  
  
  




