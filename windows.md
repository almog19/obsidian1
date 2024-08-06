- [x] ini
- [x] %SYSTEMROOT%
- [ ] file management system
- [x] host
- [ ] PowerShell
- [x] DLL
- [ ] net framework
**

   # כלי דיאגנוסטיקה Sysinternals
### ה - Registry ותוכנת ה - RegEDIT
ה - Registry הוא מאגר נתונים של מערכת הפעלה, המכיל אוסף של שדות וערכים. לכל שדה יש את הערך המתאים לו. 
ה - Registry מכיל הגדרות של תוכנות ושל מערכת ההפעלה(הגדרות גרפיקה, התקני חומרה, אבטה ועוד).
ה - RegEDIT היא תוכנה נסתרת המשמשת לצפייה ועריכה של ה - Registry.
מאגר המידע של ה Registry נטען לזיכרון RAM, בזמן שהמחשב נדלק ומערכת ההפעלה עולה.![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd6o3whwbRY1aCGm5uGWKYU6GoNMC9RuNz2CeT0Qv0DCJHxnvBKsvLw7LFLR9TSsd_tJS_NfyoTTbEdMnN0RWW7CbrniNqcYRJLtGMPVOm1CQEGtJngfB5OBtod6N10lHRmzvNSfgzSw7WqpBFzrQKiB_wg?key=l1EqxwgEJ5BV0y_UVeAong)
הוא מחולק לענפים שונים:
- ה - HKEY_CURRENT_USER(HKCU):
ה HKCU מכיל הגדרות ספציפיות למשתמש שמחובר כרגע(אייקונים, תמונת רקע,גודל פונטים ועוד)

- ה - (HKEY_LOCAL_MACHINE(HKLM:
מכיל הגדרות המשותפות לכל המשתתפים של המחשב.(התקני חומרה שהמחשב מחובר, המיקום של הדיסקים שאפשר לקרוא קצבים, הסיסמאות של המשתמשים השונים והרשאות).
### תוכנת Process explorer:
התוכנה process explorer מאפשר לנו לקבל מבט מעמיק על כל מה שהמחשב מריץ כרגע.
###### תצוגת processes:
מאפשר תצוגה של כל ה processing שרצים כרגע על המחשב.
כל שורה בצבע אחר, מסמן משהו.
הכלי מציג את אחוז ה - (CPU(central processing unit וכמות ה PHYSICAL MEMORY, ה CPU מראה עד כמה המעבד עמוס.
ה- PHYSICAL MEMORY מודד בכמה זיכרון מסוג (RAM(RANDOM ACCESS MEMORY, זיכרון מהיר שלא נשמר בין כיבוי המחשב. שהמחשב משתמש כרגע.
בתצוגת ה PROCESSES יש מספר עמודות:
- ה - process שם הקובץ
- ה - CPU - אחוז CPU
- ה - private bytes - כמות זיכרון מערכת הפעלה מקדישה ל process, לא כולל זיכרון מערכת הפעלה שטפה את ה processes האחרים.
- ה - working set - כמות הזיכרון ב RAM של process יכול לגשת
- ה - PID מספר ה - process
- ה - description
- ה - company name
##### חיסול  processes:
בעזרת האפשרות KILL PROCESS אפשר לסגור את התהליך.
ה - process explorer מאפשר לבדוק אילו תוכנות שעושות שימוש במשאב מסוים,(DLL).
### תוכנת Procmon:
ה - Process monitor, יומן אירועים של כל מה שמתבצע במחשב שלו(יכולות חיפוש וסינון). ומקבלים נתונים על כל EVENT במחשב:
- שעה
- שם process
- ה - PID
- סוג operation
- ה - path, הדרך של ה OPERATION פועל עליו, פתיחת קובץ, לאיזה ענף ברגיסטר בוצעה גישה.
- ה - result האם הפעולה הצליחה או לא

מציאת המיקום של ההגדרות בריגסטר:
1. לערוך פיטר(CTRL + L) לשנות PROCESS NAME.
2. בדיקת רק האירועים נשמרות ב REGISTRY, ולהתחיל להבטל אירועי רגיסטר שלא קשורים.
# תפקידי מערכת ההפעלה
### תהליכים Processes:
ה processים מחבר בין שלושת המרכיבים הדרושים להרצת תוכנה(קוד, זיכרון, מעבד). כל תוכנה מורכבת משורות קוד, השמורות באזורים שונים של הזיכרון. בשביל שתוכנה תופעל השורות האלו יהיו מורצות על ידי המעבד, ואזורי התוכנה צריכים להיות נגישים למעבד.
כל תוכנה שרצה עושה זאת בעזרת processים.
לדוגמה: הרצת דפדפן chrome, יפתח process שמטפל בכרום, מכיל זיכרון הנדרש לכרום, שומר את שורות הקוד של הכרום, ומקבל זמן ריצה של המעביד עבור הכרום.

כאשר process רוצה להגיע למשאב כלשהו, הוא יבצע Syscall.

ה - process, מכיל את כל המשאבים המשותפים לכל ה threads של אותה תוכנה, אין ל - process אפשרות להריץ קוד בעצמו וחייב לפחות thread אחד להריץ קוד. לכל process שנפתח הוא חולק את האוסף משאבים שלו עם ה threads שיש לו.

כל process מקבל מקום שחולק אותו עם ה threads, ומקבלים את רמת העדיפות של ה process, לכל process יש רמת אבטחה security number,
###### תהליך ה - Multi processes:
למספר רב של prcessים, יש מרחב זיכרון שונה.
##### Services/daemons(LINUX):
ה - Service הוא סוג מיוחד של process בעל שלושה מאפיינים:
1. מופעל אוטומטי על ידי מערכת ההפעלה
2. מנעול על ידי מערכת ההפעלה
3. אין לו UI, רץ מאחורי הקלעים
הניהול של ה - serviceים מתבצע בעזרת process בשם SCM(service control manager) הדואג להפעיל אוטומטי את ה - serviceים, להחזיק מידע על הסטטוס של ה - serviceים ולהעביר מידע אליו וממנו.
ה - service רץ כל הזמן ויכול להגיב לאירועים שאי אפשר לדעת מתי יקרו.
ה - SVCHOST הוא process שמכיל את service. 
כל SERVICE מסתיים ב - dll, קבצי DLL, המיעודים להרצה על ידי process המריצים דברים שונים.
### Threads:
ה - threadים זהו רצף של פקודות מבצעות משימה אחת,  לדוגמה אוסף כל הפקודות של תוכנה הוא thread.
##### Multi threads

בשביל לאפשר לכל thread להעביר את הפקודות שלו בזמן אחר, משתמשים ברכיב תזמון schedule, הוא מעניק את מושאבי העיבוד לכל thread בזמן אחר.
**דברים המשותפים על כל ה threadים של אותו process:**
- כתובת זיכרון:
כל ה - threadים רואים את אותם ערכים באותן כתובות זיכרון.
- זיכרון HEAP:
לכל ה threadים יש זיכרון אחיד של HEAP אחד,  כאשר thread מקצה זיכרון כל שאר ה threadם מקבלים גישה לאותו זיכרון.
- קוד הרצה
כל ה threadים רצים מאותו איזור זיכרון, הקוד נמצא במקום אחיד וכל thread מריץ את שורות הקוד שהוא צריך מבלי להעתיק את הקוד שוב ושוב.
- משתנים גלובליים וסטטיים:
הם חולקים את אותו אזור זיכרון ב - DATA SEGMENT.

**דברים הייחודים לכל thread:**
- רגיסטר:
כאשר מחליפים threadים צריך להחליף ערכים ברגיסטר.
- מצביע קוד:
כאשר מחליפים רגיסטר שאחרי להצביע על הפקדת קוד הבאה, הצביע גם יוחלף.
- המחסנית:
- משתנים לוקליים:
### ה - Drivers:
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfXAkZdepYYY2bNqAqhCsjSEzmtU4baX-2dQv0vpOLMrlqfoDJz_Xoc1rmtwrkZsfLt8tY5yuWUoVfqHGnml21PXfg56-hr0aMra3UykWCa5fkpEww6oF0Ft0vHUbpbk0jQnmf6RnsgO8om_P83M28stToJ?key=l1EqxwgEJ5BV0y_UVeAong)

ה - driverים אחראים על העברת מידע בין התקני החומרה(עכבר,מקלדת) למערכת ההפעלה.
יצרן החומרה מספקים את ה driverם, הם נכתבים פונקציות מיוחדות שמערכת ההפעלה חושבת עליהם. רמת ההרשאות שלהן גבוהות.
ה - driverים רצים מאחורי הקלעים אוטומטי ללא פקודה מפורשת של המשתמש.
ב - WINDOWS/LINUX DRIVERS רצים ב - kernels
פרצות אבטחה ב - driverים:
ב-  WINDOWS כל מי שרוצה לפתוח DRIVER יכול לעשות זאת, כאשר הDRIVER לא מבקש אישור WHQL, כל DRIVER שלא מבקש אישור מסוכן למשתמש.
### תפקידי הגישור של מערכת ההפעלה:
מערכת ההפעלה מגשרת בין התוכנות שמשתמשים מריצים לבין 4 גורמים:
- מעבד
- זיכרון
- מערכת הקבצים
- התקני חומרה
##### מעבד
המחשב תמיד מריץ יותר מתוכנית אחת, חלוקת המשאבים בין ה processים הכרחית,
התפקיד הראשון של מערכת ההפעלה היא לקבוע איזה process יקבל את המשאבי המעבד בזמן ששאר ה - processים יחכו לתורם.
##### זיכרון:
בשביל להריץ process של תוכנה צריך לטעון את הקוד לזיכרון, תוכנות נשמרות אוטומטי על הדיסק הקשיח, תהליך טעינת הזיכרון מתבצע על ידי מערכת ההפעלה. רוב הפעמים לכל ה - processים אין מספיק מקום בזיכרון המהיר, ומערכת ההפעלה גם דואגת לחלוקת משאבי הזיכרון בנוסף להקצאה.
מערכת ההפעלה דואג גם לאבטחה, היא דואגת שכל processים כותב רק לאזור הזיכרון שהוקצה לו. 
##### מערכת קבצים:
מערכת ההפעלה קובעת שיטה שבא הקבצים יסתדרו, ואיפה כל קובץ מתחיל ונגמר.
##### התקני חומרה:
מערכת ההפעלה בקשר עם כל ה driverים, דואגת להעברה של מידע מהם ואליהם. היא גם דואגת לעדיפויות בין driverים שונים.
# זיכרון:
### זיכרון פיזי:
זיכרון פיזי הוא חומרה מותקנת המאפשרת שמירה של רצפים בינארים(USB, דיסק קשיח). תוכנות מחשב רצות מתוך זיכרון של RAM.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcZN_ZNR4NQfEUu4px1qWAZ7fJ4cQXga_GtNuUV0XRWZJQdDwIkvcQa_1lRusFQLtMXNTiS541aZRyUUP2VD_BR1dLuzwv9O03EoIfZ8vM2HDDrTx1cpsplq2Sk8TFsUoIw9cymu01rASF2_hMOJMuH79Ad?key=l1EqxwgEJ5BV0y_UVeAong)
יש 3 דברים הנדרשים מזיכרון:
- מהירות זמן גישה, של המעבד לזיכרון(חשוב לזמן ריצת התוכניות).
- גודל
- יציבות, מידע שנשמר בזיכרון גם כאשר המכשיר לא מקבל חשמל.
אין סוג זיכרון טוב מכל הדברים הנדרשים, ולכן משלבים בין סוגי זיכרון.
תפקיד מערכת ההפעלה היא לנהל בצורה יעילה את משאבי הזיכרון שיש לה.
**דיסק קשיח:**
במקרה של דיסק קשיח, מערכת ההפעלה מפעילה DRIVER, שמביא כל פעם בלוק(4 ביתים) של ידע מהדיסק הקשיח.
אי אפשר להריץ תוכניות ישירות מהדיסק הקשיח בגלל שאין לו גישה לזיכרון רק לבלוק.
**ה - RAM:**
גודלו של ה RAM קטן ביחס לדיסק הקשיח, והזיכרון שלו נמחק ברגע שהמחשב נכבה. המעבד יכול לגשת באופן ישיר ל RAM.
ה - cache:
ה - cache נמצא קרוב למעבד. חולק ה cache לשלוש אזורים, L1,L2,L3. כש L1 הכי מהיר וקטן. פעולה שהמעבד לוקח מידע מה cache נקרא cache hit, אחר זה cache miss. 
מציאת גודל cache:
`wmic cpu get L1CACHE
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfu_0yPV1bZPU4zzlnECL6_qXtCSr2TWVD1OZT6-8m41wQzsDk5nGNatzpKemWHrTyRXcvtSlWm1TlCqcqsYHtVfW7sKgsfuACWfIxhJeIhVIfoeRmPV21j6rNN42ckvRSnD4QgNWc5CSvP36xUErWml6p5?key=l1EqxwgEJ5BV0y_UVeAong)
##### כתובת לוגית:
כתובת לוגית מחולקת ל - <span style="color:rgb(0, 176, 240)">segment</span> ו - <span style="color:rgb(0, 176, 240)">offset</span>.
### זיכרון וירטואלי:
מרחב זיכרון של process נמצא ב RAM.
לכל process יש מרחב זיכרון.
זיכרון וירטואלי מאפשר להתגבר על מספר בעיות:
- כאשר ה RAM קטן מדי להכיל את המרחב של ה - process,
- מניעת ה - process להגיע לכתובות זיכרון פיזיות של process אחר.
כאשר process פונה לכתובת לינארית זאת תהיה כתובת וירטואלית(לא אמיתית) רק דרך מנגנון של תרגום כתובות אפשר להפוך אותה לאמיתית.
המנגנון של מבצע את ההחלפה בסוגי הזיכרונות הוא PAGING
מרחב כתובות וירטואלים נראים ככה:
לכל process מצובע תרגום שונה, בין הכתובות מה שמאפשר שלנו processים של אותה כתובת וירטואלית.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd9rvep9YxDrHQEbMcxI8RgMDkA4dfS-BCunn9q2Nc_GrA4XfNNoDkNqfbrPh64SnrmLtquhlrXjemXlDvy1Iu2Yc0OfeJ1C676mXdexr0lhrCLyR4yUjHyJsqV5kOqoxy2BebSURmFyDi32JM990rImXY?key=l1EqxwgEJ5BV0y_UVeAong)

רכיב הממיר את הכתובות נקרא <span style="color:rgb(0, 176, 240)">MMU</span>(memory management unit). ה - CPU מעביר כתובת כשהוא נפגש בה ל - MMU.
## PAGING:
ה - MMU מחלק את הזיכרון הפיזי חלקים, כל חלק נקרא PAGE FRAME. כל חלק יכול להיות בגודל שונה(חזקות של 2)(בדרך כלל בגודל של 4K). כל PAGE FRAME מקבל <span style="color:rgb(0, 176, 240)">PFN</span>(PAGE FRAME NUMBER).![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcbU1Vro8dy14IhCvLO2buTGW5U0h8XwgUsijPdhWoh7NWZFbblfX3dCyVoau13JGtBnlm3o3etItDhwwB8Du4OXv6aEBS9XS_i_s4YEJ46TiiUBC2ppb2ddoHnHj1K5sAxLbFBX4n_o43KlsDka0Bkzpd1?key=l1EqxwgEJ5BV0y_UVeAong)
ה - MMU משתמש בטבלה:
אחר כך מחלק את כתובות שני חלקים, חלק ראשון המשמש להכנסת המקום הנכון בטבלה, וחלק שני המשמש לכמות הביתים שצריכים להוסיף מתחילה ה - PAGE FRAME כדי להגיע לכתובת המבוקשת.![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcKV19BirqiZaSO5wo5rJ57NX276ZrbYIVMzimb638ljC2HUR3Wxo-QogvqKLfccalUoXzgKw6MIsRl_Nuor4salp8LY_eA5Oh2qqXr9DqhaAUhpJO9Wa-K5hZXXA3aYQEUXaeWMNyiOdZ-7QcurUZeYnKT?key=l1EqxwgEJ5BV0y_UVeAong)
האינדקס של הטבלה ייצוג כ- <span style="color:rgb(0, 176, 240)">PTE</span>
## שיטת החילוק PAGE DIRECTORY:  
ויתרו על כ 20 ביט המבטאים את ה PTE(האינדקס של המיקום בטבלה). ולכן נחלק את הטבלה של ה PAGE להרבה טבלאות, מה שמאפשר לנו ליצור ל - process חדש PAGE TABLE קטן,  מערכת ההפעלה צריכה לדעת באיזה PAGE TABLE מדובר בשביל לפענח את כתובת ה PTE, ולא להפנות שני processים לאותו מרחב זיכרון.![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfYI-XBAXgd5sLirJa0HReJd4beBA-KWMgXXzRJlRhqFpvMxXqvC1lmq3uMii4wQbcxBvvAl05vlpcZg7w7EbTMefDmv4F7T67cq4fuuFDlRC4Je4KYHcgBUq0IInU4MJOn6qPAzOkZi1LYsTAiiG48Azhz?key=l1EqxwgEJ5BV0y_UVeAong)
אחרי שמרחב מתורגם מוירטואלי לפיזי, הוא נדחף ל - CACHE, ובפעם הבאה קוראים לזיכרון מסתכלים ב - TLB רק ל גודל ה PAGE.
## Page fault:
כאשר ה - PAGE FRAME לא נמצא ב RAM פעולה זאת נקראת PAGE FAULT(גורם לבזבוז זמן).
מקרה כזה קורה בכמה מקריים:
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcXtLkLIgTFaUEyczG6S9G6H68nn4ouwFB0D8a-5vgqyXlUsk7Z3pRhOYg_3IAnb11sbdyt53eBpaDwde42MMPqd6ISZlcclrO-POJuvEOO-XdGbvDNcJKLFLubmEio91JZKLyYt3hJZUQKYawgMd91Hiw?key=l1EqxwgEJ5BV0y_UVeAong)
1. כאשר חלק מה - PTE לא ממופים ל PTF, ולא מצביע על מיקום ב RAM, ה PROCESS לא מודע בכך ועדיין מבקש שנמצאת.
2. התוכנה מנסה לגשת למרחב בזיכרון שלא מורשה לגשת אליו.
# קבצים:
# %SYSTEMROOT%
ה - %SYSTEMROOT% הוא משתנה סביבתי שפונה ל - directory שבוא מערכת ההפעלה מותקנת, בדרך כלל ל <span style="color:rgb(25, 133, 74)">C:\Windows</span>. 
מאפיינים:
- שימוש:
לרוב משומש ב - scripts, command lines, קבצעי הגדרות להתייחס ל - directory של windows בדרך בלתי תלויה במערכת.
- גישה:
אפשר לגשת לערך דרך הפקודה <span style="color:rgb(0, 176, 240)">echo</span>.
- תתספריות:
ה - "%SYSTEMROOT%\\System32", מכיל קבצי מערכת והפעלה.
ה - "%SYSTEMROOT%\\SysWOW64", מכיל קבצי מערכת של 32 bit, בהתקנה של 64 bit.
ה - "%SYSTEMROOT%\\TENP", מכיל קבצים זמניים
### INI:
קבצי INI, אלא קבצעי טקסט שמשמשים להגדרות ב - windows ובאפליקציות אחרות. כגון: העדפות משתמש, פרטי חיבור הנתונים, ואפשריות ספציפיות של אפליקציות.
**מבנה:**
- סעיפים (sections):
קבצי INI מחולקים לסיעיפים, כל סעיף מתחיל עם שם הסעיף שבתוך בסוגרים מרובעים \ <span style="color:rgb(223, 58, 58)">[ ]</span>.
* מתפחות וערכים:
בכל סעיף הגדרות מוגדרות על ידי key-value-pair. 
- תגובות:
תגובות כלולות בקבצים מתחילות ב <span style="color:rgb(223, 58, 58)">;</span> או על ידי hash <span style="color:rgb(223, 58, 58)">#</span>, אפליקציות מתעלמות מתגובות.
### DLL:
קובץ DLL כולל פונקציות שונות, שמאפשר לתוכנות אחרות להשתמש בהן,
קבצי DLL(dynamic link libraries) מכילים קוד, מידע, משאבים שאפליקציות יכולות להשתמש בהן בו זמנית ב - windows. 
**מבנה ומטרה:**
- קוד ומשאבים משותפים:
קבצי DLL מכנסים אוסף של שגרות משאבים שאפליקציות יכולות להשתמש, עוזרים למודולירציה באפליקיות על ידי חילוק פונקציות משותפיות לספריות משותפיות.
- יתרונות:
מאפשר למספר תוכניות להשתמש באותו קוד ומשאבים ללא טעינת עותקים לזיכרון. 
מאפשר עדכון לחלקים באפליקציות בלי הצורך לקמפל מחדש או הפצה מחדש של האפליקציה.
**תהליך:**
- פנקיות מיוצאות(exported):
קבצי DLL מכילים פונקציחות מיוצאות, שאפליקציות יכולות לקרוא להן. הפונקציות האלו מוכרזות ב - DLL, ומוגדרות בדרך שמאפשר לתוכניות לאתר אותן ולהשתמש בהן.
- קישור דינמי:
קישור דינמי בזמן הטעינה - האפליקציה מקושרת ל - DLL בזמן קומפילציה, כאשר האפליקציה מתחילה מערכת ההפעלה טוענת את קבצי ה - DLL.
- קישור דינמי בזמן הרצה - כאשר האפליקציה בברור טוענת ופורקת את ה - DLL.
### hosts
קובץ ה - hosts משמש למפות hostname לכתובות IP, מתפקד כ DNS מקומי.
# WinAPI
ה - API - APPLICATION PROGRAMMING INTERFACE מאפשר למתכנתים לגשת לתוכנה שגורם אחר פיתח.
ה - WinAPI - זו היא דרך מתכנתי WINDOWS מאפשרים לתוכנה חיצונית לפנות ל KERNEL ולבקש ממנו שירותים.
כל מתחנת יכול להיכנס ולבדוק פונקציות קיימות, WinAPI לא פונה ישירות ל KERNEL, אלא קורא קודם כל לפונקציות מתוך (ntdll(NativeAPI,
# PowerShell
