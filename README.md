# Учимся строить графики с помощью библиотеки Matplotlib

Links:
  1. https://matplotlib.org/
  
  
## Задача

В папке data лежит архив с логами эксперимента по передачи данных. Файл 
r2183a_4srv_ifstat_c01_c08.log содержит статистику работы сетевых интерфейсов, а файл
r2183a_4srv_ziostat_c01_c08.log статистику работы дисковой подсистемы.

Пример файла r2183a_4srv_ifstat_c01_c08.log 
```bash
       bge2                ix0                 ix1                lagg0               vlan1               vlan2       
 KB/s in  KB/s out   KB/s in  KB/s out   KB/s in  KB/s out   KB/s in  KB/s out   KB/s in  KB/s out   KB/s in  KB/s out
    0.69      0.57      0.00      0.00      0.10      0.10      0.10      0.10      0.00      0.00      0.09      0.09
    0.12      0.80      0.00      0.00      0.10      0.10      0.10      0.10      0.00      0.00      0.09      0.09
    0.41      0.53      0.00      0.00      0.68      0.10      0.68      0.10      0.00      0.00      0.61      0.09
    0.42      0.55      0.00      0.00      0.10      0.10      0.10      0.10      0.00      0.00      0.10      0.10
    0.45      0.51      0.12      0.00      0.21      0.10      0.33      0.10      0.00      0.00      0.09      0.09
    0.39      0.51      0.00      0.00      0.10      0.10      0.10      0.10      0.00      0.00      0.09      0.09
    1.29      1.65      0.00      0.00      0.19      0.19      0.19      0.19      0.00      0.00      0.18      0.18
    1.08      0.90     42.79      0.00      0.16     45.95     42.95     45.95     76.17     81.88      0.09      0.09
    0.58      0.75    413.58   1932.02      0.17    427.06    413.74   2359.08    360.74   9767.35      0.15      0.09
    0.87      1.16    515.01  118532.4      0.16      0.10    515.17  118532.5    182.93  110641.1      0.15      0.09
    0.75      0.96      0.00      0.00      0.16      0.10      0.16      0.10      0.00      0.00      0.15      0.09
    1.00      1.19      0.00      0.00      0.10      0.10      0.10      0.10      0.00      0.00      0.09      0.09
    0.06      0.25      0.00      0.00      0.10      0.10      0.10      0.10      0.00      0.00      0.18      0.18
    0.40      0.52      0.00      0.00      0.10      0.10      0.10      0.10      0.00      0.00      0.09      0.09
    0.40      0.52      0.00      0.00      0.26      0.20      0.26      0.20      0.00      0.00      0.15      0.09
    0.41      0.54     66.92      0.00      0.17  17859.56     67.08  17859.56     57.97  17978.71      0.15      0.10
    0.42      0.55    706.38  47737.75      0.21  131851.5    706.59  179589.3    445.30  173926.4      0.19      0.19
    0.62      1.43    876.87  104645.7      0.16  107416.1    877.03  212061.7    488.48  206597.5      0.15      0.09
    0.77      1.08    954.95  110153.9      0.60  115780.7    955.55  225934.6    615.47  244588.5      0.53      0.00
    1.41      1.32   1004.20  120409.7      0.00  119458.8   1004.20  239868.5    504.11  211885.7      0.00      0.00
    0.12      0.89    613.77  72310.74      0.06  61446.16    613.83  133756.9    452.14  162515.0      0.06      0.00
    0.42      0.54   1045.15  128493.5      0.07  105692.3   1045.21  234185.8    598.38  226025.2      0.06      0.00

```

Пример файла r2183a_4srv_ziostat_c01_c08.log
```bash
               capacity     operations    bandwidth
pool        alloc   free   read  write   read  write
----------  -----  -----  -----  -----  -----  -----
nlsas05      267G  27.0T      0      5  28.2K   553K
nlsas06      264G  27.0T      0      6  27.3K   649K
nlsas07      289G  27.0T      0      5  25.9K   603K
nlsas08      287G  27.0T      0      6  25.6K   687K
zsystem     42.4G   514G      0      3  6.09K  13.8K
----------  -----  -----  -----  -----  -----  -----
nlsas05      267G  27.0T      0      0      0      0
nlsas06      264G  27.0T      0      0      0      0
nlsas07      289G  27.0T    346      0  43.3M      0
nlsas08      287G  27.0T    485      0  60.6M      0
zsystem     42.4G   514G      0      0      0      0
----------  -----  -----  -----  -----  -----  -----
nlsas05      267G  27.0T      0      0      0      0
nlsas06      264G  27.0T      0      0      0      0
nlsas07      289G  27.0T    320      0  40.1M      0
nlsas08      287G  27.0T    491      0  61.4M      0
zsystem     42.4G   514G      0     51      0   222K


```


Необходимо:

  1. Построить график работы сетевых интерфейсов (lagg0, ix0, ix1) по одному лог файлу, файл *_iostat.log
  1. Объеденить графики работы сетевых интерфейсов (lagg0), файлы *_iostat.log
  2. Построить график работы дисковой подсистемы (операции чтения), файлы *ziostat.log

Пример графика сетевого трафика, построен не matplotlib и приводится для примерного представления о чем речь.
 ![image](data/example.png)

