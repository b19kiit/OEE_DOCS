# IOT DATABANK

## Routes

### GET`/api/databanks/` : list

- **Input** :
```js
{
  hid : <string>
  duration : <Number>
  limit : <Number>
  sort : 
  format :
  gap : <string><options ('yes', anything_else)>
  from : <string><Date>
  to : <string><Date>
  fromUnix : <Number>
}
```

- **Output** :

```js
<Array>{
  timestamp_hour: <Date>,
	hardware_id: <String>,
	num_records: <Number>,
	values: <Object>
}
```

### GET`/api/databanks/series` : listSeries

- **Input** :

```js
{
  hid : <string>
  duration : <Number>
  limit : <Number>
  sort : 
  format :
  gap : <string><options ('yes', anything_else)>
  from : <string><Date>
  to : <string><Date>
  fromUnix : <Number>
}
```

- **Output** :

```js
<Array>{
  timestamp_hour: <Date>,
	hardware_id: <String>,
	num_records: <Number>,
	values: <Object>
}
```

### GET`/api/databanks/graph` : graph_list

- **Input** :

```js
{
  year:<Number>
  month:<Number>
  date:<Number>
}
```

### POST`/api/databanks/upload` : uploadExistingRecords

- **Input** :

```js
{
  hardware_id : <string>
  created_at : <string><Date>
  values : <Object> //update set
}
```

### GET`/api/databanks/oeedata` : sendData

Input :

```js
{
  hid:<string>,
  from:<string><Date>
  to:<string><Date>
}
```

### POST`/api/databanks/machine` : createMachineEntry

Input :

```js
{
  hid:<string>,
  c:<string><Date>
}
```

### POST`/api/databanks/meter` : createMeterEntry

Input :

```js
{
  tid:<string>
  me:<string>
}
```

### GET`/api/lastlog/` : last_log (latest log)

Input :
```js
{ limit:<Number> }
```

### GET`/api/lastlog/test` : last_testlog (latest test log)

Input :

```js
{ limit:<Number> }
```

### POST`/deploy` : start script to check webhook
Output : `Okay`

...

## timeSeries function

- **getYearDateRange(year)**

***return*** : { start: <Date><year start>, end: <Date><year end> }

- **getMonthDateRange(year, month)**

***return*** : { start: <Date><month start>, end: <Date><month end> }

- **matchHardware(hardware_id)**

***return*** :

```
$match: {
    "hardware_id" : hardware_id
}
```

- **projectWithTimeZone(timezone)**

***return*** :

```
$project: {
    "_id" : {
	day:   {   $dayOfMonth:     {   date:'$timestamp_hour', timezone: timezone } },
	week:   {   $week:     		{   date:'$timestamp_hour', timezone: timezone } },
	month:  {   $month:         {   date:'$timestamp_hour', timezone: timezone } },
	year:   {   $year:          {   date:'$timestamp_hour', timezone: timezone } },
	hour:   {   $hour:          {   date:'$timestamp_hour', timezone: timezone } },
	minute:   {   $minute:      {   date:'$timestamp_hour', timezone: timezone } }, 
    },
    "hardware_id" : "$hardware_id",
    "timestamp": "$timestamp_hour",
    "values" : {
	"$objectToArray" : "$values"
    }
}
```

- **filterDateRange(fromDate, toDate)**:

***return*** :

```
{ 
  $match: {
  	timestamp : { $gte: fromDate }  // 'gte' : '>'
	timestamp = { $lte: toDate }    // 'lte' : '<'
  }
}
```

- **sortOrder(order)**

***return*** :

```
{ 
  $match: {
  	timestamp : { $gte: fromDate }  // 'gte' : '>'
	timestamp = { $lte: toDate }    // 'lte' : '<'
  }
}
```

- **setLimit(limit)**

***return***

```
$sort: {
    "created_at": (order === 'asc'? 1:-1)
}
```

- **getMinuteQuery(options)**

***options*** : `{ from<Date>, to<Date> }`

- **getOnDemandMinuteQuery(options)**

***options*** : `{ from<Date>, to<Date> }`
