### [Immutable empty collections and iterators](https://www.javaworld.com/article/3103442/immutable-empty-collections-and-iterators.html)
文章讲述了java的Collections类中为什么要有空集合、空迭代器的方法。空集合返回的是不能修改的集合(因为没有覆盖父类add()等操作集合的方法)。  
#### 1.空集合应用举例
试想如果下面无参数构造器没有返回一个空的List，那main中调用println会抛出NullPointerException，因为私有全局变量尚未初始化。可直接使用Collections.emptyList()  
返回一个空的不可变集合。
```
class Flowers
{
   private List<String> flowers;

   Flowers()
   {
      flowers = Collections.emptyList();//返回空的List
   }

   Flowers(String... flowerNames)
   {
      flowers = new ArrayList<String>();
      for (String flowerName: flowerNames)
         flowers.add(flowerName);
   }

   @Override
   public String toString()
   {
      return flowers.toString();
   }
}

public class EmptyListDemo
{
   public static void main(String[] args)
   {
      Flowers flowers = new Flowers();
      System.out.println(flowers);
      flowers = new Flowers("Rose", "Violet", "Marigold");
      System.out.println(flowers);
   }
}
```
#### 2.空迭代器应用举例
下面代码②处将抛出NullPointerException，因为ToDoList类中的todoList并未初始化
```
class ToDo
{
   private String task;
   private String date;

   ToDo(String task, String date)
   {
      this.task = task;
      this.date = date;
   }

   @Override
   public String toString()
   {
      return task + ": "+ date;
   }
}

class ToDoList
{
   private List<ToDo> todoList;

   void add(ToDo todo)
   {
      if (todoList == null)
         todoList = new ArrayList<>();
      todoList.add(todo);
   }

   public Iterator<ToDo> iterator()
   {
      return todoList.iterator();
   }
}

public class EmptyIteratorDemo
{
   public static void main(String[] args)
   {
      ToDoList todoList = new ToDoList();
      //todoList.add(new ToDo("Mow the lawn", "April 5, 10 AM"));//①
      Iterator<ToDo> todos = todoList.iterator();//②
      while (todos.hasNext())
         System.out.println(todos.next());
   }
}
```
可以借助Collections.emptyIterator()，将iterator()方法改成如下：
```
public Iterator<ToDo> iterator()
{
   return (todoList != null) ? todoList.iterator() 
                             : Collections.emptyIterator();
}
```
上面的例子中更好的方法是用我们常用的new ArrayList()来赋值,就不需要emptyIterator()了。某些时候可能还是需要使用 emptyIterator()，具体应根据场景确定。
#### 3.总结
Collections类中的empty..方法可以帮助你构建安全的代码，避免抛出NullPointerExceptions。还能让你减少判空。比如上面空集合的例子中，toString()方法直接  
定义了```return flowers.toString();``` 而不是```return (flowers != null) ? flowers.toString() : ""```;   
具体使用应根据场景确定
