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

