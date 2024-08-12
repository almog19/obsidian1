
- [ ] Multithreading and Concurrency
- [ ] template
- [x] networking programming
- [ ] Inter-process Communication (IPC)
- [ ] Embedded Systems Programming
- [ ] Compiler Design and Implementation
- [ ] Signal Handling
- [x] Error Handling and Debugging
- [ ] \ *Concurrency and Parallelism
- [ ] **Security in C Programming**: Writing secure code, understanding buffer overflows, input validation, and other security considerations.
- [ ] Real-time Systems: Writing C code for real-time operating systems (RTOS), understanding real-time constraints, and scheduling.
- [ ] **Advanced Algorithms**: Implementing and understanding complex algorithms for sorting, searching, graph traversal, dynamic programming, etc.
# פקודות:

##### process
fork() - מפצל את התהליך לשני תהליכים אחד כילד
wait() - תהליך ממתין עד שתהליך הילד שלו מסיים
getpid() - מחזיר את מספר הזהות של התהליך
getppid() - מחזיר את מספר הזהות של תהליך האב
# קומפילציה
תהליך הקומפילציה:
### ה - preprocessing
מתנהל על ידי ה - preprocessor, שמעבד את ההנחיות ומשנה את קוד המקור לפי הקומפילציה עצמה. שמכיל מספר משימות:
- **טיפול בהנחיות:**
הנחיות של ה - preprocessor מתחילות ב - <span style="color:rgb(0, 176, 240)">#</span>.
סוגי החניות:
**הרחבת macro:**
בעזרת ההנחיות: `define#
אלו ביטויים שמבטאים ערך מסויים, ה - preprocessor מחליף אותם בערך שלהן לפני הקומפילציה
```
#define PI 3.14
#define SQUARE(x) ((x) * (x))
```

**הכללת קבצים:**
בעזרת ההנחיות: `include#
מכיל את התוכן של קובץ אחר לקוד המקור, ה - preprocessor מחליף את אותם על כל התוכן של הקובץ.
```
#include <stdio.h>  // Includes the standard I/O library header
#include "myheader.h"  // Includes a user-defined header file
```
**קומפילציה מותנית:**
בעזרת ההנחיות: `#ifdef`, `#ifndef`, `#endif`, `#else`, `#elif`
מאפשר שלקוד יתקמפל לפי תנאים מסויימים, משמש לכלולל/לא לכלולל חלק קוד מסויים.
```
//הקוד יוכלל רק כאשר המשתנה הוכרז
#ifdef DEBUG
    printf("Debug mode\n");
#endif
```
**הורדת הערות:**
ה - preprocessor מוריד את כל הערות לפני העברת הקוד לקומפיילר.
**יצירת קוד ביניים:**
אחרי preprocessing, הקוד לרוב נשמר בקובץ ביניים, בהרחבת `i.`.
### קומפילציה
הקומפיילר מתרגם את הקוד לקוד assembly.
**ניסוח וניתוח סמנטי:**
הקומפיילר בודק את החיבור ואת הסמנטי של הקוד, לודא שהוא נצמד לחוקי השפה, שגיאות, משתנים לא מוכרזים, וסוגים לא מתאימים מתפסים פה.
**אופטימציה:**
הקומפיילר מבצע אופטימציה ליצירת הקוד, מוציא חישובים מיותרים, ומשפר ביצועי לולאה.
**יצירת קוד:**
הקומפיילר מתרגם את הקוד משפה high level של C ל - low level של assembly ספציפי ל - processor.
### אסמבלי
ממיר את קוד האסמבלי לקוד מכונה(הוראות בינאריות), כך שהמעבד יכול להריץ אותו. משתמש ב - assembler ליצור עצמי קבצים ברחבת `o.` או `obj.`.
### קישור
**חיבור עצמי קבצים:**
ה - linker מחבר מספר רב של עצמי קבצים שנוצרו על ידי ה - assembler לקובץ הרצה אחד. ופותר פניות של משתנים או פונקציות בין קבצים.
**קישור ספריות:**
ה - linker גם מקשר את הספריות המשומשות.
**יצירת חומרי הפעלה:**
הפלט מתהליך הקישור הוא קובץ שיכול לרוץ, עם הרחבה לרוב של `exe.`.
# process
ל - process יש מרחב זיכרון משלו, באחד מה - segmentים.
מאפיינים:
- בידוד:
כל process מבודד מ process אחר, ולא יכול לגשת לזיכרון של process אחרי ישירות
- הקצאת משאבים:
ל - process המשואבים מוקצים על ידי מערכת ההפעלה, כגון זמן CPU, זיכרון, טיפול קבצים ועוד…
- תקשורת:
ה - processים יכולים לתקשר ביניהם דרך מנגנוני IPC.
- יצירה:
ה - processים נוצרים על ידי קריאת המערכת `()fork`,  כאשר ה - process נוצר, נוצר גם ילד ל - process. 
- החלפת קשר:
ה - CPU מחליף בין processים, מערב שמירת מצב, וטעינת המצב של ה - process האחר, 
### יצירת process
ה - `()fork` זו פונקצית בסיפרייה `unist.h`, היוצר process נוסף על ידי שיכפול קריאת ה - process, ,process כלומר <span style="font-style:italic; font-style:italic; color:rgb(251, 136, 4)">לכל process שמצבע את פקודת ה - `()fork` נוצר לו ילד</span>. כל process רץ באותו הזמן.

ל - process הילד יהיה מקום זיכרון משלו. ובעצם התוכנית תתפצל ותרוץ מספר ה - processים, לכל process יהיה ID שונה, שהפונקציה מחזירה את ערך של `pid_t`(PID), ל - process הילד מוחזר 0, לאב מוחזר ה - PID של הילד, או מוחזר 1- אם יש שגיאה.
ל<span style="color:rgb(143, 74, 196)">דוגמה</span> יצירת process:
```
#include <stdio.h>
#include <unistd.h>

int main() {
    pid_t pid = fork();

    if (pid == 0) {
        // This is the child process
        printf("Hello from the child process!\n");
    } else if (pid > 0) {
        // This is the parent process
        printf("Hello from the parent process!\n");
    } else {
        // fork() failed
        printf("Fork failed!\n");
    }

    return 0;
}
```
##### לחכות ()wait
פונקצית `()wait` מאפשר ל - main process לחכות עד שה - process ילד יסיים לרוץ.
כאשר <span style="color:rgb(251, 136, 4)"> process ילד מצבע את הפעולה `()wait` הוא ייעצר לגמרי בגלל שאין לו ילד</span>
### תקשורת בין תהליכים(IPC)
זהו מנגנון שמאפשר ל - processים לתקשר ביניהם, משומש לרוב במערכות הפעלה שה - processים חולקים מידע או מסתנרכים  את פעילותם.
בגלל של processים יש מקום זיכרון שונה הם לא יכולים לגשת ישירות לזיכרון של אחר.
מנגנונים:
- **צינורות(pipes)**
מאפשר למידע לזרום בכיוון אחד בין שני processים לרוב ילד ואב.
הכולל חוצץ שאפשר לקרוא ולכתוב בו.
לפתיחת צינור משתמשים בפונקצית `()pipe` שלוח מערך עם שני אלנמטים, שכל אלנמט משמש כמתארי הצינור כקצה של הצינור. האלמנט הראשון הוא הקורא, השני הוא הכותב
מתאר צינור זהו מפתח שמאפשר גישה למקום שרוצים לקרוא/לכתוב בו.
אחרי פתיחת הצינור אפשר לפצל את ה - processים `()fork`, שמתארי הצינור יגדירו את ה - process הילד שנוצר(מורשים), <span style="color:rgb(251, 136, 4)">המתארים הם עצמאים זה מזה</span>.
```
#include <stdio.h>
#include <unistd.h>

int main() {
    int fd[2];
    pid_t pid;
    char buffer[20];

    // Create a pipe
    if (pipe(fd) == -1) {
        perror("pipe failed");
        return 1;
    }

    // Fork a child process
    pid = fork();

    if (pid < 0) {
        perror("fork failed");
        return 1;
    }

    if (pid > 0) {  // Parent process
        close(fd[0]); // Close reading end
        write(fd[1], "Hello, child!", 14);
        close(fd[1]); // Close writing end
    } else {  // Child process
        close(fd[1]); // Close writing end
        read(fd[0], buffer, 14);
        printf("Received: %s\n", buffer);
        close(fd[0]); // Close reading end
    }
    return 0;
}
```
- **Named Pipes (FIFOs)**
- **Message Queues**
- **Shared Memory**
- **Semaphores**
- **sockets**
- **signals**
## thread
#יצירה_thread:
ב - C יוצרים thread בעזרת השימוש בספריית ה - POSIX thread(pthread).
על ידי הפונקציה `()pthread_create`.
ל<span style="color:rgb(143, 74, 196)">דוגמה</span> יצירת thread:
```
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

void* thread_function(void* arg) {
    printf("Hello from the thread!\n");
    return NULL;
}

int main() {
    pthread_t thread;
    int result = pthread_create(&thread, NULL, thread_function, NULL);

    if (result != 0) {
        printf("Thread creation failed!\n");
        return 1;
    }

    pthread_join(thread, NULL);   // Wait for the thread to finish
    printf("Thread has finished executing.\n");

    return 0;
}
```
# יחסי פונקציות/מחלקות/משתנים
### ה - scope
ה - scope מתייחס לאיזור בתוכנית שבו משתנים ופונקציות הן ניגשות.
##### יש סוגים שונים של scopeים
- **בלוק scope**
משתנה מוגדר בתוך בלוק, סוגרים מסולסלים.
המשתנים האלו ניגשים רק מתוך הבלוק הזה ונהרסים לאחר שהבלוק נגמר.
```
void function() {
    int x = 10;  // Block scope
    {
        int y = 20;  // Block scope within nested block
    }
    // y is not accessible here
}
```
- **פונקצית scope**
תגיות <span style="color:rgb(0, 176, 240)">goto</span>, בעלי פונקצית scope.
הם נראים רק בתוך הפונקציה שהן מוגדרים.
```
void function() {
    start:  // Function scope
    printf("This is a label with function scope.\n");
    goto start;
}
```
- **קובץ scope:**
משתנים ופונקציות שמוגדרים מחוץ לכל הבלוקים בעלי קובץ scope, הם ניגשים מכל מקום מהגדרת עד סוף הקובץ.
- **תוכנית scope:**
משתנים ופונקציות בעלי קישור(linkage) של <span style="color:rgb(0, 176, 240)">external</span>, הם נגישים לכל התוכנית, מספר קבצים.
### קישור linkage
ה - linkage קובע האם השם של המשתנה או פונקציה יכול להיות משותף בין קבצים.
סוגי ה - linkage:
- **ללא קישור**
השם הוא מקומי לבלוק, ולא יכול ללפנות מחוץ לבלוק, <span style="color:rgb(0, 176, 240)">auto</span>/<span style="color:rgb(0, 176, 240)">register</span>, ו - <span style="color:rgb(0, 176, 240)">static</span> בבלוק scope.
- **קישור פנימי**
שם המשתנה נראה רק בתוך הקובץ שבו הוא מוכרז, <span style="color:rgb(0, 176, 240)">static</span> בקבצי scope.
- **קישור חיצוני**
השם נראה בכל הקבצים בתוכנית, מה שמאשר לשיתוף פונקציות ומשתנים. לא מוכרזים כ - static.
```
int globalVar = 10;  // External linkage

void globalFunction() {
    // This function is visible across all files
}
```
### אחסון מחלקות
אחסון מחלקות מגדירות את ה - scope, הנראות ואת אורך החיים של המשתנים ופונקציות בתוכו. קובע איפה משתנים התאחסנו, הערך ההתחלתי שלהם ואורך שמתשנה נמשך.
##### סוגי אחסון מחלקות
- **ה - auto:**
ה - scope: בלוק scope
אורך החיים: משך הבלוק שבו הוא מוכרז
ערך התחלתי: garbage value
מקום אחסון: מחסנית זיכרון
הקישור: ללא(משתנה מקומי)
- **ה - register:**
ה - scope:  בלוק scope
אורך החיים: אורך הבלוק שבו הוא מוכרז
ערך התחלתי: garbage value
מקום אחסון: ב - register של ה - CPU, אבל לא מובטח
הקישור: ללא(משתנה מקומי)
שימוש: משתנים שניגשים אליהם הרבה פעמיים
- **ה - static:**
ה - scope: 
	למשתנים - מקומי לבלוק אבל שומר את הערך המשתנה
	לפונקציות - מגביל את הנראות של הפונקציה
אורך החיים: האורך של התוכנית כולה
ערך התחלתי: 0
מקום אחסון: בזיכרון static או global 
הקישור: קישור פנימי לקבצי scope, ללא קישור לבלוק scope
שימוש: מונע מצב שמשתנה בין פונקציות או שמוגבל בניראות של פוקציה בקובץ אחד
- **ה - extern:**
ה - scope: תוכנית scope
אורך החיים: האורך של התוכנית כולה
ערך התחלתי: 0
אחסון: זיכרון global
קישור: קישור חיצוני
שימוש: הכרזת משתנה או פונקציה גלובלית בקובץ אחרת
# זיכרון
ב - C לכל סוג נתונים יש דרישות יישור, למעבד יהיה אורך מילת עיבד בהתאם לגודל הנתונים.
סגמנטים:
1) קוד/טקסט(הוראות)
זהו סגמנט בתוכנית של עצם הקובץ, מכיל הוראות ביצוע משמש למניעת גלישה של ה - heap/stack.
2) מידע מאותחל
מכיל משתנים גלובלים, וסטטים של התוכנית. ומחולק לשני איזורים קריאה וכתיבה ורק קריאה. המכילים משתנים מסוגים שונים(קבועים ולא קבועים).
3) מידע לא מאותחל
מאותחל על ידי ה - kernel ל - 0 לפני שהתוכנית החלה ומכיל את כל המשתני הגלובלים או הסטטים שמאותחלים ל - 0 או ללא אתחול ברור בקוד מקור.
4) ה - heap
משמש להקצאה דינאמית.
5) מחסנית
מכיל תוכנת מחסנית(LIFO), מכיל משתנים אוטומטים ומידע שנשמר אחרי כל פונקציה שנקראת(רקורסיבית). סביבת הקורא נשמרת גם(רגיסטר).
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfAc8tRjLByi_IG8rNsIcbCqgSMTbxIvaxJ37bY2vU4pmCxkCrN47Dnd4ZOjZakfo6U_2YzSMKoxOy7BOZy-q-1vHFWKMEuVFbNITKQnxcqXRPeiug9pOub5czeZy7tvCN9k89rWmXIiRtDsH2vbXp9iOfS?key=uZCsKKeBkIY9pSl-1xNO2g)
### הקצאת זיכרון דינמי
זיכרון דינמי זהו תהליך שבו גודל מבנה הנתונים משתנה בזמן ההצרה, **לוקח מקום בסגמנט של ה - heap** ה - heap מתוחזק כאוסף של בלוקים(תפוסים או חופשיים). 
יש שתי סוגי הקצאות:
- מקצה מפורש(explicit allocator) - אפליקציות יקצאו וישחררו מידע
- מקצה מרומז(implicit allocator) - אפליקציות יקצאו אבל לא ישחררו מידע.
#### פרגמנטציה:
פרגמנטציה היא מצב שבו יש מספיק מקום להקצות ב - heap, אך המקום מחולק ולא בלוקים רציפים כך שאי אפשר להקצות את המקום.
יש שתי סוגים:
##### פרגמנטציה פנימית
מתרחשת כאשר המטען קטן מהבלוק, כך שנשאר מקום מחולק נוסף.
**סיבות:**
- ה - overhead של חיזוק מבנה נתונים של ה - heap
- ריפוד(padding) למטרות יישור
- החזרה של בלוק גדול לבקשה קטנה
##### פרגמנטציה חיצונית
מתרחשת כאשר יש מספיק מקום ב - heap, אבל אין בלוק יחיד שמספיק.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfZpC8oSHFdNu7oH1o1xJ3Mkq8BTAJVXqk-c99z2sk_N3sXjNw7bvC7ajXxa-A3ceeECwhFBDgsvqcBl0A9tg5u29CRLCuSycWREI95sIQwiPVovsQnI3jQRDplVkb1bkLMkwPrTdtHguODuVPaDNGimdqk?key=uZCsKKeBkIY9pSl-1xNO2g)
#### בעיות ישום
יש מספר בעיות בשחרור מקום
- לדעת כמה בלוקים לשחרר
שימוש לבלוק קודם בשביל לשמור את האורך של הבלוק(בעזרת מצביע), שדה header.
- איזה בלוק להקצאות
- מה לעשות עם המקום שנשאר
- הסרת בלוק חופשי ל - heap
##### מעקב בלוקים
יש מספר דרכים לעקוב אחרי בלוקים(תפוסים או משוחררים)
###### ה - Implicit list
מקשרים את כל הבלוקים ב - heap, בסדר רציף. משתמשים בדגל לסימון גודל הבלוק הוספה של bit אחד עם הוא תפוס.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcH3FCi6-Am7ZPtmxHTY2VEoMz0fRMTMA2SQroeM984OO-Lw_rOxBy0j5hllGE0nd-2KWaytkNFwg49Syye1Yu4uq_FftKCL84_EJ8x2FlyNdGMSWoeC2VHr-_QkcOSv1DMvTpVIt_ytex42DLMNrQbEo8?key=uZCsKKeBkIY9pSl-1xNO2g)**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcRK9ZVnttuuGJIPF_jtZNGseNUVEhVkGgvRpTVC390_lpzTsWYEmcxtI-iqt7mAjDT3z4Wm9-fkUqAKQhO6ufE55I8xDTmagRenmKaC9PJ_YMxPYSsWSjld2LNcJmRBj295v4x7VG9Uu3vvXjFFMrJnU8?key=uZCsKKeBkIY9pSl-1xNO2g)**
**תהליך החילוק:**
חילוק כאשר מקצאים מקום שקטן מהבלוק החופשי, ולכן נחלק אותו.
```
void addblock(prt p, int len)
{
	int newSize =  ((len + 1) << 1) >> 1   //rounding to even
	int oldSize = *p & -2   //mask out low bit
	*p = newSize | 1   //setting new length + allocation
	if(newSize < oldSize)
		*(p+newSize) = oldSize - newSize   //set length in remaining part of block
}
```
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXczN2r6o6jSEWjsNpH4yx58eSQ1ixEjV7zWZf01jvSEMgf15OAnyRpfniJqtFnbO-35PHvFurhihyLu_LrRQvOvQPg2RpWY_QnuDZcS4QpOtX7Str8C7xRj2KzGFgJarP6UtoVO6CK1W3TxojzNi8jDO1g?key=uZCsKKeBkIY9pSl-1xNO2g)**
**שחרור בלוק:**
על ידי שינוי הדגל
`void free_block(ptr p){ *p = *p & -2}
**תהליך התמזגות(Coalescing):**
ממזג את הבלוק שאחרי אם שניהם חופשיים.
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfU201fGgJ_xcOXoUmCbODlWx_WXCSYM1s6Au5p0a6_eIhIS2tE4y1zzWNqyvp6GYH03Z-n7WlQ1bFglkxWYUrVfzGq2REKYCssY9nL_op8cxZbPawYlOxZmLRqG0WiC42zCxGhYLsJGZ2MaEc9IbUfJVg2?key=uZCsKKeBkIY9pSl-1xNO2g)**
מיזוג עם הבלוק שאחרי:
```
void freeBlock(ptr p)
{
	*p = *p & -2   //clearing allocated bit
	next = p + *p   //find next block
	if((*next & 1) == 0)   //check if it is free
	*p = *p + *next   // add this block if not allocated
}
```
מיזוג עם הבלוק הבא נעשה על ידי הוספה של header בסוף כל בלוק.
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfPBzP4PL-DrtZadRTks47Fhyuj4XW5Oc7zMLHL5Lw1TFpuzGMxIX6RUIJ10QvwFuLssdFiuDIG_RtC3MdcQKEMoulxhhKMk9pOpF5sa11wnKDCk7qyzPmUDt5o5m85s9PMONMVVMCCd0XFWyfYhZyUm9Ya?key=uZCsKKeBkIY9pSl-1xNO2g)**
**יתרונות וחסרונות:**
זמן הקצה של O(n)
זמן שחרור של O(2n)
לא ממולץ להקצאות גדולות, בעל פרגמנטציה גדולה
###### ה - explicit list
מקשרים את כל הבלוקים החופשיים בלבד, מכיל מצבעים של קדימה ואחורה עם גודל הבלוק. 
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeuA6W65A7dGqPrBAR3JzhjetCp-kfZRo6I-7c1TDFuOz6FoxuXOUrxnKzShZKlokkND7g-DhVv_AO1izW0nv4zdn3Chhl4r6jANurrs5c6vLWmEkgb_AbPNKVtjVCav6KTHCUgLfd6MLj7LFKgKzR6v11w?key=uZCsKKeBkIY9pSl-1xNO2g)**
**תהליך החילוק:**
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfar-o4ef369qbTGRaE39MpJ4TNQZeDkE3wpMGqOupv9F_fyr4bq95shy346pB8ZXxWF-zryRhw1GZxP4WyGiv-9-HKuX-4pFDvvLFGUPmSab9CJYbvop4opFxS0qYesMZ1NTKfcJS_ARGcpM2_0dN07W0r?key=uZCsKKeBkIY9pSl-1xNO2g)**
**שחרור בלוק:**
לפי שתי שיטות:
ה - LIFO - גורם ליותר פרגמנטציה, מכניס בלוקים חופשיים כך שהרשימה תמיד מסודרת.
בעל שלושה מצבים:
1) הכנסת בלוק משוחרר לשורש הרשמיה
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdXxm-uIrM2AZ2fJlu4X071QUtt3F5xz9Yt7c6tI4O7pfwGw6W6nMKbk8dIDopU0ul0nX7lwzApXce4wS9mf1SGkpH52ryTVwwThpZiwQOuuVRHqo6iVctJjpqQli4jWs7V-5iC6679GbgK6VIJJnpiRK4?key=uZCsKKeBkIY9pSl-1xNO2g)**
2) שחרור בלוק קודם, אחרי השחרור ממזגים את הבלוק שלפניו 
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdyjsM6fSvo4Mc0jA913z7ZD9UZy_zeoZ4o-B7d1LT2XySHS8xSWOpbOD6TnA6NTg8gCyuH6xtZwQ4UCRNSsaSgvV1kc2ktNYLgbIlGecN0EFz-OEaNrx8GBlOEpOBMW4igW-zGI2w-fvpav96lDFsTfL_U?key=uZCsKKeBkIY9pSl-1xNO2g)**
3) שחרור בלוק אחרי, אחרי השחרור ממזגים את הבלוק שאחריו
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc_CD_NuujKSBxN-1JQ7VSROTusCPivYdeD95QbJDf5gp67ikpfI0Lp2B1_DfdVU-fwt2P-pDQapZZb7OJZlcuHQmZrFi1HXYoyx_nJmDZsI4KoWVIFt81WSml3MhqxBBqSNTlWhCq1DY-GJXsNfvbCiKB0?key=uZCsKKeBkIY9pSl-1xNO2g)**
1) שחרור בלוק אמצעי, ואחרי מיזוג עם שני הבלוקים שלידו
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdtz-zaSbzmHt0J4sJgd-eWjH39P2FDMKVgjpiBQhKJfibgS6CLDWVcfmraq7s0PUCWbyZlU4uZNmBtvBGvBcXJ2dtCLVbrp7swLpEo2LyqXmMmKVau2seTXxFEBHDz5uojqHZdbraoDRePdEFvqqh6skY?key=uZCsKKeBkIY9pSl-1xNO2g)**
ה - FIFO
**יתרונות וחסרונות:**
יותר מהיר ככל שיותר זיכרון מוקצה,
צורך מקום נוסף למצביעים מה שיכול לגרום פרגנמטציה פנימית,
ממולץ לאפליקציות להגדלת ביצועים וכאשר הפגרמנטציה צריכה להיות מינימלית.
###### ה - separated free list
מכיל רשימות explicit שונות, לכל גודל בלוק.
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf2G7sSA-GWf83EET8Ut32so7CxBzlHm3zQCn_MV_rsatTilb8jo_GiS9wrlgBp-zLYfwdYPZaaNOwqRi1EqDrtKK7fT8GsVxAkHd52bgdg3N_-ERxNqZT0--OZJRox19kBIxgrGn20ptxBBHB5mdc2_eFN?key=uZCsKKeBkIY9pSl-1xNO2g)**
**תהליך הקצאה:**
- חיפוש לרשימה נכונה.
- אם נמצא בלוק ראוי, מחלקים אותו ולמקם את הפיצולים ברשמיה הנכונה
- אם לא נמצא בלוק נכון עוברים לרשימה הבאה
**תהליך השחרור:**
שחרור הבלוק, מיזוג הבלוק ולמקם אותו ברשימה הנכונה
**יתרונות וחסרונות:**
זמן הקצאה נמוךO(log(n))
אתחול מהיר, first fit שווה ל - best fit
ממומלץ לאפליקציות עם טווח גדול של הקצאות בגדלים שונים שהביצוע חשוב.
#### אוסף אשפה
אוטומטי לוקח בחזרה את המאגרים ב - heap, שאפליקציות יהיו חייבות לשחרר אותן. אוטומטי משחרר את הבלוקים שאי אפשר לבשימוש(אי אפשר להגיע אליהם).
**אלגוריתם:**
אוסף האשפה מבצע סימון ואז מטאטא, סימון של כל המצביעים שאפשר לגשת אליהם ומטאטא את הלא מסומנים.
ה - `is_ptr(p)` - קובע האם p הוא מצביע
ה - `length(p)` - מחזיר את אורך הבלוק ש - p מצביע עליו, ללא ה - header.
ה - `get_roots()` - מחזיר את כל השורשים.
סימון:
```
ptr mart(ptr p)
{
	if(!is_ptr(p)) return;   //do nothing if it is not a pointer
	if(markBitSet(p)) return;   // check if already marked
	setMarkBit(p);   //mark
	for(int i = 0; i < length(p); i++)
		mark(p[i]);
	return
}
```
מטאטא
```
ptr sweep(ptr p, ptr end)
{
	while(p < end)  //while not at the end of the heap
	{
		if(markBitSet(p))
			cleanMarkBit();  //reset mark bit
		else if(allocateBitSet(p))  //if not mark but allocated
			free(p);
		p += length(p);  //adjust pointer to the next block
}
```


# מצביעים
מצביע מאפשר שליטה ישירה בזיכרון ולנהל מבני נתונים יותר טוב.
### מצביע
מצביע זהו משתנה שמכיל כתובת זיכרון של משתנה אחר, הכרזת מצביע נעשת על ידי ה \ <span style="color:rgb(247, 43, 43)">*</span>, הגדרת כתובת של משתנה נעשת על ידי <span style="color:rgb(247, 43, 43)">&</span> .
`int a = 10;`
`int `\ <span style="color:rgb(247, 43, 43)">*</span>`p = `<span style="color:rgb(247, 43, 43)">&</span>`a;   // p now holds the address of a`
##### מציע const
מצביע קבוע, שערכם(הכתובת שמצביעים) או הערך בכתובת שהם מצביעים אליו לא יכול להשתנות בהתאם לסוג שלו.
1) מצביעים לערך קבוע:
<span style="color:rgb(247, 43, 43)">const</span>` int *ptr;
המידע הוא קבוע ולא יכול להשתנות דרך המצביע, אבל המצביע עצמו יכול להצביע לכתובת אחרת
```
int a = 10;
int b = 20;
const int *ptr = &a;
// *ptr = 30;   // Error: cannot modify data
ptr = &b;   // Allowed: can point to another address

```
2) מצביעים קבועים לערך:
`int `\ <span style="color:rgb(247, 43, 43)"><span style="color:rgb(0, 176, 240)">*</span>const</span>` ptr;
המצביע הוא קבוע ולא יכול להצביע לכתובת אחרת, אבל הערך בכתובת יכול להשתנות
```
int a = 10;
int *const ptr = &a;
*ptr = 30;   // Allowed: can modify data
// ptr = &b; // Error: cannot point to another address
```
3) מצביעים קבועים לערכים קבועים:
<span style="color:rgb(247, 43, 43)">const</span> `int` \  <span style="color:rgb(0, 176, 240)">*</span><span style="color:rgb(247, 43, 43)">const</span> `ptr;
### מערכים ומצביעים
שם המערך פועל כצביע לאלמנט הראשון במערך.
```
int arr[3] = {1, 2, 3};
int *p = arr;   // p points to arr[0]
int first = *p;   // first is 1
int second = *(p+1);   // second is 2
```
### מצביעים ל - struct
מצביעים ל - struct, שימושיים להקצה דיינמית של struct, והעברתם לפונקציות. ונוצר שימוש בחץ <span style="color:rgb(247, 43, 43)">-></span> בשביל לקבוע ל - member.
### מצביעים למצביעים
מצביע למצביע שומר את הכתובת של המצביע האחר.
```
int a = 10;
int *p = &a;
int **pp = &p;
int value = **pp;   // value is 10
```
### מצביע לפונקציה
מצביע לפונקציה שומר את הכתובת של הפונקציה, מה שמאפשר לקריאה של פונקציות.
`void `<span style="color:rgb(0, 176, 80)">func</span>()` {`
    `printf("Hello, World!\n");`
`}`
`void `(\ <span style="color:rgb(247, 43, 43)">*</span><span style="font-style:italic; color:rgb(0, 176, 80)">fptr</span>)<span style="color:rgb(0, 176, 240)">()</span>` = `<span style="color:rgb(247, 43, 43)">&</span><span style="color:rgb(0, 176, 80)">func</span>`;`
<span style="color:rgb(0, 176, 80)">fptr</span>`(); // Calls func`
##### קריאה חוזרת לפונקציות(callback function)
מצביעי פונקצית יכולים לעבור כ - argument, שמחזיר את תוצאת הפונקציה.
ל<span style="color:rgb(143, 74, 196)">דוגמה</span> קריאה חוזרת:
```
#include <stdio.h>

void greet() {
    printf("Hello, World!\n");
}

int main() {
    // Declare a function pointer
    void (*fptr)() = greet;

    // Call the function using the pointer
    fptr();

    return 0;
}
```
# פיתרון שגיאות(debugging)
### טיפול בשגיאות
- **החזרת קוד:**
פונקציות מחזירות קוד מיוחד להכזרת שגיאה, לרוב החזרת קוד כולל מצביע ל - NULL, למספרים 0 או 1- או שגיאות מותאמות אישית
- **ה - errno ו - perror:** 
	ה - errno
משתנה גלובלי שנקבע על ידי קריאות המערכת, ופונקציות של ספריות. כאשר שגיאיה קוראת הוא מספק קוד שגיאה שמאשר להבין את אופי השגיאה.
	 ה - perror
מדפיס טקסט קריא שמגיב לערך של ה - errno
ל<span style="color:rgb(143, 74, 196)">דוגמה</span> errno ו - perror:
```
FILE *file = fopen("nonexistent.txt", "r");
if (!file) {
    perror("Error opening file");
    exit(EXIT_FAILURE);
}
```
- **פונקציות מותאמות לטיפול בשגיאות:**
פונקציה מותאמת אישית לטיפול בשגיאות שמכנסות רישומים, ניקוי משאבים, ודווח שגיאות
לדוגמה:
```
void handle_error(const char *msg) {
    perror(msg);
    // Additional logging or cleanup
    exit(EXIT_FAILURE);
}
```
- **קביעות(assert):**
הפונקציה `()assert` בודקת הנחיות שנעשו על ידי התוכנית, ועוזר לתפוס שגיאות לוגיות, כאשר הביטוי בתוך הפונקציה שלילי, התוכנית מדפיסה הודעת שגיאה.
`assert(pointer != NULL);
- **ה - longjmp ו - setjmp:**
הן פונקציות לקפיצות לא מקומיות, מה שמאשר עקיפה את קריאות פונקציה הרגילות ורצף החזרה
ה - setjmp שומר את המצב הנוככי של תוכנית וה - longjmp משחזר את המצב.
```
#include <setjmp.h>

jmp_buf buf;

void func() {
    longjmp(buf, 1);   // Jump back to where setjmp was called
}

int main() {
    if (setjmp(buf)) {
        printf("Error caught!\n");
    } else {
        func();
    }
    return 0;
}
```
### ניפוי באגים
- **קומפיילר אזהרות ודגלים:**
הקומפיילר משתמש באזהרות ודגלים לניפוי באגים לתפיסת שגיאות שיכולות לקרות, בזמן קומפילציה.
- **ה - GDB:**
ה - GDB מאפשר לך להיכנס לקוד לראות משתנים, לקבוע נקודות שבירה, ו - backtrace קריאת פונקציות.
פקודות:
`gdb ./program`: Start GDB with the compiled program.
`break main`: Set a breakpoint at the `main` function.
`run`:מתחיל להריץ את התוכנית
`next`: נכנס לשורת הקוד הבאה.
`print var`: מדפיס את ערך המשתנה.
`backtrace`: Display the call stack.
`continue`: Continue running the program until the next breakpoint.
- ה - valgrind:
זהו כלי לגלות נזילת זכרון, השחתת זיכרון, ובעיות זיכרון נוספות
`valgrind --leak-check=full ./program

- רישומים:
מיישם רישומים באפליקציה לעקוב אחרי זרם ההרצה ומצב המשתנים.
### כליים מתקדמים
- **ה - strace:**
זהו כלי אבחון שעוקב אחרי קראיות מערכת, ו - signalים שמתקבלים על ידי המעבד, מאפשר הבנה בין התוכנית למערכת ההפעלה.
- **ה - ltrace:**
עוקב אחרי קריאות של ספריות שנעשות על ידי התוכנית, מראה איזה פונקציות משומשות ועם איזה ארגומנטים.
# רשתות
התקשורת ברשת ב - C נעשת בעזרת socketים.
##### תהליך בתכנות socket
1) יצירת socket, פונקצית <span style="color:rgb(0, 176, 240)">()socket</span>
2) קישור socket הגדרת כתובת IP ומספר port, פונקצית <span style="color:rgb(0, 176, 240)">()bind</span>
3) הקשבה, פונקצית<span style="color:rgb(0, 176, 240)"> ()listen</span>
4) אישור החיבור, פונקצית <span style="color:rgb(0, 176, 240)">()accept</span>
5) שליחת וקבלת מידע, פונקציות <span style="color:rgb(0, 176, 240)">()send</span> ו - <span style="color:rgb(0, 176, 240)">()recv </span>בשביל TCP, ובשביל UDP יש <span style="color:rgb(0, 176, 240)">()sendto</span> ו - <span style="color:rgb(0, 176, 240)">()recvfrom</span>
6) סיגרה, פנוקצית <span style="color:rgb(0, 176, 240)">()close</span>
ל<span style="color:rgb(143, 74, 196)">דוגמה </span>שרת TCP:
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>
#include <arpa/inet.h>

int main() {
    int server_socket, client_socket;
    struct sockaddr_in server_addr, client_addr;
    char buffer[1024];
    socklen_t addr_size;
    
    // 1. Creating a socket
    server_socket = socket(AF_INET, SOCK_STREAM, 0);
    if (server_socket < 0) {
        perror("Socket creation failed");
        exit(EXIT_FAILURE);
    }
    
    // 2. Binding the socket
    server_addr.sin_family = AF_INET;
    server_addr.sin_port = htons(8080);
    server_addr.sin_addr.s_addr = INADDR_ANY;
    
    if (bind(server_socket, (struct sockaddr*)&server_addr, sizeof(server_addr)) < 0) {
        perror("Bind failed");
        close(server_socket);
        exit(EXIT_FAILURE);
    }
    
    // 3. Listening for connections
    if (listen(server_socket, 5) < 0) {
        perror("Listen failed");
        close(server_socket);
        exit(EXIT_FAILURE);
    }
    printf("Server listening on port 8080...\n");
    
    // 4. Accepting a connection
    addr_size = sizeof(client_addr);
    client_socket = accept(server_socket, (struct sockaddr*)&client_addr, &addr_size);
    if (client_socket < 0) {
        perror("Accept failed");
        close(server_socket);
        exit(EXIT_FAILURE);
    }
    printf("Connection accepted...\n");
    
    // 5. Receiving and sending data
    recv(client_socket, buffer, sizeof(buffer), 0);
    printf("Received message: %s\n", buffer);
    send(client_socket, "Hello from server", strlen("Hello from server"), 0);
    
    // 6. Closing the socket
    close(client_socket);
    close(server_socket);
    
    return 0;
}
```
ל<span style="color:rgb(143, 74, 196)">דוגמה</span> לקוח:
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>
#include <arpa/inet.h>

int main() {
    int client_socket;
    struct sockaddr_in server_addr;
    char buffer[1024];
    
    // 1. Creating a socket
    client_socket = socket(AF_INET, SOCK_STREAM, 0);
    if (client_socket < 0) {
        perror("Socket creation failed");
        exit(EXIT_FAILURE);
    }
    
    // 2. Specifying the server address
    server_addr.sin_family = AF_INET;
    server_addr.sin_port = htons(8080);
    server_addr.sin_addr.s_addr = inet_addr("127.0.0.1");
    
    // 3. Connecting to the server
    if (connect(client_socket, (struct sockaddr*)&server_addr, sizeof(server_addr)) < 0) {
        perror("Connection failed");
        close(client_socket);
        exit(EXIT_FAILURE);
    }
    printf("Connected to server...\n");
    
    // 4. Sending and receiving data
    send(client_socket, "Hello from client", strlen("Hello from client"), 0);
    recv(client_socket, buffer, sizeof(buffer), 0);
    printf("Received message: %s\n", buffer);
    
    // 5. Closing the socket
    close(client_socket);
    
    return 0;
}
```


