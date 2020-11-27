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
 
 ## GET : `/getOee`
 
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

## GET : `/csv`

- find latest report the machine and organisation admins document

- Now for each report in the array
```js
     newArray = []
					report.forEach(e => {
						newArray.push({
							availability: e.oee.availability,
							performance: e.oee.performance,
							oeePercent: e.oee.oeePercent,
							totalCount: e.nC,
							badCount: e.bC,
							'downTime(in minutes)': e.downTime / 60000,
							status: e.status,
							cycleTime: e.cycleTime,
							createdAt: getDate(e.createdAt),
							updatedAt: getDate(e.updatedAt)
						});
					});
```

- make csv for
```
					csv(
						newArray,
						report[0].machineId.machineName,
						report[report.length - 1].organisationId.organisationAdmin.email,
						req.query.email
					)
```

## GET : `/getJson`
Find and return all reports of the machine

## POST : `/injectCdetails`

Update `cDetail` of the report in reports collection

## GET : `/details`

## POST : `/downtimeDetail`

- find reports with tgId

- return downTime details with their respective types

like
```
		.aggregate([
			{ $match: { tgId: req.body.tgId } },
			{
				$sort: {
					updatedAt: -1
				}
			},
			{
				$limit: 1
			},
			{
				$project: {
					_id: 0,
					[req.body.downTimeType]: {
						$map: {
							input: {
								$slice: [
									`$${[req.body.downTimeType]}`,
									req.body.sortType * req.body.limit
								]
							},
							as: 'downTime',
							in: {
								_id: 0,
								from: {
									$dateToString: {
										format: '%Y-%m-%d/%H:%M:%S',
										date: '$$downTime.from',
										timezone: '+05:30'
									}
								},
								to: {
									$dateToString: {
										format: '%Y-%m-%d/%H:%M:%S',
										date: '$$downTime.to',
										timezone: '+05:30'
									}
								},
								cause: '$$downTime.cause',
								comment: '$$downTime.comment'
							}
						}
					}
				}
			}
		])
```
