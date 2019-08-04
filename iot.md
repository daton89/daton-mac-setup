# IoT

## Node Red

I decided to build my first IoT project to automate my small garden with Peperoncini and Tomatos plants. 

For development purpose we may want to install Node Red under Docker on our local machine.

#### Quick install <a id="quick-start"></a>

To run the `latest` container \(we use `slim` tag for alpine linux since we don't need native dependencies\):

```bash
docker run -it -p 1880:1880 -v ~/data-db/node-red-data:/data --name nodered nodered/node-red-docker:slim
```

{% hint style="info" %}
On a Raspberry Pi you must use a `rpi`-tagged image: `nodered/node-red-docker:rpi`.
{% endhint %}

{% hint style="info" %}
On Windows we need to create the volume first: 

docker volume create --name nodered

Then replace the volume option with -v nodered:/data.
{% endhint %}

 Hit `Ctrl-p` `Ctrl-q` to detach from the container. This leaves it running in the background.

To reattach to the container:

```bash
docker attach nodered
```

Now we can open the browser and navigate to http://localhost:1880.

### Deploy Node RED in production

[Securing Node RED](https://nodered.org/docs/user-guide/runtime/securing-node-red#http-node-security).

## Mosquitto

Mosquitto is a very popular MQTT Broker.

We can now create 3 volumes to:

1. Override the default mosquitto.conf.
2. To give a persistent data folder.
3. To give a persistent log folder.

{% hint style="info" %}
On Windows we need to create the volumes into C:/docker-volume/ but not in C:/Users/YOUR\_USER/SOMETHING because we finish to have permission issues.
{% endhint %}

Create a file for configure persistence and logs:

{% code-tabs %}
{% code-tabs-item title="mosquitto.conf" %}
```text
persistence true
persistence_location /mosquitto/data/
log_dest file /mosquitto/log/mosquitto.log
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Run the container:

```bash
docker run --name mqttbroker -it -p 1883:1883 -p 9001:9001 -v c:/docker-volume/mosquitto/mosquitto.conf:/mosquitto/config/mosquitto.conf -v c:/docker-volume/mosquitto/data:/mosquitto/data -v c:/docker-volume/mosquitto/log:/mosquitto/log eclipse-mosquitto
```

More info on the [Mosquitto Official Docker Hub Image](https://hub.docker.com/_/eclipse-mosquitto).

## Testing MQTT

 There’s a handy free program called [MQTT.fx](http://mqttfx.org/) which is available for Mac, Windows and Linux. Or if you’re using Chrome there’s a free Chrome Extension called [MQTT Lense](https://chrome.google.com/webstore/detail/mqttlens/hemojaaeigabkbcookmlgmdigohjobjm?hl=en).

In MQTT.fx, press the settings icon to setup a new connection. We’ll use the server address details above for this. Once we’ve setup our new connection, select it from the list and press the blue connect button.

[![](https://i0.wp.com/philhawthorne.com/wp-content/uploads/2017/07/mqtt-fx-connect.png?resize=496%2C109&ssl=1)](https://i0.wp.com/philhawthorne.com/wp-content/uploads/2017/07/mqtt-fx-connect.png?ssl=1)

Once you’ve connected to your MQTT server, we should first “subscribe” to a topic. Let’s move to the subscribe tab, and enter a topic to subscribe to. For now, let’s choose the topic home/garden/fountain which is the default for MQTT fx.

[![](https://i2.wp.com/philhawthorne.com/wp-content/uploads/2017/07/mqtt-subscribe.png?resize=502%2C120&ssl=1)](https://i2.wp.com/philhawthorne.com/wp-content/uploads/2017/07/mqtt-subscribe.png?ssl=1)

Now that we’ve subscribed to our topic, let’s move back to the Publish tab, and now we’ll send a message on the home/garden/fountain topic. In the message body, let’s type “hello world!” and then press the blue Publish button.

[![](https://i0.wp.com/philhawthorne.com/wp-content/uploads/2017/07/mqtt-send-message.png?resize=725%2C148&ssl=1)](https://i0.wp.com/philhawthorne.com/wp-content/uploads/2017/07/mqtt-send-message.png?ssl=1)

If we switch back to the Subscribe tab, we should now see our home/garden/fountain topic has a message with hello world!

