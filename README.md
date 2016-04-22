# LabRAD HighFinesse wavemeter server

LabRad server to access measurements from a [HighFiness wavelength meter](http://www.highfinesse.com/en/wavelengthmeter/28/high-precision-wavelength-meter), specifically the model `WS-7` including a multiplexer.

## Requirements

### pylabrad

Make sure you install `pylabrad` before you run the server, e.g. using `pip`:

```shell
$ pip install labrad
```

You should als set the required environment variables, e.g. in `bash`:

```shell
$ export LABRADHOST=<hostname or ip>
$ export LABRADPASSWORD=<password>
```

### Configuration

Create a configuration file with the ip/hostname and port of the
M-squared ICE module.

```shell
$ cp config.example.json config.json
$ vim config.json
...
```

*Make sure the wavemeter is connected to the same machine and the
control software is running.*

## Example usage

First, start the server:

```shell
$ python wavemeter_server.py
```

Then start an (i)python console...

```shell
$ ipython
```

... and use the settings:

```python
import labrad

cxn = labrad.connection()
wavemeter = cxn.wavemeter

wavemeter.get_channel()   # => 1
wavemeter.set_channel(2)  # => True

wavemeter.get_multiplex_mode()     # => False
wavemeter.set_multiplex_mode(True) # => True

# Get frequency of channel 3 of the multiplexer
freq = wavemeter.get_frequency(3)
if (freq != None):
  print freq # => Value(434.8298706177748, 'THz')
```
