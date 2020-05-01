# hass-lv-ws-integration
LabVIEW integration for HomeAssistant via the WebSocket API

# The goal of this integration is to enable LabVIEW users to interface with Home Assistant via the WebSocket API.
Starting from LabVIEW 2018

##Installation
###Dependencies
LabVIEW Websocket Library by MediaMongrels - https://forums.ni.com/t5/Example-Code/LabVIEW-WebSockets-Library/ta-p/3491490?profile.language=en
JKI JSON Library - https://blog.jki.net/jki/introduction-to-jki-json
Both can be installed via the VI Package Manager.

###Generating a Home Assistant Access Token
Generate a Long-Lived Access Token via Home Assistant - this can be found after clicking on your profile badge
You are advised to store your access token outside your LV code, in a text file for example. Run once the TestMainApp.vi example to create a txt file next to your project. Paste your access token into this generated txt file.

##Using this integration
This integration at the moment provides the following features>
### Connect and Authenticate to your Home Assistant instance (wsConnectAndAuthenticate.vi)
You should provide your access token (in a file or just as a string, see above), the IP address of the Home Assistant instance running and the port of the Home Assistant instance. The VI returns with a string for authentication info and with a boolean value if the authentication was successful.

### WebSocket API Handler Engine (wsHandlerEngine.vi)
This VI should be running in parallel with the rest of your application.
You send and receive WS messages via this VI using queues. The main purpose of this VI is to recognize which messages belong to Home Assistant events and channel those to a User Event so those can be managed in an Event Structure.

### Register / Unregister for Home Assistant Events (wsRegUnregEvents.vi)
This VI registers/unregisters for the events that are being fired on the Home Assistant Event Bus. If you wish to register for all events leave the event name input empty.

### Call Home Assistant Service (wsCallService.vi)
This VI calls a Home Assistant Service. The service data field is optional. If you wish to add Service Data then connect the result of a Flatten to JSON String to this input. 

### Fetch all States (wsFetchStates.vi)
This VI fetches the states of all Home Assistant Entities and returns them in an array of clusters.

##Example Code
The TestMainApp.vi example shows you the basic usage of the integration with simple examples.

##ToDo
Events are now returned as simple JSON strings. A JSON to Cluster unflattening will be implemented soon. Now I am collecting experience about how it would be really comfortable to use.
