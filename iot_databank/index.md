# IOT DATABANK

## Routes

### list

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

### listSeries

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

### graph_list

- **Input**
```js
{
  year:<Number>
  month:<Number>
  date:<Number>
}
```

- **Output**

```js
{

}
```
