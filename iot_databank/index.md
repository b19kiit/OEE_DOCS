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

- **Output**
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

- **Output**
```js
<Array>{
  timestamp_hour: <Date>,
	hardware_id: <String>,
	num_records: <Number>,
	values: <Object>
}
```

### GET`/api/databanks/graph` : graph_list

- **Input**
```js
{
  year:<Number>
  month:<Number>
  date:<Number>
}
```

### POST`/api/databanks/upload` : uploadExistingRecords

- **Input**
```js
{
  hardware_id : <string>
  created_at : <string><Date>
  values : <Object> //update set
}
```

### GET`/api/databanks/oeedata` : sendData

Input
```js
{
  hid:<string>,
  from:<string><Date>
  to:<string><Date>
}
```

### POST`/api/databanks/machine` : createMachineEntry

Input
```js
{
  hid:<string>,
  c:<string><Date>
}
```

### POST`/api/databanks/meter` : createMeterEntry

Input
```js
{
  tid:<string>
  me:<string>
}
```

### GET`/api/lastlog/` : last_log (latest log)

Input
```js
{ limit:<Number> }
```

### GET`/api/lastlog/test` : last_testlog (latest test log)

Input
```js
{ limit:<Number> }
```

### POST`/deploy` : start script to check webhook
Output : `Okay`

