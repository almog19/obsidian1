כתובת IP - internet protocol,  מחולק ל - section של מספרים, כל קבוצה נקראת octets. ה octets הראשונה מתשמתש כשורש והאחרונה משתמש כ - broadcasting.
קבוצות כתובת IP:

| שם  | טווח      | sub mask      | subnet    | host       | תיאור                    |
| --- | --------- | ------------- | --------- | ---------- | ------------------------ |
| A   | 1 - 126   | 255.0.0.0     | 126       | 16,777,214 | הרבה מארחים לרשתות       |
| B   | 128 - 191 | 255.255.0.0   | 16,384    | 65,534     | הרבה מארחים לרשתות       |
| C   | 192 - 223 | 255.255.255.0 | 2,097,152 | 254        | הרבה רשתות עם פחות מאחים |
| D   | 224 - 239 |               |           |            | שידור רב                 |
| E   | 240 - 254 |               |           |            | נסיוני                   |
**כתובת IP פרטית**
כתובות IP פרטיים הם כתובות שמאפשרים למכשירים להיות מחוברים לרשת מבלי חיבור ישיר לרשת,  כתובות פרטיות לא יכול לגשת לאינטרנט ישירות, מאפשר רשת יותר בטוחה למכשירים
### מכשירים:
**מכשיר switch**
מכשיר רשת שמחובר למכישרים אחרים ב - LAN, המשתמש בכתובת MAC להעביר מידע ליעד המכשיר.
כאשר מכשיר שולח frame מידע,  ה switch מקבל אותו באחד מה portים שלו, בודק את ה frame מוציא את מקור ה MAC, שומר את הכתובת במאגר ה mac table/CAM שלו לפעם הבאה, CAM זאת טבלה שמשייכת כלובת MAC ל - port.
שליחת ה frame:
* אם הכתובת היעד נמצא ב CAM, ה switch שולח את ה frame ל - port שמקושר לכתובת ה MAC.
- כאשר כתובת היעד לא נמצא ב - CAM, נשלח שידור broadcast לכל המכשירים שמחוברים ל - switch, המכשיר בעל הכתובת MAC הנכונה שולח frame בחזרה, וה - switch מוסיף אותו ל CAM.
### סוגי רשתות:
 - **רשת מקומית LAN:**
ה - LAN - local area network, זאת רשת המחוברת מכשירים, באיזור גאוגרפי מוגבל. משומש להעביר מידע ומשאבים בין מכשירים אחרים. 
מכילים router, switch, נקודות גישה ואת המכשירים המחוברים לשרת. ובעלי טופולוגיה פיזית או ווירטואלית.
*  **רשת ווירטואלית מקומית VLAN:**
ה - VLAN - virtual local area networkזאת תת קבוצה לוגית, מתוך רשת פיזית גדולה יותר, נוצר על ידי חילוק מכשיר הגדרת מכשיר אינטרנט, ה - VLAN מאפשר מכשירים להתנהג כאילו הם באותה רשת מקומית, למרות שהם לא מחוברים זה לזה פיזית.
הוא מחלק את הרשת ומפחית את ה - broadcasting domain, 
מאפשר ל - administrator לחלק את הרשתות לא לפי מיקום פיזי ולחלק switch למספר switchים ווירטואלים,
מחולק לפי portים/ כתובת mac/ פרוטוקולים.
ומוסים תיוג לכל מכשיר לפי קבוצת ה - VLAN שלו ב ethernet frame.
* **רשת רחבה WAN:**
ה - WAN - wide area network, זה רשת תקשורת, מורחבת באזור גיאוגרפי גדול, המשמשת לחיבור רשתות קטנות אחרות. בדרך כלל רשת מקומית LAN, ששני הרשתות יוכלו לתקשר.
משתמש בשיטות שונות לחבר אתרים, VPN, חיבור אינטרנט ציבורי, חיבור לווניי ועוד…
![[Pasted image 20240729215959.png#center|550]]
- **רשת ווירטואלית פרטית VPN:**
ה - VPN - virtual private network יוצרת רשת בטוחה, ומוצפנת יותר מאשר הרשת אחרת, הרשת הווירטואלית מספקת למשתמשים לגשת לאירגוני רשת מרחוק.
-  אינטרנט תחתי Metro Ethernet:
מספק חיבור אינטרנט באיזור עירוני, דרך תשתיות.
- החלפת תוויות רבי פרוטוקולים MPLS:
ה - MPLS - multiprotocol label switching, זאת טכניקה לעברת מידע בביצוע מהיר לתקשורת בין רשתות, מכוון מידע מרשת אחת לאחרת לפי הדרך ה - labels הכי קצרים ולא לפני כתובות IP ומבלי לחפש ב - routing table.

### תהליך ה - routing:
**ה - router:**
ה - router הוא מכשיר רשת מחבר הרבה רשתות, ומכוון חבילות מידע בין הרשתות, המכשיר משתמש בכתובות IP לעברת חבילות ליעד, קובע את הדרך הכי טובה שבא החבילה תעבור, ורושם מידע ב routing table.
**ה - routing table**:
ה - routing table זהו מבנה נתונים ש routerים ומכשירי רשת משתמשים בשביל להקבוע את הדרך הכי טובה להעביר packet ליעד שלהם, זה מכיל דרכים שמפרטים יעדי רשת שונים. כל כניסה ב routing table מספק מידע על איך להגיע ליעד ספציפי.
ה - <span style="color:rgb(143, 75, 195)">router, משתמש ב routing table לקבוע לאיזה router הוא ישלח את (packet(hop</span>
מאפיינים:
- יעד כתובת IP
הכתובת IP של יעד הרשת/שרת
- ה - Subnet mask
מראה את ה subnet mask
- הקפיצה הבא
הכתובת של ה IP של ה router או gateway, שה - packet יעבור.
- הממשק interface
הממשק הרשת שדרכו ה packet תעבור
- ה - Metrics
ערך המציין את העלות של הדרך הזאת.
- סוג route
המקור של המידע של הדרך, סטטי/דינמי/ישיר.
תהליך:
1. ה - router בודק את כתובת ה IP של היעד של ה packet שהגיע.
2. ה - router מתייעץ עם ה routing table, המכיל דרכים שונות ליעד והקפיצות הכלולות בו(hop).
3. חיפוש לפי הקידומת של הכתובת שהכי מתאימה ליעד ה - IP בשביל למצוא את הכניסה הכי טובה ב - routing table.) כלומר, (LPM) הוא מחפס ל subnet שהכי דומה התחלה שלה ליעד ה - IP שמכילה את הילד.
4. לפי השלב השלישי הוא מחליט את הקפיצה הבא, לקפיצה יש שתי סוגים:
- כתובת IP ספציפית של ה router הבא.
- ממשק שדרכו מעבירים את ה packet.
ל<span style="color:rgb(221, 49, 49)">דוגמה:</span>
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf-hMRt2eBLNaQd6QDj9SUq4rwR-VojJPt_j8z4485DgwX-aqcPjhDGm672tJOH2yfwH4RC0f6JpaT9t9SOVotSxG-nL5QWLJhy4FnOjHwuekXMHKis9uR0mJMvcjZy8EMqEkGf69j9XPg5bwlBzlWQ7cvl?key=pCG6NpNkQxSboGcR5dCMBA)

אם יעד כתובת ה IP, נמצאת ב subnet, בכתובת 192.168.1.0/24, הקפיצה הבאה תיהיה 10.0.0.2
אם היעד לא נמצא בשום subnet, הכתובת הבסיסית תשומש 0.0.0.0/0, והקפיצה הבא תיהיה 192.168.0.1 באמצעות הממשק eth1.
פקודות לראות את ה routing table:
Linux: `netstat -r`
Linux: `ip route show`
Windows: `route print`
### טופולוגיות

ה - Topology זה סדר/מערך של אלמנטים שונים(קשרים,צמתים) זה מתאר איך מכשירים/צמתים כגון מחשבים, ראוטרים ו - switches. מחוברים זה וזה ואיך מידע עובר/זורם דרך האינטרנט. Topologies יכולים להיות פיזיים או לוגיים.
פיזי - מתאר את המערך הפיזי של הרשת, המיקום של מכשירים והחיבור ביניהם.
לוגי - מתאר את הדרך המידע עובר ברשת, בלי יחס למערך הפיזי.
סוגים של טופולוגים:
**Bus:** 
מתאר את כל המכשירים המחוברים לכבל יחיד מרכזי(backbone). משומש ברשת קטנה.
יתרונות: כל להתקין, חסכוני בכבלים
חסרונות: כאשר הכבל המרכזי(backbone) נכשל כל הרשת נכשלת גם, הביצואים יורדים ככול שיש יותר מכשירים.

**Star**:

מתאר את כל המכשירים המחוברים ל - switch/hub. ואת המידע העובר דרכו. משומש ברשת ביתית
יתרונות: כל התקין ולנהל, כאשר כבל מתנתק רק המכשיר שלו נופל.
חסרונות: כאשר ה switch/hub משתבשים כל הרשת משתבשת, דורש יותר כבלים מה BUS.

**Ring**:

מכשירים מחוברים בעיגול, לכל מכשיר יש שני שכנים. משומש בדרך כלל ב WAN
יתרונות: פועל תחת עומס כבד, packets עוברים בכיוון אחד(מוריד את הסיכוי להתנגשויות).
חסרונות: כאשר מכשיר אחד משתבש כל הרשת משתבשת.

**Mesh**:
כל המכשיר מחובר לכל מכשיר אחר, יש חיבור מלא(FULL MESH) וחיבור חלקי.
יתרונות: אמין, מספק דרכים רבות למידע לעבור.
חסרונות: יקר ומסובך להתקנה.
**tree**:
שילוב של BUS ו - STAR.
יתרונות: מאוזן וכל לניהול, מתאים לרשתות גדולות.
חסרונות: כאשר צומת שורש משתבשת כל הרשת יכולה להיות מושפעת, מסובך יותר BUS STAR.
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcHUZli-ulJ00cfXqfdkmF1i5gvaggMTt2P1O5_9cdtGL2ogBy4KLb0Dv9MAeNytFMLk7falRDWKHI_EhqFK0XGXnNjgVV4WeZdcxzZG5HDrAZdWOxNdKBFYsk1VQQZ9f6bKmqymBmd6MEHu_-d2oriU7Q?key=pCG6NpNkQxSboGcR5dCMBA)**
### פרוטוקולים
#### פרוטוקול בשכבה 3 network
##### פרוטוקול ICMP:
פרוטוקול ICMP - internet control message protocol, משומש לאבחון בעיות בתקישורת ברשת, קובע האם המידע הגיע ליעד. 
מכיל מספר סוגי הודעות:
1) בקשת ותגובת echo: בודק את החיבור בין שני מכשירים
2) יעד לא ניתן להשגה: מציין שהחבילה לא הצליחה להגיע ליעד
3) זמן רחיג: ה - TLL של החבילה פג תוקף
4) שינוי כיוון: מיידע את המארח שישתמש בדרך אחר
5) החלשת הזרם: מבקש מהשלוח לפחית את כמות החבילות הנשלחות, בעקבות פקקים ברשת
כאשר אחד מהבעיות האלו נוצרות מתווצר הודעת ICMP, מתכנס בשכבת ה IP, וממשיך בדרכו למכשיר היעד.
חבילת ICMP:
type - מכיל את סוג ההודעה של הפרוטוקול
code - מכיל מידע נוסף על הבעיה
checksum - מוודא שכל המידע הגיע לפי מספר הביטים
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeCSzEVxdNONPwWryyZQsshxDsT8cTeQTWwNKJ81j_0HImct7zguFLcb_QZry-V2MD0x_aLIOo9-fkBsvSrEDMDkuUsKODQGMRlE-1bgKhBcoTDKhom4cDlM_kRA-z_MylkPIj0f53wyEV6YojkHlRMam5M?key=pCG6NpNkQxSboGcR5dCMBA)**
###### מאפיין ה - TTL:
ה - TLL - time to live, משמש למנוע מחבילות לנוע ברשת לנצח, על ידי הגבלת הקפיצות(hop) בין routerים, אחרי כל החבילה מגיעה ל - router, ערך ה TLL יורד באחד, כאשר הוא מגיע ל - 0 חבילה תיזרת והודעת ICMP תשלח למוקר כתובת ה - IP הודעת על פג תוקף(time exceeded).
###### פקודת ping:
פקודת PING - packet internet groper משומש בשביל פתרון בעיות ברשת,
- בודק האם הגשת לשרת, 
- יש חיבור רשת בין שתי נקודות קצה, 
- כרטיס הרשת עובד כראוי, דרך שימוש בכתובת loopback/localhost
- ובעיות ב - DNS, דרך שימוש ב - domain name ולאחר מכאן בכתובת ה - IP.
תהליך:
נשלחות 4 חבילות למקור ה - IP,  כאשר השרת יקבל את החבילות הוא ישלח את אותן חבילות בחזרה עם אותו מטען, sequence number ו - timestamp.  יש תוצאות שונות, כאשר השרת לא נגיש, ה router לא מוצא את שורש השרת, לא כל החבילות חזרו מה שגורם ל packet loss. 
###### פקודת ה - traceroute:
פקודה המשתמש להראות את כל ה - routerים שהחבילה עוברת דרכם ברשת, משמש לאבחין באיזה שלב/router נמצאת הבעיה.
תהליך:
נשלחות 3 חבילות למקור ה - IP, כאשר ה - TLL שלהן מתחיל מ - 1 ויעלה לאט לאט עד שיגיע ליעד. כאשר החבילות חוזרות למכשיר השולח הן מספקות מידע כגון: כתובת IP, rout trip time, מספר קפיצות).
**מידע יכול לחזור גם כ - \* שמציין שה - router תוכנן לא לספק מידע או שיש לו בעיה.**
![[Pasted image 20240729214132.png#center|550]]
###### **כתובות loopback:**
זאת כתובת IP מיוחדת המשמשת לבדיקת תוכנת רשת על מכונה מקומית מבלי לשלוח packet ברשת.
כתובות:
IPv4 - 127.0.0.1
IPv6 - ::1
כאשר עושים ping לרשת loopback, ה - packetים נשלחים למחסנית של תוכנת רשת, ומייד נשלחים בחזרה.
##### פרוטוקול ARP:
הפרוטוקול ARP - address resolution protocol, זה פרוטוקול תקשורת שממפה את IP address ל MAC address ברשת המקומית.
דרך הפעולה:
- בקשה:

כשמכשיר רוצה לתקשר עם מכשיר אחר ברשת המקומית, הוא צריך את ה - MAC address. אם יש למכשיר השולח את ה - IP address של מכשיר היעד. הוא שולח בקשה ל - ARP request packet. 
- שידור Broadcast:
הבקשה של ה ARP משדרים לכל המכשירים ברשת המקומית.
- תגובה:
המכשיר עם ה IP המתאים מגיב עם ARP reply, המכילה את ה - MAC address של המכשיר.
- שמירה ב - Caching:
המכשיר שמוציא את הבקשה מקבל את ARP reply, מאחסן את מיפוי כתובת ה IP ל MAC ב ARP table לשימוש עתידי שלא יצטרך לשדר(BROADCAST) עוד הפעם.
##### פרוטוקול NAT:
פרוטוקול ה - NAT - network address translation, זו טכניקה ברשת למפה מחדש מרחב של כתובת IP לכתובת אחרת, על ידי שינוי של המידע של הרשת ב IP header של ה packet בזמן שהיא עובר בדרך שמנתב את התנועה. 
**מאפיינים:**
- שימור כתובת IP
מאשר לכמה מכשירים ברשת מקומית לחלוק כתובת IP ציבורית, כאשר הוא שומר על מספר כתובות IP ציבוריות.
- בטיחות:
NAT מספק שכבה של ביטחון, בעזרת הסוואה של כתובות ה - IP הפנימיות מהרשת החיצונית.
- שקופיות:
המכשירים ברשת המקומית ממשיכים להתקשר כרגיל כאשר NAT דואג לתרגום.
סוגים:
- סטטי
ממפה כתובת IP פרטית אחד לכתובת IP ציבורית אחת, משומש לכתובת IP עקבית.
- דינאמי
ממפה כתובת IP פרטית לכתובת IP ציבורית מאגר של כתובות, כאשר מספר המכשירים שצריכים גישה פחות ממספר כתובות פנויות.
- PAT, overloading
ממפה מספר רב של כתובות IP פרטיות לכתובת IP ציבורית אחת, או פחות ממספר. דרך שימוש ב PORT שונים. משומש כאשר מספר מכשירים חולקים כתובת IP אחת.
**תהליך:**
- תנועה יוצאת(LAN -> WAN)
מכשיר ברשת המקומית שולח PACKET לרשת החיצונית, ה NAT משנה את כתובת ה IP ב HEADER, לכתובת שלו. ומתעד את המיפוי בטבלת ה TRANSLATION
- תנועה נכנסת(WAN -> LAN)
כאשר תגובה של PACKET חוזרת מרשת חיצונית, ה NAT בודק בטבלת ה TRANSLATION, לכתובת IP פרטית תואמת, ומספר PORT, משנה את כתובת היעד ב PACKET HEADER ומעביר את זה למכשיר הפנימי הנכון.
**חסרונות:**
- פרוטוקולים שמציינים את כתובת ה IP בגוף ההודעה.
- לוקח זמן ל NAT לעבד מה שיגרום להוריד את ביצוע הרשת
- יכול לסבר תקשורת בין קצה לקצה.
##### פרוטוקול OSPF:
פרוטוקול ה - OSPF - open shortest path first, הוא פרוטוקול ניתוב בפרוטוקול IP, המשתמש באלגוריתם של link state. נופל לקבוצה של IGP, בין מערכת אוטונומית אחידה.
מייסד מפה (link-state database) של הטופולוגיה של הרשת, המשומשת לחישוב הדרך הקצרה ביותר.
כל ראוטר מחשב עצמאי את ה ROUTING TABLE שלו, בעזרת האלגוריתם של SPF,(דייקסטרה). משתמש ב - LSA, LINK STATE ADVERTISEMENTS, ליידע את שאר הראוטרים טופולוגיית הרשת.
הוא משתמש בכתובות multicast לשליחת מידע על ניתוב.
**תהליכים:**
- הכרה Hello packets:
ראוטרים משתמשים ב - HELLO PACKETS לגלות זה את זה, והופכים להיות שכנים.
- החלפה של ה - LSA:
שכנים מחליפים ביניהם LSA בשביל לבנות link state database זהה.
- חישוב דרך הכי קצרה:
כל ראוטר משתמש בדייקסטרה לכל יעד ומעדכן את ה ROUTING TABLE.
#### פרוטוקולים בשכבה 4 transport
##### פרוטוקול TCP:
פרוטוקול TCP - transmission control protocol, הוא פרוטוקול שמתחיל את החיבור בין השולח למקבל לפני שמידע מתקבל.
מאפיינים:
- אמינות:
ה - TCP מוודא שהמידע נשלח ומגיע בדיוק ובאותו סדר שנשלח.
- זרם Flow control:
ה - TCP מנהל את קצב העברות בין השולח למקבל בהתאם לצפיפות ברשת, מונע צפיפות ברשת.
- בקשה חוזרת:
ה - TCP מזהה בעיה במידע שנשלח ומוציא בקשה לשליחה חוזרת של המידע.
- הקמת וסיום החיבור:
ה - TCP משתמש ב three way handshake להקים את התקשורת בין המכשירים וב four way handshake לסיים אותו.
![[Pasted image 20240729215324.png#center|550]]
![[Pasted image 20240729215413.png#center|500]]
**

##### UDP

שכבה רביעית - Transport layer

פרוטוקול UDP - user datagram protocol, הוא פרוטוקול ללא חיבור, לא מתחיל את החיבור בין מכשירים לפני שליחת מידע, משומש למשחקים ברשת, לייבים

**
#### פרוטוקולים בשכבה 7 application:

##### פרוטוקול DHCP:
פרוטוקול ה - DHCP -  Dynamic host configuration protocol, זה מנהל רשת פרוטוקול משמש לאוטומט של תהליך של הגדרת מכשיר לרשת של ה IP
מאפשר למכשירים לקבל כתובות IP, ופרטים הדרושים להגדרת הרשת משרת של DHCP.
**פרטים:**
- IP address
- Subnet mask
- Default gateway
- DNS server
**מאפיינים:**
- קבלת כתובת IP אוטומטית
הפרוטוקול DHCP, באופן דינאמי מקצה כתובת IP למכשירים ברשת. כאשר מכשיר מצטרף לרשת הוא הוא מבקש כתובת IP משרת ה DHCP, שמקצה כתובת פנוייה מרף הכתובות הפנויות(SCOPE).
- קבלת IP זמני:
השרת DHCP מגדיר כתובת IP לזמן קצוב, אחרי הזמן הקצוב הכתובת הוא יכול לתת למכשיר אחר את אותה כתובת IP.
**תהליך:**
1. גילוי
כאשר מכשיר מתחבר לרשת הוא משדר(BROADCAST) הודעה של DHCPDISCOVER לאתר את השרים הזמינים של DHCP.
2. הצעת DHCP
שרתים של DHCP ברשת מגיבים עם הודעת DHCPOFFER שמציעים את פרטי ה IP.
3. בקשת DHCP
הלקוח בוחר אופצה אחת ומגיב עם DHCPREQUEST.
4. הודעה DHCP
שרת ה DHCP מודיע עם הודעה של  DHCPACK לאשר את פרטי ה IP.
##### פרוטוקול ה - HTTP:

פרוטוקולה - HTTP - Hyper test transfer protocol, משומש בשביל להעביר דפי אינטרנט ברשת 
- בקשה ותגובה:
לקוח שרת מודל, הלקוח שולח בקשה לשרת, השרת הגיב באם המשאב המבוקש.
Port - 80
methods:
הפרוטוקול הגדיר שיטות לציין את הפעולה הרצוייה במשאב המבוקש.
GET - מחזיר נתונים מהשרת
POST - שולח מידע לעבד את המשאב.
PUT - מחליף את כל ההצגה של משאב היעד עם המידע שהועלה
DELETE - מוחק את כל המשאבים המצוינים
CONNECT - עושה ‘מנהרה’ לשרת על ידי ה URL
HEAD - כמו גיט אבל מעביר את שורת המצב ואת ה אידר
OPTION - מתאר את דרך התקשור של משאב היעד
TRACE - מבצע בדיקה המראה את הדרך למשאב היעד
Status code:
פרוטוקול המגדיר מצבי קוד לציין סוג שגיאה כתוצאה מבקשת הלקוח.
1xx - מידע) הבקשה התקבלה, ממשיך בתהליך)
2xx - הצלחה) הפעולה הגיעה בהצלחה, הובנה וקובלה)
3xx - שינוי כיוון) פעולה נוספת צריכה, בשביל שהבקשה תצליח)
4xx - שגיאה בלקוח) הבקשה מכילה שגיאה בתחביר או לא יכולה להשלים)
5xx - שגיאה שרת) השרת לא הצליח להשלים את הבקשה, הבקשה בסדר)
header:
ה - header של HTTP מכיל מידע נוסף על בקשה/תגובה או על המשאב. HEADER מכילים:
###### פרוטוקול ה -HTTPS:
גרסה בטיחותי של HTTP, דרך שימוש ב SSL/TLS להצפין מידע בין הלקוח לשרת.
Port - 443
##### פרוטוקול ה - FTP 
פרוטוקול ה - FTP - File transport protocol, משמש להעביר קבצים בין לקוח לשרת, מאפשר להוריד/לעלות ולנעל קבצים בשרת
Port - 21(command), 20 (data)
##### פרוטוקול ה - IMAP
פרוטוקול ה - IMAP - Internet message access protocol, משמש ללקוחות של אימייל לשחזר הודעות משרת המייל.מאפשר למשתמשים לנהל את המייל שלהם כאילו זה היה מקומי.
Port - 143, 993(SSL/TLS)
##### פרוטוקול ה - SMTP
Simple message transfer protocol, משמש להעברת מידע בין שרתים, לא נותן לשחזר הודעות
Port - 23,587,465(SSL)
##### פרוטוקול ה - SSH 
Security shell, מספק דרך מסופקת לגשת ולנהל מכשירים ברשת מרחוק. 
Port - 22
##### פרוטוקול ה - telnet
משמש לתקשר מרחוק עם מחשב או מכשיר רשת אחר, מאפשר למשתמשים להתחבר למכשירים מרחוק ולנהל אותם ואת command line interface, לא בטיחותי.
Port - 23