# Задание 1
Предположим, у нас есть код, позволяющий вывести список групп товаров, а также товары, находящиеся в каждой группе. Задача заключается в том, что необходимо добавить к имеющемуся коду функциональность вложенных групп товаров.

В приложенном файле ***test_base.sql*** находится дамп базы данных MySQL, содержащий две таблицы:

1.	**groups** – таблица групп товаров, содержит поля:
    - id – идентификатор группы
    - id_parent – идентификатор «родительской» группы
    - name – название группы
2.	**products** – таблица товаров, содержит  поля:
    - id – идентификатор товара
    - id_group – идентификатор группы товаров
    - name – название товара


Необходимо написать PHP-скрипт, удовлетворяющий следующим требованиям:
1.	При запуске выводит список (ul) групп товаров первого уровня (groups.id_parent=0), название каждой группы является ссылкой, которая вызывает этот же скрипт с GET-параметром “group”, равным id группы. Возле названия должно быть написано общее количество товаров в группе (количество товаров в самой группе и во всех ее подгруппах). Пока не выбрана ни одна группа – также выводится список всех товаров.
2.	При переходе по ссылке (выборе группы товаров первого уровня) – кроме списка групп товаров первого уровня выводится также список всех подгрупп выбранной группы, все имена подгрупп также являются ссылками, и возле названия подгруппы находится количество товаров, содержащихся в этой подгруппе. Также выводятся все товары, отнесенные к выбранной группе (и всем ее подгруппам). 
3.	Количество уровней вложенности групп не ограничено.
4.	Набор используемых технологий ограничен: php, mysql, html, xslt (не обязательно). При реализации использование каких-либо библиотек или фреймворков разрешается только для шаблонизации (вывода информации).
5.	Допустимо добавление новых полей в таблицы. Изменять  логику работы или типы полей, удалять поля в любой таблице запрещено в целях сохранения обратной совместимости с имеющимся кодом (предполагаем что он есть). В случае добавления полей для всех вновь добавленных полей необходимо подготовить запрос/скрипт, заполняющий их данными, либо описать словами логику работы такого запроса/скрипта. 
6.	Никакое специальное оформление не требуется, оцениваться будет логика работы с вложенными группами товаров – sql-запросы и код php, реализующий эту логику, а также html код, реализующий вложенные списки.
 

«Эталонный» результат работы скрипта:
![Example Program Result Part 1](/img/task1-img-1.png)
![Example Program Result Part 2](/img/task1-img-2.png)
![Example Program Result Part 3](/img/task1-img-3.png)

---

# Задание 2

Необходимо написать плагин для  jQuery, который каждые 30 мс собирает данные о положении курсора мыши на странице и времени, а затем отправляет их на сервер. Данные должны представлять массив объектов с координатами точек и времени, которое курсор провел в них. Серверную часть реализовывать не надо.

Плагин должен принимать следующие настройки:

    - checkInterval  - период сбора данных (по умолчанию 30мс)
    - sendInterval – период отправки данных на сервер (по умолчанию 3с)
    - url – адрес, на который будут отправляться данные 

Плагин должен вызываться как метод некоторого jQuery-объекта, и координаты мыши должны рассчитываться относительно координат этого объекта. Пример вызова плагина:

```$(“div.container”).trackCoords({url: ‘/save.php’});```

---

# Задание 3 (необязательное)
Необходимо разработать сайт на YII версии 2.0

На сайте должны быть следующие страницы:
- Главная страница (www.example.com/) - представляет собой список пользователей
- Страница отправки заявки (www.example.com/request) - представляет собой форму со следующими полями: 
- выбор получателя из списка пользователей 
- контактные данные отправителя 
- текст заявки
- Страница пользователя (www/example.com/([a-zA-Z0-9]+)) - у каждого пользователя есть произвольный текстовый альяс (кроме request), по которому открывается его страница. На ней данные пользователя + форма заявки без выбора получателя

Для решения задачи необходимо использовать стандартные методы YII

При отправке заявки из общей формы после выбора юзера - надо аяксом подгружать и отображать сведения о нем.

---

# Задание 4 (необязательное)

Используя XSLT преобразования на сервере (PHP-классы XsltProcessor и DomDocument) преобразовать исходный xml-документ 
(***users.xml***) в html по заданию:

1) Вывести дерево типов пользователей
2) Вывести список пользователей вида:

        Имя Фамилия | Привязанные категории: Категория1, категория2...
        Имя Фамилия | Привязанные категории: Категория1, категория2...
        Имя Фамилия | Привязанные категории: Категория1, категория2...
    
    
**Структура XML:**

Узел usertypes - содержит типы пользователей вида:

    <usertype>
      <id>1</id>                     - Идентификатор типа
      <id_parent>14</id_parent>		 - Идентификатор родителя (0 для корневых элементов)
      <title>Арендатор</title>  	 - Название типа
    </usertype>

Узел userlinks - содержит привязки пользователей к типам:

    <link>
      <id_user>7126</id_user>        	- Идентификатор пользователя
      <id_usertype>3</id_usertype>    	- Идентификатор типа
    </link>
    
Узел userlinks - содержит описания пользователей:

    <user>
      <id>7126</id>            		- Идентификатор
      <fname>Сидор</fname>        	- Имя
      <sname>Михайлов</sname>    	- Фамилия
    </user>
    
Язык написания - PHP.

---

# Задание 5 (необязательное)

Используя XSLT преобразования на сервере (PHP-классы XsltProcessor и DomDocument) преобразовать исходный xml-документ (***cities.xml***) в html.

В документе содержится список городов. Каждый город имеет следующую структуру:

    <node>
      <id>1</id> - идентификатор города
      <id_region>1</id_region> - идентификатор региона
      <name>Москва</name>  - название города
      <name_latin>msk</name_latin>  - латинское название города
    </node>

Необходимо вывести алфавитный указатель городов, по аналогии со страницей:
http://www.beboss.ru/kn?change

Каждый город в указателе должен быть ссылкой, в качестве адреса (href) ссылки необходимо указать name_latin данного города.



