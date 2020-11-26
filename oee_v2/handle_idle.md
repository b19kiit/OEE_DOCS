- 
```css
time of idle = <current_time in a the user's timezone>
```

- Using DownTime plans of the machine, we check if the Idle Down is planned or a defect/error

- If the idle stituation was planned and no repetative in planedDownTime array then, Then add this report as planedDownTime

- Else the report is added as unPlanedDownTime

## Function used to compare date
```js
function compareDate(from,to,test){
    if (test >= from && test <= to) {
        return true
    } else {
        return false
    }
};
```
