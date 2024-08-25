# קומפילציה:
 קומפילציה ב - java מכיל מספר צעדים שבוספם הקוד ב - java יהפוך קוד ב - byte שהמכונה יכולה להריץ.
 ### תהליך:
1) **כתיבת קוד המקור:**
- קובץ המקור ב - java: הקובץ שנשמר בסיומת java. מכיל את הקוד הקריא

2) **קומפילציה:**
- הקומפילר של java(javac):
קובץ המקור עובר לקומפילר, שמתרגם את קוד המקור לקוד של byte. ונשמר בקובץ עם סיומת class.
- בדיקת תחביר(syntax):
במהלך הקומפילציה, הקומפילר בודק בקוד המקור לבעיות בתחביר.
- יצירת קוד byte:
לאחר שאין בקוד שגיאות, הקומפילר מייצר קוד byte ל JVM - java virtual machine.  קוד ה byte הוא מצב ביניים שעצמי מפלטפורמה כאשר ה - JVM יכול להריץ אותו.

3) **טעינת מחלקה:**
- טוען המחלקה:
כאשר תוכנית ה - java רצה הטוען מחלקה של ה - JVM טוען את הקובץ בסיומת class. לזיכרון.
טוען המחלקה אחראי למציא וטעינה של כל המחלקות הדרושות לתוכנה.

4) **בדיקת קוד ה - byte:**
- מאמת הקוד:
ה - JVM מכיל מאמת קוד byte שבודק וטוען את קוד ה - byte לתקינות ואבטחה. 
המאמת מוודא קוד ה - byte נצמד לבטיחות של ה - JVM.

5) **ביצוע:**
- ה - JIT ,just in time:
משתמש בקומפילר של JIT להמיר קוד ה - byte שפת קוד נטיבית,  זה מתרחש בזמן ההרצה ומשפר ביצועים.
- מתורגמן:
ה - JVM מכיל מתורגמן שמריץ את קוד ה - byte פקודה אחרי פקודה.
![[Pasted image 20240802092100.png]]
### ה - JVM
ה - JVM - java virtual machine, הוא חלק חשוב ב - java. שמשמש כסביבת ריצה לקוד ה - byte, המפשט את החומרה ומערכת הפעלה הבסיסית.
**מאפיינים:**

- המצעי מפלטפורמות:
ה - JVM מאפשר לתוכנת ה - java לרוץ על כל מכשיר או מערכת הפעלה.

- מנהל זיכרון:
ה - JVM מכיל אוסף אשפה שמנהל אוטומתי את הזיכרון, ולוקח בחזרה זיכרון של עצמים שלא בשימוש.

- בטיחות:
מספק סביבת הרצה בטוחה, על ידי אכיפת הגישות, והפעלת קוד ה byte ב- sandbox.

- ביצועים:
ה - JVM מספק קומפילר JIT - just in time, שממיר את קוד ה byte לשפת מחשב נטיבית.
# יחסי משתנים פונקציות ומחלקות
### משנים עם גישה:
סוגי הגישות השונות של מחלקות ופונקציות ומשתנים

**ה - public:**
מחלקה - המחלקה נגישה לכל מחלקה אחרת
פונקציה/משתנה - יכול לגשת מכל מחלקה

**ה - protected:**
מחלקה - לא יכול למשש למחלקות ברמה העליונה
פונקציה/משתנה - יכול לגשת מכל מחלקה מאותו package, או subclass(גם מ - packageים אחרים)

**ה - private:**
מחלקה - לא יכול למשש למחלקות ברמה העליונה
פונקציה/משתנה - יכול לגשת מאותו מחלקה בלבד

**רגיל:**
מחלקה - נגישה לכל מחלקה באותו package
פונקציה/משתנה - נגיש בכל מקום באותו package
### משנים ללא גישה:
**ה - static:**
משתנה - שייך למחלקה, ולא ל - instance של המחלקה
פונקציה - יכולה להיקרא ללא יצירה של instance של מחלקה

**ה - final:**
מחלקה - המחלקה לא יכולה לרשת
פונקציה - הפונקציה לא יכול להיות overridden על ידי מחלקה שיורשת
משתנה - ערך המשתנה לא יכול להשתנות

**ה - abstract:**
מחלקה - המחלקה לא יכולה להיות מופעלת וכנראה תכיל פונקציות abstract
פונקציות - הפונקציות ללא גוף, וחייבות מייושמות על ידי המחלקות היורשות

**ה - synchronized:**
פונקציה - הפונקציה ניתנת לגישה על ידי thread אחד באותו זמן

**ה - volatile:**
משתנה - ערך המשתנה לעולם לא יהיה cached thread-locally,כל הקריאה והכתיבה תישלח ישירות לזיכרון הראשי.

**ה - transient:**
משתנה - המשתנה לא יעבור בסידרה.

# ירישה:
כאשר מחלקה מקבלת פונקציות ומשתנים מכיתה אחרת.
מחלקת אב(super class), זאת מחלקה שהתכונות שלה מחלקה אחרת תירש.
מחלקת ילד(sub class), זאת מחלקה היורשת את התכונות.
השימוש במילה extends משתמש בשביל לזה לקוח ממחלקה קיימת.
`// Superclass`
`class `<span style="color:rgb(25, 133, 74)">Animal</span>` {`
    `void eat() {`
        `System.out.println("This animal eats food.");`
    `}`
`}`

`// Subclass`
`class Dog` <span style="color:rgb(223, 58, 58)">extends</span> <span style="color:rgb(25, 133, 74)">Animal</span> `{
    `void bark() {`
        `System.out.println("The dog barks.");`
    `}`
`}` 

`public class Main {`
    `public static void main(String[] args) {`
        `Dog dog = new Dog();`
        `dog.eat();   // Inherited method`
        `dog.bark();   // Subclass method`
    `}`
`}`

## סוגי הגישות:

<span style="color:rgb(0, 176, 240)">public</span> - ניגש להכל.
<span style="color:rgb(0, 176, 240)">protected</span> - מאפשר לגשת לכיתת ילד או אותו package
<span style="color:rgb(0, 176, 240)">default</span> - מאפשר גישה באותו package
<span style="color:rgb(0, 176, 240)">private</span> - לא מאפשר גישה לכיתת ילד
מילה <span style="color:rgb(0, 176, 240)">super</span> המשמשת לפנות לעצם באופן מיידי
`class `<span style="color:rgb(25, 133, 74)">Animal</span> `{`
    `Animal() {`
        `System.out.println("Animal constructor");`
    `}`
    `void eat() {`
        `System.out.println("This animal eats food.");`
    `}`
`}`

`class Dog `<span style="color:rgb(0, 176, 240)">extends</span> <span style="color:rgb(25, 133, 74)">Animal</span> `{`
    `Dog() {`
        <span style="color:rgb(223, 58, 58)">super</span>`();   //Calls the constructor of Animal class`
        `System.out.println("Dog constructor");`
    `}`
  
  `void display() {
        <span style="color:rgb(223, 58, 58)">super</span>`.eat(); // Calls the eat method of Animal class
    `}
`}`
### יש סוגים שונים של ירישות ב - java:
- ירישה אחידה:
כאשר מחלקה לוקח את התכונות רק ממחלקה אחת.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXed0GPJxoXi02wpWIBUxzS5uMQ1nO5po0qzkon_PwVFlt6niXcwZXh2-8PAu76Uh6OUBML7Wfqo7LcCpR4OFgFVFBPcZWMpc-5IBPrj9YQ6u0EGKIlsjARY14Ap_DrWwDXYXZHOl6U8-Fa-l4SiqlHY53I?key=NlnaCHnnX5v_3XcYPkzT-w)

-  ירושה רב שכבתית:
מחלקה יורשת מכיתת אב אחת, ומורישה למחלקה אחרת

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeygRE4-EcU45jpPWdN9p-OXWbya1d-lxQt5Wjoy6Mr53c124RT_-reyS7lT2S36U88Lv4AKLM108K1BetBckJ68AL9Un7Mok6_eJuy-cqAYQ1pB2p52f8bRxhbk9iR9W531tWbR6XfU1iKcrEectZPA0MG?key=NlnaCHnnX5v_3XcYPkzT-w)

- ירושה מדורגת:
 ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcvBVIgZwZFIFnamTrGF0mbs6L_pf_BO62mwbh4auumYKeaUoruoTyD8EWbhEDFUAURW27x2AoeInsi-dDzlnTfLr5JvepwlikTZwTsTAWmB8b-8rLGgLoFMVZ-cuRW0cZNZmvd9vXVuEDBJqVvd_QYP1lf?key=NlnaCHnnX5v_3XcYPkzT-w)
מחלקה אחת משתמש כמחלקה אב למספר כיתות
### הפשטות (abstraction):
זו פעולה מראה רק פריטים חיוניים למשתמש, פונקציה של abstract חייבת להיות מיושמת עוד פעם במחלקה היורשת. אי אפשר ליצור עצם של מחלקה ב abstract, ולכן המחלקה הזאת משומשת להיות המחלקה המורישה.
על מנת ליישם פונקציה של abstract, משתמשים ב <span style="color:rgb(223, 58, 58)">Override</span><span style="color:rgb(223, 58, 58)">@</span>.

`abstract class `<span style="color:rgb(25, 133, 74)">Animal</span>` {`
    `// Abstract method (does not have a body)`
    <span style="color:rgb(223, 58, 58)">abstract</span>` void `<span style="color:rgb(25, 133, 74)">sound</span>`();`
    `// Concrete method`
    `void eat() {`
        `System.out.println("This animal eats food.");`
    `}`
`}`

`class Dog `<span style="color:rgb(0, 176, 240)">extends</span> <span style="color:rgb(25, 133, 74)">Animal</span>` {`
<span style="color:rgb(223, 58, 58)">    @Override</span>
    `void `<span style="color:rgb(25, 133, 74)">sound</span>`() {`
        `System.out.println("The dog barks.");`
    `}`
`}`

`public class Main {`
    `public static void main(String[] args) {`
        `Dog dog = new Dog();`
        `dog.sound();  // Outputs: The dog barks.`
        `dog.eat();   // Outputs: This animal eats food.`
    `}`
`}`

### ממשק (interface):
כיתת <span style="color:rgb(0, 176, 240)">interface</span>, זהו סוג של התייחסות ב - java. המכיל רק קבועים.
לא יכול להכיל פונקציות בנייה או שדה של משתנים
כל הפונקציות במחלקה הזאת נחשבות כמו פונקציות abstract, מחלקה יכולה לרשת מספר כיתות אב בעזרת interface
<span style="color:rgb(223, 58, 58)">interface</span> <span style="color:rgb(25, 133, 74)">Animal</span> `{`
    `void `<span style="color:rgb(25, 133, 74)">sound</span>`();   // Abstract method`
    `default void eat() {`
        `System.out.println("This animal eats food.");`
    `}`
`}`

`class Dog `<span style="color:rgb(223, 58, 58)">implements</span> <span style="color:rgb(25, 133, 74)">Animal</span> `{`
<span style="color:rgb(0, 176, 240)">    @Override</span>
    `public void `<span style="color:rgb(25, 133, 74)">sound</span>`() {`
        `System.out.println("The dog barks.");`
    `}`
`}`

`public class Main {`
    `public static void main(String[] args) {`
        `Dog dog = new Dog();`
        `dog.sound();  // Outputs: The dog barks.`
        `dog.eat();   // Outputs: This animal eats food.`
    `}`
`}`
### ירושה מרובה:
גאבה לא מאפשר ירושה מרובה ישירות, כלומר מחלקה יורשת ממספר מחקות אב. אפשר שמחלקה תירש ממספר מחלקות אב בעזרת ממשק interface.
`// First interface`
<span style="color:rgb(223, 58, 58)">interface</span> <span style="color:rgb(25, 133, 74)">Animal</span> `{`
    `void eat();`
`}` 

`// Second interface`
<span style="color:rgb(223, 58, 58)">interface</span> <span style="color:rgb(25, 133, 74)">Mammal</span> `{`
    `void walk();`
`}`

`// Third interface`
<span style="color:rgb(223, 58, 58)">interface</span> <span style="color:rgb(25, 133, 74)">Bird</span>` {`
    `void fly();`
`}`

`// Class implementing multiple interfaces`
`class Bat `<span style="color:rgb(223, 58, 58)">implements</span> <span style="color:rgb(25, 133, 74)">Animal</span>, <span style="color:rgb(25, 133, 74)">Mammal</span>, <span style="color:rgb(25, 133, 74)">Bird</span>` {`
    `@Override`
    `public void eat() {`
        `System.out.println("Bat is eating.");`
    `}`
    
    @Override
    public void walk() {
        System.out.println("Bat is walking.");
    }
    
    @Override
    public void fly() {
        System.out.println("Bat is flying.");
    }
`}`
### הבדלים בין abstract ל - interface:
Interface:
- יכול להיות גם פונקציות abstract וגם פונקציות רגילות 
- יכול להיות עם משתנים
- יכולות להיות פונקציות בנייה
- המחלקה יכולה להרחיב רק מחלקת extends אחת.
abstract
- יכול להיות רק פונקציות abstract
- לא יכול להכיל משתנים, רק קבועים
- לא יכול להכיל פונקציות בנייה
- יכול להרחיב מספר מחלקות extends

#### עטיפה (encapsulation):
זו דרך להסתיר פרטים המיישמים את המחלקה מגישה חיצונית, ומאפשר רק יישום חיצוני. כאשר מכריזים את המשתנים של המחלקה כ - private. ומוסיפים getters ו - setters שבעזרתם המשתמש יכול לתקשר עם המחלקה.
`public class Person {`
    `// Private fields`
    <span style="color:rgb(223, 58, 58)">private</span>` String name;`
    <span style="color:rgb(223, 58, 58)">private</span>` int age;`
    
    // Constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
  
    // Public getter for name
    public String getName() {
        return name;
    }
  
    // Public setter for name
    public void setName(String name) {
        this.name = name;
    }
    
    // Public getter for age
    public int getAge() {
        return age;
    }

    // Public setter for age
    public void setAge(int age) {
            this.age = age;
        }
    }
`}`

#### רב צורתי(polymorphism):
מאפשר לעצמים להתייחס למשתנים של מחלקת האב שלה כאילו הם המשתנים של המחלקה עצמה.
סיגי ה polymorphism:
- Compile time polymorphism(overloading)
- Runtime polymorphism(overriding)

**Compile-Time polymorphism:**
שיטת ה - overloading מאפשר ליותר מפונקציה אחת להיות עם אותה שם, אך חתימה שונה(המשתנים שמקבלת).

`class MathOperation {`
    `// Method to add two integers`
    `int add(int a, int b) {`
        `return a + b;`
   `}`
    
    // Method to add three integers
    int add(int a, int b, int c) {
        return a + b + c;
    }
    
    // Method to add two double values
    double add(double a, double b) {
        return a + b;
    }
`}

**Run-Time polymorphism:**
שיטת ה - overriding מתרחשת כאשר המחלקה היורשת מכילה יישום לפונקציה שקיימת במחלקת האב.

`class `<span style="color:rgb(25, 133, 74)">Animal</span>` {
    `void `<span style="color:rgb(25, 133, 74)">sound</span>`() {`
        `System.out.println("This animal makes a sound.");`
    `}`
`}`

`class Dog` <span style="color:rgb(0, 176, 240)">extends</span> <span style="color:rgb(25, 133, 74)">Animal</span> `{
<span style="color:rgb(223, 58, 58)">    @Override</span>
    `void` <span style="color:rgb(25, 133, 74)">sound</span>`() {
      `  System.out.println("The dog barks.");`
   ` }`
`}`

`class Cat` <span style="color:rgb(0, 176, 240)">extends</span> <span style="color:rgb(25, 133, 74)">Animal</span> `{`
<span style="color:rgb(223, 58, 58)">    @Override</span>
    `void` <span style="color:rgb(25, 133, 74)">sound</span>`() {
        `System.out.println("The cat meows.");
    `}
`}

# מבני נתונים ב - java
#### רשימה של מערכים Array list:
רשימה של מערכים פועלת כמו מערך אך בעל היכולת לשנות את גודלו, להוסיף או למחוק איברים.

```
ArrayList<String> list = new ArrayList<>();
list.add("Apple");
list.add(1,"Banana");
list.add("Orange");
String fruit = list.get(0); // Returns "Apple"
list.set(1, "Blueberry"); // Changes "Banana" to "Blueberry"
list.remove(2); // Removes "Orange"
list.size(); // number of elements
list.contains(“Apple”); // boolean if key is contained

//loop for the element in the list
for (String fruit : list) {
    System.out.println(fruit);
} 
```
#### רשימה מקושרת linked list:
זאת שרשרת דו כיוונית, כל איבר מקושר לאיבר הקודם והאיבר הבא.
```
// Creating a LinkedList
LinkedList<String> fruits = new LinkedList<>();

// Adding elements
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Orange");

// Accessing elements
System.out.println("First fruit: " + fruits.get(0));

// Modifying elements
fruits.set(1, "Blueberry");
// Removing elements
fruits.remove(2);

// Iterating over elements
for (String fruit : fruits) {
System.out.println(fruit);
}

// Checking size
System.out.println("Number of fruits: " + fruits.size());

// Adding elements to the beginning and end
fruits.addFirst("Strawberry");
fruits.addLast("Grapes");

// Accessing first and last elements
System.out.println("First fruit: " + fruits.getFirst());
System.out.println("Last fruit: " + fruits.getLast());

// Removing first and last elements
fruits.removeFirst();
fruits.removeLast();
```
#### מפה hash map:
מפה ב java זהו משתנה של key-value pair.
```
HashMap<String,Integer> map = new HashMap<String,Integer>();
map.put(“john”, 1234);  //adding/updating this pair to the map
map.get(“john”);  //getting the value of the specified key
map.containsKey(“john”);  //check if the key is existing in the map list
map.remove(“john”);  //removing the item of the map based of the key
```
# ה - threads:
ה - threads הם דרך הביצוע של מספר משימות באותו הזמן בתוכנית, מה שמאפשר את הביצוע של התוכנית.
ה - thread זהו היחידה הקטנה ביותר של process, שיכול להיות מתוזמן להרצה.
ה - multithreading היכולת להרציץ מספר threadים באותו הזמן.
##### יצירת thread:
1) הארכה של המחלקה thread
- בעזרת יצירת מחלקה שמאירכה <span style="color:rgb(0, 176, 240)">extends</span> את המחלקה <span style="color:rgb(0, 176, 80)">Thread</span> 
- שינוי הפונקציה <span style="color:rgb(0, 176, 80)">()run</span> עם הקוד שה - thread יבצע
- יצירת instance של המחלקה וקריא של פונקצית ה - <span style="color:rgb(0, 176, 80)">()start</span>
`class `<span style="color:rgb(0, 176, 80)">MyThread</span> <span style="color:rgb(247, 43, 43)">extends</span> <span style="color:rgb(0, 176, 80)">Thread</span>` {`
	    `public void`<span style="color:rgb(0, 176, 80)">run()</span>` {`
        `System.out.println("Thread is running");`
    `}`

`public static void main(String[] args) {`
        <span style="color:rgb(0, 176, 80)">MyThread</span>` t1 = new `<span style="color:rgb(0, 176, 80)">MyThread</span>`();`
        `t1.`<span style="color:rgb(0, 176, 80)">start()</span>`; // Starts the thread and calls the run() method`
    `}`
`}`
2) יישום את ממשק ה - Runnable
- יצירת מחלקה שמיישמת <span style="color:rgb(0, 176, 80)">Runnable</span> 
- שינוי הפונקציה <span style="color:rgb(0, 176, 80)">()run</span> עם הקוד שה - thread יבצע
- יצירת instance של המחלקה עם העצם של <span style="color:rgb(0, 176, 80)">Runnable</span>, וקריאה של <span style="color:rgb(0, 176, 80)">()start</span>.
`class `<span style="color:rgb(0, 176, 80)">MyRunnable</span> <span style="color:rgb(247, 43, 43)">implements</span> <span style="color:rgb(0, 176, 80)">Runnable</span>` {`
    `public void `<span style="color:rgb(0, 176, 80)">run()</span>` {`
        `System.out.println("Thread is running");`
    `}`

  `public static void main(String[] args) {`
        <span style="color:rgb(0, 176, 80)">MyRunnable</span> `myRunnable = new `<span style="color:rgb(0, 176, 80)">MyRunnable</span>`();`
        `Thread t1 = new Thread(`<span style="color:rgb(0, 176, 80)">myRunnable</span>`);`
        `t1.`<span style="color:rgb(0, 176, 80)">start()</span>`; // Starts the thread and calls the run() method`
    `}`
`}`
##### מעגל החיים של ה - thread:
ה - thread יכול להיות רק במצב אחד באותו הזמן
1) חדש:
ה - thread מוצר אבל לא נקרא
2) ניתן להרצה (Runnable):
כאשר ה - thread מוכן לרוץ ומחכה לזמן של ה - CPU
3) ריצה:
כאשר ה - thread מתבצע
4) נחסם (blocked):
כאשר ה - thread חסום ומחכה לנעילת מוניטור
5) מחכה(waiting):
כאשר ה - thread מחכה ללא הגבלת זמן ל - thread אחר לבצע פעולה מסויימת
6) המתנה מתוזמנת(timed waiting):
כאשר ה - thread מחכה לזמן מסויים
7) מסתיים(terminated):
כשה - thread סיים את הביצוע שלו
##### פונקציות של thread:
- פונקצית התחלה ()start:
מתחיל את ה - thread
- פונקצית הרצה ()run:
מכיל את הקוד שה - thread מצבע
- פונקצית השעיה (long millis)sleep:
שם את ה - thread בהשעיה למשך מספר המילי שניות
- מחכה ()join:
מחכה ל - thread אחר להסתיים
- לתת זכות קדימה ()yield:
גורם ל - thread שרץ באותו הזמן לעצור זמני ולאפשר ל thread אחר לרוץ
- הפרעה ()interrupt:
מפריע ל - thread
### סיכרון Synchronization:
כאשר מספר threadים ניגשים למשאב משותף, הם יכול לגרום לבעיות של נתונים לא עקביים ותנאי גזע.
הפקודה <span style="color:rgb(247, 43, 43)">Synchronized</span> מאפשר לשלוט ב - threadים האלו.
**פונקצית סיכרון:**
מסכרן את כל הפונקציה
`public `<span style="color:rgb(247, 43, 43)">synchronized</span>` void `<span style="color:rgb(0, 176, 80)">synchronizedMethod</span>`() {`
    `// code`
`}`
**בלוק מסוכרן:**
מסכרן בלוק של פקודות בתוך פונקציה
`public void method() {`
    <span style="color:rgb(247, 43, 43)">synchronized</span> `(this) {`
        `// code`
    `}`
`}`
דוגמה לסיכרון:
פונקצית ה - printTable מסתכרנת, דבר שמוודא שרק thread אחד יכול לרוץ בזמן שבוא העצם Table.
```
class Table {
    synchronized void printTable(int n) {
        for (int i = 1; i <= 5; i++) {
            System.out.println(n * i);
            try {
                Thread.sleep(400);
            } catch (InterruptedException e) {
                System.out.println(e);
            }
        }
    }
}

class MyThread1 extends Thread {
    Table t;

    MyThread1(Table t) {
        this.t = t;
    }

    public void run() {
        t.printTable(5);
    }
}

class MyThread2 extends Thread {
    Table t;

    MyThread2(Table t) {
        this.t = t;
    }

    public void run() {
        t.printTable(100);
    }
}

public class TestSynchronization {
    public static void main(String args[]) {
        Table obj = new Table();
        MyThread1 t1 = new MyThread1(obj);
        MyThread2 t2 = new MyThread2(obj);
        t1.start();
        t2.start();
    }
}
```
# שגיאות
### שגיאות קומפילציה
שגיאות שמתרחשות בזמן הקומפילציה, כאשר קוד ה - java ממומר לקוד של ביטים. השגיאות מונעות המקוד להיות ממומר בהצלחה.
השגיאות מתרחשות לפני שהקוד מורץ, קשורים בעיקר לחיבור של הקוד.
סיבות נפוצות:
- שגיאות חיבור
- שימוש בנתונים לא תואמים
- מחלקה/פונקציה שלא נמצא, שימוש במשתנים שלא הוכרזו
- קוד שלא ניתן להשגה, קוד שלא ירוץ אף פעם.
### שגיאות הרצה
שגיאות שמתרחשות אחרי שהקוד התקמפל בהצלחה, ועכשיו מורץ, יכול לגרום לתוכנה להסתיים באופן לא צפוי לא לפעול כראוי.
סיבות נפוצות:
- ה - NullPointerException, עצם שלא אותחל.
- אורך מערך מחוץ לגבולות
- שגיאות מתמטיות
- לעשות cast לעצם לתת מחלקה שלא ה - instance שלו.
- פתיחה של קובץ לא קיים
- אין זיכרון פנוי
