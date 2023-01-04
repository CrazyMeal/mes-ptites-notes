#streamelements #stream #code

```html
<div class="main-container">
	<video muted="false">
	    <source src={{someVideo}} type="video/webm">
	</video>
</div>
```

```javascript
let fieldData, commandName;

let streamElementsUser;
let commandFromStreamElements;

let lastTimeCommandWasSent;
let video;

window.addEventListener('onEventReceived', async function (obj) {
    if (obj.detail.event.listener === 'widget-button') {

        if (obj.detail.event.field === 'testMessage') {
            let emulated = new CustomEvent("onEventReceived", {
                detail: {
                    listener: "message", event: {
                        service: "twitch",
                        data: {
                            time: Date.now(),
                            text: "!project",
                            isAction: !1,
                            msgId: "43285909-412c-4eee-b80d-89f72ba53142"
                        },
                    }
                }
            });
            window.dispatchEvent(emulated);
        }
        return;
    }

  	// Controls
  	const data = obj.detail.event.data;
  	console.log("data", data);
  	console.log("streamElementsUser", streamElementsUser);
    if (obj.detail.listener !== "message") return;
  
  	if (!data.text.startsWith("!")) {
        console.log("Message not sarting by ! ==> KO");
        return;
    }

    const command = await getStreamElementsProjectCommand();
  	const commandWithoutExclamationPoint = data.text.replace("!", "");
  	//console.log("commandName", commandName);
  	//console.log("commandWithoutExclamationPoint", commandWithoutExclamationPoint);
  	//console.log("command.aliases", command.aliases);
  
  	if (data.text === commandName || command.aliases.includes(commandWithoutExclamationPoint)) {
      console.log("Trigger the command " + commandName + " ==> OK");
    } else {
      console.log("Message not corresponding to command ==> KO");
      return;
    }
  	
  
  	if (command.enabled) {
      console.log("Command is enabled ==> OK");
    } else {
      console.log("Command is disabled ==> KO");
      return;
    }
  
  	
  	const currentTime = Date.now();
  	const commandCooldown = command.cooldown.global * 1000;
  	const nextPossibleTime = lastTimeCommandWasSent + commandCooldown;
  	console.log("ExecutionTime time", new Date(currentTime));
    console.log("Cooldown", commandCooldown);
    console.log("Last time", new Date(lastTimeCommandWasSent));
    console.log("Last time + cooldown", new Date(nextPossibleTime));
  
  	const commandWasNeverExecuted = typeof lastTimeCommandWasSent === 'undefined';
  	const cooldownIsExpired = currentTime > nextPossibleTime;
	const messageSenderIsBroadcaster = streamElementsUser.providerId === data.userId;
  	console.log("commandWasNeverExecuted", commandWasNeverExecuted);
  	console.log("lastTimeCommandWasSent", lastTimeCommandWasSent);
    if (commandWasNeverExecuted || cooldownIsExpired || messageSenderIsBroadcaster) {
      console.log("Command triggered after cooldown ==> OK");
    } else {
      console.log("Command triggered before cooldown and not broadcaster ==> KO");
      return;
    }
  
  /*
  	if (lastTimeCommandWasSent && currentTime <= nextPossibleTime) {
      console.log("Command triggered before cooldown ==> KO");
      return;
    } else {
      console.log("Command triggered after cooldown ==> OK");
      
    }
    */
  
  	video.style.display = "block";
  	video.play();
  	lastTimeCommandWasSent = Date.now();
});

window.addEventListener('onWidgetLoad', async function (obj) {
  
  
  
  const dropdown = obj.detail.fieldData.someDropdown;
  dropdown.options = ["A", "B"];
  
  //SE_API.setField('someDropdown2', dropdown);
  
  fieldData = obj.detail.fieldData;
  commandName = fieldData.commandName;
  video = document.getElementsByTagName("video")[0];
  
  video.addEventListener("ended", function(event) {
  	console.log("Video ended");
    video.style.display = "none";
  });
  
  
  
  //console.log(obj.detail.channel.apiToken);
  
  streamElementsUser = await getChannelId(obj.detail.channel.apiToken);
  
  //console.log("streamElementsUserID", streamElementsUser._id);
  
  //console.log("Widget loaded at " + new Date(Date.now()));
});

async function getStreamElementsProjectCommand() {
  const commandsResponse = await fetch(`https://api.streamelements.com/kappa/v2/bot/commands/${streamElementsUser._id}`)
  									.then(response => response.json());
  
  const command = commandsResponse.filter(commandInfo => commandInfo.command === commandName.replace("!", ""))[0];            
  console.log(command);
  return command;
}

async function getChannelId(apiToken) {
	return fetch("https://api.streamelements.com/kappa/v2/channels/me", {
            "headers": {
                "accept": "application/json, text/plain, */*",
                "authorization": `apikey ${apiToken}`
            }, "method": "GET"
        }).then(response => response.json());
}

```


```css
body {
  padding: 0;
  margin: 0;
}

.main-container {
  position: absolute;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  margin: 0;
  padding: 0;
}

video {
  display: none;
  width: 100%;
  height: auto;
  margin: 0;
  padding: 0;
}
```

```json
{
 "someDropdown": {
    "type": "dropdown",
    "label": "Choose an option:",
    "value": "blue",
    "options": {
      "blue": "Blue thing",
      "apple": "Some apple",
      "7": "Lucky number"
    }
  }, 
  "commandName": {
    "type": "text",
    "label": "Command name to bind",
    "value": "!project"
  },
   "videoToPlay": {
   "type": "video-input",
   "label": "Video to play"
 },
  "testMessage": {
    "type": "button",
    "label": "Test message",
    "value": "Test message"
  }
}
```