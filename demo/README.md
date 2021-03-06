# Simple demo of using PyHLA

## 1. Simulated input file

1000 cases and 1000 controls were simulated by the following command: 

```
python simHLAtypes.py 1000 1000 999 > sim_input.txt
```

## 2. Data summary

```
python ../PyHLA.py --input sim_input.txt --summary --digit 4 --out test_summary_digit4.txt
```

output:

```
Sample size: 2000
Number of cases: 1000
Number of controls: 1000

Gene level summary
------------------------------------------------------------------
                Gene   CaseCount   CtrlCount  TotalCount
                   A        2000        2000        4000
                   B        2000        2000        4000
                   C        2000        2000        4000
                DQA1        2000        2000        4000
                DQB1        2000        2000        4000
                DRB1        2000        2000        4000

Allele level summary
------------------------------------------------------------------
              Allele   CaseCount   CtrlCount  TotalCount    CaseFreq    CtrlFreq   TotalFreq
             A*01:01         625         349         974      0.3125      0.1745      0.2435
             A*02:01         315         342         657      0.1575      0.1710      0.1643
             A*02:03         265         331         596      0.1325      0.1655      0.1490
             A*03:01         265         350         615      0.1325      0.1750      0.1537
             A*11:01         275         316         591      0.1375      0.1580      0.1477
             A*23:01         255         312         567      0.1275      0.1560      0.1417
             B*01:01         404         412         816      0.2020      0.2060      0.2040
             B*02:01         398         421         819      0.1990      0.2105      0.2047
             B*03:01         411         397         808      0.2055      0.1985      0.2020
             B*11:01         373         375         748      0.1865      0.1875      0.1870
             B*15:02         414         395         809      0.2070      0.1975      0.2023
             C*01:01         419         428         847      0.2095      0.2140      0.2117
             C*01:02         412         381         793      0.2060      0.1905      0.1983
             C*02:01         373         406         779      0.1865      0.2030      0.1948
             C*03:01         405         423         828      0.2025      0.2115      0.2070
             C*07:02         391         362         753      0.1955      0.1810      0.1883
          DQA1*01:01         516         487        1003      0.2580      0.2435      0.2507
          DQA1*03:01         512         509        1021      0.2560      0.2545      0.2552
          DQA1*05:05         498         515        1013      0.2490      0.2575      0.2532
          DQA1*06:01         474         489         963      0.2370      0.2445      0.2407
          DQB1*01:01         432         508         940      0.2160      0.2540      0.2350
          DQB1*02:02         411         492         903      0.2055      0.2460      0.2258
          DQB1*03:01         427         466         893      0.2135      0.2330      0.2233
          DQB1*05:02         730         534        1264      0.3650      0.2670      0.3160
          DRB1*01:01         502         490         992      0.2510      0.2450      0.2480
          DRB1*02:01         491         498         989      0.2455      0.2490      0.2472
          DRB1*03:03         504         512        1016      0.2520      0.2560      0.2540
          DRB1*05:03         503         500        1003      0.2515      0.2500      0.2507

Population level summary
------------------------------------------------------------------
              Allele  popCaseCount   popCaseFreq  popCtrlCount   popCtrlFreq
             A*01:01           547        0.5470           322        0.3220
             A*02:01           286        0.2860           310        0.3100
             A*02:03           253        0.2530           301        0.3010
             A*03:01           249        0.2490           316        0.3160
             A*11:01           254        0.2540           290        0.2900
             A*23:01           242        0.2420           288        0.2880
             B*01:01           359        0.3590           362        0.3620
             B*02:01           357        0.3570           379        0.3790
             B*03:01           374        0.3740           359        0.3590
             B*11:01           342        0.3420           342        0.3420
             B*15:02           373        0.3730           354        0.3540
             C*01:01           368        0.3680           373        0.3730
             C*01:02           368        0.3680           341        0.3410
             C*02:01           340        0.3400           365        0.3650
             C*03:01           354        0.3540           381        0.3810
             C*07:02           359        0.3590           328        0.3280
          DQA1*01:01           450        0.4500           434        0.4340
          DQA1*03:01           449        0.4490           442        0.4420
          DQA1*05:05           449        0.4490           452        0.4520
          DQA1*06:01           413        0.4130           432        0.4320
          DQB1*01:01           391        0.3910           445        0.4450
          DQB1*02:02           362        0.3620           442        0.4420
          DQB1*03:01           383        0.3830           400        0.4000
          DQB1*05:02           604        0.6040           461        0.4610
          DRB1*01:01           446        0.4460           426        0.4260
          DRB1*02:01           422        0.4220           443        0.4430
          DRB1*03:03           443        0.4430           444        0.4440
          DRB1*05:03           437        0.4370           440        0.4400

```

## 3. Association analysis

```
python ../PyHLA.py --input sim_input.txt --assoc --digit 4 --test chisq --freq 0.05 --adjust FDR --perm 1000 --out test_assoc_chisq_digit4.txt
```

output:

```
              Allele  A_case  B_case  A_ctrl  B_ctrl  F_case  F_ctrl    Freq   P_Chisq   Chisq  DF      OR     L95     U95     P_adj    P_perm   PermN  permNA
             A*01:01     625    1375     349    1651  0.3125  0.1745  0.2435  4.03e-24 102.635   1  2.1503  1.8522  2.4964  2.42e-23  9.99e-04       0       0
             A*02:01     315    1685     342    1658  0.1575  0.1710  0.1643    0.2672  1.2311   1  0.9063  0.7666  1.0715    0.2672    0.2607     260       0
             A*02:03     265    1735     331    1669  0.1325  0.1655  0.1490    0.0039  8.3301   1  0.7701  0.6465  0.9174    0.0078    0.0040       3       0
             A*03:01     265    1735     350    1650  0.1325  0.1750  0.1537  2.31e-04 13.5577   1  0.7200  0.6055  0.8563  6.94e-04    0.0020       1       0
             A*11:01     275    1725     316    1684  0.1375  0.1580  0.1477    0.0747  3.1766   1  0.8496  0.7132  1.0121    0.0896    0.0679      67       0
             A*23:01     255    1745     312    1688  0.1275  0.1560  0.1417    0.0111  6.4444   1  0.7906  0.6614  0.9451    0.0167    0.0100       9       0
             B*01:01     404    1596     412    1588  0.2020  0.2060  0.2040    0.7836  0.0754   1  0.9757  0.8366  1.1379    0.9677    0.7363     736       0
             B*02:01     398    1602     421    1579  0.1990  0.2105  0.2047    0.3887  0.7431   1  0.9318  0.7991  1.0865    0.9677    0.3467     346       0
             B*03:01     411    1589     397    1603  0.2055  0.1985  0.2020    0.6087  0.2621   1  1.0444  0.8950  1.2187    0.9677    0.5335     533       0
             B*11:01     373    1627     375    1625  0.1865  0.1875  0.1870    0.9677  0.0016   1  0.9934  0.8474  1.1646    0.9677    0.8901     890       0
             B*15:02     414    1586     395    1605  0.2070  0.1975  0.2023    0.4786  0.5020   1  1.0607  0.9090  1.2377    0.9677    0.4725     472       0
             C*01:01     419    1581     428    1572  0.2095  0.2140  0.2117    0.7569  0.0959   1  0.9734  0.8364  1.1329    0.7569    0.7193     719       0
             C*01:02     412    1588     381    1619  0.2060  0.1905  0.1983    0.2341  1.4156   1  1.1025  0.9436  1.2880    0.4290    0.2088     208       0
             C*02:01     373    1627     406    1594  0.1865  0.2030  0.1948    0.2014  1.6324   1  0.9001  0.7696  1.0527    0.4290    0.1638     163       0
             C*03:01     405    1595     423    1577  0.2025  0.2115  0.2070    0.5071  0.4401   1  0.9466  0.8123  1.1032    0.6338    0.4655     465       0
             C*07:02     391    1609     362    1638  0.1955  0.1810  0.1883    0.2574  1.2826   1  1.0996  0.9383  1.2886    0.4290    0.2098     209       0
          DQA1*01:01     516    1484     487    1513  0.2580  0.2435  0.2507    0.3071  1.0432   1  1.0803  0.9363  1.2464    0.8062    0.2677     267       0
          DQA1*03:01     512    1488     509    1491  0.2560  0.2545  0.2552    0.9422  0.0053   1  1.0079  0.8744  1.1619    0.9422    0.8841     884       0
          DQA1*05:05     498    1502     515    1485  0.2490  0.2575  0.2532    0.5607  0.3384   1  0.9560  0.8290  1.1025    0.8062    0.5235     523       0
          DQA1*06:01     474    1526     489    1511  0.2370  0.2445  0.2407    0.6046  0.2681   1  0.9598  0.8303  1.1095    0.8062    0.5704     570       0
          DQB1*01:01     432    1568     508    1492  0.2160  0.2540  0.2350    0.0052  7.8223   1  0.8092  0.6989  0.9369    0.0069    0.0070       6       0
          DQB1*02:02     411    1589     492    1508  0.2055  0.2460  0.2258    0.0025  9.1540   1  0.7928  0.6832  0.9199    0.0050    0.0030       2       0
          DQB1*03:01     427    1573     466    1534  0.2135  0.2330  0.2233    0.1491  2.0818   1  0.8936  0.7699  1.0371    0.1491    0.1139     113       0
          DQB1*05:02     730    1270     534    1466  0.3650  0.2670  0.3160  3.32e-11 43.9811   1  1.5780  1.3794  1.8053  1.33e-10  9.99e-04       0       0
          DRB1*01:01     502    1498     490    1510  0.2510  0.2450  0.2480    0.6871  0.1622   1  1.0327  0.8946  1.1921    0.9418    0.6244     624       0
          DRB1*02:01     491    1509     498    1502  0.2455  0.2490  0.2472    0.8259  0.0484   1  0.9814  0.8500  1.1330    0.9418    0.7892     789       0
          DRB1*03:03     504    1496     512    1488  0.2520  0.2560  0.2540    0.7993  0.0646   1  0.9791  0.8492  1.1289    0.9418    0.7173     717       0
          DRB1*05:03     503    1497     500    1500  0.2515  0.2500  0.2507    0.9418  0.0053   1  1.0080  0.8737  1.1630    0.9418    0.8811     881       0

```

## 4. Zygosity test

```
python ../PyHLA.py --input sim_input.txt --zygosity --test chisq --freq 0.05 --level allele --out test_zygosity_chisq_allele.txt
```

output

```
ID                         Hom_P       Het_P       Zyg_P  Hom_OR  Het_OR  Zyg_OR
A*01:01                   0.0140    1.21e-19    2.46e-11  1.7966  0.4207  4.2708
A*02:03                   0.0313      0.0830      0.0052  0.4607  1.2014  0.3835
A*03:01                   0.0986      0.0067      0.0073  0.5786  1.3283  0.4356
A*23:01                   0.2454      0.0557      0.0706  0.6351  1.2269  0.5176
DQB1*01:01                0.1337      0.0624      0.0156  0.7132  1.1974  0.5956
DQB1*02:02                0.3971    1.98e-04      0.5269  1.2272  1.4313  0.8574
DQB1*05:02                0.0449    6.60e-08    1.10e-07  1.3974  0.5967  2.3418
```

## 5. Interaction test

```
python ../PyHLA.py --input sim_input.txt --interaction --test chisq --freq 0.05 --level allele --out test_interaction_chisq_allele.txt
```

output:

```
ID1         ID2                   P3          P4          P5          P6          P7          P8          P9         P10       OR3       OR4       OR5       OR6       OR7       OR8       OR9      OR10
A*01:01     DQB1*01:01      2.02e-05    1.03e-20      0.0018      0.6760    2.49e-17    1.29e-06    4.41e-05      0.9143      1.86      3.11      0.63      1.06      2.93      1.97      0.58      0.98
A*01:01     DQB1*02:02      2.03e-05    2.35e-19      0.0012      0.6990    1.58e-19    5.72e-05    3.56e-07      0.0805      1.90      2.93      0.61      0.95      3.09      1.80      0.51      0.78
A*01:01     DQB1*05:02      3.58e-30      0.7335    1.04e-16      0.1562      0.1302    4.62e-27    5.43e-33      0.1333      4.38      1.06      3.44      0.83      1.27      3.66      5.11      1.24
A*02:03     DQB1*01:01        0.6254      0.0087      0.9140      0.0064      0.7436      0.0125      0.5939      0.2414      0.92      0.70      0.97      0.74      0.95      0.68      1.10      0.84
A*02:03     DQB1*02:02        0.9060      0.0056      0.6946    1.08e-04      0.7636      0.0025      0.0506      0.8305      0.97      0.69      0.92      0.65      1.05      0.64      1.35      0.96
A*02:03     DQB1*05:02        0.0025      0.9438      0.1818    8.75e-11    1.72e-06      0.0803      0.0041      0.9186      0.65      1.02      1.27      2.01      0.51      1.30      0.65      1.02
A*03:01     DQB1*01:01        0.0146      0.0250      0.0991      0.0656      0.5252    1.02e-04      0.3040      0.6694      0.67      0.74      0.74      0.82      0.91      0.55      0.85      0.93
A*03:01     DQB1*02:02        0.6532    2.21e-04      0.9193    5.87e-05      0.7786    4.20e-04      0.0194      0.7661      0.92      0.61      0.97      0.64      0.95      0.59      1.43      0.95
A*03:01     DQB1*05:02        0.0012      0.3981      0.0655    9.52e-10    1.68e-08      0.1997      0.0115      0.7665      0.63      0.88      1.39      1.93      0.45      1.22      0.68      0.95
A*23:01     DQB1*01:01        0.7345      0.0111      0.9360      0.0071      0.7173      0.0178      0.0244      0.7423      0.94      0.70      1.00      0.75      0.94      0.70      1.41      1.06
A*23:01     DQB1*02:02        0.1058      0.1556      0.0392      0.0046      0.4740    1.59e-04      0.6564      0.3111      0.76      0.82      0.68      0.73      1.12      0.56      1.08      1.16
A*23:01     DQB1*05:02        0.0117      0.9898      0.1024    4.93e-10    1.68e-06      0.0625      0.0011      0.3799      0.69      0.99      1.35      1.94      0.51      1.33      0.61      0.88
```


