# RRDTOOL VSB PROJECT

VSB project

## TUTORIAL

Krok č.1:
```
 rrd rrdtool create test.rrd --start now --step 1 DS:x:DERIVE:30:-2:2 RRA:AVERAGE:0.5:1:5000 DS:y:DERIVE:30:-2:2 RRA:AVERAGE:0.5:1:5000 DS:z:DERIVE:30:-2:2 RRA:AVERAGE:0.5:1:5000
```
Vygeneruje nový test.rrd


Krok č.2:
```
rrdtool dump test.rrd test.xml
```
Vygeneruje z test.rrd -> test.xml se kterým se dá dále pracovat.
-> DOPLNIT DATA + další úpravy
-> DOPLNIT TIMESTAMP! případně nechat vygenerovaný.


Krok č.3:
```
rrdtool restore test.xml test_actual.rrd
```
Vygeneruje nový rrd soubor: test_actual.rrd


Krok č.4:
-> nyní pro aktuálnost před generováním grafu:
```
rrdtool update test_actual.rrd N:1:1:1
```
-> není otestováno, ale mělo by dolpnit aktuální timestamp

```
rrdtool graph mygraph.png --title="Accelerometer" --x-grid SECOND:30:MINUTE:1:MINUTE:5:0:%H:%M --start -6000 --end -800 --vertical-label "Acc" --rigid --upper-limit 2 --lower-limit -2 DEF:x=test_actual.rrd:x:AVERAGE LINE2:x#000000:x DEF:y=test_actual.rrd:y:AVERAGE LINE2:y#f44265:y DEF:z=test_actual.rrd:z:AVERAGE LINE2:z#2702f7:z
```
Zde je nutné specifikovat: [--start] [--end]

## Výsledek:
![alt text](https://github.com/besters/vsb-rrdtool/blob/master/mygraph.png?raw=true)

## Užitečné odkazy:

**Timestamp generator:** (http://www.timestampgenerator.com/)

**Dokumentace RRDtoolu:** (https://oss.oetiker.ch/rrdtool/doc/rrdtool.en.html)