# Timestamp_TDC1

This is a quickstart of S-Fifteen's Instrument
[TDC1](https://s-fifteen.com/collections/timetaggers/products/tdc1-time-to-digital-converter)
4-Channel 2ns Time to Digital Converter

## Installation
The TDC1 uses a USB communications device class and does not need any additional device
driver. It will identify itself as a serial device on all modern OS
- Windows (COMXX)
- Linux/Unix (/dev/ttyACMX)
- Mac (/dev/tty.XX)
There is no need for setting Baud rate or parity for the serial interface.

### Additional Software

To simplify usage and development, there are several software and repositories that can
be used.

### Python package
The [S15lib](https://github.com/s-fifteen-instruments/pyS15/tree/master) python library contains classes of
S-Fifteen Instruments devices. The library also has `g2lib` which holds histogramming
and cross-correlation functions .

This can be installed from via git+pip install
```console
pip install git+https://github.com/s-fifteen-instruments/pyS15.git@no_compile
```

With TTL signals sent into channels 1 and 2, a [quick](https://github.com/s-fifteen-instruments/pyS15/blob/master/examples/TDC1_g2_coincidences.py) measurement of g2 between these two
channels can be done via
```python
from S15lib.instruments import TimestampTDC1

ts = TimestampTDC1()
ts.level = ts.TTL_LEVELS

c = ts.count_g2(
    t_acq=1, # 1 second
    bin_width=2, # 2 nanosecond
    bins=41, # 41 bins in histogram
    ch_stop_delay=0, # 0 nanosecond
    ch_start=1, # channel 1
    ch_stop=2, # channel 2
)
                        
histo = c["histogram"]
time_ax = c["time_bins"]
```
Timestamp mode collection Python [script](https://github.com/s-fifteen-instruments/pyS15/blob/master/examples/TDC1_sample_timestamp_collect.py)

### Python GUI
A python GUI can be found [here](https://github.com/s-fifteen-instruments/tdc1_GUI). This GUI gives
real-time counter data of all four channels or cross-correlation (g2) measurement
between any two channels.

### Labview
Sample labview codes which uses the NI-VISA package to control the Timestamp can be found [here](https://github.com/s-fifteen-instruments/Timestamp_TDC/tree/master/labview)
[Further labview information](https://github.com/s-fifteen-instruments/Timestamp_TDC1/wiki/TDC1-Documentation#user-content-Labview_Interface)
## Further information
For detailed documentation on the TDC1, refer to the [wiki
page](https://github.com/s-fifteen-instruments/Timestamp_TDC/wiki/TDC1-Documentation).

 
Feel free to play with the code but please credit us if you are publishing your own version.
