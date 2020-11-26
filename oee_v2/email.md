# Email System

## Framework Used:
[nodemailer](https://nodemailer.com/about/)

## Essential config:

```jsx
  maildist:{
      host: <string> <host address>,
      port: <Number> <mostly 587>,
      secure: <bool> <true if you have ssl key>,
      auth: {
          user: <string>,
          pass: <password>
      },
      tls: {
          ciphers: 'SSLv3'
      }
  }
```

## Usage

```js
sendEmail({
    from:<string> <sender_name>,
    to:<string> <email_address>,
    subject:<string>,
    html:<string> <html>,
    onError: <funtion(err)>,
    onSuccess: <funtion(success)>
})
```
