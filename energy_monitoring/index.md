# Energy_Monitoring

## `/api/header/`

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
