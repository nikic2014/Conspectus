# JUnit

1. [Первые шаги](#example) 
1. [Жизненный цикл сборки](#life-cycle)
1. [Полезные ресурсы](#res)


**UnitTest** или модульное тестирование - тестирование минимальной рабочей
единицы программы, те тестирование методов.

## Первые шаги <a name="example"></a>

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

Также существует множество других сравнений:

1. assertEquals() и assertNotEquals()
1. assertArrayEquals()
1. assertIterableEquals()
1. assertLinesMatch()
1. assertNotNull() и assertNull()
1. assertNotSame() и assertSame()
1. assertTimeout() и assertTimeoutPreemptively()
1. assertTrue() и assertFalse)
1. assertThrows()

Аналогично можно использоватьь assumeEquals и тд. В случае провала таких
тестов,они просто игнорируются, не выбрасывая исключения.

При желание в анотацию @Test можно написать (expected = needExeption), и тогда
тест пройдет, только при выбрасывание нужного исключения.

Вспомогательные методы:
1. @BeforeClass - запускается только один раз при запуске теста (static).
1. @Before - запускается перед каждым тестовым методом.
1. @After - запускается после каждого метода.
1. @AfterClass - запускается после того, как отработали все тестовые методы.

## Жизненный цикл тестирующего класса <a name="life-cycle"></a>

При запуске каждого тестового метода создается объект тестового класса.

1. @BeforeClass - запускается для создания тестового класса.
1. Для каждого метода создается экземпляр тестового класса. Затем для каждого
   метода запускается метод с аннотацией @Before, затем сам тестовый метод
   @Test, и затем вспомогательный метод с аннотацией @After.
1. В самом конце запускается @AfterClass после выполнения всех тестовых
   методов.


# Полезные ресурсы <a name="res"></a>

1. [User guid](https://junit.org/junit5/docs/5.0.0/user-guide/)
