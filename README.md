# munin-dht
Munin plugin for reading temperature and humidity from DHT modules. DHT11, DHT22, AM2302. Uses dhtreader python library.

requires <a href="https://github.com/adafruit/Adafruit-Raspberry-Pi-Python-Code/tree/master/Adafruit_DHT_Driver_Python">Adafruit_DHT_Driver_Python</a>

based on
<a href="https://github.com/gajdipajti/munin-rpi-temp">https://github.com/gajdipajti/munin-rpi-temp</a>
<a href="https://github.com/agx/munin-dht">https://github.com/agx/munin-dht</a>


USAGE
link dht_ to munin plugins. For DHT11 on GPIO 4 use:
    ln -s $PWD/dht_ /etc/munin/plugins/dht_11_4

configure munin mode, add to /etc/munin/plugin-conf.d/munin-node
    [dht_*]
    user root

    [dht_11_4]
    env.where Living room

You can then check if it's working via

    munin-run dht_foo

Restart the munin node afterwards to get the results reported to the server:

    service munin-node restart

