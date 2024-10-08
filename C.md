
- [x] Multithreading and Concurrency
- [x] argc and argv
- [ ] template
- [x] networking programming
- [x] Inter-process Communication (IPC)
- [ ] Embedded Systems Programming
- [ ] Compiler Design and Implementation
- [x] Signal Handling
- [x] Error Handling and Debugging
- [x] \ *Concurrency and Parallelism
- [x] **Security in C Programming**: Writing secure code, understanding buffer overflows, input validation, and other security considerations.
- [ ] Real-time Systems: Writing C code for real-time operating systems (RTOS), understanding real-time constraints, and scheduling.
- [ ] **Advanced Algorithms**: Implementing and understanding complex algorithms for sorting, searching, graph traversal, dynamic programming, etc.
# פקודות:

##### ה - process
fork() 
מפצל את ה - process לשני processים, אחד כילד
wait()
תהליך ממתין עד ש - process הילד שלו מסיים
getpid() 
מחזיר את ה - ID של ה - process
getppid() 
מחזיר את ה - ID של process האב
###### ה - thread
pthread_self()
מחזיר את ה -ID של ה - thread, שה - API מנהל
gettid()
מחזיר את ה - ID **הפנימי** של ה - thread, של מערכת ההפעלה
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
# ה - UNIX process
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
###### exec()
משפחת פונקציות המחליפות את ה - process image באחרת, כל הפונקציות טוענות את תוכנית החדשה לזיכרון של ה - process העכשוי.
פונקציות(l -> list, v -> array, p -> path, e -> environment(set of variables))
`execl(const char *path, const char *arg, ..., NULL)`
טוען תוכנית חדשה דרך ה - path המצווין, רשימת הארגומנטים נגמרת ב - NULL.
`execle(const char *path, const char *arg, ..., NULL, char *const envp[])`
כמו `()execl` אבל ארגומנטים עוברים דרך מערך של מצביעים למחרוזת

 `execlp()`
 מחפש תוכנות שיכולות לרוץ בתיקיה של ה - path
`execv()`
`execve()`
`execvp()`
כאשר <span style="color:rgb(251, 136, 4)">ה - exec הצליח התוכנית לא תמשיך בהרצה</span>
ל<span style="color:rgb(169, 80, 237)">דוגמה של execl</span>:
```
#include <stdio.h>
#include <unistd.h>

int main() {
    printf("Before exec\n");

    // Replacing the current process with the "ls" command
    execl("/bin/ls", "ls", "-l", (char *)NULL);

    // If exec is successful, this line is never reached
    printf("After exec\n");

    return 0;
}
```
##### לחכות לסיום process
פונקצית `()wait` מאפשר ל - process האב לחכות עד שה אחד ה - process ילד יסיים לרוץ.
כאשר <span style="color:rgb(251, 136, 4)"> process ילד מצבע את הפעולה `()wait` הוא ייעצר לגמרי בגלל שאין לו ילד</span>
הפונקציה מקבלת פרמטר של מצביע(מספרי) של מצב ה - process ילד. ומחזיר את ה - PID של הילד שסיים את התהליך. <span style="color:rgb(251, 136, 4)">כאשר ל - process יש מספר ילדים הוא יחכה ויחזיר כאשר אחד מהילד סיים את התהליך.</span>
פונקצית `()waitpid` גרסה יותר ספציפית של `()wait`, מאפשר ל - process האב לחכות ל - process ילד מסויים,  המקבל את מספר ה - pid, כאשר שווה ל 1- הוא מתנהג כמו `()wait` כאשר שווה ל 0 הוא מחכה לכל process באותה קבוצה של הקורא לפונקציה.
ה - status של ה - process, ואופציה שמגדירה את ההתנהגות של הפונקציה, WNOHANG מחזיר מיד אם אין ילדים.
### תקשורת בין תהליכים(IPC)
זהו מנגנון שמאפשר ל - processים לתקשר ביניהם, משומש לרוב במערכות הפעלה שה - processים חולקים מידע או מסתנרכים  את פעילותם.
בגלל של processים יש מקום זיכרון שונה הם לא יכולים לגשת ישירות לזיכרון של אחר.
מנגנונים:
###### צינורות(pipes)
מאפשר למידע לזרום בכיוון אחד בין שני processים לרוב ילד ואב.
הכולל חוצץ שאפשר לקרוא ולכתוב בו.
לפתיחת צינור משתמשים בפונקצית `()pipe` שלוח מערך עם שני אלנמטים, שכל אלנמט משמש כמתארי הצינור כקצה של הצינור. האלמנט הראשון הוא הקורא, השני הוא הכותב
מתאר צינור זהו מפתח שמאפשר גישה למקום שרוצים לקרוא/לכתוב בו.
אחרי פתיחת הצינור אפשר לפצל את ה - processים `()fork`, שמתארי הצינור יגדירו את ה - process הילד שנוצר(מורשים), <span style="color:rgb(251, 136, 4)">המתארים הם עצמאים זה מזה</span>.
בכתיבת/שליחת <span style="color:rgb(251, 136, 4)">מחרוזת/מערך שולחים גם את אורך המערך, במחרוזת שולחים את האורך פלוס אחד(NULL).</span>
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
###### Named Pipes (FIFOs)
ליצירת קובץ FIFO מתשמשים בפונקציה `()mkfifo`, שלוקח את ה - path של הקובץ שנוצר, bit רשות(מי יכול לגשת למה בקובץ).
הפונקציה מחזירה 0 או 1-, כאשר errno שונה מ - EEXIST יש בעיה אחרת.
פתיחת הקובץ נעשת בעזרת הפונקציה `()open`, שלוקח פרמטרים של של הקובץ, ודגל הפתיחה(איזה מטרה יפתח הקובץ) לכתיבה `O_WRONLY`,<span style="color:rgb(245, 131, 0)">מחזיר את המתאר של הקובץ</span>, מה שמאפשר לשימוש כמו צינור רגיל. <span style="color:rgb(245, 131, 0)">פעולת הפתיחה חוסת את הקובץ עד ש - process אחר פותח את הקובץ מדגל פתיחה מסוג אחר</span>
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/stat.h>

int main() {
    const char *fifo_name = "/tmp/my_fifo";
    char buffer[20];

    // Create a named pipe (FIFO)
    mkfifo(fifo_name, 0666);

    if (fork() > 0) {   // Parent process
        int fd = open(fifo_name, O_WRONLY);
        write(fd, "Hello, FIFO!", 13);
        close(fd);
    } else {   // Child process
        int fd = open(fifo_name, O_RDONLY);
        read(fd, buffer, 13);
        printf("Received: %s\n", buffer);
        close(fd);
    }

    unlink(fifo_name);   // Remove the FIFO
    return 0;
}
```
###### ה - Message Queues
מאפשר ל - processים להחליף הודעות בתור, הודעות נשמרות בתור עד שמקבלים שה - process שמקבל אותן מחזיר אותן.
```
#include <stdio.h>
#include <stdlib.h>
#include <sys/ipc.h>
#include <sys/msg.h>

// Message structure
struct msg_buffer {
    long msg_type;
    char msg_text[100];
} message;

int main() {
    key_t key;
    int msgid;

    // Generate unique key
    key = ftok("progfile", 65);

    // Create message queue and return ID
    msgid = msgget(key, 0666 | IPC_CREAT);

    if (fork() > 0) {   // Parent process
        message.msg_type = 1;
        sprintf(message.msg_text, "Hello, Message Queue!");
        msgsnd(msgid, &message, sizeof(message), 0);
        printf("Message sent: %s\n", message.msg_text);
    } else {   // Child process
        msgrcv(msgid, &message, sizeof(message), 1, 0);
        printf("Message received: %s\n", message.msg_text);
    }

    msgctl(msgid, IPC_RMID, NULL);   // Destroy the message queue
    return 0;
}
```
###### ה - Shared Memory
מאפשר למספר processים לגשת לאותו מרחב זיכרון, בדרך יותר מהירה אך שדורשת סנכרון ומניעת התנגשויות
```
#include <stdio.h>
#include <stdlib.h>
#include <sys/ipc.h>
#include <sys/shm.h>

int main() {
    key_t key = ftok("shmfile", 65);
    int shmid = shmget(key, 1024, 0666 | IPC_CREAT);
    char *str = (char *)shmat(shmid, (void *)0, 0);

    if (fork() > 0) {   // Parent process
        sprintf(str, "Hello, Shared Memory!");
        printf("Data written: %s\n", str);
        wait(NULL); // Wait for the child process
    } else {   // Child process
        sleep(1);   // Ensure parent writes first
        printf("Data read: %s\n", str);
        shmdt(str);
        shmctl(shmid, IPC_RMID, NULL);   // Destroy the shared memory
    }

    return 0;
}
```
######ה - semphores
משומשים לסנכרון processים, לרוב דרך שילוב זיכרון משותף, מוודא ש - process אחד ניגש לחלק חשוב בזמן מסויים.
```
#include <stdio.h>
#include <stdlib.h>
#include <sys/ipc.h>
#include <sys/sem.h>

void sem_wait(int semid) {
    struct sembuf op = {0, -1, 0};
    semop(semid, &op, 1);
}

void sem_signal(int semid) {
    struct sembuf op = {0, 1, 0};
    semop(semid, &op, 1);
}

int main() {
    key_t key = ftok("semfile", 65);
    int semid = semget(key, 1, 0666 | IPC_CREAT);
    semctl(semid, 0, SETVAL, 1);

    if (fork() > 0) {   // Parent process
        sem_wait(semid);
        printf("Parent is in critical section\n");
        sleep(2);
        printf("Parent leaving critical section\n");
        sem_signal(semid);
    } else {   // Child process
        sem_wait(semid);
        printf("Child is in critical section\n");
        sleep(2);
        printf("Child leaving critical section\n");
        sem_signal(semid);
    }

    semctl(semid, 0, IPC_RMID);   // Remove semaphore set
    return 0;
}
```
###### ה - sockets
מאפשר דרך ל - processים לתקשר ביניהם דרך הרשת באותו מכשיר, השימוש בפרוטוקולים של TCP/IP ו - UDP.
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

int main() {
    int server_fd, new_socket;
    struct sockaddr_in address;
    int addrlen = sizeof(address);
    char buffer[1024] = {0};
    const char *hello = "Hello from server";

    if ((server_fd = socket(AF_INET, SOCK_STREAM, 0)) == 0) {
        perror("socket failed");
        exit(EXIT_FAILURE);
    }

    address.sin_family = AF_INET;
    address.sin_addr.s_addr = INADDR_ANY;
    address.sin_port = htons(8080);

    bind(server_fd, (struct sockaddr *)&address, sizeof(address));
    listen(server_fd, 3);

    if ((new_socket = accept(server_fd, (struct sockaddr *)&address, (socklen_t *)&addrlen)) < 0) {
        perror("accept");
        exit(EXIT_FAILURE);
    }

    read(new_socket, buffer, 1024);
    printf("Message received: %s\n", buffer);
    send(new_socket, hello, strlen(hello), 0);
    printf("Hello message sent\n");

    return 0;
}
```

 
## thread
ה - threadים מאפשרים ביצוע של חלקים מהתוכנה, כמו פונקציה.
ל<span style="color:rgb(245, 131, 0)">פני יצירת ה - thread צריך להגדיר מקום(משתנה) שבו ה - API שומר מידע על ה - thread</span>
ה - threadים משתפים את המשאבים שלהן, כך שמהשתנים משותפים
##### יצירה thread
ב - C יוצרים thread בעזרת השימוש בספריית ה - POSIX thread(pthread).
על ידי הפונקציה `()pthread_create`, פרמטרים:
מציע למקום שה - API שומר מידע
יחס ה - thread
כתובת הפונקציה שה - thread יבצע.
מצביע לארגומנט המשומש בפונקציה, <span style="color:rgb(245, 131, 0)">כאשר יוצרים כתובת לארגומנט הוא יכול להשתנות בזמן הרצת ה - thread בעיקר כאשר יש הרבה threadים, עדיף להקצות מקום ולשחרר אותו בסוף הפונקציה.</span>
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
    pthread_t thread;   //הגדרת מקום לשמירת מידע
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
##### לחכות לסיום thread
אפשר לחכות ל - thread בעזרת הפונקציה `()pthread_join`, המקבלת את המקום ששומר מידע על ה - thread ומה שפקודות ה - thread מחזירות.
הפונקציה גם מאפשר לקבל את את המצביע שהפונקציה שה - thread מבצע, בעזרת מצביע למצביע של void.
הערך <span style="color:rgb(245, 131, 0)">שמוחזר הוא מקומי שנשמר ב - stack segment, ובגלל זה צריך להקצות מקום ב - heap. </span>
לדוגמה <span style="color:rgb(169, 80, 237)">של קבלת הערך מפונקציה של thread:</span>
```
void* thread_function(void* arg) {
    int num = 10;
    int* ptr = malloc(sizeof(int));   //להקצות מקום
    *ptr = num;
    return (void*) ptr;
}

int main() {
	int* num;
	pthread_t t;
	pthread_create(&thread, NULL, thread_function, NULL);
	pthreat_join(t,(void**) num);
}
```
#####  ניתוק thread
הפונקציה `;(threadName&)pthread_detach` מנתקת את ה - thread מה thread הראשי.
ה - thread המנותק לא יכול להצטרף בחזרה.
משתמשים בזה כאשר יש threadים שעדיין רצים אבל ה - thread הראשי לא צריך להמשיך לרוץ.
חשוב לסיים את ה - thread הראשי עם הפקודה `;()pthread_exit`.
אפשר ליצור thread כמנתוק בעזרת הפונקציה `;()pthread_create` דרך השימוש בפרמטר השני.
מתשמשים<span style="color:rgb(245, 131, 0)"> בדרך הזאת כאשר ה - thread סיים את ההרצה שלו לפני שנותק ולא הצטרף בחזרה.</span> 
```
pthread_att_t detachedThread;   //יצירת משתנה
pthread_att_init(&detachedThread);   //אתחול המשתנה
pthread_att_destroy(&detachedThread);
pthread_att_setdetachedstate(&detachedThread, PTHREAD_CREATE_DETACHED);   //מצב מנותק
pthread_create(&threadName,&detachedThread,&function,NULL);
```

## ה - multithreading
[[Linux#multithreading]]
דרך להקבלה על ידי יצירת מספר threadים באותו process, כל thread חולק את מרחב הזיכרון של thread אחר באותו process.
מה שיכול לגרום ל - <span style="color:rgb(245, 131, 0)">race condition</span> שבו שני threadים ניגשים לאותו משאב זיכרון באותו הזמן וישבשו את משאב הזיכרון.
ביצירת<span style="color:rgb(245, 131, 0)"> threadים בלולאה, צריך לחלק את יצירת ה - thread ולחכות ל - thread להסתיים לשתי לולאות שונות</span>
הפקודה `;()pthread_exit` דומה לפונקצית return, אבל כאשר משתמשים בה ב - thread הראשי(process) יסיים את ההרצה שלו, אבל יחכה עד שכל ה - threadים שיצר לסיים את ההרצה שלהן.
### סנכרון
בשביל למנוע ששני threadים ישתמשו באותו מידע יש מספר מנגנונים:
 ##### ה - mutex
נועל את המשאב כך שרק thread אחד יכול לגשת אליו באותו הזמן, כך שהפקודות בין הנעילה לפתיחה יבצעו רק על ידי thread אחד באותו הזמן בשביל למנוע race condition.
פקודות:
```
pthread_mutex_t mutexName;   //יצירת מוטקס
pthread_mutex_init(&mutexName,NULL);   //מאתחל את המוטקס
pthread_mutex_destroy(&mutexName);   //סוגר/הורס את המוטקס
pthread_mutex_lock(&mutexName);
pthread_mutex_trylock(&mutexName);   //ינסה לנעול את המשאב
pthread_mutex_unlock(&mutexName);
```
הפקודה `;()pthread_mutex_trylock` מנסה לנעול את המשאב, אם אין thread שמצבע את הפקודות והמשאב ננעל אז ה - thread האחר יעבור הלאה, כאשר מהפוקדה נועלת היא מחזירה 0.
###### ה - mutex רקורסיבי:
מאפשר שימוש של אותו mutex באותו thread מספר פעמיים מבלי שיקרה deadlock.
ה <span style="color:rgb(245, 131, 0)">- mutex יכול להינעל ולהפתח רק על ידי אותו thread.</span>
על ידי שינוי היחס של ה - mutex:
```
pthread_mutexattr_t recursiveMutexAttr;
pthread_mutexattr_init(&recursiveMutexAttr);
pthread_mutexattr_destroy(&recursiveMutexAttr);
pthread_mutexattr_settype(&recursiveMutexAttr, PTHREAD_MUTEX_RECURSIVE);
pthread_mutex_init(&mutexName,&recursiveMutexAttr);
```

 ###### ה - condition variables
- משתני מצב:
חוסמים thread מסויים עד שמצב מסויים קורה. משתף פעולה עם ה - mutex לסנכרון על ידי נעילת threadים עד מצב מסויים.
ה - threadים מחכים עד מצב מסויים ומודעים כאשר המשתנה השתנה.
משתמש בין הפקודות שה - mutex.
פקודות:
```
pthread_mutex_t condName;   //יצירת תנאי משתנה
pthread_cond_init(&condName,NULL);   //מאתחל את תנאי המשתנה
pthread_cond_destroy(&condName);   //סוגר/הורס את תנאי המשתנה
pthread_cond_wait(&condName,&mutexName);
pthread_cond_singnal(&condName);
```
הפקודה `;()pthread_cond_singal` מסמן רק ל - thread אחד לבדוק את משתנה התנאי עוד פעם, <span style="color:rgb(245, 131, 0)">לפי העדיפויות של ה - threadים.</span>.
הפקודה `;()pthread_cond_signal`  משדר סימון לכל ה - threadים המחכים, לבדוק באותו הזמן את משתנה התנאי
###### ה - deadlocks
זהו מצב שבו מספר threadים לא יכולים להתקדם בגלל שהם מחכים למשאב ש - thread אחרי נועל שלא יכול שחרר אותו.
סיטואציות:
- מחזיק ומחכה
מצב ש - thread מחזיק משאב אחד ומחכה למשאב אחר בזמן שהוא נעול ולא משחרר את המשאב שלו.
- המתנה מעגלית
מספר threadים מחכים אחד לשני בצורה מעגלית, שכל thread נועל משאב מסויים שה - thread האחר צריך בשביל לשחרר את המשאב שלו
דרכי התמודדות:
- מחזיק ומחכה
דרישה מה - thread לקבל את כל המשאב בפעם אחת
- המתנה מעגלית
לתקף סדר שבוא המשאבים יקובלו.
##### ה - semaphores
שולט בגישה למשאב מ - threadים רבים, יותר גמיש מ - mutexes, מאפשר הגבלה למספר threadים מסויים לגשת למשאב כאשר שאר ה - threadים מחכים.
מאפשר גם לכל ה - threadים לעשות `post` כאשר thread מבלי שתיהיה לו הגישה למשאב.
```
#include <semaphore.h>

sem_t semaphore;
sem_init(&semaphore, 0, 1);
sem_destroy(&semaphore);
sem_wait(&semaphore);
sem_post(&semaphore);
```
הפקודה שמהתחלת את ה - semaphore מקבלת עוד שני פרמטרים, דגל להאם יש הרבה processים(0 יש רק אחד, 1 יש יותר מאחד). והערך ההתחלתי של ה - semaphore.
הפקודה `;()sem_wait` בודקת את ערך ה - semaphore, כאשר הוא 0 ולא יכול לרדת יותר אז ה - thread ימתין על ה - semaphore. כאשר הערך גדול מ - 0. הוא יוריד את הערך באחד ויתחיל להריץ. 
הפקודה `;()sem_post` מגדיל את ערך ה - semaphore באחד.
הפקודה `;sem_getvalue(&semaphore,varToStore)` מאחסנת את ערך ה -semaphore במשתנה, אבל הערך יכול להשתנות מ - race condition. ולא יהיה הערך הנכון.

##### מחסום(barrier)
עוצר את ההרצה של threadים גורם להם לחכות לעצם של ה - barrier ואז באותו הזמן מאפשר ל - threadים לעבור.
אותו thread יכול החכות באותו barrier מספר פעמיים אחרי שעבר אותו כל פעם.
```
pthread_barrier_t barrierName;
pthread_barrier_init(&barrierName, NULL, numOfThreads);
pthread_barrier_destroy(&barrierName);
pthread_barrier_wait(&barrierName);
```
ברכת threadים
זאת דרך בהקבלת תכנות, לניהול threadים עובדים לביצוע מספר משימות במקביל במקום יצירת threadים נוספים כל פעם שצריך לבצע משימה.
מאפשר דרך שימוש **חוזר** של threadים קיימים, חוסך את היצירה והריסת threadים נוספים.
מאפיינים:
- יצירת הברכת threadים:
מאותחל עם מספר קבוע של threadים, שנוצרים בהתחלה ונשארים עד שמוקצים למשימה.
- תור משימות:
משמש להחזקת משימות שצריכות להיעבד על ידי ה - threadים בברכה, כאשר משימה הסתיימה הוא לוקח משימה נוספת המתור.
- ה - threadים העובדים:
ה - threadים בבריכה נקראים ה - threadים העובדים, שמחכים באופן רציץ למשימות להיות זמינות בתור.  אחר כך ה - thread בוחר במשימה, מבצא אותה וחוזר להמתין למשימה הבאה.
##### החלפת קשר(context switching)
בלינוקס ה - CPU מחליף בין threadים או processים,
## ה - signals
ה - signals משמשים לשליחת הודעה ל - process/thread בשביל לידע אותו לגבי אירוע.
##### שליחת signalים
שליחת signal נעשת על ידי הפונקציה `()kill`, ל - process או קבוצת processים.
`int kill(int pid, int sig);
ה - pid זהו ה - ID של איזה process ישלח לו ה - signal.
כאשר שווה ל 0 הוא ישלח לכל ה - processים באותו הקבוצה של השולח
כאשר שווה ל 1- הוא ישלח לכל ה - processים שלשולח יש גישה לשלוח להם
דוגמה <span style="color:rgb(143, 74, 196)">לשליחת SIGTERM, ל - PID מסויים:</span>
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <signal.h>

int main(int argc, char *argv[]) {
    if (argc != 2) {
        fprintf(stderr, "Usage: %s <pid>\n", argv[0]);
        exit(EXIT_FAILURE);
    }

    pid_t pid = atoi(argv[1]);

    // Send SIGTERM signal to the specified process
    if (kill(pid, SIGTERM) == -1) {
        perror("kill");
        exit(EXIT_FAILURE);
    }

    printf("SIGTERM signal sent to process %d\n", pid);
    return 0;
}
```
##### ה - handle signals
###### פונקציית ()sigaction
מאפשר שליטה נוסף על הטיפול ב - process, כגון חסימת signalים אחרים, ושחזור פעולות קודמות.
משתמש ב - struct, שבתוכו מתואר הטיפול ב - signalים. בעל איבר שמכיל את הפונקציה שב - signal שמתקבל ותטפל בו`sa_handler`.
פונקצית `()sigaction` לוקחת את מספר ה - signal, הפנייה ל - structure, ואם יש sigaction ישן הוא יהיה הפרמטר השלישי.
דוגמה של הפונקציה ()sigaction:
```
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>

// Signal handler function
void handle_signal(int signal) {
    printf("Caught signal %d\n", signal);
    exit(1);   // Exit the program
}

int main() {
    struct sigaction sa;

    // Specify the signal handler
    sa.sa_handler = handle_signal;

    // Block all other signals during the execution of the handler
    sigfillset(&sa.sa_mask);

    // No special flags
    sa.sa_flags = 0;

    // Register the handler
    sigaction(SIGINT, &sa, NULL);

    // Infinite loop to keep the program running
    while (1) {
        printf("Running...\n");
        sleep(1);
    }

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
#### פרגמנטציה
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
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfPBzP4PL-DrtZadRTks47Fhyuj4XW5Oc7zMLHL5Lw1TFpuzGMxIX6RUIJ10QvwFuLssdFiuDIG_RtC3MdcQKEMoulxhhKMk9pOpF5sa11wnKDCk7qyzPmUDt5o5m85s9PMONMVVMCCd0XFWyfYhZyUm9Ya?key=uZCsKKeBkIY9pSl-1xNO2g)
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
# ה - command line arguments
ה - arguments הם הדברים שעוברים ל - command line כאשר הקוד מתבצע,
- ה - argc:
ה - argc(arguments count), סופר את כמות האלמנטים במערך argv(מערך של מחרוזות) 
- ה - argv:
ה - argv(arguments vectors), זהו מערך של 
# בטיחות
### הצפת מאגר(buffer overflow)
כאשר מידע עולה על המקום זיכרון המוקצה, דבר שיכול לגרום ל - overwrite של הזיכרון הסמוך לו.
מניעות:
- בדיקת מידע
לבדוק שהמידע שנכנס מתאים לגודל המאגר המוקצה
- אפשרות ביטחות מהקומפיילר
שימוש במנגוני ביטחון של מחסנית(stack Guard), מה שיכול לאבחן ולמנוע הצפת מאגר
שגיאות:
- integer overflow
- dangling pointers
- memory leaks
- multiple thread access the same shared recourses
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
