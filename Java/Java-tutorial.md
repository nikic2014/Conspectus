# Учебник по Python

## Оглавление
1. [Roadmap](#road-map)
1. [Введение в Java](#introduction-to-Java)
    1. [База](#base)
    1. [Классы](#classes)
    1. [Аннотации](#annotation)
    1. [Исключения](#exeption)
    1. [Generics](#generics)
    1. [Optional](#optional)
    1. [Streams](#streams)
1. [Логирование](#logging)
1. [Docker: приложение в коробке]()
1. [Оптимизация и мониторинг docker-образов. DockerHub]()
1. [Факты](#facts)
1. [Полезные ресурсы](#res)
1. [Проекты](#project)

# Roadmap <a name="road-map"></a>

![Изображение](Road-map.png)


# Введение в Java  <a name="introduction-to-Java"></a>

Java - строго типизированный объектно-ориентированный язык программирования
общего назначения, разработанный компанией Sun Microsystems (в последующем
приобретённой компанией Oracle). Разработка ведётся сообществом, организованным
через Java Community Process; язык и основные реализующие его технологии
распространяются по лицензии GPL. Права на торговую марку принадлежат корпорации
Oracle.

Приложения Java обычно транслируются в специальный байт-код, поэтому они могут
работать на любой компьютерной архитектуре, для которой существует реализация
виртуальной Java-машины.

## База <a name="base"></a>

Для того чтобы считать информацию используется класс **Scanner**:

~~~
import java.util.Scanner;

Scanner scan = new Scanner(System.in);
a = scan.nextInt();

System.out.println("A:" + a);
~~~

**Типы данных:** 
1) целые числа (byte, short, int, long);
2) числа с плавающей точкой (float, double);
3) логический (boolean);
4) символьный (char).


**Логические операции:**
1) ! — оператор отрицания;
2) && — оператор логическое И (сокращенный);
3) || — оператор логическое ИЛИ (сокращенный);
4) & — оператор побитовое И;
5) | — оператор побитовое ИЛИ;
6) ^ — оператор побитовое исключающее ИЛИ.


**Условные конструкции:** if: 
~~~
if (5<3) {
   System.out.println(5);
}
else {
   System.out.println(3);
}
~~~

**Тернарный оператор:**
~~~
(a >= 18) ? a : 18;
~~~

**swich:**

Для его использования объекты должны быть константами.
~~~
int a1 = 1;
final int a2 = 2;
final int a3 = 1;

switch (a1) {
   case a2:
         System.out.printf("Hello and welcome!\n");
         break;
   case a3:
         System.out.printf("Hello!\n");
         break;
}
~~~

**Циклы:**

~~~
for (int i = 1; i < 9; i++) {
	// тело цикла
    System.out.printf("Квадрат числа %d равен %d \n", i, i * i);
}


int j = 1;
do { // начинаем цикл
   System.out.printf("Квадрат числа %d равен %d \n", i, i * i);
   j++;
}
while (j < 9); // проверяем условие цикла


while (k < 10){
	System.out.printf("Квадрат числа %d равен %d \n", k, k * k);
   k++;
}
~~~

**Массивы**

Одномерные массивы:
~~~
int[] a = new int[5] {1, 2, 3, 4, 5}
~~~

Двумерные массивы:
~~~
int[][] a = new int[2][2] {{1, 2}, {1, 3}};
~~~

**Коллекции**

![Изображение](collection.png)

Пример использования:

~~~
import java.utils.ArrayList;

ArrayList<Integer> b = new ArrayList<>();
b.add(5);
b.add(2);
System.out.println(b.get(0));

for(Integer i : b){
   System.out.println(i);
}
~~~

**Функции** 

Тк в java все является классами, то нет как таковых функций вне классов, есть
только методы.

Пример:
~~~
public static int test() {
   return 5;
}
~~~

## Классы <a name="classes"></a>

**Модификаторы доступа**
- public - данный класс, поле или метод доступен из других классво или методов.

- protected - данная сущность будет доступна только внутри данного класса или
  класса наследника.

- private - данная сущность будет видна / доступна только внутри данного класса.

Пример создания классов и наследования:
~~~
public class Test_class {
    public int a;
    public int b;

    protected int z = 1212;
    public Test_class(int a, int b){
        this.a = a;
        this.b = b;
    }
}

public class Test_chaild extends Test_class {
    public int c;

    public Test_chaild(int a, int b, int c) {
        super(a, b);
        this.c = c;
    }
}


public class Test_chaild_chaild extends Test_chaild {
    public Test_chaild_chaild(int a, int b, int c) {
        super(a, b, c);
        System.out.println(this.z);
    }
}
~~~

Чтобы переписать метод другого класса используется аннотация @Override, а чтобы
вызвать такой же метод у родителя supet.method():

~~~
public class Test_chaild extends Test_class {
    public int c;

    public Test_chaild(int a, int b, int c) {
        super(a, b);
        this.c = c;
    }
    public void test() {
        System.out.println("test_child");
    }
}

public class Test_chaild_chaild extends Test_chaild {
    public Test_chaild_chaild(int a, int b, int c) {
        super(a, b, c);
        System.out.println(this.z);
    }
    @Override
    public void test() {
        super.test();
        System.out.println("test_child_child");
    }
}
~~~

**Абстрактные классы**

Абстрактные классы - классы объекты, которых никогда не будут создаваться, те
они нужны для того, чтобы на их основе написать потомков. 

Такая же концепция используется и для абстрактных методов. Если мы в классе
потомке не реализуем данный метод, то у нас появится ошибка.

Чтобы сделать класс абстрактным нужно написать:

~~~
public abstract class Test_class {
    public int a;
    
    public Test_class(int a){
        this.a = a;
    }

    public abstract test(int a);
}
~~~

**Вложенные классы**

Вложенный класс ничем не отличается от обычного, за исключеним того, что
находится внутри другого класса.

~~~
public  class Test_class {
    public int a = 5;

    public Test_in_test{
        public int b = 3;
    }
}
~~~

**Анонимные классы**

Анонимные классы - это классы, которые будут созданы всего один раз, поэтому
создавать для них объект - нет смылса. 

Допустим у нас есть класс Car, и мы хотим сделать объект fly Car.
~~~
Car flyCar = new Car(...) { 
   @0verride
   public void move0bject(float speed) {
      super.move0bject(speed);
      System.out.println("Машина летит");
   }
};
~~~

**Static** Статичные поля или методы - это такие поля или методы, которые не
принадлежат конкретной сущности, а являются общими для всего класса.

Внутри статичных методов можно работать только со статичными полями и методами.
~~~

public class Test {
   public static a;
}

Test new_test = new Test();
new_test.a = 5; // error

Test.a = 5;
~~~


**Final**

При указание **final** к переменной - она становится константой.

При указание модификатора доступа **final** к методу, данный метод становится не
переопределяемым.

При указание **final** к классу - он больше не может иметь потомков.


**Interface**

Своего рода абстрактный класс, в котором мы только указываем методы без их реализации. Поля внутри интерфейся являются константами и переопределить иили изменить их не получится.

~~~
public class Test_class implements for_Test {
    public int a = 5;

    @Override
    public void set(int a) {
        this.a = a;
    }

    @Override
    public int get() {
        return this.a;
    }
}

public intarface for_Test {
   public void set(int a);
   public int get();
}
~~~


# Аннотации <a name="annotation"></a>

Аннотации в Java являются своего рода метками в коде, описывающими метаданные
для функции/класса/пакета. Например, всем известная Аннотация @Override,
обозначающая, что мы собираемся переопределить метод родительского класса. Да, с
одной стороны, можно и без неё, но если у родителей не окажется этого метода,
существует вероятность, что мы зря писали код, т.к. конкретно этот метод может и
не вызваться никогда, а с Аннотацией @Override компилятор нам скажет, что: "Я не
нашел такого метода в родителях... что-то здесь нечисто".

Каждая из аннотаций имеет 2 главных обязательных параметра: 

- Тип хранения (Retention);
- Тип объекта над которым она указывается (Target).

Под "типом хранения" понимается стадия до которой "доживает" наша аннотация
внутри класса. Каждая аннотация имеет только один из возможных "типов хранения"
указанный в классе RetentionPolicy:

- SOURCE - аннотация используется только при написании кода и игнорируется
  компилятором (т.е. не сохраняется после компиляции). Обычно используется для
  каких-либо препроцессоров (условно), либо указаний компилятору

- CLASS - аннотация сохраняется после компиляции, однако игнорируется JVM (т.е.
  не может быть использована во время выполнения). Обычно используется для
  каких-либо сторонних сервисов, подгружающих ваш код в качестве plug-in
  приложения

- RUNTIME - аннотация которая сохраняется после компиляции и подгружается JVM
  (т.е. может использоваться во время выполнения самой программы). Используется
  в качестве меток в коде, которые напрямую влияют на ход выполнения программы
  (пример будет рассмотрен в данной статье)


**Тип объекта над которым указывается**

Данное описание стоит понимать практически буквально, т.к. в Java аннотации
могут указываться над чем угодно (Поля, классы, функции, т.д.) и для каждой
аннотации указывается, над чем конкретно она может быть задана. Здесь уже нет
правила "что-то одно", аннотацию можно указывать над всем ниже перечисленным,
либо же выбрать только нужные элементы класса ElementType:

- ANNOTATION_TYPE - другая аннотация
- CONSTRUCTOR - конструктор класса
- FIELD - поле класса
- LOCAL_VARIABLE - локальная переменная
- METHOD - метод класса
- PACKAGE - описание пакета package
- PARAMETER - параметр метода public void hello(@Annontation String param){}
- TYPE - указывается над классом

1) ~~~
   @Override
   Retention: SOURCE;
   Target: METHOD.

   Данная аннотация показывает, что метод над котором она прописана наследован у родительского класса.
   ~~~
2) ~~~
   @Deprecated
   Retention: Runtime;
   Target: CONSTRUCTOR, FIELD, LOCAL_VARIABLE, METHOD, PACKAGE, PARAMETER, TYPE.

   Данная аннотация указывает на методы, классы или переменные, которые является "устаревшими" и могут быть убраны в последующих версиях продукта.
   ~~~
3) ~~~
   @SuppressWarnings
   Retention: SOURCE;
   Target: TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR, LOCAL_VARIABLE

   Данная аннотация отключает вывод предупреждений компилятора, которые касаются элемента над которым она указана. Является SOURCE аннотацией указываемой над полями, методами, классами.
   ~~~
4) ~~~
   @Retention
   Retention: RUNTIME;
   Target: ANNOTATION_TYPE;

   Данная аннотация задает "тип хранения" аннотации над которой она указана. Да эта аннотация используется даже для самой себя... магия да и только.
   ~~~
5) ~~~
   @Target
   Retention: RUNTIME;
   Target: ANNOTATION_TYPE;

   Данная аннотация задает тип объекта над которым может указываться создаваемая нами аннотация. Да и она тоже используется для себя же, привыкайте...
   ~~~

## Исключеня <a name="exeption"></a>

Обработка исключений в Java основана на использовании в программе следующих
ключевых слов:

- try – определяет блок кода, в котором может произойти исключение;
- catch – определяет блок кода, в котором происходит обработка исключения;
- finally – определяет блок кода, который является необязательным, но при его
  наличии выполняется в любом случае независимо от результатов выполнения блока
  try.
- throw – используется для возбуждения исключения;
- throws – используется в сигнатуре методов для предупреждения, о том что метод
  может выбросить исключение.

~~~
public String input() throws MyException {
      BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
    String s = null;

    try {
        s = reader.readLine();
    } catch (IOException e) {
        System.out.println(e.getMessage());
    } finally {
        try {
            reader.close();
        } catch (IOException e) {
            System.out.println(e.getMessage());
        }
    }

    if (s.equals("")) {
        throw new MyException("String can not be empty!");
    }
    return s;
}
~~~

## Generics <a name="generics"></a>

Дженерики (обобщения) — это особые средства языка Java для реализации
обобщённого программирования: особого подхода к описанию данных и алгоритмов,
позволяющего работать с различными типами данных без изменения их описания.

~~~
class Test<T, U>
{
    T obj1; 
    U obj2; 
 
    Test(T obj1, U obj2)
    {
        this.obj1 = obj1;
        this.obj2 = obj2;
    }
 
    public void print()
    {
        System.out.println(obj1);
        System.out.println(obj2);
    }
}

class Main
{
    public static void main (String[] args)
    {
        Test <String, Integer> obj =
            new Test<String, Integer>("GfG", 15);
 
        obj.print();
    }
}
~~~

## Optional <a name="optional"></a>

Optional - это объект-контейнер, который может содержать или не содержать
нулевое значение. Ссылка на объект класса Optional может быть null Если значение
присутствует, метод isPresent() вернет true.

Позволяет избавиться от проверки на null Без этого класса приходилось писать
проверку на NullPointerException. Благодарю этому один объект Optional можно
сравнить с другим объектом Optional через метод equals(), даже если они хранят в
себе ссылки на null.

Получить элемент Optional get() Метод класса Optoinal – возвращает значение,
если оно присутствует, в противном случае бросит NoSuchElementException.



## Streams <a name="streams"></a>

С выходом Java 8 появилась поддержка функционального программирования. Стало
возможным конструировать сложные цепочки операций над потоком данных.

Stream API – по сути это поток данных и последовательные операции над ними.

Интерфейсы Stream, IntStream, LongStream и DoubleStream – это потоки объектов и примитивных типов int, long и double.

Интерфейс Stream представляет собой последовательность элементов, поддерживающих последовательные и параллельные агрегатные операции.

~~~
public interface Stream<T> extends BaseStream<T,Stream<T>>
~~~

К агрегатным операциям относят различные операции над выборкой, например, получение числа элементов, получение минимального, максимального и среднего значения в выборке, а также суммирование значений.

Stream не предоставляет средств для прямого доступа к элементам или манипулирования ими. Вместо этого он описывает источник данных и вычислительные операции, которые будут выполняться над этими данными.

# Факты <a name="facts"></a>

Чтобы стравнить две строки нужно использовать не == , а метод equals()

~~~
if (a.equals("Привет") {
   "Привет"
}
else {
   "Пока"
}
~~~

**При наследвание сын может обращаться к protected полям бабушки.**


**Архитектура современных веб сервисов**

![Изображение](arhetectyre.png) 

# Полезные ресурсы <a name="res"></a>

Литература: 

Ресурсы:

1. [Песочница для запуска кода](https://replit.com/languages/python3)

1. [Песочница для работы с
   гитом](https://learngitbranching.js.org/?locale=ru_RU)

1. [Лекции от школы
   бэкенда](https://www.youtube.com/watch?v=PxIqLgjtQ5Y&list=PLQC2_0cDcSKBHamFYA6ncnc_fYuEQUy0s&index=2)

1. [Установка и базовые консольные команды PostgreSql для
   Linux](https://www.youtube.com/watch?v=kWUW3sMK0Mk)

1. [Официальный сайт SqlAlchemy](https://docs.sqlalchemy.org/en/20/)

1. [Архитектура web
   приложений](https://www.youtube.com/watch?v=ZgojwJEcLn8&t=623s)

# Проекты <a name="project"></a>
