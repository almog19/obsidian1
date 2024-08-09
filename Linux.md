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
##### תהליכים ו - thread:
ps/top
strace
עוקב אחרי system call שנעשות על ידי ה - process
gdb
מנפה שגיאות, שבודק ושולט בביצוע של processים ו - threadים
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
### ה - processים:

ל - process יש שתי סוגים לרוץ:
- חזית, כאשר התהליך מקבל input ומציג על המסך
- מאחורי הקלעים, כאשר התהליך רץ ברקע ללא input 
סוגי תהליכים:
- אבא ובן
לכל process של משתמש יש process אב.
- יתום
כאשר תהליך האב מפסיק/נעצר לפני שתהליך הבן הפסיק ה PPID שלו יהיה של ה - init.
- ה - daemon
תהליכים עם הרשאות של ה ROOT, לרוב רצים ברקע מחכים ל PROCESSים
##### ה - daemon:
זהו תהליך רקע, לכל process יש daemon. לתהליך של daemon יש את האות d בסוף השם.
###### ה - systemd
ה - systemd אחראי על ה - daemonים, וגם המתחל הראשי של המערכת(init).
אפשר להשתמש ב - <span style="color:rgb(0, 176, 240)">systemctl</span> לשליטת daemonים:
`systemctl option daemonName`
###### ה - process schedule:
מנגנון 
### ה - threadים:
יחידה בסיסית של הרצה, מכיל מספר דברים:
- ה - thread id
- סופר תוכנית
- ה - register set
- מחסנית
ה - threadים שייכים לאותו process חולקים את מחלקת הקוד, מחקלת המידע, משאבי מערכת הפעלה(פתיחת קבצים, וסימונים).
##### סימונים signals:
סימונים הן דרך לתקשר בין kernel מערכת ההפעלה ול - process, הם נשלחים מה - kernel ליידע את ה - process לגבי אירוע. וה - process יכול להגיב/לחסום/להתעלם מהסימון.
sigkill(kill - 9), משמש לעצירת תהליכים, מבלי לתת להם זמן לשמירת מצב ולא יכול להתעלם ממנו
sigterm(kill - 15) משמש לעצירת תהליכים, ומאשר זמן לשמירת מצב או האפשרות להתעלם
`signalType -signalNum PIDNum
`kill -15 4193
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcND_hFIzbkeYelYVZgttyIQ3kMyO-2elVWHxJO55rcW3rI3S0BsuemxszEfCXRaMM7Sqlzmu0-LyRe5lGnB2oyIluUGLXbJkPhVtHNzOeidjIlSufkpSH11dJed1fqspWuwtmQn-v2YNJUB_Cr-6FSP9c?key=K78lYRAqjyzdkRYM8UeOAQ)
### הקבלה ו - multithreading
הקבלת תהליכים זאת היכולת של מערכת לבצע מספר משימות באותו הזמן.
לינוקס משתמש ב - system call של ()fork בשביל ליצור process חדש
לינוקס משתמש בספריית pthread לייצירת thread, בפונקציה `()pthread_create`.
##### סנכרון:
בשביל למנוע ששני threadים ישתמשו באותו מידע יש מספר מנגנונים:
- **הדרה הדדית(mutexes):**
נועל את המשאב כך שרק thread אחד יכול לגשת אליו באותו הזמן.
פקודות:
```
pthread_mutex_lock()
pthread_mutex_unloc()
```
- **ה - Semaphores:**
שולט בגישה למשאב מ - threadים רבים, יותר גמיש מ - mutexes אבל גם יותר מסובך
- משתני מצב:
חוסמים thread מסויים עד שמצב מסויים קורה.
פקודות:
```
pthread_cond_wait()
pthread_cond_singnal()
```
##### החלפת קשר(context switching):
בלינוקס ה - CPU מחליף בין threadים או processים,