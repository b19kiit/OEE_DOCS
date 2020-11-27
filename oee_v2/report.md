# report.js

## mqttHandler subscriptions

- `oee/idle/+`

- `oee/unidle/+`

- `oee/counter/+`

# Handling the mqtt topics 

## `oee/idle`

- Use [handleIdle](/OEE_DOCS/oee_v2/handle_idle)

- Publish on topic `oee/requstSync/${tgId}`

## `oee/unidle/`

- Use [handleUnIdle](/OEE_DOCS/oee_v2/handleUnIdle)

- Publish on topic `oee/requstSync/${tgId}`

- send email to oganisation admin

## `oee/counter/`
 
- open report schema of the perticular tg

- find the latest updated document

- updateCounter
 Update report document
 ```js
  ['cDetail.' + nC]: {
    time: Date.now(),
    cycleTime
  }
 ```
 - send notification to the organisation admin
 
 # routes
 
 # GET : `/getOee`
 
 - find latest reports of 'tgId'
 
 - respond user with
 ```js
    res.json({
      oee: report.oee,
      downTime: report.downTime,
      operatingTime: report.updatedAt - report.createdAt,
      bC: report.bC,
      nC: report.nC,
      status: report.status,
      cycleTime: report.cycleTime,
      worker: w ? w.wemail + '/' + w.wphone : '#',
      MTTR: report.MTTR,
      MTBF: report.MTBF,
      UpTime: report.UpTime,
      createdAt: report.createdAt,
      updatedAt: report.updatedAt,
      ictpu: report.ictpu,
      quantity: report.quantity,
      ppId: report.ppId
      // bCdetails: report.bCdetails
    })
```
