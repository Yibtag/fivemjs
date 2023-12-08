# FIVEM JS

**Fivem js is a library that makes creating nuis easier!**

## Using it

Using it with normal script tags:

index.html
```html
<!-- ! WARRNING ! Make sure that the fivem js script -->
<!-- tag is above the ones youre using it in! -->
<script src="libs/fivemjs.js"></script>
<script src="app.js"></script>
```

If you want to use it with defer make sure that the fivemjs tag also has defer:

```html
<!-- ! WARRNING ! Make sure that the fivem js script -->
<!-- tag is above the ones youre using it in! -->
<script defer src="libs/fivemjs.js"></script>
<script defer src="app.js"></script>
```

## Sending messages to the client

app.js
```js
// The first argument is the callback name
// The secound is the body that the callback recives
// The function also returns a normal https response body
const response = await SendNUIMessage("test", {
    message: "Test"
})
```

client.lua
```lua
-- First argument is the callback name
-- The secound one is a function of wich the first argument is the body
RegisterNUICallback("test", function (body, callback)
    print(body.message)
end)
```

## Reciving messages

app.js
```js
// The first argument is the callback name
// The secound argument is the function wich recives the body
// The third argument is a list of objects that will be recived in data
// ! WARRNING ! Adding items that you dont send from lua will result in a error!
RegisterNUICallback("test", function (data) {
    console.log(data.message)
}, ["message"])
```

client.lua
```lua
-- The first argument is a json object
-- in the object you can specify anything.
-- The special field reserved for the callback
-- name is `type`.
SendNUIMessage({
    type="test",
    message="Hello"
})
```

## Registering nui keybinds

Before listening for keypresses the nui must be in focus to recive keybinds. You can do this by:

client.lua
```lua
-- The first argument specifies if it is focused!
-- The secound argument specifies if the nui
-- shuld have a cursur or not.
SetNuiFocus(true, true)
```

app.js
```js
// The first argument is the key you want to listen to.
// If this is not working check that the key supplied is a
// valid javascript key.
// The secound argument is the function that gets called when
// the key is pressed!
RegisterKeybind("Escape", function () {
    console.log("Escape")
})
```