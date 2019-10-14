<!DOCTYPE html>
<html>
<head>
<title>Page Title</title>
</head>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>

<script src="https://cdnjs.cloudflare.com/ajax/libs/paho-mqtt/1.0.1/mqttws31.js" type="text/javascript"></script>
    <script>
    // Create a client instance
var ip = "farmer.cloudmqtt.com";
var port = "35607";
var usessl = true;
var id = (((1 + Math.random()) * 0x10000) | 0).toString(16).substring(1);
var username = 'wptqdsrw';
var password = '3XVAkjUx1KQ4';
var message, client;
var connected = false;
var widgetRepository = {}; //property names are datastreams(keys), values are widget objects


$( document ).ready(function() {
            
    $( "#auto" ).click(function() {
        
        message = new Paho.MQTT.Message("auto")
  message.destinationName = "User1 - Movimiento";
      client.send(message);
        
        
        });
    
    
    
    
    $( "#manual" ).click(function() {
        
        message = new Paho.MQTT.Message("manual")
  message.destinationName = "User1 - Movimiento";
      client.send(message);
        
        
        });
    
    
    
});
        
        
        
        
function connectMQTT() {
    client = new Paho.MQTT.Client(ip, Number(port), id);
    client.onConnectionLost = onConnectionLost;
    client.onMessageArrived = onMessageArrived;
    client.connect({
        userName: username,
        password: password,
        useSSL: usessl,
        onSuccess: onConnect,
        onFailure: onFailure
    });
}

        
        
   
       connectMQTT();      
       // set callback handlers


// connect the client

function onFailure() {
  // Once a connection has been made, make a subscription and send a message.
  console.log("onfailure");
  client.subscribe("World");
 
}

        
        
// called when the client connects
function onConnect() {
  // Once a connection has been made, make a subscription and send a message.
  console.log("onConnect");
    


  client.subscribe("User1 - Movimiento");
  
}

// called when the client loses its connection
function onConnectionLost(responseObject) {
  if (responseObject.errorCode !== 0) {
    console.log("onConnectionLost:"+responseObject.errorMessage);
  }
}

// called when a message arrives
function onMessageArrived(message) {
  console.log("onMessageArrived:"+message.payloadString);
}
    
    
    </script>
<body>
<input type="button" id="auto" value="Click me">
    <input type="button" id="manual" value="Click me manual">

<h1>This is a Heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
