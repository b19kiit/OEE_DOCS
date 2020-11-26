# Notifications

## Essential config

```
notification_server : <string><http hostname>
```

## Notify Class

### Storage
Stored in mongodb colletion notifications

Schema:
```js
{
    user_id : <string><mongodbObjectId>,
    time    : <Number><UNIX appoch time>,
    key     : <Notification key><used to prevent repeted messages>,
    msg     : <string>
}
```

### API request

URL : `config.notification_server+'/api/user/notification'`

Body:
```js
body_raw = JSON.stringify({
    userId:<string><mongodbObjectId>,
    category:<string><catagory>,
    msg:<Notification key>,
    href:href
})
```

## Usage
Use static funtion sent in Notify Class

```js
const notify = require('../helpers/notify')
notify.send(
  <string><mongodbObjectId>,
  <string><catagory><oee....>,
  <string><message body>,
  <url><link in notification>,
  <string><key><used to prevent repeted messages>
)
```
