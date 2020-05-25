# MQ135 in Python

## MCP3008

Im Python Programm kommuniziere ich mit einem MCP3006 Chip dessen Methoden und Erklären findet man in folgenden Dokumenten:

* [MCP 3008 Theorie](https://github.com/dkupert-tgm/SYT_SWISS-ARMY-KNIFE/blob/master/MCP3008.md)
* [MCP 3008 Python](https://github.com/dkupert-tgm/SYT_SWISS-ARMY-KNIFE/blob/master/Python_MCP3008.md)

## Notwendige Konstanten

Alle Werte die ich benutzen werden im folgenden Dokument begründet: [MQ135](https://github.com/dkupert-tgm/SYT_SWISS-ARMY-KNIFE/blob/master/MQ135.md)

```python
MQ135_PULLDOWNRES = 22000.0
MQ135_EXPONENT = -2.769034857
MQ135_SCALINGFACTOR = 116.6020682

ADC_REFRES = 1024.0
PPM = 416.0

CALIBARAION_SAMPLE_TIMES     = 50
CALIBRATION_SAMPLE_INTERVAL  = 500      

READ_SAMPLE_INTERVAL         = 50       
READ_SAMPLE_TIMES            = 5  
```

## Werte auslesen

```python
def MQRead(self, mq_pin):
    rs = 0.0
    for i in range(self.READ_SAMPLE_TIMES):
        # hier wird der Widerstand des MQ135 ausgerechnet
        rs += self.MQResistanceCalculation(self.adc.read(mq_pin))
        time.sleep(self.READ_SAMPLE_INTERVAL/1000.0)
        rs = rs/self.READ_SAMPLE_TIMES
        return rs
```

## Kalibrieren

```python
def MQCalibration(self, mq_pin):
    resvalue = self.MQResistanceCalculation(-self.adc.read(mq_pin))
    val = float(resvalue * math.exp( math.log(self.MQ135_SCALINGFACTOR/self.PPM) / self.MQ135_EXPONENT))
    return val
```

## Werte ausrechnen

```python
def MQGetPercentage(self):
    ret = 0
    validinterval = 0
    validinterval = self.MQResistanceCalculation(-self.adc.read())/self.Ro
    ret = self.MQ135_SCALINGFACTOR * math.pow(validinterval, self.MQ135_EXPONENT)
    return ret
```

## Quellen

[1] "Cheap C02 Meter using MQ135" [online](http://davidegironi.blogspot.com/2014/01/cheap-co2-meter-using-mq135-sensor-with.html) |zuletzt besucht 26.05.2020

