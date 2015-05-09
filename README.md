# munin-dht-plugin
Munin plugin for reading temperature and humidity from DHT modules. DHT11, DHT22, AM2302. Uses dhtreader python library.

requires <a href="https://github.com/adafruit/Adafruit-Raspberry-Pi-Python-Code/tree/master/Adafruit_DHT_Driver_Python">Adafruit_DHT_Driver_Python</a>

based on
<a href="https://github.com/gajdipajti/munin-rpi-temp">https://github.com/gajdipajti/munin-rpi-temp</a>
<a href="https://github.com/agx/munin-dht">https://github.com/agx/munin-dht</a>


USAGE

link dht_ to munin plugins. For DHT11 on GPIO 4 use:
    
    ln -s $PWD/dht_ /etc/munin/plugins/dht_11_4

configure munin mode, add to /etc/munin/plugin-conf.d/munin-node. You can set name of sensor, number of tries to fetch values (sometimes sensor dhtreader doesn't return values) and number of successful readings from which script counts average and removes outlier values, this should eliminate reading errors or anomalies. If you don't want to use more tries, set env.try_count to 1. If you don't want to count average, set env.average to 1. env.try_count should be greater or equal to env.average
    
    [dht_*]
    user root

    [dht_11_4]
    env.where Living room
    env.try_count 10
    env.average 4

You can then check if it's working via

    munin-run dht_11_4

Restart the munin node afterwards to get the results reported to the server:

    service munin-node restart

