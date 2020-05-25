# Python MCP 3008



## Import

Um den MCP3008 mittels SPI benutzen zu können brauchen wir das Paket 'spidev' 

```python
from spidev import SpiDev
```

## Konstruktor

```python
class MCP3008:
    def __init__(self, bus = 0, device = 0):
        self.bus, self.device = bus, device
        self.spi = SpiDev()
        self.open()
        self.spi.max_speed_hz = 1000000 # 1MHz
```

## Lesen

Um die Werte des MCP3008 lesen zu können benutzen wird folgende Methode

```python
def read(self, channel = 0):
    cmd1 = 4 | 2 | (( channel & 4) >> 2)
    cmd2 = (channel & 3) << 6

    adc = self.spi.xfer2([cmd1, cmd2, 0])
    data = ((adc[1] & 15) << 8) + adc[2]
    return data

    
```

### Quelle

