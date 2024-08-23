- [x] package management
- [x] text processing
- [ ] system programming with c
- [x] Concurrency and Multithreading
- [x] processes and threads
- [ ] kernel programming
- [ ] file system advanced(custom file system using FUSE)
- [ ] security
- [ ] Performance Tuning and Monitoring
# פקודות
##### טקסט:
##### process & thread:
ps/top
strace
עוקב אחרי system call שנעשות על ידי ה - process
gdb
מנפה שגיאות, שבודק ושולט בביצוע של processים ו - threadים
###### משפחת ()exec


# שירות terminal

# ניהול package
# עיבוד טקסט
משומש בשביל לעבד, ניתוח, בעזרת פקודות:
<span style="color:rgb(223, 58, 58)">awk</span>
מאפשר סריקה ועיבוד טקסטים
<span style="color:rgb(223, 58, 58)">sed</span> 

דפוס אותיות:
כל אות יחידה -> .
אפס מופעים או יותר מהאות הקודמת -> *
התחלה של שורה -> ^
סוף של שורה -> $
# תהליכים
### ה - processים
[[c#UNIX process]]
ל - process יש שתי סוגים לרוץ:
- חזית, כאשר התהליך מקבל input ומציג על המסך
- מאחורי הקלעים, כאשר התהליך רץ ברקע ללא input 
סוגי תהליכים:
- אבא ובן
ה - process יכול ליצור עוד process, דרך השימוש בפונקצית `()fork`. ש process הילד הוא עתק של process האב, הילד מקבל ערך של 0 מהפונקציה, והאב מקבל את ה - PID של הילד מהפונקציה.
לכל process יש אב חוץ מ - init או systemd. 
הילד יורש מהאב מספר דברים, סביבת משתנים, מתארי קבצים, והעדיפויות.
- יתום
כאשר תהליך האב מפסיק/נעצר לפני שתהליך הבן הפסיק ה PID שלו יהיה של ה - init.
- זומבי כאשר process של ילד מפסיק, המצב יציא שלו נשאר בטבלת ה - processים עד שהאב קורא את זה. ומזמן את הפונקציה `()wait`.
- ה - daemon
תהליכים עם הרשאות של ה ROOT, לרוב רצים ברקע מחכים ל PROCESSים.
##### תקשורת בין תהליכים(IPC)
[[c#UNIX process#תקשורת בין תהליכים(IPC)]]
##### ה - daemon
זהו תהליך רקע, לכל process יש daemon. לתהליך של daemon יש את האות d בסוף השם.
###### ה - systemd
ה - systemd אחראי על ה - daemonים, וגם המתחל הראשי של המערכת(init).
אפשר להשתמש ב - <span style="color:rgb(0, 176, 240)">systemctl</span> לשליטת daemonים:
`systemctl option daemonName`
##### ה - process schedule
מנגנון של ה - kernel שבו קובע איזה process ירוץ בזמן מסויים ועם אילו עדיפויות.
**טכניקות:**
- קביעת הוגנת(CFS) שבו המטרה לתת לכל process או thread זמן הוגן.
- קביעת זמן אמת, שבו משימות העלי עדיפות גבוההות יותר נקבעות, 
לפי FIFO שבו המשימות עם עדיפויות גבוהות רצות עד של מסתיימות, או עד שיש משימה עם עדיפות יותר גבוהה.
או לפי RR(round robin), כמו FIFO אבל עם פריסות זמן, שמאפשר למשימות עם אותן סדר עדיפויות לרוץ גם.
###### עדיפויות וערך nice
עדיפות סטטית משתמש לקביעת זמן אמת, מ 1 עד 99 ככל שיותר גבוהה כך יותר עדיף.
עדיפות דינאמית משמש ל - process רגיל, לפי ערך nice מ - 20- ל - 19, ככל שיותר נמוך כך יותר עדיף.
איזון טעינה, ה - schedule גם מאזן את העומס ההעבודה על פני מספר רב של CPU.
##### סימונים signals:
סימונים הן דרך לתקשר בין kernel מערכת ההפעלה ול - process, הם נשלחים מה - kernel ליידע את ה - process לגבי אירוע. וה - process יכול להגיב/לחסום/להתעלם מהסימון.
sigkill(kill - 9), משמש לעצירת תהליכים, מבלי לתת להם זמן לשמירת מצב ולא יכול להתעלם ממנו
sigterm(kill - 15) משמש לעצירת תהליכים, ומאשר זמן לשמירת מצב או האפשרות להתעלם
`signalType -signalNum PIDNum
`kill -15 4193
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcND_hFIzbkeYelYVZgttyIQ3kMyO-2elVWHxJO55rcW3rI3S0BsuemxszEfCXRaMM7Sqlzmu0-LyRe5lGnB2oyIluUGLXbJkPhVtHNzOeidjIlSufkpSH11dJed1fqspWuwtmQn-v2YNJUB_Cr-6FSP9c?key=K78lYRAqjyzdkRYM8UeOAQ)
### ה - threadים
[[C#thread]]
יחידה בסיסית של הרצה, מכיל מספר דברים:
- ה - thread id
- סופר תוכנית
- ה - register set
- מחסנית
ה - threadים שייכים לאותו process חולקים את מחלקת הקוד, מחקלת המידע, משאבי מערכת הפעלה(פתיחת קבצים, וסימונים).
**יצירה:**
ה - thread נוצר כמו בשפה C, אבל עם היכולת לחשיבות ספציפית:
- **קישור ספריות:**
בזמן קומפילציה של תוכנה המשתמש ב POSIX thread, צריך לקשר לסיפריה pthread דרך השימוש בדגל ``pthread-`.
- **יחסי threadים:**
- **רמת kernel:**
רמת המשתמש שווה לרמת kernel thread, כלומר ה - thread מתנהלים על ידי ה - kernel מה שגורם להם להיות יותר "כבדים".
- **פונקציות:**
ה - `()clone` משמש ליצירת thread עם שליטה עדינה במשאבים משותפים.
ה - `()gettid` משמש לקבלת ה - ID של ה - thread
- **ביטול threadים:**
הפקודה `()pthread_cancel` מאפשר ל - thread אחד לבקש סיום של thread אחר.
- **הגנת threadים:**
## הקבלת תהליכים
### concurrency
הקבלת תהליכים זאת היכולת של מערכת לקדם מספר משימות בו זמנית.
דרכי מימוש:
- ה - processים, שימוש בקריאת מערכת של `()fork` ליצירת מספר processים.
- ה - threadים, שימוש במספר threadים לביצוע חלקים שונים על ידי הפונקציה `()pthread_create`
- אסיכנרוני I/O, לאתחל פעולת I/O, ולהמשיך להריץ דברים אחרים בזמן המתנה לפעולת I/O להסתיים.[[input & output#אסינכרוני I/O]]
#### multithreading
[[C#ה - multithreading]]
##### סנכרון
בשביל למנוע ששני threadים ישתמשו באותו מידע יש מספר מנגנונים:
 ###### ה - mutex
[[C#ה - mutex]]
###### ה - semaphores
[[C#ה - semaphores]]
#### Parallelism
מכיל הרצה של מספר משימות באותו הזמן, דבר הדורש מספר processים או ליבות, ב - parallelism משימות רצות באותו הזמן על ידי מעבדים שונים. כלומר שכל process או thread בעל מקום זיכרון משלו ולא ניגשים למשתנים של אחרים.
בניגוד ל - concurrency שכל ה - threadים או processים ניגשים לאותו מקום בזיכרון, לאותו משתנים.
דרכי מימוש:
- מערכת מרובת ליבות
במערכת הזאת מספר threadים רצים על ליבות שונות.
- ה - openMP
זהו מודל תכנות מקביל המספק הוראות להקביל קוד.
