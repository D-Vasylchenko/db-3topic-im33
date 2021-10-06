#  Система управління відкритими даними. Аналіз предметної області



## Вступ

В цьому документі викладено аналіз предметної області. Розглянуто основні визначення, підходи, моделі та способи вирішення завдання, представлено порівняльну характеристику існуючих засобів вирішення завдання, проаналізовано їхні переваги та недоліки.

## Основні визначення

**Відкриті дані** (open data) - дані, які вільно доступні для машиночитаемого використання і подальшої передруку без обмежень авторського права, патентів та інших механізмів контролю. Під час аналізу відкритих даних, ми стикаємося з 'Великим даними'

**Вели́кі да́ні (Big Data)**  — набори інформації (як структурованої, так і неструктурованої) настільки великих розмірів, що традиційні способи та підходи (здебільшого засновані на рішеннях класу бізнесової аналітики та СУБД) не можуть бути застосовані до них

**Предметна область (бази даних)** — це сфера застосування конкретної бази даних.

**БД (DB) - База даних (database)**. Структурована сукупність даних, які відображають стан об'єктів певної предметної області та зв'язки між ними.

**СУБД (DBMS)** - Систе́ма управління базами да́них(Databast Manage System) . Набір взаємопов'язаних даних (база даних) і програм для доступу до цих даних[1]. Надає можливості створення, збереження, оновлення та пошуку інформації в базах даних з контролем доступу до даних. 

**Банк даних** –  складова в автоматизованих системах керування та інформаційно-обчислювальних системах, яка здійснює централізоване інформаційне забезпечення колективу користувачів, або сукупності задач, які розв'язуються в системі. 

**Модель даних**— це система правил, згідно з якими створюють структуру даних, здійснюють доступ до даних та змінюють їх.

**АIC** - Автоматизована інформаційна система

**Набір даних** (англ. data set) у термінології IBM — файл з організацією у вигляді записів

    
## Підходи та способи вирішення завдання

#### Процес проектування БД

Процес проектування БД може бути поданий у вигляді **моделі** бізнес-процесів. Бізнес-модель процесу проектування дозволяє:

·      відобразити суб'єктивну думку розробника БД на процес проектування конкретної БД;

·      врахувати особливості ІТ-проекту;

·      скласти план проектування конкретної БД;

·      прорахувати тривалість проектних робіт (створити тимчасову модель проектування).

·      завдання зворотного впливу.

#### Найбільш великі професійні завдання (етапи) проектування БД 

Такими завданнями (етапами) є:

·      **збір й аналіз вхідних даних** – це початковий етап проектування, на якому здійснюється збір і контроль якості результатів аналізу ПО БД, готується план проектування БД;

·      **створення логічної моделі БД** – це етап, на якому на підставі інформаційної моделі ПО БД створюється логічна структура БД, незалежна від її реалізації;

·      **створення фізичної моделі БД** : внутрішня схема – це етап, на якому на підставі логічної моделі БД створюється фізична структура БД, залежна від її

реалізації.

·      **створення серверного коду** – це етап, на якому на підставі функціональної моделі ПО БД створюється серверний код БД у вигляді тригерів, збережених процедур і пакетів. Ці модулі створюються розробником БД і виконуються сервером;

·      **проектування модулів додатків БД** – це етап, на якому створюються специфікації модулів додатків, розробляються стратегії тестування БД і додатків, створюється план тестування додатків БД і готуються тестові дані;

·      контроль якості проектування БД полягає в перевірці якості результатів проектування на кожному його етапі;






### Модель даних DDF

 **Модель даних DDF** описує спосіб упорядкування даних та визначення того, як частини даних співвідносяться між собою. Використовується для визначення наборів даних. Кожен набір даних DDF визначає п’ять наборів даних: поняття(Concepts), метадані(Metadata), сутності(Entities), точки даних(Datapoints) and синоніми(Synonyms).

#### 1. Дані в DDF 
Дані в DDF  зберігаються в парах **ключ-значення**, які називаються **DataPoints**. Ключ складається з двох або більше вимірів, тоді як значення складається з одного показника.


 #### 2. Сутності(Entities)

**Властивість** надає додаткову інформацію про дискретне поняття.
Наприклад, концепція країни може мати властивості повне ім'я, широту чи довготу.

**Домен сутності** - це дискретна концепція, у якій перераховані всі її можливі значення. Таким чином, він чітко визначає область поняття. Крім того, перерахування всіх можливих значень дає можливість визначити властивості для кожного значення.
Наприклад, ми можемо перетворити країну в домен сутності, перерахувавши всі країни. Таким чином, ми можемо визначити повну назву, широту та довготу для кожної країни.

**Сутність** - це одне значення в домені сутності.
Наприклад, Швеція чи Австрiя є суб’єктами господарювання у країні домену сутності.

**Набір сутностей** - це набір сутностей у домені сутності.
Наприклад, замість домену сутності країна може бути сутністю, що набирається в географічних місцях домену сутності, поряд з іншими наборами сутностей, такими як місто, світовий_регіон та провінція.

 #### 3) Типи понять

DDF має ряд заздалегідь визначених типів понятть. Поняття отримують тип шляхом встановлення властивості concept_type поняття. DDF також дозволяє визначити власні типи концепцій. Визначеними типами концепцій є:

**Рядок**

Рядок символів

**Міра**

Числове значення

**Інтервал**

Інтервал між двома числовими значеннями. Інтервал - це завжди інтервал у певному масштабі. Шкала може бути визначена додаванням концепції міри як області інтервалу.Значенням інтервалу є два числа у форматі масиву JSON.
Роль

**Роль** - це набір сутностей, який містить точно такі ж сутності, як і інший набір сутностей. Це дозволяє використовувати одну і ту ж сутність, встановлену кілька разів у таблиці, але в іншій ролі . 

Набір сутності може мати нуль або більше ролей. Наприклад, столиця - це роль міста. Політичний_капітал - це ще одна роль міста. Будь-яке значення капіталу або політичного_капіталу повинно бути посиланням на місто. Ролі також можна використовувати як деталізації. Коли роль використовується як деталізація, вона деталізується до набору сутності, роллю якої є роль.
Складені поняття

**Складене поняття** - це поєднання 2 або більше інших понять.

Наприклад, народження людини може складатися з міста та року, які завжди відбуваються разом. Інший приклад - міграційний потік. Це завжди трапляється з одного місця в інше. У цьому випадку нам потрібні ролі, щоб запобігти дублюванню заголовків таблиць. Ролі також додають значення вживанню слова "місто". Можливо багато інших способів структурування. Моделі даних залежить від того, яку саме структуру вони використовуватимуть.

**Час**

Поняття рік, місяць, день, тиждень та квартал - це особливі випадки наборів сутностей у часі домену сутності. Вони є особливими випадками, оскільки сутності не є явно перерахованими. Вони виведені за визначеними часовими форматами. Ці формати переважно відповідають базовому формату ISO 8601. Однак ми використовуємо малі регістри та додали інтервал чверті. Формати інтервалів часу роблять їх однозначно ідентифікованими. Значення можна проаналізувати, щоб з’ясувати, який інтервал воно представляє, тобто немає неоднозначних значень часу.

**Спеціальні типи понятть**

Ви можете призначити свій власний concept_type концепції, якщо він не є одним із вищезазначених типів концепцій. Концепції з користувацьким типом концепції не мають обмежень щодо можливих значень. Прикладами є геофігури, URL-адреси або BLOB-зображення.
Метада́ні

**Метада́ні**
 (англ. Metadata, походить від лат. meta — мета, кінцевий пункт, межа, край і, власне, дані), у загальному випадку, — це дані, що характеризують або пояснюють інші дані. Наприклад, значення «123456» само по собі недостатньо виразне. А якщо значенню «123456» зіставлено достатньо виразне ім'я «поштовий індекс» (що вже є метаданими), то в цьому контексті значення «123456» більш осмислене — можна витягати інформацію про місцеположення адресата, що має даний поштовий індекс.
Відмінність між даними і метаданими:

Метадані використовуються для підвищення якості пошуку. Пошукові запити, що використовують метадані можуть врятувати користувача від зайвої ручної роботи з фільтрації. Інформуючи комп'ютер про те, які елементи даних зв'язані і як ці зв'язки враховувати, стає можливим здійснювати достатньо складні операції по фільтрації та пошуку. Наприклад, якщо пошукова система «знає» про те, що «Ван Гог» є «голландським художником», то вона може видати у відповідь на запит про голландських художників веб-сторінку про Ван Гога, навіть якщо слова «голландський художник» не зустрічаються на цій сторінці. Такий підхід, званий представленням знань, знаходиться у сфері інтересів Семантичної павутини та штучного інтелекту.
Застосуваня метаданих

Метадані створюються для оптимізації алгоритмів стиснення з втратою якості. Наприклад, якщо до відео додаються метадані, що дозволяють комп'ютеру розділити зображення на основну частину і фонову, то остання може бути стиснута сильніше, що дозволить досягти більшого коефіцієнта стиснення.

Деякі види метаданих призначені для забезпечення можливості різних видів представлення деяких даних. Наприклад, якщо до зображення додаються метадані, що містять інформацію про те, яка частина зображення найважливіша (допустимо, зображення людини), то програма для проглядання зображень на маленькому екрані (такому, як на мобільному телефоні), може відобразити тільки цю найважливішу частину зображення. Аналогічно використовуються метадані, що дозволяють зробити доступними для сліпих діаграми і зображення, шляхом їх перетворення для виводу на спеціальні пристрої, або читання їх опису з використанням програмного забезпечення, що перетворює текст в мову.

Інші описові метадані можуть використовуватися автоматизованими робочими потоками. Наприклад, якщо деяка «розумна» програма «знає» вміст і структуру даних, то дані можуть бути автоматично перетворені і передані іншій «розумній» програмі як вхідні дані. В результаті, користувачі будуть врятовані від необхідності виконання безлічі рутинних операцій, якщо дані надані для роботи таким «небагатослівним» програмам.

Метадані стають важливі у World Wide Web внаслідок необхідності забезпечення пошуку корисної інформації серед величезної кількості доступної. Метадані, створені вручну мають велику цінність, оскільки це гарантує свідомість. Якщо веб-сторінка на якусь певну тему містить слово або фразу, то всі інші веб-сторінки на цю тему можуть містити таке ж слово або фразу.

## Порівняльна характеристика існуючих засобів вирішення завдання

### [Dataverse](https://dataverse.org/) ###
Dataverse - це open-source програмне забезпечення, яке призначене
для поширення, збереження, пошуку та аналізу відкритих даних. Воно
полегшує надання даних іншим особам, тобто робить дані більш доступними.
Головна особливість цього сервісу в тому, як він дозволяє
організовувати інформацію. Dataverse репозиторій зберігає в собі
віртуальні архіви, які називаються Dataverse колекціями. Кожна
Dataverse колекція містить в собі сети інформації (datasets) або інші
Dataverse колекції. Сети інформації в свою чергу містять в собі
описові метадані та файли з даними (документація, код та інше).
Головною метою даного програмного забеспечення є автоматизація
більшості рутинної роботи професійних архівістів та збереження/розповсюдження
інформації про автора даних.

### [Gapminder](https://www.gapminder.org/) ###
Незалежна освітня некомерційна організація, яка виявляє систематичні помилки щодо важливих світових тенденцій і пропорцій та використовує достовірні дані для розробки легко зрозумілих навчальних матеріалів, щоб позбавити людей від їх помилкових уявлень. Швидкий веб-сайт зі зручним інтерфейсом та цікаво поданим матеріалом у вигляді тесту, що надає статичні дані про країни всього світу.

### [The World Bank DataBank](https://databank.worldbank.org/home.aspx) ###
Веб-ресурс, на якому розміщується інформація щодо різних індикаторів розвитку країн світу. Збором і розміщенням даних займається організація World Bank, метою якої є боротьба з бідністю у світі. На основі аналізу зібраних даних, World Bank направляє фінансову допомогу в малорозвинені країни, а після інвестування слідкує за позитивними зрушеннями в економіці та рівнем життя людей, фіксуючи показники в своїй базі даних.

### [Statistics Poland](https://stat.gov.pl/en/) ###
Головна державна платформа Польщі, яке займається збором та публікацією статистичних даних, що стосуються економіки, населення та суспільства країни, на національному та місцевому рівнях.

### [Eurostat](https://ec.europa.eu/eurostat/web/main/data/database) ###
Cтатистичне управління Європейського Союзу. Головна місія - надавати високоякісні статистичні дані про Європу. Eurostat розробляє європейську статистику у партнерстві з Національними статистичними інститутами та іншими національними органами держав-членів ЄС. Це партнерство відоме як Європейська статистична система (ЄСС).
Веб-сайт Eurostat надає прямий і безкоштовний онлайн-доступ до всіх статистичних баз даних Євростату та електронних публікацій. База даних Євростату охоплює дані для таких країн:
- країни-члени ЄC
- країни-кандидати до ЄС
- єврозона
- країни EFTA

### [Google Public Data Explorer](https://www.google.com/publicdata/directory) ###
опис

**Порівняльна таблиця:**

Критерії:
- 🟢 - функція реалізована вдало
- 🟡 - функція реалізована, проте має деякі недоліки
- 🔴 - функція реалізована невдало
- ⚪️ - функція не реалізована


| Категорія | Критерій| Dataverse| Gapminder| The World Bank DataBank| Statistics Poland| Eurostat | Google Public Data Explorer|
|:----:| :-----------: |:-:| :-:| :--:| :--:| :--:| :--:|
| **Functionality (функциональні вимоги)** | Створення, публікація, редагування датасетів | 🟢 | ⚪️ | ⚪️ |  ⚪️ | ⚪️ |  🟢 |
|  | Data visualisations tools |🔴  (доступно лише через сторонні сервіси)| 🟢 | ⚪️ | 🟢 | 🟢 |  🟢 |
|  | Roles and permissions | 🟢 | 🔴 (реєстрація є, але ніяких прав і дозволів вона не надає) | 🔴 (є лише звичайний користувач і працівник банку) | ⚪️ | 🔴 (присутня можливість реєстрації, але вона робить доступними лише деякі спеціальні датасети) | ⚪️ |
|  | Пошук | 🟢 | 🟡 (стандартний, без фільтрів) | 🟢 | 🟢 | 🟢 |  🟡 (відсутність фільтрів) |
|  | Поділ даних за тегами, темами, критеріями | 🟢 | 🟢 | 🟢 | 🟡 (тем не багато, покривають не всі аспекти) | 🟢 | 🟢 | 
| **Usability (вимоги до зручності роботи)** | Підтримка англійської мови | 🟢 | 🟢 | 🟢 | 🟢 | 🟢 | 🟢 | 
|  | Наявність гайду з користування сайтом (Документація)| 🟢 | ⚪️ | ⚪️ | 🟡 (гайду нема, але є карта сайту, яка може допомогти) | 🟢 |  🟢 |
|  | UI/UX | 🟢 | 🟢 | 🟡 | 🟡 | 🟡 | 🟡 | 🟡 |
| **Reliability (вимоги до надійності)** | License and attribution | 🟢 | 🟢 | 🟢 | 🔴 (немає чітко сформульованих прав на дані) | 🟢 | 🟢 |
| **Performance (вимоги до продуктивності)** | оцінка за допомогою утиліти Lighthouse (від 0 до 100) | 🟡 81 | 🟢 96 | 🟡 56 | 🟡 87 | 🟡 61 | 🟢 89 |
| **Supportability (вимоги до підтримки)** | Feedback opportunity | 🟢 | 🟢 | 🟡 (наявні лише контактний номер телефону і адреса) | 🟢 | 🟢 |  🟢 | 
| | Актуальність даних | 🟡 (актуальність даних залежить лише від того, хто їх завантажує) | 🟡 (деякі категорії не заповнені оновленими даними за останні роки) | 🟡 (оновлюється раз у рік) | 🟢 | 🟢 | 🟡 (актуальність даних залежить лише від того, хто їх завантажує) |

## Висновки

В результаті проведення аналізу, наша команда дійшла висновку, що серед існуючих засобів вирішення завдання відсутній ідеальний інструмент, який задовольняє потреби та має достатній функціонал для вирішення задачі управління відкритими даними. Серед проаналізованих прикладів виділяється веб-застосунок Dataverse, який має більшість інструментів для реалізації повного життєвого циклу даних, проте в ньому відсутні засоби візуалізації даних, а також вирішальним є те, що наразі він працює в режимі обмеженого доступу та лише моделює управління відкритими даними. Тому було вирішено створити нову веб-систему для реалізації повного життєвого циклу даних.

## Посилання

*https://docs.google.com/document/d/1Cd2kEH5w3SRJYaDcu-M4dU5SY8No84T3g-QlNSW6pIE/edit#heading=h.w37ji581nnqj*
*https://www.google.com/publicdata/directory*
*https://uk.wikipedia.org/wiki/%D0%9F%D1%80%D0%B5%D0%B4%D0%BC%D0%B5%D1%82%D0%BD%D0%B0_%D0%BE%D0%B1%D0%BB%D0%B0%D1%81%D1%82%D1%8C*
*https://uk.wikipedia.org/wiki/%D0%91%D0%B0%D0%B7%D0%B0_%D0%B4%D0%B0%D0%BD%D0%B8%D1%85*
*http://www.kievoit.ippo.kubg.edu.ua/kievoit/2013/118/118.html*
*http://bookwu.net/book_organizaciya-baz-danih-i-znan_997/13_1.2.4-proces-proektuvannya-bd*