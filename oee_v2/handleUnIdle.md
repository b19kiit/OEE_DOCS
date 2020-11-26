# handleUnIdle

- Find planedDownTime details of a machine in reports

- If the planedDownTime array contains any report of idle state, then report is update in 'planedDownTime' catagory

- If the unPlanedDownTime array contains any report of idle state, then report is updated in 'unPlanedDownTime' catagory

## Updating the report document in DB

```js
let toUpdate = {}; //update in object of the downtime array
cause ? toUpdate[`${cat}.$.cause`] = 'Miscellaneous' : '';
comment ? toUpdate[`${cat}.$.comment`] = 'No Comment' : '';
toUpdate['status'] = 'started';
toUpdate[`${cat}.$.to`] = unidle;
```
- if down time was unplanned
then add unidle to report document
`downTime = unidle.getTime() - focus.from.getTime()`
