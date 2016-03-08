# LiveToken-Base

Easily implement token authentication (unique and temporary code) in your meteor project.
This is the base package, you could probably check: livetoken-ui wich will give you access to a minimal user interface.

## Registration

First register yourself on livetoken.io (it's free !) and retrieve your API Key (client_id) from your administration space.


## Install

Install with meteor
  ```sh
    meteor add benmz:livetoken-base
  ```

## Configuration and usage

Configure on server side (replace the xxxxx with your client API Key):
  ```coffeescript
    if Meteor.isServer
      Meteor.startup () ->
        configLiveToken
         auth: 'EMAIL-ONLY'
         client_id: 'xxxxxxxxxxxxxxxxxxx'
  ```

Use it in your code (exemple below use):
  ```coffeescript
    'submit #login': (evt) ->
      evt.preventDefault()
      options = { email: $('input[name=email]').val() }
            
      Meteor.requestToken options, (err, res) ->
        if err
          console.log err.reason
        else
          console.log res.Email
  ```

## Methods available

Different methods can be used to interrogate livetoken.io

### Meteor.getAuthMethods()
No parameters, will send back the authentication methods choosen

### Meteor.registerUser()
Allow you to create a new user with phone field.
Required: email
Optional: phone, name, surname, company

### Meteor.requestToken()
Allow to request a token from livetoken.io
Required: email, phone (depending of your authentication configuration)

### Meteor.loginWithToken
Will basically check the token entered by user with the received one.
Required: email, phone (depending of your authentication configuration)

## Configuration options
There's different options available in order to configure your authentication method.
These options must be set on server-side to Accounts.livetoken object

auth: define the authentication method
    options are: EMAIL-ONLY / PHONE-ONLY / EMAIL-OR-PHONE / EMAIL-AND-PHONE

client_id: define your client API key fo livetoken.io

retry: define the max number of attempts your client can try token code before it gets invalidated (default: 3)

timeout: define the max number of seconds before a token is invalidated (default: 300)


