# Maven

1. [Maven - жизненный цикл сборки](#life-cycle)
1. [Команды](#command) 
1. [POM](#pom)
1. [Полезные ресурсы](#res)

## Maven - жизненный цикл сборки <a name="life-cycle"></a>

Цикл сборки проекта состоит из:

1. Очистки (clean);
2. Сборки (build);
3. Формирование отчета (site);

Основные фазы сборки:

1. *-resourse - подготовка ресурсов
1. validate - валидация (без компиляции)
1. compile - компилирование проекта;
1. test - тестирование с помощью JUnit тестов;
1. package - упаковка в jar файлы или war, ear в зависимости от типа проекта;
1. integration-test - запуск интеграционных тестов;
1. install - копирование jar (war, ear) в локальный репозиторий;
1. deploy - публикация файла в удалённый репозиторий.

Фазы сборки проекта выполняются в данном порядке, и пре вызове следующей
выполняются все предыдущие.

Особняком стоят фазы clean и site. Они не выполняются, если специально не
указаны в строке запуска.

clean - удаление всех созданных в процессе сборки артефактов: .class, .jar и др.
файлов. В простейшем случае результат — просто удаление каталога target. 

site - предназначена для создания документации.

Т.к. команда mvn понимает когда ему передают несколько фаз, то для сборки
проекта создания документации "с нуля" выполняют: 

~~~
mvn clean package site
~~~

## Команды <a name="command"></a>

Команды в maven бывают предварительные и завершающие.

Чтобы запустить создание проекта из консоли можно вызвать команду:
~~~
mvn archetype:generate
~~~

Аналогично можно создать проект из IDE выбрав при создании проекта maven.

## POM <a name="pom"></a>

Информация для программного проекта, поддерживаемого Maven, содержится в
XML-файле с именем pom.xml (от Project Object Model). При исполнении Мавен
проверяет прежде всего, содержит ли этот файл все необходимые данные и все ли
данные синтаксически правильно записаны.

Корневой элемент **project**, в котором прописана схема облегчающая
редактирование и проверку, и версия POM.

~~~
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    ...
</project>
~~~

Внутри тега **project** содержится основная и обязательная информация о проекте:

~~~
<groupId>com.examclouds</groupId>
<artifactId>courses</artifactId>
<version>1.0-SNAPSHOT</version>
~~~

В Maven каждый проект идентифицируется парой groupId, artifactId.

Во избежание конфликта имён, groupId - наименование организации или
подразделения. Обычно записывают доменное имя организации или сайта проекта.

artifactId - название проекта.

Внутри тега version хранится версия проекта.

Тройкой groupId, artifactId, version (далее - GAV) можно однозначно
идентифицировать jar файл приложения или библиотеки. Если состояние кода для
проекта не зафиксировано, то в конце к имени версии добавляется "-SNAPSHOT" что
обозначает, что версия в разработке и результирующий jar файл может меняться.

Тег **packaging** определяет какого типа файл будет создаваться как результат
сборки. Возможные варианты pom, jar, war, ear.

Тег является необязательным. Если его нет, используется значение по умолчанию -
jar.

Также добавляется информация, которая не используется самим Maven, но нужна для
программиста, чтобы понять, о чём этот проект:

~~~
<name>powermock-core</name> название проекта для человека
<description>PowerMock core functionality.</description> Описание проекта
<url>http://www.powermock.org</url> сайт проекта
~~~

Зависимости - следующая очень важная часть pom.xml - тут хранится список всех
библиотек (зависимостей) которые используются в проекте. Каждая библиотека
идентифицируется так же как и сам проект - тройкой groupId, artifactId, version
(GAV). Объявление зависимостей заключено в теге
**\<dependencies>...\</dependencies>**. 

Кроме GAV при описании зависимости может присутствовать тег **\<scope>**. Он
задаёт, для чего библиотека используется. В данном примере говорится, что
библиотека с GAV junit:junit:4.4 нужна только для выполнения тестов.

~~~
<dependencies>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.39</version>
    </dependency>

    <dependency>
        <groupId>com.h2database</groupId>
        <artifactId>h2</artifactId>
        <version>1.4.196</version>
    </dependency>
</dependencies>
~~~

Тег **\<build>**  не обязательный, так как существуют значения по умолчанию.
Этот раздел содержит информацию по самой сборке:

- где находятся исходные файлы,
- где ресурсы,
- какие плагины используются. 

~~~
<build>
    <sourceDirectory>src</sourceDirectory>
    <resources>
        <resource>
            <directory>resources</directory>
        </resource>
    </resources>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>2.0.2</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
                <encoding>UTF-8</encoding>
            </configuration>
        </plugin>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-checkstyle-plugin</artifactId>
            <version>2.17</version>
            <configuration>
                <suppressionsLocation>suppressions.xml</suppressionsLocation>
            </configuration>
        </plugin>
    </plugins>
</build>
~~~

- \<sourceDirectory> - определяет, откуда Maven будет брать файлы исходного
  кода. По умолчанию это src/main/java, но вы можете определить, где это вам
  удобно. Директория может быть только одна (без использования специальных
  плагинов).

- \<recources> и вложенные в неё теги \<recource> определяют, одну или несколько
  директорий, где хранятся файлы ресурсов. Ресурсы в отличие от файлов исходного
  кода при сборке просто копируются. Директория по умолчанию src/main/resources.

- \<outputDirectory> - определяет, в какую директорию компилятор будет сохранять
  результаты компиляции - *.class файлы. Значение по умолчанию - target/classes.

- \<finalName> - имя результирующего jar (war, ear ...) файла с соответствующим
  типу расширением, который создаётся на фазе package. Значение по умолчанию —
  artifactId-version.

Maven плагины позволяют задать дополнительные действия, которые будут
выполняться при сборке. Например, в приведённом примере добавлен плагин, который
автоматически делает проверку кода на наличие "плохого" кода и потенциальных
ошибок.

# Полезные ресурсы <a name="res"></a>

1. [Плейлист
   Maven](https://www.youtube.com/watch?v=Hky0f4X3TK0&list=PL1zJrLkuWT67KutVoHZ3EhGswNkMcRIX2&index=2)

1. [Мини введение в
   Maven](https://www.examclouds.com/ru/java/java-core-russian/lesson20)