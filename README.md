# munin-dht-plugin
Munin plugin for reading temperature and humidity from DHT modules. DHT11, DHT22, AM2302. Uses dhtreader python library.

## Sample graph

<img src="http://ra100.github.io/munin-dht-plugin/images/dht_11_4-day.png" />

requirements
* <a href="https://github.com/adafruit/Adafruit_Python_DHT">Adafruit_Python_DHT</a>

based on
<a href="https://github.com/gajdipajti/munin-rpi-temp">https://github.com/gajdipajti/munin-rpi-temp</a>
<a href="https://github.com/agx/munin-dht">https://github.com/agx/munin-dht</a>

## INSTALLATION

install Adafruit_DHT_Driver_Python driver (for prerequisities check <a href="https://github.com/adafruit/Adafruit-Raspberry-Pi-Python-Code/tree/master/Adafruit_DHT_Driver_Python">driver repository</a>)
```
git clone git@github.com:adafruit/Adafruit_Python_DHT.git
cd Adafruit_Python_DHT
python setup.py build
sudo python setup.py install

cd ..
git clone git@github.com:ra100/munin-dht-plugin.git
cd munin-dht-plugin
sudo ln -s $PWD/dht_ /etc/munin/plugins/dht_SENSORTYPE_GPIOPIN
```
USAGE

link dht_ to munin plugins. For DHT11 on GPIO 4 use:
```
ln -s $PWD/dht_ /etc/munin/plugins/dht_11_4
```
configure munin mode, add to /etc/munin/plugin-conf.d/munin-node. You can set name of sensor, number of tries to fetch values (sometimes sensor dhtreader doesn't return values) and number of successful readings from which script counts average and removes outlier values, this should eliminate reading errors or anomalies. If you don't want to use more tries, set env.try_count to 1. If you don't want to count average, set env.average to 1. env.try_count should be greater or equal to env.average

```
[dht_*]
user root

[dht_11_4]
env.where Living room
```

You can then check if it's working via
```
sudo munin-run dht_11_4
```

Restart the munin node afterwards to get the results reported to the server:
```
sudo service munin-node restart
```