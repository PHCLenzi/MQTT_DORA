# MQTT_DORA
Explore and test the communication protocol through languages

To start using MQTT with Python in Linux, you can follow these steps:

1. Install the Mosquitto broker and client:

   ```
   sudo apt-get install mosquitto mosquitto-clients
   ```

2. Install the Paho-MQTT library for Python:

   ```
   pip install paho-mqtt
   ```

3. Create a Python script to connect to the Mosquitto broker and publish and/or subscribe to MQTT topics. Here is a simple example script that connects to the broker, publishes a message to a topic, and subscribes to the same topic to receive the message:

   ```python
   import paho.mqtt.client as mqtt

   # Define MQTT parameters
   broker = "localhost"
   port = 1883
   topic = "test"

   # Define callback functions
   def on_connect(client, userdata, flags, rc):
       print("Connected with result code " + str(rc))

   def on_publish(client, userdata, mid):
       print("Message published")

   def on_message(client, userdata, msg):
       print("Message received: " + str(msg.payload))

   # Create MQTT client and connect to broker
   client = mqtt.Client()
   client.on_connect = on_connect
   client.on_publish = on_publish
   client.on_message = on_message
   client.connect(broker, port)

   # Publish a message to the topic
   message = "Hello, MQTT!"
   client.publish(topic, message)

   # Subscribe to the topic
   client.subscribe(topic)

   # Loop to listen for incoming messages
   client.loop_forever()
   ```

4. Run the Python script in a terminal window:

   ```
   python script.py
   ```

   This will start the script and connect to the Mosquitto broker. You should see output in the terminal window indicating that the script has connected to the broker and published a message to the topic. The script will also subscribe to the topic and wait for incoming messages.

   You can use the Mosquitto `mosquitto_sub` command-line tool to subscribe to the same topic and send messages to the Python script:

   ```
   mosquitto_sub -t test -h localhost -p 1883
   ```

   This will subscribe to the `test` topic on the local Mosquitto broker and display any incoming messages in the terminal window.

That's it! With these steps, you can start using MQTT with Python in Linux.
