# Energy_Monitoring

## Routes

### `/api/header/`

***Input***

```js
{ HardwareId:<string> }
```

***Output***

```js
{
  response.current_load = <Number>
    response.electricity_consumption = <Number>
    response.currentbilling = <Number>
    response.current_meter_reading = <Number>
    response.last_date = <Number>
    response.current_balance = <Number>
    response.carbon_footprint = <Number>
    response.carbon_emission = <Number>
    response.next_billdate = <Date YYYY MM DD>
    response.current_in_red = <Number>
    response.current_in_blue = <Number>
    response.current_in_yellow = <Number>
    response.voltage_in_vry  = <Number>
    response.voltage_in_vyb  = <Number>
    response.voltage_in_vbr  = <Number>
    response.voltage_in_vrn  = <Number>
    response.voltage_in_vyn  = <Number>
    response.voltage_in_vbn  = <Number>
}
```

### `/api/graph/`

***Input***

```js
{ 
  data_limit: <string><options 'minutely', 'hourly', 'daily', 'weekly'>
  hour: <Number>
  date: <Number>
  month: <Number>
  year: <Number>
}
```

***Output***

```js
<Array>{
  "vry": <Number>,
  "vyb": <Number>,
  "vbr": <Number>,
  "vrn": <Number>,
  "vyn": <Number>,
  "vbn": <Number>,
  "ir": <Number>,
  "iy": <Number>,
  "ib": <Number>,
  "electricity_consumption": <Number>,
  "minutes":<Date>,
  "time": <Number><UNIX APPX><seconds>,
  "created_at": <Number><UNIX APPX>,
  "electricity_consumption": <Number>,
  "currentbilling": <Number>
}
```

### `/api/fetchminutes/`

***Input***

```js
{
  HardwareId : <string>, 
  to : <string><Date>,
  from : <string><Date>
}
```

***Output***

```js
{
  Kwh : <Number><seconds>
  value : <Object><FetchData>
}
```

## Classes/Functions

### class FetchData

- **constructor (thing_id, end_date, start_date, limit = 100, sort = 'asc', duration, format= true)**

- **services()**

***return***

```js
<Promise>{
  resolve : {
    
  }
}
```
