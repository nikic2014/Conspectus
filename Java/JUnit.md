# JUnit


1. [Maven - жизненный цикл сборки](#life-cycle)
1. [Команды](#command) 
1. [POM](#pom)
1. [Полезные ресурсы](#res)


**UnitTest** или модульное тестирование - тестирование минимальной рабочей
единицы программы, те тестирование методов.

## Первые шаги 

Допустим у нас есть класс:

~~~
public class two_m_class {
    public int first_method(){
        return 1;
    }
    public int second_method(){
        return 5;
    }
}
~~~

Мы хотим покрыть его тестами, для этого мы создаем еще один класс в котором
прописываем тесты для всех функций:

~~~
import static org.junit.jupiter.api.Assertions.*;

class TestTest {
    @org.junit.jupiter.api.Test
    void test1_for_Test1() {
        two_m_class a = new two_m_class();

        assertEquals(a.for_Test1(), 1);
    }

    @org.junit.jupiter.api.Test
    void test2_for_Test1() {
        two_m_class a = new two_m_class();

        assertEquals(a.for_Test1(), 2);
    }

    @org.junit.jupiter.api.Test
    void test1_for_Test2() {
        two_m_class a = new two_m_class();

        assertEquals(a.for_Test2(), 5);
    }

    @org.junit.jupiter.api.Test
    void test2_for_Test2() {
        two_m_class a = new two_m_class();

        assertEquals(a.for_Test2(), 2);
    }
}
~~~


Для того чтобы протестировать метод используется анотация
@org.junit.jupiter.api.Test или @Test и метод assertEquals, который сравнивает
два значения на равенство.
