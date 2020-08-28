# reactionInhebrew
//https://makecode.microbit.org/#tutorial:39288-06014-79996-03263
# משחק תגובה מהיר וכיפי
reaction game
משחק- זמן תגובה      
##Step 0
מחקו את לולאת הלעולמים
`|| basic.forever||`
## Step 1
בשלב הראשון נכין ארבעה משתנים
  משתנה 1 שנקרא לו- התחלה שקרית
שהוא משתנה בוליאני(אמת או שקר)
משתנה 2  שנקרא -משחק 
שגם הוא בוליאני
משתנה -3  התחלה
 ומשתנה -4 סיום
השתמשו בלבנות משתנים `||variables.set to||`
ובלבנות הלוגיקה 
`||logic.False||` במקום המתאים
```blocks
let running = false
let false_start = false
let end = 0
let start = 0
running =false
false_start = false
end = 0
start = 0
```
## Step 2
הוסיפו שני מצבי קלט:
כפתור של התחלה שיהיה מחובר לסיכה 0
כפתור של משחק שיהיה מחובר לסיכה 1
השתמשו בלבנות הסגולות 
```blocks
input.onPinPressed(TouchPin.P0, () => {

})
input.onPinPressed(TouchPin.P1, () => {

})
```
## Step 3
לתוך הלולאה של כפתור התחלת המשחק ה (P0)נכניס אלמנט של ספירה לאחור
הכניסו שלוש לבנות תצוגה כחולות שמראות את המספרים מ-3 עד 0
`||basic.showNumber||`
בסיום הוסיפו לבנת ניקוי מסך
`||basic.clearScreen()||`
```blocks
input.onPinPressed(TouchPin.P0, () => {
    basic.showNumber(3)
    basic.showNumber(2)
    basic.showNumber(1)
    basic.clearScreen()
})
```
##Step 4
:לתוך הלולאה  ,כאשר נלחץ כפתור 0,  `||input. on pin pressed||`נכניס שתי שורות קוד שיאפסו את המשתנים
משחק והתחלה שקרית למצב  שקרי
השתמשו בלבנות  המתאימות

```blocks
input.onPinPressed(TouchPin.P0, ()=>{
running = false
false_start = false
})
```
##Step 5

כדי להתחיל את זמן התגובה בצורה ראנדומלית, נשתמש בלבנות מתמטיקה
  `||math.random||`
והשהייה
`||basic.pause||`
הוסיפו  שורת הקוד של השהייה ללולאת כפתור 
התחלת המשחק 
`||input.on pin pressed ||`
והגדירו ערכים ל1000 + ערך ראנדומלי בין 0-2000
```blocks
basic.pause(1000 + randint(0, 2000))
```
##Step 6
זמן התגובה במשחק מתחיל להספר כאשר המצב של התחלה_שקרית 
איננו מתקיים. כלומר, כאשר לוחצים בכפתור ההתחלה(כפתור 0) בזמן הלא נכון-שהוא כל זמן אחר מלבד התחלה.
לשם כך עלינו להכניס לולאת תנאי לתוך הקוד
`||logic:if then||`
כאשר הכפתור ילחץ בזמן המשחק, נורת לד אחת תדלק בנקודה ראנדומלית על ציר ה-XY
של התצוגה
```blocks
if (!(false_start)) {
        start = input.runningTime()
        running = true
        led.stopAnimation()
        basic.clearScreen()
        led.plot(randint(0, 4), randint(0, 4))
    }
```
##Step 7
הקוד של לולאת כפתור 0 צריך להראות כך:
```blocks
input.onPinPressed(TouchPin.P0, () => {
    basic.showNumber(3)
    basic.showNumber(2)
    basic.showNumber(1)
    basic.clearScreen()
    running = false
    false_start = false
    basic.pause(1000 + randint(0, 2000))
    if (!(false_start)) {
        start = input.runningTime()
        running = true
        led.stopAnimation()
        basic.clearScreen()
        led.plot(randint(0, 4), randint(0, 4))
    }
})
```
##Step 8
כיצד נדע מה מהירות התגובה שלנו? לשם כך נשתמש בלולאה השניה שיצרנו
כאשר נלחץ כפתור 1 (P1(
`||input.onPinPressed||`
ראשית נכניס לולאת תנאי 
`||logic.if else||`
```blocks
input.onPinPressed(TouchPin.P1, () => {
    if (running) {
        
    } else {
        
    }
})
```
##Step 9
לתוך לולאת התנאי
נוסיף שורות קוד של תצוגה
שורה 1-
נחזיר את משתנה למצב-שקר
שורה2- נגדיר משתנה סיום לערך של 
ה-קלט
שורה 3- 
תצוגה ייחודית למצב הרצה
ושורה 4- השהייה
שורה 5- מחשבת את הזמן כמונה כהפרש בין משתנה ה-סיום למשתנה התחלה
```blocks
input.onPinPressed(TouchPin.P1, () => {
    if (running) {
        running = false
            end = input.runningTime()
            basic.showLeds(`
                # # . . .
                # # . . .
                # # . . .
                # # . . .
                # # . . .
                `)
            basic.pause(1000)
            basic.showNumber(end - start)
    } else {
            
    }
})
   
```
!!! אתם יכולים לשנות את התצוגה - זה לא כל כך משנה
##Step 10
מה קורה כאשר יש פספוס?
לתוך לולאת ה-else
נוסיף מצב תצוגה חדש ונשנה את ערך משתנה התחלה_שקרית ל- לאמת
`||logic.True||`
```blocks
input.onPinPressed(TouchPin.P1, () => {
    if (running) {
        running = false
        end = input.runningTime()
        basic.showLeds(`
            # # . . .
            # # . . .
            # # . . .
            # # . . .
            # # . . .
            `)
        basic.pause(1000)
        basic.showNumber(end - start)
    } else {
        false_start = true
        basic.showLeds(`
            . . . . .
            # . # . .
            . # . . .
            # . # . .
            . . . . .
            `)
    }
})
```
##Step 11
כדי להרחיב את המשחק ולעשות אותו מעניין כדאי להוסיף שחקן.
השתמשו בלבנת 
לולאה כאשר נלחץ כפתור 2
בנו קוד מתאים
לפי הקוד שכתבנו לשחקן 1
עליכם לשנות את סמני התצוגה כדי להבדיל בין שחקן לשחקן
```blocks
input.onPinPressed(TouchPin.P2, () => {
    if (running) {
        running = false
        end = input.runningTime()
        basic.showLeds(`
            . . . # #
            . . . # #
            . . . # #
            . . . # #
            . . . # #
            `)
        basic.pause(1000)
        basic.showNumber(end - start)
    } else {
        false_start = true
        basic.showLeds(`
            . . . . .
            . . # . #
            . . . # .
            . . # . #
            . . . . .
            `)
    }
})
```
##Step 11
הורידו את המשחק ללוח המיקרוביט
`|download|` @boardname@
שחקו במשחק עליכם להניח יד אחת על GND
וביד השניה להקיש על רבוע האלומיניום ששיך לכם
##Step 12
כדי לתעד ולעקוב אחרי מהירות התגובהצלמו את עצמכם והעלו
לקשור הבא
זה די משעשע!
https://flipgrid.com/7120893b
