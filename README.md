                                            #Hypothesis
Ho: There is no significant association between demographic and health factors with metabolic syndrome. Ha: There is a significant association between demographic and health factors with metabolic syndrome.
library(dplyr)
## Warning: package 'dplyr' was built under R version 4.3.3
## 
## Attaching package: 'dplyr'
## The following objects are masked from 'package:stats':
## 
##     filter, lag
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
library(ggplot2)
## Warning: package 'ggplot2' was built under R version 4.3.3
df<-read.csv('C:/Users/ashac/OneDrive - Indiana University/Third Semester/Security and Privacy/Second Semester/Applied Statistics/Metabolic Syndrome.csv')
df
##       seqn Age    Sex   Marital Income        Race WaistCirc  BMI Albuminuria
## 1    62161  22   Male    Single   8200       White      81.0 23.3           0
## 2    62164  44 Female   Married   4500       White      80.1 23.2           0
## 3    62169  21   Male    Single    800       Asian      69.6 20.1           0
## 4    62172  43 Female    Single   2000       Black     120.4 33.3           0
## 5    62177  51   Male   Married     NA       Asian      81.1 20.1           0
## 6    62178  80   Male   Widowed    300       White     112.5 28.5           0
## 7    62184  26   Male    Single   9000       Black      78.6 22.1           0
## 8    62189  30 Female   Married   6200       Asian      80.2 22.4           0
## 9    62191  70   Male  Divorced   1000       Black        NA   NA           1
## 10   62195  35   Male             2500       Black      99.0 28.2           0
## 11   62199  57   Male             9000       White     107.8 28.0           0
## 12   62202  36   Male   Married   8200 MexAmerican      97.0 24.7           1
## 13   62205  28   Male    Single   9000       White     106.0 28.9           0
## 14   62208  38   Male   Married   3500    Hispanic      82.7 22.2           0
## 15   62209  62 Female Separated   2500 MexAmerican      92.9 26.0           0
## 16   62214  22 Female Separated   3500       Black      89.0 23.8           0
## 17   62215  65 Female   Married   1500       White      94.0 26.7           0
## 18   62217  77 Female    Single   1600 MexAmerican     118.6 30.6           1
## 19   62218  38 Female    Single   8200       Black     120.3 45.4           0
## 20   62224  29 Female   Married   5400    Hispanic      90.1 27.2           0
## 21   62226  80   Male   Married   5400    Hispanic      97.2 28.4           0
## 22   62228  50   Male   Married   8200       White     136.1 43.4           0
## 23   62231  48 Female   Married   9000 MexAmerican     111.0 33.2           0
## 24   62236  61   Male   Married   9000       Asian      90.8 23.2           0
## 25   62239  22 Female              300    Hispanic      78.9 23.3           0
## 26   62248  65   Male   Married   4500       Asian     104.2 26.6           1
## 27   62250  34   Male   Married   9000 MexAmerican      95.1 25.9           0
## 28   62264  77   Male   Married   3500       White     112.0 31.1           0
## 29   62265  52   Male   Married   3500       White     110.0 31.4           1
## 30   62266  64   Male  Divorced   2000       White      74.6 16.6           1
## 31   62278  72 Female   Married   3500       White      91.9 28.3           0
## 32   62282  57 Female  Divorced   2500       Black      90.0 23.7           0
## 33   62284  64 Female   Married   4500       White        NA 25.6           0
## 34   62286  30   Male    Single     NA       Black     130.3 41.0           0
## 35   62288  29   Male    Single   2500       White      78.0 20.1           0
## 36   62291  56   Male   Married   8200       Other     104.5 29.9           0
## 37   62295  69 Female   Widowed    800    Hispanic     103.5 32.7           2
## 38   62308  78 Female   Married   3500       White      94.9 24.6           0
## 39   62309  47 Female   Widowed   1600 MexAmerican     100.3 34.0           1
## 40   62316  39   Male   Married   1600    Hispanic      80.3 21.5           0
## 41   62317  46   Male   Married   3500       White     107.0 27.6           0
## 42   62326  69   Male   Married   6200       White     106.9 26.4           0
## 43   62332  22   Male             1600       White     110.7 32.6           0
## 44   62339  29   Male   Married   9000       White      98.2 29.2           0
## 45   62342  38 Female   Married   4500       White     103.8 32.9           0
## 46   62345  38 Female   Married   9000       White     103.8 31.9           0
## 47   62349  23 Female   Married   2000       White     104.0 38.0           0
## 48   62353  80   Male   Married   9000       White     105.4 27.8           0
## 49   62357  36   Male   Married   9000       White      93.7 25.6           0
## 50   62363  44 Female  Divorced   2500       White      89.7 25.8           0
## 51   62366  80   Male   Married   2500       White      88.6 21.7           2
## 52   62367  50   Male   Married   9000       Asian      94.2 27.4           0
## 53   62370  21   Male    Single   9000       Asian      67.5 18.3           0
## 54   62377  78 Female   Widowed   1000       White      85.2 24.7           0
## 55   62378  68 Female  Divorced   4500    Hispanic      97.0 33.2           0
## 56   62384  40   Male Separated   3500       White     108.2 30.5           0
## 57   62386  35   Male   Married   4500       Other     119.7 38.4           0
## 58   62390  25 Female    Single   4500       Asian      69.6 18.7           0
## 59   62393  20   Male    Single   3500 MexAmerican      87.8 27.1           0
## 60   62397  70 Female   Widowed   1500 MexAmerican     125.4 40.6           0
## 61   62399  53 Female   Married   2000 MexAmerican      94.4 30.7           0
## 62   62402  48   Male Separated   2500       Asian      82.0 23.3           0
## 63   62409  80 Female   Widowed   1000       White     115.0 30.5           1
## 64   62411  51 Female    Single   3500       Black     100.1 26.3           0
## 65   62413  65   Male             2000       White     127.5 40.0           0
## 66   62418  80   Male   Widowed   2500       White     101.9 23.5           2
## 67   62419  80   Male   Married   2000       White     102.9 26.5           0
## 68   62421  23   Male    Single    300       Asian      82.4 24.5           0
## 69   62424  20   Male    Single   1000    Hispanic     106.0 30.4           0
## 70   62430  27   Male   Married   5400    Hispanic     114.2 37.9           0
## 71   62431  54   Male    Single    800       Black      73.7 18.9           0
## 72   62444  23 Female    Single    300       Black      97.1 33.6           0
## 73   62449  38 Female   Married   8200    Hispanic      89.1 26.4           0
## 74   62464  32   Male             3500       White      98.6 28.2           0
## 75   62465  44 Female   Married   8200       Black      90.8 27.8           0
## 76   62467  65   Male   Married   2000       White      95.0 25.6           0
## 77   62471  76 Female  Divorced     NA       White     101.2 28.0           0
## 78   62474  71 Female   Widowed   1000       White     140.6 56.3           1
## 79   62475  22   Male              300       White      85.1 25.8           0
## 80   62476  40   Male    Single   1000       White      93.1 25.8           0
## 81   62479  36 Female   Married   6200       Asian     100.9 28.1           0
## 82   62480  43   Male   Married   8200       White     100.0 28.5           0
## 83   62481  39 Female Separated   6200    Hispanic      93.6 27.7           0
## 84   62482  32 Female             2500       White      94.4 26.5           0
## 85   62491  61 Female   Married   9000       Asian      94.7 27.8           0
## 86   62494  28   Male   Married   3500    Hispanic      86.9 26.8           0
## 87   62495  44   Male    Single   6200       White      99.3 28.6           0
## 88   62501  30 Female   Married   8200       White      83.3 25.6           0
## 89   62502  35   Male             1000       Black     112.0 36.5           0
## 90   62504  30 Female             1000    Hispanic     111.5 38.9           0
## 91   62510  80 Female   Married   3500       White      99.9 29.8           0
## 92   62512  39   Male   Married   9000       Asian      81.4 19.1           0
## 93   62515  42 Female    Single    300    Hispanic      96.3 31.6           0
## 94   62522  54   Male  Divorced   5400       White     105.4 31.2           0
## 95   62524  23   Male    Single   3500       White      82.3 24.0           0
## 96   62526  62 Female   Married   1700    Hispanic      97.2 28.7           0
## 97   62527  79   Male    Single     NA       Black      95.0 25.8           0
## 98   62528  40   Male               NA    Hispanic      87.7 24.8           0
## 99   62529  59   Male   Married   1700       Black     136.8 45.6           0
## 100  62539  60   Male   Widowed    800       Black     103.3 31.9           1
## 101  62549  53   Male   Married   4500       Asian      83.0 21.5           0
## 102  62551  37 Female   Married   9000       White     147.3 48.2           0
## 103  62556  31 Female   Married   6200       Asian      80.0 22.4           0
## 104  62560  56 Female   Married     NA       Black      93.8 26.4           0
## 105  62565  23   Male    Single   2000       Asian     111.3 31.7           0
## 106  62571  32 Female    Single   8200       White      92.7 27.8           0
## 107  62573  48 Female  Divorced   1000       White     110.8 29.6           0
## 108  62575  24 Female   Married   1700       White      73.2 22.0           1
## 109  62579  78   Male   Married   2000 MexAmerican      94.4 23.8           0
## 110  62585  80 Female   Widowed   1000       Black     101.8 34.3           1
## 111  62587  73   Male             1000       White      98.9 24.8           0
## 112  62593  72 Female   Widowed   3500       White     115.3 34.5           0
## 113  62596  52 Female   Married   2000       Asian     105.9 32.5           0
## 114  62601  65   Male   Married   8200       Black      92.6 26.1           0
## 115  62602  80 Female   Widowed   4500       White      92.2 25.8           0
## 116  62612  38 Female   Married   5400       Asian     100.2 30.5           0
## 117  62616  37 Female   Married   1600       Asian      75.5 19.3           0
## 118  62619  80   Male    Single   3500       White     100.8 24.9           1
## 119  62632  29   Male    Single   2000       Asian     154.7 48.3           0
## 120  62634  68   Male   Married   4500       White     117.8 32.6           0
## 121  62635  27 Female   Married   2000       Asian      90.1 26.1           0
## 122  62658  68   Male  Divorced   2500       White     112.8 34.5           0
## 123  62661  35   Male    Single   3500       White      87.8 21.2           0
## 124  62671  69   Male  Divorced     NA       Black      87.5 26.3           0
## 125  62673  34   Male   Married   4500 MexAmerican        NA 33.8           0
## 126  62674  33 Female   Married   2500       White      81.7 21.5           0
## 127  62677  30 Female   Married   6200 MexAmerican      87.0 27.3           0
## 128  62678  68   Male   Married   2000    Hispanic      92.8 23.7           0
## 129  62682  62 Female   Widowed   1000       White     120.5 34.9           0
## 130  62683  55 Female   Married     NA       Asian      82.3 22.3           0
## 131  62684  29 Female   Married   6200       White     115.7 34.0           0
## 132  62690  26 Female    Single     NA       Black     112.7 35.4           0
## 133  62691  31   Male    Single   3500       Black      80.5 23.6           0
## 134  62694  37   Male    Single   1000       White     133.6 40.1           0
## 135  62701  29 Female             4500    Hispanic     101.8 29.9           0
## 136  62707  49 Female   Married   2500       White     105.0 30.5           0
## 137  62708  52   Male   Married   2500       Asian      81.4 21.9           0
## 138  62716  42 Female   Married   1700       Asian      79.3 23.3           0
## 139  62718  63   Male    Single   2500       Black     100.6 26.8           0
## 140  62719  74   Male Separated   4500    Hispanic      97.5 27.6           0
## 141  62727  80 Female   Married   2500       White      97.5 30.8           2
## 142  62732  71 Female   Married    800 MexAmerican     126.9 38.8           0
## 143  62735  39   Male   Married   9000       White      84.5 22.4           0
## 144  62736  40 Female    Single   2500       Black      87.5 22.8           0
## 145  62737  58   Male   Married   1000       Asian      82.5 23.6           1
## 146  62744  37   Male   Married   5400    Hispanic     114.8 33.9           0
## 147  62746  38 Female   Married     NA    Hispanic      97.9 28.6           0
## 148  62750  45 Female  Divorced   1000       Asian      80.1 20.3           1
## 149  62757  54   Male  Divorced   6200       White     127.7 36.1           0
## 150  62759  22 Female    Single   5400       Black        NA 32.3           0
## 151  62763  29   Male   Married   9000       White     112.0 31.8           0
## 152  62764  51 Female    Single    300    Hispanic     122.5 48.6           0
## 153  62765  29 Female   Married   3500       Asian        NA 18.9           0
## 154  62768  38 Female Separated   1600 MexAmerican      96.4 32.2           1
## 155  62771  30   Male    Single    800       Black      92.5 27.4           1
## 156  62773  50 Female  Divorced    300       White      83.4 23.2           0
## 157  62777  28   Male    Single   2000       Other      92.3 25.4           0
## 158  62787  21 Female    Single   9000       Asian      73.0 22.5           0
## 159  62789  26 Female             2000       Asian      96.2 31.8           0
## 160  62792  52 Female  Divorced   1000       White     133.0 42.3           0
## 161  62804  69   Male   Married   8200       White     107.8 30.8           0
## 162  62808  44 Female   Married   2000 MexAmerican     100.8 31.4           0
## 163  62809  51 Female   Widowed    300       White      82.8 21.0           1
## 164  62811  40 Female    Single   2500       Black     109.2 37.0           0
## 165  62814  72   Male   Widowed   2000       Black      89.6 24.4           0
## 166  62817  41   Male             1000       Black     112.2 31.9           0
## 167  62838  44 Female    Single   1000       Black      80.2 22.3           0
## 168  62840  60   Male   Married   2000       White     126.5 35.8           0
## 169  62847  44   Male   Married   9000    Hispanic      96.3 26.5           0
## 170  62849  40 Female   Married   9000       Black     163.5 68.7           0
## 171  62851  27   Male    Single   2000       White      82.9 24.0           1
## 172  62855  47 Female  Divorced   8200       White     109.1 38.0           0
## 173  62859  53 Female  Divorced   3500       Black     120.1 34.9           0
## 174  62860  55   Male   Married   2500       Asian      74.0 20.9           0
## 175  62861  80 Female   Married   2000       White      74.4 18.4           1
## 176  62864  57 Female    Single    300       White     103.0 29.9           0
## 177  62871  48   Male   Married   9000       Other      96.9 24.6           0
## 178  62874  33 Female             2500 MexAmerican     101.0 31.5           0
## 179  62876  74 Female   Widowed   3500       White     106.6 33.5           0
## 180  62881  57 Female   Married   9000       White      93.9 25.0           0
## 181  62883  80 Female   Married   3500       White      89.0 25.1           0
## 182  62885  60   Male   Widowed   9000       Black        NA 30.0           0
## 183  62892  50   Male             1600       Black      92.9 28.5           0
## 184  62893  21 Female Separated   2500 MexAmerican     104.2 34.9           1
## 185  62899  45 Female               NA    Hispanic      82.6 24.5           0
## 186  62900  68 Female   Widowed   2500       Black      94.2 31.3           0
## 187  62916  22   Male    Single   1600 MexAmerican     108.0 31.7           0
## 188  62919  34 Female   Married    300       White      76.8 20.6           0
## 189  62922  31 Female    Single   2500       White      75.5 22.7           0
## 190  62927  63   Male   Married   9000       White     109.0 30.8           0
## 191  62928  43 Female    Single   2500       Black     119.4 33.5           0
## 192  62929  68   Male   Married     NA       Black     100.6 28.1           1
## 193  62930  23   Male    Single   1600 MexAmerican     101.9 31.2           0
## 194  62936  35 Female   Married   2000       White      82.0 23.5           0
## 195  62937  63 Female   Married   2000       Black     106.1 37.6           0
## 196  62941  55 Female Separated   1600       Black      76.1 20.3           0
## 197  62945  48 Female   Married   9000       Black      88.3 28.1           0
## 198  62948  79   Male   Married   9000       White     119.8 34.8           0
## 199  62955  31 Female   Married   9000       White      76.9 18.3           0
## 200  62982  66 Female   Widowed   1000       White     110.0 33.6           1
## 201  62985  68   Male   Married   3500       Asian     101.0 27.1           0
## 202  62993  34 Female   Married   8200       White      86.0 24.5           0
## 203  62997  60   Male   Married   1000       White     124.0 36.4           0
## 204  63002  54 Female   Married   4500    Hispanic     106.6 30.2           0
## 205  63003  40   Male   Married   1500       White     120.5 34.1           0
## 206  63004  38 Female   Married   9000       Asian      66.2 18.5           0
## 207  63010  78 Female   Widowed   3500       Black     111.7 30.1           0
## 208  63012  65   Male   Married   6200       White     102.3 26.7           0
## 209  63021  46 Female    Single   3500       Asian      80.0 24.5           0
## 210  63022  49   Male   Married   8200       White     101.4 28.9           0
## 211  63023  25   Male             1000       White      77.3 22.4           0
## 212  63030  21   Male             1000 MexAmerican      93.7 25.9           0
## 213  63036  74 Female  Divorced    800       Asian     111.7 35.3           2
## 214  63040  54 Female   Married     NA       Asian      78.7 19.1           0
## 215  63041  35   Male    Single   9000       Asian      91.8 27.1           0
## 216  63043  20 Female    Single     NA       Asian      86.4 24.6           0
## 217  63050  24   Male    Single   6200       Black      88.0 27.3           0
## 218  63051  30   Male   Married   8200       Asian      89.5 24.9           0
## 219  63056  21   Male    Single   1000       Asian      67.8 18.9           0
## 220  63057  29   Male    Single   2500       White      84.2 20.8           0
## 221  63064  61   Male Separated   1000       Black      87.2 18.7           1
## 222  63077  38   Male   Married   9000       White      88.7 24.4           0
## 223  63081  62   Male   Married   3500       Other      97.0 25.3           1
## 224  63082  59 Female              800       White      83.0 22.1           0
## 225  63083  71 Female   Widowed   3500       White     114.9 34.3           1
## 226  63088  44   Male   Married   6200       Asian        NA 26.9           0
## 227  63091  70   Male             4500       White     121.8 31.3           0
## 228  63094  80   Male   Married   3500       White     110.8 28.4           0
## 229  63097  70   Male   Married   3500       White      94.3 21.6           0
## 230  63106  50   Male  Divorced   1000       White      95.4 27.9           0
## 231  63107  66 Female   Married   1000    Hispanic      86.4 23.5           0
## 232  63109  41 Female   Married   8200       White     113.2 36.3           0
## 233  63112  66 Female   Married   2500       Asian      92.8 24.6           0
## 234  63116  34 Female    Single   4500       White      73.0 19.4           0
## 235  63117  24   Male             2000       Asian      91.0 26.2           0
## 236  63123  55   Male    Single    800       Black        NA 34.5           0
## 237  63124  54 Female   Married   5400       Asian      86.4 23.1           1
## 238  63125  46 Female   Married   3500       Black      88.8 25.3           0
## 239  63126  44   Male   Married   9000       White      99.1 27.0           0
## 240  63127  28   Male   Married   8200       Asian      89.9 27.7           0
## 241  63133  24   Male             4500 MexAmerican      98.4 29.8           0
## 242  63137  49   Male   Married   9000       Asian     101.5 24.7           0
## 243  63139  25 Female   Married   1000       Black     108.5 34.3           0
## 244  63141  34 Female   Married   6200       Black     105.4 31.9           0
## 245  63142  54   Male   Married   6200       Black      97.3 25.1           0
## 246  63143  70   Male   Married   1600       Asian     104.6 30.9           0
## 247  63145  50   Male Separated   2000       Black      75.5 19.6           2
## 248  63147  41   Male   Married   2500       White     109.4 30.0           0
## 249  63152  62 Female    Single    300       Asian      87.3 22.0           0
## 250  63156  70 Female   Married   4500       White      91.5 29.0           0
## 251  63159  48   Male   Married   1600       White     127.1 37.6           0
## 252  63167  37   Male   Married   1700       Asian     101.2 29.2           0
## 253  63172  68 Female   Widowed   2500 MexAmerican      93.0 24.1           0
## 254  63177  60   Male Separated   6200       Black      88.6 24.0           0
## 255  63180  50   Male   Married   9000       Asian      92.0 26.2           0
## 256  63183  44 Female    Single   1600       Black     103.2 34.1           0
## 257  63188  60 Female Separated   1000       Black     136.2 54.2           1
## 258  63191  30 Female   Married   3500       White      81.4 24.2           0
## 259  63195  59   Male   Married   4500    Hispanic     103.1 27.4           0
## 260  63196  39   Male   Married   1700       Black      90.5 26.3           0
## 261  63203  80 Female   Widowed   1000       White     107.0 27.8           1
## 262  63205  67   Male   Married   3500       White        NA 20.8           0
## 263  63209  39   Male   Married   4500       White     105.2 27.6           0
## 264  63211  46 Female   Married   8200       White     124.0 40.8           0
## 265  63214  37   Male             2000 MexAmerican     110.0 31.9           0
## 266  63218  35   Male   Married   1000 MexAmerican     101.3 30.3           0
## 267  63219  39   Male    Single   9000       Asian      79.9 20.6           0
## 268  63220  27   Male    Single    800       White      98.6 26.3           0
## 269  63221  67 Female   Widowed   4500 MexAmerican     121.3 37.0           0
## 270  63224  31 Female   Married   3500 MexAmerican     103.0 29.3           0
## 271  63230  48   Male    Single   5400       Asian      96.0 28.2           0
## 272  63231  42 Female    Single    300    Hispanic        NA 30.9           0
## 273  63234  35 Female    Single   1000       Asian      90.5 24.6           0
## 274  63236  80   Male  Divorced   1000    Hispanic     105.0 29.4           2
## 275  63242  59   Male   Married   2500 MexAmerican      90.2 25.4           0
## 276  63248  75   Male   Married   9000       White     102.4 26.6           0
## 277  63260  42 Female Separated     NA       Other      78.0 21.3           0
## 278  63263  53   Male   Married   2500    Hispanic     102.9 29.2           0
## 279  63272  20 Female    Single     NA       Other      74.4 22.3           0
## 280  63276  67   Male   Widowed   1000       White     138.5 41.0           0
## 281  63281  40   Male   Married   2500 MexAmerican      88.2 29.1           0
## 282  63284  79   Male   Married   3500       White     100.2 30.6           0
## 283  63285  80 Female   Widowed   1000       White      95.0 26.2           1
## 284  63287  78 Female   Widowed     NA       Black      97.0 25.9           2
## 285  63291  47   Male  Divorced   8200       Black     126.0 40.5           0
## 286  63293  61 Female   Widowed   2000 MexAmerican      84.1 30.1           0
## 287  63295  80   Male   Married   2500       White      97.1 23.3           0
## 288  63296  55 Female   Married   9000       Asian      78.8 23.2           0
## 289  63298  22 Female    Single   9000       Asian      65.8 19.4           0
## 290  63302  28   Male    Single   2000       White      88.2 22.6           0
## 291  63305  37   Male  Divorced   3500       White      93.0 26.7           0
## 292  63308  28   Male    Single    800       Black      81.0 22.9           0
## 293  63312  74   Male   Married   3500       White     102.3 23.5           1
## 294  63320  27 Female   Married   3500       Asian      74.0 20.9           0
## 295  63323  48 Female   Married   9000       Asian      70.7 19.3           0
## 296  63326  51 Female   Married     NA       Black     114.4 38.9           0
## 297  63329  71 Female   Married   9000       White     102.4 31.1           0
## 298  63330  51   Male   Married   1700       White      76.0 20.2           1
## 299  63331  31 Female   Married   2500       White     145.3 50.8           0
## 300  63338  31   Male  Divorced   8200       Black      93.3 30.4           0
## 301  63340  26   Male   Married   2000       White     104.1 29.7           0
## 302  63341  48   Male   Married   5400       Asian     112.5 31.9           0
## 303  63343  45 Female   Married   8200       White     139.5 43.0           0
## 304  63344  26 Female   Married   9000 MexAmerican      78.0 21.0           0
## 305  63345  68 Female   Married   2500       Black      80.4 21.5           0
## 306  63352  64   Male   Married   9000       White        NA 22.9           1
## 307  63353  23 Female   Married    300       White     106.4 31.5           0
## 308  63357  31 Female             1600 MexAmerican     114.0 39.2           0
## 309  63360  80 Female   Widowed   4500       White      76.1 15.7           0
## 310  63363  65 Female    Single    800       Other     123.3 36.7           0
## 311  63365  50 Female   Married   2000    Hispanic     101.0 30.2           0
## 312  63373  29 Female    Single   5400       Asian        NA   NA           0
## 313  63377  39 Female    Single   9000       Black     118.0 37.5           2
## 314  63383  51   Male   Married   2500       Black     109.0 33.5           0
## 315  63385  62 Female             2000       Black     106.8 33.3           0
## 316  63387  20   Male    Single    300       Black      74.1 21.2           0
## 317  63389  80   Male   Married   2500       White      97.1 22.7           0
## 318  63391  70   Male   Married   3500    Hispanic     103.6 30.7           0
## 319  63400  21 Female             2500       Black      97.1 28.6           1
## 320  63426  58   Male  Divorced   1000       White     105.8 26.9           0
## 321  63436  80 Female   Widowed   9000       White        NA 21.2           2
## 322  63439  51   Male   Married   6200    Hispanic     114.6 32.3           2
## 323  63442  51 Female  Divorced   1600       Black     116.2 33.6           0
## 324  63451  28   Male    Single   1500       Black      88.2 28.4           1
## 325  63453  48   Male   Married   1500 MexAmerican     123.0 38.5           2
## 326  63456  80   Male   Widowed   9000 MexAmerican      81.6 19.6           1
## 327  63463  61 Female   Married   9000       White      83.4 21.7           0
## 328  63466  49   Male    Single   8200       Black      85.0 22.8           0
## 329  63472  24 Female             2000       White      94.6 24.6           0
## 330  63473  80   Male   Married   3500       White        NA 20.8           1
## 331  63474  74   Male   Married   3500       White     112.4 31.8           0
## 332  63481  48 Female   Married   1600    Hispanic      99.7 29.8           0
## 333  63482  43 Female   Married   6200       Black      94.8 27.3           0
## 334  63489  32   Male   Married   6200       White     125.2 37.8           0
## 335  63496  58   Male  Divorced   2500       White      99.9 26.0           0
## 336  63498  70 Female   Widowed   2500       Black        NA 30.1           0
## 337  63499  33 Female             4500    Hispanic     115.5 43.2           0
## 338  63502  73   Male   Married   2000       White     120.3 33.5           1
## 339  63504  54   Male   Married   6200 MexAmerican     112.9 31.8           0
## 340  63510  56 Female   Married   9000       White      90.6 21.6           0
## 341  63515  54 Female   Married   8200       White      95.2 27.1           0
## 342  63519  54   Male Separated   5400       Black      95.4 25.5           0
## 343  63523  22 Female    Single   3500       Other      75.5 21.0           0
## 344  63528  34 Female   Married   2500       Black     140.7 49.2           0
## 345  63529  23   Male    Single   1600       White      79.5 19.1           0
## 346  63531  32   Male             1500 MexAmerican      94.1 28.0           0
## 347  63532  54   Male Separated   1700       Black     117.7 33.9           1
## 348  63534  39   Male   Married   4500    Hispanic      91.6 27.3           0
## 349  63541  70   Male   Married   1700    Hispanic      91.6 25.8           1
## 350  63543  74 Female   Married   1500       Asian      87.0 25.6           0
## 351  63550  51 Female    Single    800       Black     113.7 37.3           0
## 352  63551  54 Female   Married   9000       White      94.3 28.6           0
## 353  63559  41   Male   Married   9000       Asian      90.5 24.9           0
## 354  63560  40   Male   Married   3500       White     107.2 31.1           0
## 355  63562  22   Male    Single    300       White      74.2 20.1           0
## 356  63566  62 Female   Widowed   1000       Black     118.2 38.8           0
## 357  63569  49 Female    Single     NA    Hispanic     100.4 30.7           2
## 358  63571  36   Male             6200       Asian      85.0 25.4           0
## 359  63572  28 Female    Single   3500       White      95.8 33.8           0
## 360  63573  20 Female    Single   3500       Black      71.5 20.0           0
## 361  63576  46   Male             9000    Hispanic      99.0 27.7           0
## 362  63579  63   Male    Single   4500       White      88.3 24.3           1
## 363  63589  80   Male   Married     NA       Asian      94.5 24.8           1
## 364  63593  77   Male   Married     NA       White     112.8 31.9           0
## 365  63602  34   Male             2000       Black      73.8 20.5           0
## 366  63607  41   Male   Married   9000 MexAmerican     100.5 28.9           0
## 367  63609  66   Male   Married   2000       Other      96.3 26.7           0
## 368  63613  30   Male   Married   5400    Hispanic      84.6 19.5           0
## 369  63614  58 Female  Divorced    800       White     102.4 28.8           0
## 370  63615  26 Female    Single   5400       White      78.0 23.6           0
## 371  63625  23 Female              800 MexAmerican      82.1 22.5           1
## 372  63629  36 Female   Married   3500       Asian      76.8 20.1           0
## 373  63632  80 Female   Married   3500       White      86.0 24.3           2
## 374  63633  48   Male   Married   9000       Black     110.2 30.6           1
## 375  63635  79   Male   Married   3500       White        NA   NA           1
## 376  63638  47 Female   Married   6200       White     116.0 35.0           1
## 377  63642  25   Male              800       Black      96.6 28.9           0
## 378  63648  31 Female   Married   3500       White     125.3 45.1           0
## 379  63657  30   Male   Married   8200       Asian     103.5 28.3           0
## 380  63659  80   Male   Widowed   8200       White     111.0 29.7           0
## 381  63661  46 Female   Married    800       White      97.1 26.2           0
## 382  63662  80   Male   Married   6200       White     109.0 29.3           0
## 383  63663  42 Female Separated   1600 MexAmerican      88.1 28.8           0
## 384  63664  58   Male  Divorced   5400       Other      98.0 27.3           0
## 385  63665  56   Male    Single   8200    Hispanic     102.4 29.6           2
## 386  63669  31   Male   Married   4500       White      99.8 30.1           0
## 387  63673  43   Male   Married   2500       White     112.6 32.7           0
## 388  63684  54 Female  Divorced   3500       Black      99.8 28.8           0
## 389  63685  60 Female   Married   2000    Hispanic      87.3 26.3           0
## 390  63689  66 Female   Married   9000       White     102.3 26.4           0
## 391  63690  29   Male   Married   9000       Asian      82.9 22.2           0
## 392  63692  22 Female    Single    800       Black      78.1 24.9           0
## 393  63697  41   Male   Married   6200       Black      92.1 27.0           0
## 394  63699  47 Female    Single   2500       Black      82.5 24.9           0
## 395  63700  40   Male Separated   8200       Black     109.0 31.9           1
## 396  63701  55   Male   Married   9000       White      89.4 25.7           0
## 397  63708  63   Male   Married   4500       Asian     109.6 30.9           1
## 398  63719  21   Male    Single   2000       White      72.9 19.3           0
## 399  63721  22 Female    Single   4500       White      73.0 18.3           0
## 400  63723  62 Female   Married   2000 MexAmerican     101.8 32.1           1
## 401  63731  51   Male  Divorced    300    Hispanic        NA 28.9           0
## 402  63736  36   Male   Married   2500       Black     116.1 36.7           0
## 403  63739  71 Female   Widowed    800       Black      81.5 20.4           0
## 404  63741  72   Male             1600 MexAmerican     101.0 25.7           0
## 405  63744  50 Female   Married   9000       White      82.4 22.0           0
## 406  63750  20 Female    Single    300       Black      85.2 28.0           0
## 407  63752  60   Male  Divorced   1000       White      99.7 27.2           0
## 408  63753  33   Male             1000 MexAmerican      90.0 26.0           0
## 409  63759  56   Male   Married   8200       White      86.0 21.8           0
## 410  63761  21 Female   Married   3500    Hispanic      82.7 22.0           0
## 411  63762  23   Male   Married   2000       White      97.2 28.3           0
## 412  63765  80   Male   Widowed   8200       White      89.4 23.8           1
## 413  63768  64   Male   Married   1700    Hispanic      96.1 25.0           1
## 414  63771  43   Male   Married   3500       White     122.7 39.9           0
## 415  63777  41 Female    Single     NA       White      98.7 33.5           0
## 416  63781  63 Female             4500    Hispanic     104.2 30.4           0
## 417  63784  40 Female   Married   5400 MexAmerican      91.3 23.3           0
## 418  63787  30   Male   Married   2500       White      80.7 20.0           0
## 419  63799  69   Male   Married   2500       Asian      93.2 27.2           2
## 420  63802  48 Female  Divorced   3500       Black     117.0 34.9           0
## 421  63806  70   Male   Married   1700       White     108.3 30.2           0
## 422  63813  67   Male   Widowed   1600       Black      94.9 24.3           1
## 423  63818  40 Female  Divorced    300       White     114.6 34.8           0
## 424  63820  58 Female  Divorced   2000       Black      96.8 27.0           0
## 425  63828  64 Female   Married   6200       White      88.7 26.1           0
## 426  63829  42 Female   Married   6200       White      72.0 18.7           0
## 427  63831  23 Female             1700       Black     100.4 30.4           0
## 428  63837  70 Female   Widowed   6200       White     121.6 39.7           0
## 429  63838  78 Female   Widowed   1600       White     109.7 30.8           0
## 430  63841  27   Male   Married   6200 MexAmerican     109.8 33.1           0
## 431  63845  43   Male  Divorced   1000       White     107.1 31.9           1
## 432  63849  34   Male   Married   8200       White      96.3 30.1           0
## 433  63853  36 Female   Married   9000       White      74.5 18.5           1
## 434  63856  20 Female    Single    300       Black      68.5 18.7           1
## 435  63858  20 Female             4500    Hispanic     106.2 39.1           0
## 436  63859  55   Male   Married   1000       Black     115.0 33.5           0
## 437  63860  50 Female   Married   5400       Other      90.3 27.3           0
## 438  63871  45 Female   Married   3500       Black     115.5 33.6           0
## 439  63877  20 Female    Single    300       Black      64.7 17.7           1
## 440  63879  76   Male   Widowed   3500       White      99.6 23.6           2
## 441  63887  64 Female   Widowed   3500       White     127.2 40.1           0
## 442  63890  60 Female Separated   1000    Hispanic     108.3 38.7           1
## 443  63905  23   Male    Single    800       Asian        NA 18.8           0
## 444  63909  62 Female   Married   1000       White     100.8 32.2           0
## 445  63915  40 Female   Married   3500       White     133.5 36.7           0
## 446  63916  34   Male   Married   1600       White     129.5 38.4           0
## 447  63923  52 Female   Married   9000       Black     100.5 30.0           0
## 448  63924  29 Female Separated   1600       Black     130.0 41.9           1
## 449  63929  34 Female   Married   9000    Hispanic     109.7 33.3           0
## 450  63936  35   Male    Single   3500       White     114.0 32.2           0
## 451  63939  66   Male   Married   2000       Black      97.3 27.8           0
## 452  63941  53 Female   Married   5400       Asian      78.9 19.0           0
## 453  63942  42 Female   Married   1700       White      70.5 18.1           0
## 454  63944  20   Male    Single     NA       White     127.0 43.3           0
## 455  63945  29 Female    Single   6200       White      97.8 30.1           0
## 456  63946  39   Male   Married   2500       White     102.2 29.8           0
## 457  63948  50 Female             8200       Black     100.0 28.1           0
## 458  63954  41   Male   Married   2500       Asian      93.5 29.8           0
## 459  63957  59 Female    Single   3500 MexAmerican     112.2 35.4           0
## 460  63959  41   Male             2500       White      96.7 26.1           0
## 461  63960  21   Male    Single   2500       Black     138.1 43.2           0
## 462  63966  34 Female              300       Black     124.6 42.0           0
## 463  63967  24 Female    Single   2000       Asian      78.5 22.9           0
## 464  63977  22 Female    Single   2500       Black      86.4 25.3           0
## 465  63982  69 Female   Widowed   3500       White     122.1 32.7           0
## 466  63983  31   Male   Married   2000       White     101.5 27.0           0
## 467  63984  24   Male    Single   2500       Other      81.1 24.0           0
## 468  63989  53 Female  Divorced   1000       Other        NA 13.6           0
## 469  63991  44 Female    Single    800       Black      97.9 26.9           0
## 470  63992  44   Male    Single    300       White     137.5 40.0           1
## 471  63997  79 Female   Widowed   1500       White      90.1 24.3           0
## 472  63999  44 Female   Married   9000       Asian      74.8 21.6           0
## 473  64000  31   Male    Single     NA       Black     109.2 31.8           0
## 474  64013  80   Male   Widowed    800       Asian     105.3 27.4           0
## 475  64021  62 Female   Married   6200 MexAmerican     103.2 34.2           0
## 476  64024  62 Female  Divorced   1600       White     135.8 47.2           0
## 477  64025  31   Male             8200       White      93.7 26.5           0
## 478  64029  22   Male    Single   3500 MexAmerican     105.4 32.0           0
## 479  64032  46   Male  Divorced   4500 MexAmerican      99.0 26.8           0
## 480  64034  62 Female   Married   2000 MexAmerican     101.3 27.1           2
## 481  64036  69   Male             2000       White     120.1 30.3           1
## 482  64037  28   Male             9000       Other      97.2 29.1           0
## 483  64042  39   Male   Married   1600       White      92.5 26.9           0
## 484  64046  39 Female              800       Black     112.1 31.8           2
## 485  64047  34 Female   Married   4500       White      95.0 31.5           0
## 486  64055  59 Female   Widowed   1600       Black     116.1 39.1           1
## 487  64059  68 Female   Widowed    300       Black      90.2 22.1           0
## 488  64065  46   Male   Married   9000       White     105.6 29.3           0
## 489  64071  67   Male   Widowed   2000       Black      97.6 27.1           0
## 490  64072  50 Female   Married   2500 MexAmerican     110.0 33.9           0
## 491  64084  80   Male   Widowed   1500       White     112.3 30.8           1
## 492  64086  45 Female   Married   5400       Asian      74.8 21.2           0
## 493  64089  54 Female   Married   9000       Other     114.3 32.8           0
## 494  64095  37   Male   Married   8200       White     106.2 31.1           0
## 495  64111  33 Female    Single    300       Black     112.0 33.1           0
## 496  64113  80 Female   Widowed   1000       White     117.7 30.6           1
## 497  64120  77   Male Separated     NA    Hispanic     115.5 31.4           0
## 498  64127  69 Female   Married   3500       Asian     103.7 30.1           0
## 499  64128  59   Male  Divorced   2500       White        NA 39.2           0
## 500  64130  69   Male   Married     NA       Asian      97.0 23.9           2
## 501  64133  36 Female   Married   4500       White      78.8 22.1           0
## 502  64139  32 Female             1600    Hispanic      80.0 25.7           0
## 503  64147  34 Female             1000 MexAmerican      86.4 25.5           0
## 504  64154  59 Female  Divorced   8200       Black     112.2 34.4           0
## 505  64157  68 Female             2000       White      70.2 19.7           0
## 506  64158  27   Male   Married   3500       Black      92.5 26.1           0
## 507  64159  75   Male   Married   2000 MexAmerican        NA 23.9           1
## 508  64161  51 Female    Single   9000       Black     144.4 59.0           0
## 509  64163  48   Male   Married   9000       Asian      98.6 30.3           0
## 510  64164  47   Male   Married   6200       Black        NA 51.1           0
## 511  64167  21 Female    Single    300       Asian      65.6 17.1           0
## 512  64179  52   Male   Married   2000 MexAmerican     106.4 31.9           0
## 513  64180  31 Female   Married   5400    Hispanic      78.7 25.4           0
## 514  64191  72   Male   Married   1600    Hispanic     109.0 25.3           0
## 515  64192  42   Male   Married   9000       White     104.6 28.7           0
## 516  64194  63 Female   Married   9000       Black      93.5 30.2           0
## 517  64198  76 Female   Widowed   1000       Black     104.8 31.4           0
## 518  64203  35   Male              800       White      98.7 28.1           0
## 519  64213  37   Male               NA MexAmerican     127.0 40.1           0
## 520  64222  39   Male   Married   6200       White      92.1 24.9           0
## 521  64228  44   Male    Single   9000       White     121.7 37.0           0
## 522  64231  68   Male   Married   3500    Hispanic     122.2 35.8           0
## 523  64234  29   Male    Single   9000 MexAmerican     127.5 38.6           0
## 524  64235  56 Female             1700 MexAmerican      99.5 38.0           1
## 525  64244  40 Female    Single    800       White      80.2 23.5           0
## 526  64247  42   Male   Married   2000 MexAmerican      85.4 24.7           0
## 527  64248  38 Female    Single   9000       White      87.2 24.9           0
## 528  64252  61   Male   Married   2000    Hispanic      95.2 25.2           0
## 529  64261  67   Male   Married   9000       Asian      91.6 24.5           0
## 530  64263  62 Female   Married   2500 MexAmerican      78.3 25.7           0
## 531  64266  31   Male             9000       White      95.6 26.5           0
## 532  64270  47 Female   Married   2000       Other     123.5 42.0           1
## 533  64281  44   Male   Married   8200    Hispanic     119.7 36.6           0
## 534  64286  56 Female   Married   9000       Asian      85.8 24.0           0
## 535  64290  65 Female  Divorced   6200       Black     122.5 35.6           0
## 536  64298  68 Female   Widowed   6200       Black     106.2 33.5           0
## 537  64308  31 Female             1000    Hispanic      85.4 27.9           0
## 538  64309  78 Female   Married   1500       White        NA 35.5           0
## 539  64313  65   Male             4500 MexAmerican      95.7 25.8           0
## 540  64315  52 Female    Single   2500       White      91.0 24.9           0
## 541  64325  44   Male  Divorced   8200       White     105.3 28.9           0
## 542  64326  29   Male             5400       White      77.0 18.8           1
## 543  64328  78   Male   Married    800 MexAmerican      77.0 17.7           0
## 544  64329  80   Male   Married   5400       White     128.5 34.9           0
## 545  64333  46   Male  Divorced   2000       Asian      86.3 26.4           0
## 546  64335  27 Female               NA       White      73.1 18.4           0
## 547  64336  31   Male             3500       White     112.0 30.5           0
## 548  64343  63   Male   Married   9000       White     108.0 32.4           0
## 549  64345  21   Male    Single    300       Other      80.7 20.6           0
## 550  64349  24 Female    Single     NA       Asian      72.9 18.8           0
## 551  64364  80 Female  Divorced   1700       White      76.8 22.7           1
## 552  64367  39 Female   Married   9000       Asian      79.8 23.3           0
## 553  64368  70   Male  Divorced    800       Black      95.6 24.3           0
## 554  64370  25   Male    Single   1000       White      75.9 21.6           0
## 555  64376  58   Male  Divorced   1000       White      91.6 22.5           0
## 556  64379  20 Female    Single   1000       Black      77.7 25.0           0
## 557  64381  61 Female   Married   9000       White      87.4 24.0           1
## 558  64382  24   Male              300       Asian      68.2 17.8           0
## 559  64383  26 Female Separated   1500       Black     107.6 33.0           0
## 560  64390  45 Female    Single   1600       Black     100.9 34.2           0
## 561  64391  26 Female             2500    Hispanic      78.2 21.7           0
## 562  64396  51 Female  Divorced     NA       White      93.4 29.0           0
## 563  64399  45 Female  Divorced   1000       White      84.8 25.4           0
## 564  64405  78   Male   Married   1000       Asian        NA   NA           0
## 565  64417  20 Female    Single   9000       White      77.8 21.9           0
## 566  64419  63 Female   Married   2000 MexAmerican     125.9 45.0           0
## 567  64427  37   Male   Married   9000       White     121.2 36.5           0
## 568  64433  80   Male   Married   2500       White      90.5 23.1           0
## 569  64436  34 Female             8200    Hispanic      95.2 28.4           0
## 570  64437  21 Female    Single    800       Black      97.1 29.3           0
## 571  64439  53   Male   Married   9000       White      97.3 26.3           0
## 572  64446  47   Male   Married   3500       White      98.1 26.3           0
## 573  64447  41 Female    Single   1600       White      85.0 24.7           0
## 574  64451  32   Male             2500       White      95.1 27.7           0
## 575  64459  55 Female   Married   6200       White     138.5 43.6           1
## 576  64463  80 Female   Widowed   1500       White      86.7 23.9           0
## 577  64471  37 Female   Married   9000       White      85.5 25.5           0
## 578  64473  79   Male   Married   2500       Black     100.0 30.0           0
## 579  64474  40   Male   Married   9000       Black     107.0 34.3           0
## 580  64475  62   Male   Married   4500    Hispanic      94.7 25.8           0
## 581  64484  26 Female   Married   9000       Asian      76.3 20.9           0
## 582  64485  32   Male             1000    Hispanic     111.5 35.4           0
## 583  64488  39 Female Separated   1600       Black      90.1 30.4           0
## 584  64494  39 Female    Single   5400       Black     109.1 38.7           0
## 585  64497  60   Male    Single   2000       White     112.1 32.7           0
## 586  64498  47 Female   Married   9000       Asian      79.2 20.8           0
## 587  64499  63   Male   Married   5400 MexAmerican     101.2 28.3           0
## 588  64500  29 Female             5400       White      72.3 22.5           0
## 589  64504  57 Female   Widowed   1600       Black      84.5 25.3           0
## 590  64524  28   Male    Single    800       White      79.2 20.6           0
## 591  64525  21 Female   Married   2000       White      70.0 19.9           0
## 592  64526  49 Female             4500       White     125.7 39.5           0
## 593  64532  43 Female   Married   9000       Black      92.8 27.7           0
## 594  64536  75 Female   Married   9000       White      97.0 28.1           1
## 595  64544  69   Male   Married   8200       Asian     102.4 29.7           0
## 596  64548  59 Female   Widowed    800       Asian     101.6 27.2           0
## 597  64558  62   Male   Married   8200       Black     107.3 29.6           0
## 598  64559  70 Female   Married   3500       White     132.2 39.4           0
## 599  64567  37   Male   Married   9000    Hispanic      91.0 23.1           0
## 600  64584  41   Male   Married     NA       Asian      88.2 24.9           0
## 601  64591  51   Male   Married   1600       Black      92.4 26.4           0
## 602  64592  29 Female             3500 MexAmerican      97.7 32.6           0
## 603  64593  47   Male   Married   9000       Asian      89.8 24.3           0
## 604  64602  59 Female   Widowed   8200 MexAmerican      84.3 23.3           0
## 605  64603  40 Female   Married   9000       Asian        NA   NA           0
## 606  64604  50 Female  Divorced   2000    Hispanic     109.3 38.3           0
## 607  64606  59 Female   Widowed   2000    Hispanic     129.3 40.2           0
## 608  64611  50   Male   Married   8200       Black     137.0 45.8           0
## 609  64617  60   Male   Married     NA    Hispanic     104.4 32.9           0
## 610  64620  36   Male   Married   1700       Asian      78.8 19.9           2
## 611  64621  38   Male   Married   8200    Hispanic     104.0 26.9           0
## 612  64625  69   Male   Married   3500       Black      95.8 26.0           0
## 613  64632  21   Male    Single   6200    Hispanic     101.6 30.6           0
## 614  64637  77   Male   Married     NA    Hispanic     122.5 35.5           0
## 615  64639  58   Male   Married   5400       Black     132.2 43.1           0
## 616  64646  80   Male   Married   3500       White      95.0 25.8           1
## 617  64648  36   Male   Married   9000 MexAmerican      74.2 20.5           0
## 618  64651  58   Male    Single   1000       White     111.3 31.1           0
## 619  64663  33 Female   Married   3500       Other     102.8 34.7           0
## 620  64664  48 Female  Divorced   1600       White     105.0 36.3           0
## 621  64669  60 Female  Divorced   2500       White      85.3 23.5           0
## 622  64672  22   Male    Single   3500       Black      79.6 26.6           0
## 623  64674  39 Female   Married   3500 MexAmerican      85.0 28.0           0
## 624  64679  38 Female  Divorced   3500       Asian      77.0 25.0           0
## 625  64682  42   Male   Married   8200       White     107.2 32.5           0
## 626  64687  24 Female             1600       Black      86.8 25.8           0
## 627  64689  42 Female    Single   1600 MexAmerican      85.6 26.2           0
## 628  64695  38 Female   Married   8200       Asian      79.6 20.7           0
## 629  64703  22 Female    Single   2000    Hispanic      90.0 25.3           0
## 630  64706  20 Female    Single   2500       Black     100.0 32.5           0
## 631  64720  29   Male             4500       Black      74.2 20.6           0
## 632  64721  56   Male  Divorced   2000       Black     114.1 31.4           1
## 633  64722  33 Female   Married   3500 MexAmerican      75.0 25.0           0
## 634  64725  39 Female             4500       White     110.4 34.3           0
## 635  64726  55   Male   Married   4500       Black     101.2 26.0           0
## 636  64734  68 Female   Married   2000       Black     111.6 32.4           0
## 637  64739  21 Female    Single   9000       Black      90.8 30.2           0
## 638  64742  56   Male  Divorced   1600       Black     116.8 38.0           0
## 639  64746  29   Male    Single   9000       Black     102.3 30.2           0
## 640  64756  72   Male   Married   6200    Hispanic      96.2 28.0           0
## 641  64759  80   Male   Married   2000       White     101.8 24.8           0
## 642  64765  32   Male   Married   3500       White     108.6 33.7           0
## 643  64768  27   Male   Married   2500       White      81.9 23.4           0
## 644  64769  51   Male    Single    800       Black      90.1 26.0           0
## 645  64771  64   Male  Divorced   1000 MexAmerican      99.1 26.3           0
## 646  64779  30 Female    Single   3500       Black     129.2 48.4           0
## 647  64782  50   Male  Divorced    800       White      80.5 21.0           0
## 648  64789  67   Male   Married   9000       Black     120.3 30.9           0
## 649  64794  29 Female             2500       Black        NA 37.1           0
## 650  64802  42   Male    Single   4500       Black      82.0 21.9           0
## 651  64803  35   Male   Married   2500       White     104.8 29.1           0
## 652  64805  38   Male    Single    800       Black     142.0 48.0           1
## 653  64807  35 Female   Married   8200       White      88.5 26.7           0
## 654  64816  21   Male    Single    300       Other      85.0 22.1           0
## 655  64821  62   Male Separated   4500       Black     122.0 36.4           0
## 656  64824  62   Male  Divorced    800       White     132.2 32.7           0
## 657  64828  58 Female   Married   2000 MexAmerican      92.1 26.5           0
## 658  64831  24   Male    Single   2000       Other      87.0 26.8           0
## 659  64832  32   Male             3500 MexAmerican     103.0 30.5           0
## 660  64833  37 Female   Married   2000 MexAmerican     108.9 37.2           0
## 661  64839  37   Male   Married   8200 MexAmerican     103.6 32.0           0
## 662  64843  50 Female   Married   2500       Black     115.4 35.2           0
## 663  64854  69 Female   Married   2500    Hispanic     107.7 29.4           0
## 664  64857  54 Female  Divorced   1600       White     127.0 47.7           0
## 665  64859  46 Female   Married   4500       White      96.0 26.5           0
## 666  64866  25 Female    Single   1600       Black      84.4 25.3           0
## 667  64871  49 Female   Married   8200       White      86.0 23.1           0
## 668  64873  41 Female   Married   9000       White      83.2 23.5           0
## 669  64876  47   Male  Divorced   1000       White      93.5 23.7           0
## 670  64877  46   Male    Single    300       Black     111.5 32.5           0
## 671  64882  65   Male   Married   8200       White     106.9 27.6           0
## 672  64892  21   Male    Single   2000       Black      81.3 25.1           0
## 673  64893  23 Female    Single   9000       White      71.3 18.9           0
## 674  64897  42   Male             1600       Asian      82.2 20.2           0
## 675  64898  45   Male   Married    800       Black      76.0 22.8           0
## 676  64904  52 Female             1600       White     106.2 28.7           0
## 677  64908  60 Female  Divorced   2500 MexAmerican      96.2 27.0           0
## 678  64914  31   Male    Single   3500       Asian      74.7 18.9           0
## 679  64916  31   Male    Single   1000       White      97.0 29.1           0
## 680  64923  64 Female   Married   4500       Black     106.0 32.8           0
## 681  64928  80   Male  Divorced   2500       Black      79.5 21.3           0
## 682  64930  74   Male  Divorced   1600       White     107.2 27.9           2
## 683  64931  59 Female   Married   2500       Black      87.0 23.2           2
## 684  64933  41 Female   Married   9000 MexAmerican     111.7 30.5           0
## 685  64948  61 Female   Widowed   2000       Black     115.0 35.9           0
## 686  64951  22   Male   Married   1600       White     100.0 28.9           0
## 687  64953  44 Female   Married   1000       White      70.2 19.1           0
## 688  64954  54 Female  Divorced   3500       Asian      70.5 18.6           0
## 689  64962  32 Female   Married   8200       Black     105.0 34.7           0
## 690  64963  55   Male    Single   8200       Black     146.7 45.0           0
## 691  64968  50 Female   Married   9000       Black      79.2 21.8           0
## 692  64974  42 Female    Single   3500       Black     128.1 42.3           0
## 693  64976  69   Male   Married   6200       Black     100.8 26.6           0
## 694  64978  56 Female   Married   2000    Hispanic      95.1 27.5           0
## 695  64979  47 Female    Single    800       Black     113.1 42.9           0
## 696  64981  46   Male   Married   2000       White     101.3 27.4           0
## 697  64994  27   Male   Married   2000       White      83.0 23.9           0
## 698  64998  54   Male    Single   5400       White     116.8 33.1           0
## 699  65002  68   Male               NA       White      84.6 23.0           0
## 700  65005  71 Female   Married   1700       White      94.9 29.1           0
## 701  65006  47 Female Separated   8200       Black      97.3 29.4           0
## 702  65007  24 Female   Married   8200       Asian     113.7 28.8           0
## 703  65009  51 Female    Single   2500       Black     155.9 55.8           0
## 704  65014  59 Female   Married   5400       White     109.5 33.7           0
## 705  65022  29 Female    Single   9000       Asian      72.6 21.7           0
## 706  65028  80   Male   Married   1000       White      88.1 19.4           0
## 707  65032  76 Female   Married   2500       White      92.6 25.8           0
## 708  65036  49 Female   Married   6200       Black     121.0 37.7           0
## 709  65046  74   Male   Married   9000       White      87.4 27.6           0
## 710  65049  24   Male   Married   3500    Hispanic      80.7 23.7           0
## 711  65051  80 Female   Widowed   1000    Hispanic      98.0 27.2           1
## 712  65052  42   Male   Widowed   9000       White      96.8 27.7           0
## 713  65058  80 Female   Married     NA       White      80.6 20.0           0
## 714  65061  38   Male   Married   6200       Asian     104.8 29.7           0
## 715  65065  34 Female   Married   6200       White     113.3 29.2           0
## 716  65067  42 Female   Married   5400       White      74.0 21.0           0
## 717  65069  62   Male   Married   1000 MexAmerican      79.6 24.7           0
## 718  65074  42   Male             6200       Black     147.5 56.6           1
## 719  65077  60   Male   Married     NA    Hispanic      91.3 23.9           0
## 720  65085  51   Male   Married   1600       Black     101.6 29.6           0
## 721  65086  46   Male   Married   9000       White      87.3 25.8           0
## 722  65087  74 Female   Widowed   3500    Hispanic     101.2 27.7           0
## 723  65091  33   Male   Married   2000       White      93.3 27.5           0
## 724  65095  41 Female   Married   3500 MexAmerican     102.4 29.4           0
## 725  65098  68 Female   Married   3500       Black      96.7 31.1           0
## 726  65105  24 Female    Single   6200       Black      88.5 27.7           0
## 727  65106  32   Male             2500       Black      82.0 24.2           0
## 728  65113  43   Male   Married   2500       Asian      87.9 24.2           0
## 729  65129  45 Female   Married   1600       Black      90.8 28.2           0
## 730  65132  33 Female             1600 MexAmerican      85.4 25.3           0
## 731  65135  55   Male   Married   9000       Asian      96.8 27.6           0
## 732  65141  21   Male    Single   1600 MexAmerican      69.1 17.9           0
## 733  65143  62   Male  Divorced   2000       Asian      93.0 25.2           0
## 734  65145  57 Female   Married   6200 MexAmerican      80.3 21.9           0
## 735  65149  31   Male             2000       Black      98.0 29.6           0
## 736  65156  44   Male  Divorced   2000       White      83.5 22.0           0
## 737  65163  70   Male   Married   1700       White     114.6 31.3           0
## 738  65174  31 Female   Married   8200       White     102.6 29.7           0
## 739  65177  22   Male    Single   6200       White      80.3 22.8           0
## 740  65182  45   Male             1000    Hispanic      87.9 24.7           0
## 741  65188  59 Female   Married   9000       Asian      91.5 25.7           1
## 742  65189  63   Male               NA    Hispanic     107.4 31.3           1
## 743  65191  30 Female             2500       Asian      73.9 18.2           0
## 744  65194  31   Male    Single   2000       Asian      83.0 22.5           0
## 745  65195  43   Male   Married   9000       Black     125.1 39.4           0
## 746  65199  51 Female   Married   3500       Asian      87.2 24.6           0
## 747  65201  77 Female   Married   9000       White      80.3 22.9           0
## 748  65202  45   Male Separated   2000    Hispanic      87.0 25.6           0
## 749  65205  56   Male             3500       White      85.2 22.8           0
## 750  65210  48 Female  Divorced   1000       White     102.6 31.1           0
## 751  65217  22 Female    Single    800    Hispanic      64.5 18.8           0
## 752  65218  74   Male   Married   1000       Asian      93.9 21.4           0
## 753  65220  80   Male   Widowed   1000       Black      94.4 26.6           0
## 754  65229  31   Male    Single   8200       White      88.5 24.8           0
## 755  65230  43   Male             2000       White      86.2 23.0           0
## 756  65234  80   Male   Married     NA       White        NA 28.8           0
## 757  65237  25 Female              300       White      72.0 27.2           0
## 758  65243  35 Female             6200 MexAmerican      98.7 28.0           1
## 759  65249  23 Female    Single    800       White      82.6 22.9           0
## 760  65262  35   Male    Single   3500       Asian      88.6 22.8           0
## 761  65267  37 Female   Married   9000       Asian      72.8 19.1           0
## 762  65269  24   Male   Married    300       White      97.0 29.7           0
## 763  65270  24   Male   Married   2000       White     103.0 30.4           0
## 764  65271  27 Female             2500       White      96.4 31.8           0
## 765  65280  62   Male  Divorced    300 MexAmerican        NA 32.2           2
## 766  65286  30   Male   Married   9000       Asian      75.7 21.9           0
## 767  65288  41 Female  Divorced   8200 MexAmerican      88.0 24.6           0
## 768  65289  73 Female   Married   2500       Black     111.6 29.3           0
## 769  65296  80   Male   Married   5400       White        NA 26.7           1
## 770  65297  72   Male   Married   1600       Asian      98.1 28.2           0
## 771  65298  49   Male   Married   8200       White      89.9 25.3           0
## 772  65299  29   Male             6200       White      82.8 22.7           0
## 773  65306  30 Female   Married   2500       White      82.8 23.9           0
## 774  65310  40   Male  Divorced   2500       White     137.5 45.2           0
## 775  65320  39   Male    Single   1000       White      98.4 27.6           0
## 776  65326  44 Female   Married   2000       Asian     100.7 31.3           1
## 777  65331  54 Female    Single    800       Black     116.9 36.3           0
## 778  65334  60 Female  Divorced    800    Hispanic     106.2 34.4           2
## 779  65335  55   Male   Married   5400       Asian     107.0 29.3           0
## 780  65338  22 Female    Single    300       Asian      77.5 22.2           0
## 781  65339  60   Male             6200    Hispanic     123.5 37.5           1
## 782  65341  42   Male   Married   8200       White      91.1 22.9           0
## 783  65348  45 Female   Married   9000       White     100.4 29.5           0
## 784  65351  36   Male  Divorced   2000       White        NA   NA           0
## 785  65352  53   Male   Married     NA       Asian      87.7 22.4           0
## 786  65353  42 Female   Married   9000       Black      95.4 28.9           0
## 787  65355  37   Male   Married   2000       Black     103.3 30.4           0
## 788  65368  23   Male   Married   1000       White      65.8 16.7           0
## 789  65370  28 Female   Married   2500       White     116.2 39.0           0
## 790  65374  80 Female   Married   1600       White     112.3 30.1           1
## 791  65375  52 Female   Married   9000       White      83.0 27.4           0
## 792  65384  72 Female    Single   3500       Asian      81.0 22.1           1
## 793  65391  51   Male   Married   4500       Asian      79.8 22.0           0
## 794  65393  78   Male   Married   1600       White     129.0 37.3           0
## 795  65394  71 Female   Widowed   1600       White      87.5 24.1           0
## 796  65395  77   Male    Single    800       Other     115.9 32.8           0
## 797  65396  54   Male  Divorced     NA       Asian     104.4 28.4           0
## 798  65399  59   Male   Married   9000       Black      90.4 24.8           0
## 799  65401  55   Male    Single   1600       White     103.8 24.4           0
## 800  65402  33   Male    Single   9000       White      77.5 21.1           0
## 801  65404  27 Female    Single   2500       Asian      64.8 18.7           0
## 802  65410  71 Female   Widowed   9000       Asian        NA 20.5           0
## 803  65412  41   Male   Married   4500       Asian      82.8 21.4           0
## 804  65416  23   Male    Single   2000       Asian      76.2 22.9           0
## 805  65421  70 Female   Widowed   1600 MexAmerican     131.4 38.5           0
## 806  65423  50   Male Separated   2500 MexAmerican     107.4 29.8           0
## 807  65427  64 Female   Married    800       White     104.5 36.9           0
## 808  65431  73   Male Separated   1600       Black      92.7 25.4           0
## 809  65433  60 Female  Divorced   8200       White     133.5 39.2           0
## 810  65436  28   Male    Single   1000       Asian     106.3 31.2           0
## 811  65446  65   Male   Married   2500       Black     100.3 28.1           0
## 812  65448  64 Female   Married   1500       Black        NA 17.4           1
## 813  65450  49 Female             2500 MexAmerican      83.6 24.8           1
## 814  65451  33 Female   Married   9000       White      97.2 29.1           0
## 815  65454  36 Female  Divorced   6200       Asian      75.9 21.5           0
## 816  65457  25   Male    Single   9000       Asian      90.3 24.9           0
## 817  65458  63   Male   Married   9000       White     115.5 30.2           1
## 818  65460  64 Female   Widowed   2000    Hispanic     104.1 32.0           0
## 819  65464  29 Female   Married   8200       Black      92.2 30.0           0
## 820  65469  58   Male  Divorced     NA       White     140.8 44.2           1
## 821  65473  60 Female   Widowed    800       Black      80.8 20.6           0
## 822  65476  32 Female    Single    300       Black     135.5 53.1           0
## 823  65485  42   Male   Married   2500       White     124.9 39.4           0
## 824  65490  20 Female    Single    300       Black      90.5 27.7           0
## 825  65492  65 Female   Married   2500       Asian      83.0 20.7           0
## 826  65500  46   Male  Divorced   4500       Black      98.6 31.6           0
## 827  65501  24 Female    Single    300       White      75.0 22.8           0
## 828  65503  44 Female   Married   1600 MexAmerican     124.6 42.8           0
## 829  65505  55   Male   Married   9000       Asian      87.0 22.4           0
## 830  65506  50   Male    Single   1600 MexAmerican      92.9 27.6           2
## 831  65518  45   Male   Married   2500       Black     115.0 35.0           0
## 832  65524  63   Male   Married   3500 MexAmerican      91.5 23.0           0
## 833  65530  40   Male  Divorced   2000       White     110.6 28.0           0
## 834  65534  31 Female    Single    300       Black      93.8 30.9           0
## 835  65539  27   Male    Single   9000       Asian      98.2 27.1           0
## 836  65546  22 Female    Single   2500       Black      95.8 25.8           0
## 837  65547  63 Female   Widowed    800       White     114.5 31.6           0
## 838  65548  47 Female   Married   8200       White     127.4 46.7           0
## 839  65549  80   Male   Widowed   2000       White     100.5 27.4           1
## 840  65553  42 Female Separated    800    Hispanic      80.1 23.7           0
## 841  65555  20 Female    Single    800       White      65.5 19.2           0
## 842  65557  30 Female    Single     NA    Hispanic      99.9 32.1           0
## 843  65562  62 Female    Single   2500       Black     133.5 49.2           0
## 844  65565  27   Male             2500       White     100.5 29.0           0
## 845  65571  74 Female   Widowed   1000       Asian      94.2 27.3           0
## 846  65575  28   Male             1600    Hispanic      81.8 21.5           0
## 847  65585  49 Female   Married   4500       Asian      82.0 22.5           0
## 848  65587  78   Male   Married   2500       White     109.0 29.3           0
## 849  65589  69   Male   Married   1600       Asian     108.9 29.6           0
## 850  65590  43 Female    Single   5400       Black      96.5 33.1           0
## 851  65594  60 Female Separated   1600       Black      80.7 21.9           1
## 852  65621  63   Male   Married   8200       Black     126.1 38.8           0
## 853  65625  23   Male    Single    800       Asian     126.0 38.4           0
## 854  65628  56   Male   Widowed   2500 MexAmerican        NA   NA           0
## 855  65633  57   Male    Single    300       White      96.9 26.8           0
## 856  65635  29 Female    Single   1600       Black      98.3 30.8           0
## 857  65637  66   Male  Divorced   3500       Black      97.7 25.5           0
## 858  65640  65 Female   Widowed    300       Black        NA 43.6           0
## 859  65642  41 Female   Married   8200       White      95.4 34.6           0
## 860  65645  80   Male   Married   3500       White      98.5 24.1           0
## 861  65647  29 Female   Married   2000       White     106.4 33.3           0
## 862  65648  61   Male  Divorced   1600       Black     100.8 29.2           0
## 863  65649  37 Female    Single   8200       Black      85.2 25.9           0
## 864  65650  79 Female   Widowed     NA       Asian      83.0 20.2           0
## 865  65653  30 Female   Married   1600       Black     119.0 40.9           0
## 866  65660  73 Female   Widowed    800       White     145.6 51.8           1
## 867  65663  24 Female   Married   2000       White      92.6 30.4           0
## 868  65669  47   Male  Divorced   4500       White     130.2 40.1           1
## 869  65672  22 Female    Single   1000       Other      76.7 23.5           1
## 870  65675  66   Male   Married   6200 MexAmerican     135.4 44.8           2
## 871  65678  33   Male             2500       White      98.8 27.7           0
## 872  65688  54 Female   Married   9000       White      88.5 25.0           0
## 873  65705  63 Female Separated   1600 MexAmerican     111.5 35.2           2
## 874  65711  46   Male   Married     NA       Asian      99.1 27.6           0
## 875  65712  75   Male   Married   2500    Hispanic     119.8 36.0           2
## 876  65726  23   Male    Single   1000       Asian      76.1 22.0           0
## 877  65736  71   Male   Married   2000       Asian     102.7 28.2           0
## 878  65737  53 Female   Married   8200       White     102.4 28.2           0
## 879  65738  35   Male   Married   1000       White      91.3 26.9           0
## 880  65739  71   Male   Married   4500       White      97.7 23.6           0
## 881  65741  26   Male             4500 MexAmerican      98.8 31.3           0
## 882  65743  40 Female   Married   9000       Black        NA 23.4           0
## 883  65745  27   Male   Married   9000       White     102.1 28.1           0
## 884  65748  64   Male  Divorced   2000       Black      93.9 25.0           1
## 885  65751  54   Male   Married    300 MexAmerican     100.0 26.2           0
## 886  65752  21   Male    Single     NA       Asian      79.5 22.5           0
## 887  65753  30 Female             1000       White     106.3 37.3           0
## 888  65754  50 Female    Single   1500 MexAmerican     122.5 43.7           0
## 889  65757  45 Female    Single   5400       White     107.5 35.8           1
## 890  65758  67 Female   Married   1000       Asian      84.2 24.3           1
## 891  65764  73 Female   Married   2500       White     118.3 35.8           0
## 892  65772  80 Female Separated   2500       Black     103.1 30.4           2
## 893  65774  24   Male             2500 MexAmerican     110.7 34.9           0
## 894  65781  41 Female    Single   2500       Asian      88.6 27.5           0
## 895  65782  53 Female   Married   9000       Black     106.6 34.8           0
## 896  65783  25   Male    Single   6200       White      93.2 24.8           0
## 897  65784  57 Female  Divorced   3500       Black      79.1 25.9           0
## 898  65787  39   Male  Divorced   3500       White      95.4 28.4           0
## 899  65797  52 Female  Divorced   4500       Black      96.0 31.8           0
## 900  65798  26 Female   Married   1600    Hispanic     123.2 38.5           0
## 901  65800  61 Female   Married   9000       White     104.9 31.0           0
## 902  65804  59   Male   Married   8200       White     111.0 31.6           0
## 903  65807  49   Male   Married   8200       White     102.1 31.6           0
## 904  65808  65   Male   Married   5400       Black      87.8 26.2           0
## 905  65812  30   Male   Married   2500       Asian      79.7 21.9           0
## 906  65822  63   Male   Widowed   2000       White     116.8 30.2           0
## 907  65823  37   Male Separated    300 MexAmerican     104.0 29.5           0
## 908  65837  66   Male  Divorced     NA       Black     111.1 31.2           1
## 909  65838  63   Male   Married   3500    Hispanic     105.6 30.7           0
## 910  65841  63   Male    Single   9000       White     125.8 34.2           0
## 911  65850  58   Male   Married   2000 MexAmerican     100.6 25.6           2
## 912  65852  29 Female             6200    Hispanic      66.9 22.0           0
## 913  65854  56   Male   Married   5400       Other      89.6 24.5           1
## 914  65863  33 Female    Single   4500       Asian      78.0 19.7           0
## 915  65865  34 Female   Married   1700    Hispanic        NA   NA           0
## 916  65869  66 Female   Widowed   1600       Black     107.3 40.0           0
## 917  65874  43 Female   Married   6200       White      91.3 25.5           0
## 918  65876  36   Male   Married    300       Black     137.5 46.0           2
## 919  65879  32 Female   Married   9000 MexAmerican      87.6 25.9           0
## 920  65880  26 Female    Single   1600 MexAmerican      83.1 25.8           0
## 921  65885  69   Male             1600       White     101.6 21.9           0
## 922  65889  30   Male    Single   2500    Hispanic     103.4 33.9           0
## 923  65892  80 Female   Widowed   1000       White      97.7 28.3           1
## 924  65902  22 Female    Single   3500       Black      96.8 23.8           0
## 925  65909  35   Male   Married   6200       Asian      78.1 19.0           0
## 926  65910  36   Male   Married   9000       Asian     109.2 31.1           1
## 927  65911  76 Female   Married   2000       White     110.1 35.1           1
## 928  65918  34 Female   Married   1700       Asian      66.2 17.9           0
## 929  65920  36 Female             1600       White     106.7 37.5           0
## 930  65923  62   Male  Divorced   8200       White      79.9 20.7           0
## 931  65927  65 Female   Married   4500       White     119.1 33.3           0
## 932  65929  64   Male   Married   2000       White     116.6 31.5           0
## 933  65931  22   Male    Single   1700       Asian      74.6 18.2           0
## 934  65951  50 Female   Married   8200       White     107.7 33.1           0
## 935  65953  24 Female    Single   2000 MexAmerican      87.2 25.7           0
## 936  65954  66 Female   Married   1700       Black      85.7 21.6           0
## 937  65955  80 Female   Married   1600       White      93.6 23.7           0
## 938  65963  60 Female   Widowed     NA       Asian      90.9 25.8           0
## 939  65967  36 Female   Married   4500    Hispanic      84.1 23.5           0
## 940  65974  63 Female   Married   6200       White      94.3 25.8           0
## 941  65978  57   Male    Single   2500       White     117.5 34.4           1
## 942  65988  20   Male    Single    300       Other      75.3 19.4           0
## 943  65991  26 Female    Single   2500       White      78.8 22.3           0
## 944  65992  61 Female   Married   8200       Black      95.3 27.9           0
## 945  65994  62   Male   Married     NA       Black     105.5 30.5           1
## 946  66000  54 Female  Divorced   6200    Hispanic      89.0 25.7           0
## 947  66010  40 Female             2500       White      72.7 18.1           0
## 948  66013  23   Male   Married    800    Hispanic     102.6 32.5           0
## 949  66015  64   Male   Married   4500       Asian      92.3 25.1           0
## 950  66022  35 Female   Married   1700       Black      92.1 31.8           0
## 951  66026  65   Male  Divorced   9000       White     121.3 36.3           0
## 952  66032  36   Male             8200    Hispanic      96.7 29.0           0
## 953  66033  37 Female   Married     NA       White      77.0 23.1           1
## 954  66036  70 Female   Married   5400       White      87.0 22.6           0
## 955  66040  24 Female             2500    Hispanic      77.8 26.2           0
## 956  66043  64 Female   Married   1700       White     105.6 33.2           0
## 957  66049  73   Male   Married   6200    Hispanic     121.2 32.5           1
## 958  66052  43 Female  Divorced   3500       White     140.1 46.9           0
## 959  66054  33 Female   Married   9000       White      82.1 23.5           0
## 960  66056  57 Female  Divorced   6200       Black      77.9 21.5           0
## 961  66058  74 Female   Married   4500       White     104.0 29.4           0
## 962  66066  80 Female   Widowed   9000       White     110.1 34.8           0
## 963  66068  76   Male   Married   2000       Asian      84.7 21.2           1
## 964  66071  65 Female   Married   3500       Black     105.1 34.6           0
## 965  66079  54   Male    Single   1600       Black     110.9 33.8           1
## 966  66083  21   Male    Single   1000       White      81.0 22.3           0
## 967  66089  34   Male    Single   1000       White      91.7 23.4           0
## 968  66090  25 Female    Single   3500 MexAmerican     116.0 34.2           0
## 969  66093  41 Female    Single   2000       Black     114.5 39.0           0
## 970  66094  25   Male    Single   2500       Asian      78.7 20.8           0
## 971  66095  72 Female   Married   4500       White     116.5 42.2           0
## 972  66101  20 Female              300       White      90.7 25.0           0
## 973  66103  25   Male    Single   2500       White     124.7 37.2           0
## 974  66104  50 Female Separated   1000       White      81.0 20.5           0
## 975  66109  32   Male             2500       White     127.7 37.7           0
## 976  66110  63   Male   Married   9000       White     107.0 29.3           0
## 977  66111  26 Female    Single   9000       Black      81.9 24.2           0
## 978  66123  29 Female             1600       White     126.5 45.9           0
## 979  66126  67 Female   Married   5400       Black      83.0 23.3           0
## 980  66131  36 Female   Married   2500       White      96.4 25.1           0
## 981  66136  27   Male   Married   5400       White      86.0 22.8           0
## 982  66138  36 Female   Married   9000       Asian      82.8 22.9           0
## 983  66140  63 Female    Single     NA       Black     106.0 35.2           0
## 984  66157  80   Male   Married   3500       White      93.0 23.4           0
## 985  66162  60 Female   Married   9000    Hispanic      97.3 30.3           1
## 986  66167  23 Female   Married   2000       Asian      83.7 25.0           0
## 987  66177  44   Male    Single   2500       Black      85.7 26.4           0
## 988  66178  62   Male   Married   8200       Black     123.1 38.0           0
## 989  66179  23 Female    Single    800       Asian      63.1 17.8           0
## 990  66186  45 Female   Married   1500 MexAmerican     103.2 30.9           0
## 991  66191  56 Female   Married   1000       Black     100.5 28.2           0
## 992  66194  63 Female   Married   9000       White      85.5 27.4           0
## 993  66201  45   Male   Married   4500       White     101.2 29.1           0
## 994  66202  61   Male   Married     NA       Asian      89.8 22.3           0
## 995  66207  80   Male   Widowed   3500       Black     134.5 38.2           1
## 996  66210  63 Female   Married   1000       Black     124.2 37.8           0
## 997  66214  70 Female   Married   3500       White        NA 16.2           1
## 998  66222  47   Male   Married   3500       Black      81.8 21.8           0
## 999  66224  80 Female   Widowed    800       White        NA 26.1           1
## 1000 66229  71   Male   Married   9000       White     102.2 27.1           0
## 1001 66230  64 Female Separated   4500    Hispanic      90.5 24.7           0
## 1002 66233  25 Female   Married   8200       Asian      83.2 23.3           0
## 1003 66234  26   Male   Married   2500       White     101.5 31.1           0
## 1004 66235  33 Female   Married   2000       Asian      83.2 22.8           0
## 1005 66237  52   Male   Married   4500    Hispanic     110.9 33.1           0
## 1006 66238  61 Female   Widowed   2500       Black      97.6 34.4           0
## 1007 66240  47   Male Separated   8200       Asian      86.7 25.8           0
## 1008 66241  50 Female Separated   2000    Hispanic     114.0 29.6           0
## 1009 66243  39 Female             9000       Black      96.2 28.9           0
## 1010 66246  40   Male    Single     NA       White     119.0 33.2           0
## 1011 66247  70   Male   Widowed    800       Black     115.1 32.0           0
## 1012 66249  27 Female    Single   2500       Asian      77.8 19.1           0
## 1013 66253  38 Female   Married   5400       White     103.8 28.4           0
## 1014 66254  64 Female    Single   3500    Hispanic      98.5 30.3           0
## 1015 66259  45   Male   Married   4500       Asian      80.1 23.2           0
## 1016 66261  52   Male    Single   1000       White      94.4 28.3           0
## 1017 66268  58   Male   Married   9000       White      97.6 28.5           0
## 1018 66270  76   Male   Married   1500       Asian     108.1 29.9           1
## 1019 66271  80   Male   Married   1000       White      81.3   NA           2
## 1020 66279  62   Male    Single   1700       Black     114.8 40.2           0
## 1021 66280  69 Female   Married     NA       Asian      85.2 22.0           1
## 1022 66283  33 Female   Married   8200       Black     119.6 40.2           0
## 1023 66289  41   Male    Single   3500       White     108.4 34.5           0
## 1024 66290  63 Female   Married   5400       White      91.4 23.4           0
## 1025 66300  35 Female             1000       White     104.6 35.4           0
## 1026 66302  45 Female Separated    300       White      83.3 23.3           0
## 1027 66308  55   Male   Widowed   1000       White      87.0 22.7           0
## 1028 66309  30 Female    Single   1600       Other      72.7 21.6           1
## 1029 66310  53 Female   Married   1000       Asian      77.0 18.7           0
## 1030 66311  39   Male   Married   9000       Other      92.4 23.0           2
## 1031 66317  43   Male   Married   6200       White      97.0 26.3           0
## 1032 66320  21   Male    Single   2500       Black      83.0 26.7           0
## 1033 66321  71 Female  Divorced   2500       White     101.0 31.5           0
## 1034 66323  49 Female   Married   2000 MexAmerican        NA   NA           0
## 1035 66325  24 Female   Married   6200       Black      77.0 18.1           0
## 1036 66327  60   Male   Married   9000    Hispanic     127.7 35.0           0
## 1037 66331  77 Female   Widowed    800       White     101.4 33.9           0
## 1038 66334  37   Male   Married   3500 MexAmerican     114.5 37.6           0
## 1039 66335  35   Male             2000       White     102.0 28.3           0
## 1040 66338  31 Female             6200       White      84.7 24.7           0
## 1041 66341  51   Male   Married   9000       White      95.5 28.0           0
## 1042 66342  32 Female  Divorced    300       White      96.5 25.3           0
## 1043 66343  20 Female    Single    300       White     118.4 34.6           0
## 1044 66347  80   Male   Married   1700       White     100.4 24.4           0
## 1045 66349  24 Female   Married   2500       Asian      93.0 30.5           0
## 1046 66355  62   Male   Married   2000       Asian      89.0 22.9           0
## 1047 66362  55 Female Separated   2000       White      93.6 24.5           0
## 1048 66377  43   Male   Married    300       White      90.3 24.1           0
## 1049 66378  59 Female  Divorced   2500       White     115.0 32.9           0
## 1050 66384  38 Female   Married   2500       White      85.6 23.1           0
## 1051 66386  50 Female Separated   6200    Hispanic     105.0 34.9           0
## 1052 66389  55   Male   Married   1700       White     120.9 30.5           0
## 1053 66391  28 Female   Married   9000       White      79.5 21.4           0
## 1054 66393  43 Female    Single   2000       Other      84.2 24.0           0
## 1055 66396  46 Female    Single   2000       Asian     128.1 41.2           0
## 1056 66399  61   Male   Married   9000       Black     107.7 32.3           0
## 1057 66404  35 Female   Married   8200       White      98.6 27.8           1
## 1058 66409  36 Female   Married   2500       White      89.5 26.6           0
## 1059 66429  69 Female  Divorced    800    Hispanic      81.0 23.2           0
## 1060 66431  23 Female             2500       White      79.5 24.0           0
## 1061 66436  74 Female   Married   2000       Asian     110.1 35.3           0
## 1062 66438  44   Male  Divorced   1000    Hispanic     109.6 30.6           0
## 1063 66439  48 Female    Single   3500 MexAmerican      98.4 35.5           0
## 1064 66443  38 Female    Single   1600 MexAmerican     108.5 34.9           1
## 1065 66444  43 Female    Single   9000       Black      79.6 23.0           0
## 1066 66449  62   Male  Divorced     NA       Asian      94.6 22.6           0
## 1067 66451  52 Female    Single   5400    Hispanic      97.0 30.0           0
## 1068 66456  70 Female Separated   3500       Black      88.3 31.5           0
## 1069 66457  70   Male   Married   1000    Hispanic     125.6 40.5           1
## 1070 66460  37   Male   Married   9000       White      86.1 22.7           0
## 1071 66462  57   Male  Divorced   4500       Black     102.2 28.8           0
## 1072 66464  21   Male    Single   1600 MexAmerican     100.4 29.7           0
## 1073 66473  56   Male    Single   9000       White      97.2 23.2           0
## 1074 66476  60   Male  Divorced   5400       White     119.5 34.0           0
## 1075 66487  31   Male    Single     NA       Black     112.8 35.4           0
## 1076 66494  47   Male   Married   2500       White     113.3 36.8           0
## 1077 66497  25 Female    Single   1600       Black      93.9 33.4           0
## 1078 66503  50   Male   Married   9000       Black     103.6 32.1           0
## 1079 66504  70   Male  Divorced   4500       White     125.1 36.1           1
## 1080 66505  34   Male   Married   2000 MexAmerican      83.2 23.0           0
## 1081 66507  74   Male  Divorced   4500       White     110.5 31.2           1
## 1082 66515  70 Female  Divorced   9000       Asian      75.6 20.2           0
## 1083 66518  80 Female   Widowed   2500       Black     102.7 32.0           0
## 1084 66525  47   Male  Divorced   2500       White     106.6 28.8           0
## 1085 66536  52 Female   Married     NA    Hispanic      81.1 22.6           0
## 1086 66538  69   Male   Married   4500       White     100.0 25.2           0
## 1087 66542  63   Male   Married   4500       Black     124.5 35.0           2
## 1088 66551  22   Male    Single   1000       White      98.2 32.8           0
## 1089 66552  45   Male   Married   2500    Hispanic     101.5 26.5           0
## 1090 66558  54 Female   Married   9000       White      92.4 22.5           0
## 1091 66561  42 Female  Divorced   1000 MexAmerican     100.9 31.8           0
## 1092 66563  73 Female   Married   3500       Black     107.5 34.6           0
## 1093 66568  52 Female  Divorced   9000       White      89.0 24.7           0
## 1094 66573  63   Male   Married   2000 MexAmerican     112.1 29.2           1
## 1095 66582  55   Male   Widowed   6200       Asian      75.5 20.2           0
## 1096 66585  40   Male   Married   9000       Asian      93.3 27.1           0
## 1097 66587  47   Male   Married   4500    Hispanic      93.3 24.8           0
## 1098 66591  34   Male   Married   9000       White     110.3 35.0           0
## 1099 66594  61   Male  Divorced   1000 MexAmerican     115.5 33.6           1
## 1100 66597  54 Female Separated   3500 MexAmerican     113.1 37.8           1
## 1101 66599  31 Female             3500       White     127.7 38.6           0
## 1102 66603  34 Female   Widowed   1000       White      94.6 27.4           0
## 1103 66620  64   Male   Married   9000       White      99.1 26.6           0
## 1104 66623  62   Male  Divorced   1700       Asian     101.2 26.6           0
## 1105 66635  78   Male   Married   5400       Asian      99.0 26.9           0
## 1106 66641  46 Female   Married   3500       White     122.5 35.5           0
## 1107 66642  41   Male   Married   8200       White     101.1 28.2           0
## 1108 66644  63 Female             1600       White      90.0 23.8           0
## 1109 66653  42   Male             2000       White      95.7 25.8           0
## 1110 66663  62   Male   Married   9000       Asian      89.9 23.2           0
## 1111 66672  60   Male   Married   9000 MexAmerican     107.7 30.6           0
## 1112 66679  30   Male   Married   9000       Asian      95.1 28.1           0
## 1113 66685  29   Male             1500 MexAmerican     114.0 32.4           0
## 1114 66687  53 Female    Single   6200    Hispanic      80.1 22.0           0
## 1115 66690  65   Male   Married   1600 MexAmerican     109.8 30.9           0
## 1116 66695  60   Male  Divorced    800       White     124.5 36.5           0
## 1117 66699  33   Male   Married   3500       White     112.0 32.8           0
## 1118 66701  75   Male   Married   2000    Hispanic     113.6 36.4           0
## 1119 66702  47   Male    Single   1500       Black      95.2 25.6           0
## 1120 66710  66   Male   Married   3500       Asian      99.0 24.7           0
## 1121 66712  31   Male    Single   1700       Asian      98.5 25.9           0
## 1122 66713  60 Female   Married   2000       White      87.9 24.6           0
## 1123 66714  21 Female    Single   9000 MexAmerican      74.2 19.0           0
## 1124 66716  30   Male   Married   1600       Black      86.7 27.6           0
## 1125 66721  47 Female   Married   9000       Asian        NA   NA           0
## 1126 66725  57   Male   Married   4500       White     103.7 27.9           0
## 1127 66728  71 Female   Married   1600       Asian      87.3 24.6           2
## 1128 66738  59   Male   Married   9000    Hispanic      86.9 24.1           0
## 1129 66743  68 Female Separated   1600    Hispanic      94.3 26.9           0
## 1130 66759  57 Female  Divorced   3500       Black     123.7 40.2           0
## 1131 66763  80 Female   Married   3500       White      90.0 26.2           0
## 1132 66766  39   Male   Married   8200       White      82.4 18.8           0
## 1133 66770  22 Female             2500       White     121.0 44.6           0
## 1134 66771  31 Female   Married   1000    Hispanic     107.0 34.3           0
## 1135 66777  39   Male   Married   1000    Hispanic     139.2 42.4           0
## 1136 66781  68   Male   Married   1600    Hispanic     105.9 31.7           0
## 1137 66785  60 Female   Married   9000       Asian      72.2 20.3           0
## 1138 66788  31   Male               NA    Hispanic      78.1 23.2           0
## 1139 66789  38 Female   Married   2500       White      88.8 30.5           0
## 1140 66793  50   Male    Single   3500       Black     107.1 30.8           0
## 1141 66795  23   Male             1000       White      71.0 20.8           0
## 1142 66796  70   Male   Married   5400       White     104.7 28.1           0
## 1143 66798  56 Female   Married    800    Hispanic      96.2 30.5           0
## 1144 66802  43 Female             2000       White      80.3 20.7           0
## 1145 66811  29   Male    Single     NA       Asian      97.5 29.2           0
## 1146 66817  72 Female   Widowed    800       White     126.2 38.7           0
## 1147 66819  20   Male    Single   2500       White      78.6 21.7           0
## 1148 66838  65 Female   Widowed   3500       White     118.0 33.5           0
## 1149 66839  25 Female    Single    300       Asian      71.7 17.0           0
## 1150 66848  52 Female   Married   9000       White      80.1 21.6           0
## 1151 66851  46 Female   Widowed   9000       White     107.2 28.7           0
## 1152 66861  21   Male    Single   2500       Black     117.6 37.5           0
## 1153 66869  54 Female   Married   9000       Black     115.9 36.4           0
## 1154 66873  54 Female   Married   1700       White     142.8 59.2           0
## 1155 66874  31 Female   Married   9000       White      93.4 27.2           0
## 1156 66875  69 Female   Married   1600       Asian      86.4 24.1           0
## 1157 66876  62 Female   Married   9000       White      97.0 26.5           0
## 1158 66881  40 Female   Married   9000       Asian      83.1 21.7           0
## 1159 66885  76   Male   Married   2000       Black      90.7 24.8           0
## 1160 66893  60   Male   Married   5400       White     152.4 54.1           0
## 1161 66896  64   Male   Married   1000       Black      95.1 27.5           0
## 1162 66897  28 Female   Married   5400       Black     104.7 29.8           1
## 1163 66898  45 Female    Single   2500       Black      78.7 20.2           0
## 1164 66903  39 Female   Married   3500       White      74.4 19.3           0
## 1165 66904  27   Male               NA       Black      68.8 17.9           0
## 1166 66905  25 Female    Single   2000       Asian      68.8 18.7           0
## 1167 66907  37 Female   Married   8200       Asian      96.5 28.3           0
## 1168 66911  40   Male  Divorced   1600       White      80.4 21.1           0
## 1169 66914  51 Female   Married   5400       Asian      76.0 21.2           0
## 1170 66918  72   Male   Married   9000       White     126.7 34.6           0
## 1171 66924  36   Male   Married   9000    Hispanic      95.0 28.1           0
## 1172 66925  23 Female    Single    800       White      85.6 22.0           0
## 1173 66927  20   Male    Single    300    Hispanic     105.3 32.6           0
## 1174 66929  63 Female   Married   8200       Black      99.3 27.3           0
## 1175 66933  34   Male   Married   1700       Asian      77.7 21.1           0
## 1176 66938  62 Female   Married   8200       Asian      84.6 27.2           0
## 1177 66942  43 Female   Married   2500       White     143.7 47.8           0
## 1178 66943  46 Female  Divorced    800       White     101.5 31.8           0
## 1179 66954  27 Female    Single   6200       White      88.9 24.5           0
## 1180 66956  21 Female   Married   1000       White      91.0 25.9           0
## 1181 66957  62   Male   Married   2500       White     114.2 33.7           0
## 1182 66959  43 Female    Single   1000 MexAmerican      95.0 29.7           0
## 1183 66961  36   Male   Married   6200       Asian      94.5 25.3           0
## 1184 66981  42   Male   Married   1600       White     128.3 42.3           0
## 1185 66984  75   Male   Married   6200       White     140.6 43.7           0
## 1186 66985  77 Female   Widowed   1000    Hispanic        NA 21.5           0
## 1187 66988  40 Female    Single   1000       Black     102.2 33.9           0
## 1188 67001  76   Male   Married   4500       White      98.7 26.8           0
## 1189 67003  68   Male  Divorced   9000       White     101.9 28.0           0
## 1190 67011  67 Female Separated    800       Black      76.0 22.9           0
## 1191 67015  22 Female    Single   3500       Black      95.5 26.4           0
## 1192 67020  78   Male   Married   8200       White     127.5 35.0           1
## 1193 67026  40   Male   Married   1700    Hispanic     102.1   NA           0
## 1194 67032  32 Female   Married   2500       Other      74.6 21.1           0
## 1195 67037  66 Female   Married   1600    Hispanic     119.7 37.1           0
## 1196 67039  31 Female   Married   5400       White      72.3 19.6           0
## 1197 67041  36 Female    Single   1000       Black      83.7 22.9           0
## 1198 67055  71 Female   Married   1600       White      93.1 24.3           0
## 1199 67056  54   Male   Married   1700       Asian     107.6 30.2           0
## 1200 67058  42   Male   Married   9000       Black      82.0 21.8           0
## 1201 67059  29 Female Separated   1000       White      96.6 29.8           0
## 1202 67061  36 Female   Married   8200       Black     106.7 35.0           0
## 1203 67066  65   Male   Married   1600       White     100.5 26.6           0
## 1204 67067  23   Male             1000    Hispanic      99.0 30.8           0
## 1205 67074  37 Female   Married   3500    Hispanic      92.2 27.3           0
## 1206 67081  50 Female   Married   2000 MexAmerican     113.5 36.8           0
## 1207 67083  26   Male    Single   9000       White     101.0 31.7           0
## 1208 67089  29 Female    Single   2500       Black     123.3 39.7           0
## 1209 67098  62 Female    Single   1600       Black      79.3 21.7           0
## 1210 67106  21   Male    Single    800    Hispanic      88.1 25.2           0
## 1211 67112  64 Female   Married   9000 MexAmerican      84.0 25.2           0
## 1212 67113  55 Female   Married   9000       White      77.0 20.0           0
## 1213 67115  59   Male Separated   5400    Hispanic     113.0 33.1           0
## 1214 67116  31 Female    Single   6200 MexAmerican      97.1 29.3           0
## 1215 67121  39   Male   Married   2000       Asian      98.5 28.5           0
## 1216 67123  33 Female    Single   2000       Black      84.2 26.4           0
## 1217 67126  22 Female    Single     NA       Other      76.2 24.3           0
## 1218 67134  29   Male    Single   5400    Hispanic      87.5 24.0           0
## 1219 67143  33   Male    Single   4500    Hispanic      81.9 22.0           0
## 1220 67144  54   Male   Married   9000       Asian      97.5 24.7           0
## 1221 67165  46 Female  Divorced    800       White      99.6 27.3           0
## 1222 67175  49   Male  Divorced     NA       White     102.1 28.9           0
## 1223 67182  44 Female   Married   6200       Black     108.0 32.3           0
## 1224 67184  42   Male             5400 MexAmerican     106.6 32.5           0
## 1225 67189  70 Female   Widowed   1600       Asian      91.0 27.1           0
## 1226 67190  36 Female   Married   8200       White     104.8 27.3           0
## 1227 67191  33 Female   Married   2500       White      91.3 28.2           0
## 1228 67192  55 Female   Married   4500       White      94.9 28.1           0
## 1229 67193  37   Male   Married   4500       Black      89.2 26.2           0
## 1230 67194  51   Male   Married   6200       Black      99.6 26.4           0
## 1231 67195  49   Male   Married   5400       White     102.0 29.6           0
## 1232 67197  73 Female   Married   9000       White        NA   NA           1
## 1233 67199  41   Male   Married   9000       Other      91.0 24.5           0
## 1234 67200  30   Male    Single   4500       White      94.3 26.7           0
## 1235 67209  80 Female   Widowed   2000       White      97.8 25.5           1
## 1236 67214  39   Male    Single   8200       White      91.2 26.3           0
## 1237 67222  80 Female   Married   2500       White     109.1 35.6           0
## 1238 67226  43 Female    Single   2000       Black      97.1 26.1           0
## 1239 67229  65   Male             3500       White     133.3 38.3           0
## 1240 67230  59   Male   Married   9000       Black      78.2 22.8           0
## 1241 67232  48 Female   Married    300       White      99.0 33.4           0
## 1242 67236  48 Female   Married     NA MexAmerican     111.3 36.0           1
## 1243 67237  51 Female Separated   1700 MexAmerican      80.4 21.9           0
## 1244 67239  50 Female Separated   1600    Hispanic     105.2 33.9           0
## 1245 67243  68 Female  Divorced   1000       Black     107.8 31.1           0
## 1246 67250  43 Female             1600       Other      93.5 29.3           0
## 1247 67258  73 Female   Married   2500       White     132.6 43.0           0
## 1248 67259  45   Male   Married   9000       White     111.5 34.3           0
## 1249 67264  77 Female   Widowed   1600       White      99.5 24.2           0
## 1250 67270  42 Female   Married   2500       White     107.0 37.9           0
## 1251 67273  44   Male   Married   2000 MexAmerican      90.0 27.9           0
## 1252 67274  46 Female   Married   5400       Asian      80.0 21.5           0
## 1253 67275  77   Male   Married   1000       White      95.4 23.8           0
## 1254 67279  32 Female    Single    800       Black      76.5 19.8           0
## 1255 67280  27   Male    Single   2500 MexAmerican        NA   NA           0
## 1256 67281  42 Female               NA MexAmerican     112.1 35.3           1
## 1257 67283  56 Female   Married   9000       Asian      95.9 27.4           0
## 1258 67285  70 Female   Widowed   2500    Hispanic     115.3 36.6           0
## 1259 67293  53   Male   Married   9000       White      83.0 22.1           0
## 1260 67306  51   Male Separated    800       Black      95.3 26.8           0
## 1261 67308  21   Male             1000       Asian      99.2 26.7           0
## 1262 67310  46   Male             2000    Hispanic     107.5 31.9           0
## 1263 67315  51 Female  Divorced   3500       Black      89.8 24.9           0
## 1264 67318  26   Male    Single   6200       Black      83.7 25.3           0
## 1265 67322  20   Male    Single     NA       Black      79.8 22.6           0
## 1266 67327  75   Male   Married   2500       White     106.8 27.4           0
## 1267 67332  45 Female    Single   3500       Asian      93.3 28.8           0
## 1268 67338  24   Male    Single   1600       Black      94.2 31.7           0
## 1269 67339  70   Male   Married   5400       White     110.7 25.9           0
## 1270 67341  74   Male   Married   4500 MexAmerican     102.5 25.3           0
## 1271 67343  58   Male  Divorced   1600       Black      85.8 22.7           0
## 1272 67346  80   Male  Divorced   1700       White     122.7 34.1           0
## 1273 67349  42   Male   Married   6200       Black     146.4 50.8           0
## 1274 67355  22 Female             3500 MexAmerican      98.4 27.4           0
## 1275 67361  59   Male   Married   1600       White     112.1 28.7           0
## 1276 67362  47 Female   Married   4500       Asian      99.4 27.9           1
## 1277 67367  32 Female   Married   2500 MexAmerican      87.3 24.9           0
## 1278 67373  64 Female   Married     NA    Hispanic     110.1 33.6           1
## 1279 67375  45 Female  Divorced   3500       Black     109.6 37.3           0
## 1280 67380  58 Female    Single   2000       Black     126.0 47.1           0
## 1281 67385  47   Male    Single   1600       Other      82.8 23.6           0
## 1282 67390  56 Female  Divorced   5400       White      71.4 18.2           0
## 1283 67392  41   Male   Married   5400    Hispanic     104.0 31.2           0
## 1284 67395  55 Female   Married   1000       Black      99.4 29.9           0
## 1285 67397  20   Male    Single   6200       Black      73.2 23.0           0
## 1286 67400  61   Male   Married   8200       Asian      95.8 27.6           0
## 1287 67407  64   Male   Married   9000       White      92.0 23.3           0
## 1288 67414  77 Female   Widowed   1000       Black     119.5 36.5           0
## 1289 67417  58 Female   Married   9000       Asian      75.5 20.5           0
## 1290 67420  22   Male  Divorced   8200    Hispanic      74.6 20.9           0
## 1291 67424  32 Female    Single   1000       Black     148.0 54.4           0
## 1292 67431  61   Male   Married     NA       Asian      85.7 21.8           0
## 1293 67433  65   Male  Divorced   1600 MexAmerican     150.7 47.0           1
## 1294 67436  23 Female    Single   1600       Black      77.8 20.3           1
## 1295 67438  61   Male   Married   2000       Black     110.8 30.5           1
## 1296 67439  36 Female   Married   4500       Asian      88.5 30.0           0
## 1297 67442  39 Female    Single   3500       Black      91.7 28.8           0
## 1298 67445  38 Female   Married   1600 MexAmerican      79.6 24.7           0
## 1299 67450  55   Male    Single   2500       White     122.0 33.6           0
## 1300 67454  76 Female   Married   2500       White      90.7 24.2           0
## 1301 67455  70   Male   Married   2500       White     100.2 27.6           0
## 1302 67462  38 Female  Divorced   1000 MexAmerican     127.4 38.0           0
## 1303 67463  28   Male   Married   9000       White     113.8 32.5           0
## 1304 67466  55   Male   Married   2000    Hispanic      86.2 22.8           0
## 1305 67474  38   Male   Married   1700       Black     116.0 34.6           0
## 1306 67475  52   Male  Divorced   6200       Black     126.2 37.1           0
## 1307 67480  62 Female   Widowed   9000       Black      97.0 33.1           0
## 1308 67481  69 Female  Divorced   1000    Hispanic      86.5 21.8           0
## 1309 67483  64 Female  Divorced    800    Hispanic      91.6 25.9           0
## 1310 67484  23 Female    Single    800       Black        NA 24.9           1
## 1311 67487  75 Female   Widowed   1000       Black        NA 26.7           1
## 1312 67488  29   Male    Single   3500       Asian      81.8 22.8           0
## 1313 67493  76   Male   Married   5400       Black      92.9 22.9           0
## 1314 67494  34   Male  Divorced   1600       White      91.8 23.3           0
## 1315 67499  73   Male   Married   9000    Hispanic     120.6 32.1           0
## 1316 67501  62 Female   Married   6200       Other     118.0 31.8           0
## 1317 67503  45 Female    Single   3500       White     114.5 37.8           0
## 1318 67516  47 Female    Single   2500       Black     109.6 33.4           0
## 1319 67517  36 Female   Married   2000       White     127.5 41.2           0
## 1320 67519  63   Male   Widowed   2500       Black     103.5 26.7           1
## 1321 67520  79   Male   Married   1600       White     145.8 48.9           1
## 1322 67526  33   Male             3500 MexAmerican     105.7 32.7           0
## 1323 67527  29 Female             1000       Black     139.1 49.4           0
## 1324 67530  52   Male Separated   1600 MexAmerican      99.9 30.2           0
## 1325 67532  71 Female   Married   2500       White      82.7 21.4           0
## 1326 67534  56 Female   Widowed    800       White      95.0 25.9           0
## 1327 67538  25   Male   Married   2500       Black      80.5 23.6           0
## 1328 67539  27 Female   Married   2000       White     122.9 39.2           0
## 1329 67545  22 Female             1600       White      78.8 20.7           0
## 1330 67546  30 Female   Married   3500    Hispanic      91.6 29.4           0
## 1331 67564  43 Female   Married   9000 MexAmerican     108.5 31.3           0
## 1332 67577  60 Female  Divorced   4500       White      92.0 30.1           0
## 1333 67580  67 Female   Widowed   1000       White      99.5 24.8           0
## 1334 67587  80 Female   Widowed   3500       White      82.2 23.6           0
## 1335 67591  40   Male   Married   8200       Asian      89.4 23.0           0
## 1336 67595  49   Male    Single   2000       White     108.4 29.6           0
## 1337 67597  41 Female    Single   1700       Black      83.4 27.0           0
## 1338 67598  80 Female  Divorced   6200    Hispanic      99.5 28.5           0
## 1339 67603  62 Female   Married   8200       Asian      79.7 26.6           0
## 1340 67613  21 Female    Single   3500       Asian      84.6 29.0           0
## 1341 67614  53   Male   Married   2000 MexAmerican     106.8 29.7           0
## 1342 67616  63   Male              800       White      87.2 20.6           0
## 1343 67629  70 Female   Widowed   1700       Asian      85.9 23.7           1
## 1344 67632  51 Female   Married   3500 MexAmerican      83.1 26.4           0
## 1345 67635  65   Male   Married   2500 MexAmerican     101.2 26.4           0
## 1346 67642  24 Female             4500 MexAmerican      93.2 31.3           0
## 1347 67643  76   Male   Married   9000       White     103.0 30.6           0
## 1348 67646  48   Male   Married   2000       Asian      88.6 25.0           0
## 1349 67647  70 Female Separated   1000       Black     106.1 29.3           0
## 1350 67652  46   Male  Divorced   2500       White     103.7 26.9           2
## 1351 67661  80   Male   Married   1600       White     100.5 26.5           0
## 1352 67665  33 Female   Married   2000       White        NA   NA           0
## 1353 67675  66   Male   Married   4500 MexAmerican      95.9 24.3           0
## 1354 67690  40 Female    Single   1000       Black     106.6 35.6           0
## 1355 67694  62   Male   Widowed   1700       Black     100.4 30.9           0
## 1356 67696  67 Female    Single   3500       Asian      92.7 23.5           0
## 1357 67698  63 Female   Married   5400       White      77.9 20.3           0
## 1358 67699  32   Male   Married   5400       Black      91.8 26.6           0
## 1359 67703  72   Male   Married   2500 MexAmerican     117.6 33.7           0
## 1360 67707  46   Male   Married    800       White     114.6 32.2           0
## 1361 67708  49   Male   Married   2500       White     114.6 31.8           0
## 1362 67714  75   Male   Widowed    800       White     113.8 27.6           0
## 1363 67718  49 Female  Divorced   2000       White     115.3 38.5           0
## 1364 67719  35   Male   Married   8200       Black      82.3 24.6           2
## 1365 67727  32 Female   Married   2000       White      94.3 27.7           0
## 1366 67740  52   Male Separated   1600 MexAmerican     107.8 30.7           0
## 1367 67741  28 Female   Married   4500       White      99.0 23.3           0
## 1368 67751  20 Female    Single   3500       White     129.8 44.3           0
## 1369 67754  36 Female   Married   9000       Asian      81.2 23.2           0
## 1370 67756  28   Male    Single   3500       Black      98.7 31.3           0
## 1371 67763  37 Female   Married   8200       White     113.3 29.4           0
## 1372 67764  76   Male   Widowed   2000    Hispanic     108.7 27.4           0
## 1373 67766  62 Female  Divorced   1600       White     106.7 34.3           0
## 1374 67769  54 Female   Married   3500 MexAmerican        NA   NA           0
## 1375 67772  73 Female   Married   5400       White      96.1 27.6           0
## 1376 67776  54   Male   Married   3500 MexAmerican     108.5 30.9           0
## 1377 67778  31   Male   Married   1000       White      92.5 27.1           0
## 1378 67779  56 Female   Married   6200       White      79.8 24.5           0
## 1379 67781  41 Female   Married   5400    Hispanic      83.2 22.1           0
## 1380 67785  38 Female   Married   1600       White      85.5 24.5           0
## 1381 67786  45   Male    Single   1000       White     106.6 28.6           0
## 1382 67788  62   Male   Married   1600 MexAmerican      90.0 25.2           0
## 1383 67793  39   Male   Married   3500 MexAmerican      93.6 30.8           0
## 1384 67794  51   Male   Married     NA    Hispanic      92.5 23.3           0
## 1385 67797  45   Male  Divorced     NA    Hispanic        NA 28.0           0
## 1386 67799  38 Female   Married   2500       White     106.0 37.8           0
## 1387 67808  80 Female   Widowed   4500       White        NA 29.7           2
## 1388 67818  21 Female    Single   9000       Black      73.7 22.3           0
## 1389 67819  79 Female   Widowed   1000       Other      92.1 25.6           0
## 1390 67820  47 Female Separated   3500       Black      96.5 29.4           1
## 1391 67822  80 Female   Married   1000       White      91.2 24.5           0
## 1392 67828  67   Male   Married   1600       Black      92.4 24.0           0
## 1393 67833  80   Male   Married   2000       White     102.2 26.3           0
## 1394 67834  33 Female    Single   2500       White      94.0 28.2           0
## 1395 67838  52   Male    Single     NA       Black        NA   NA           0
## 1396 67840  28   Male  Divorced   2000       White      97.0 29.3           0
## 1397 67841  58   Male   Married   9000       Asian      94.9 25.0           0
## 1398 67844  23   Male   Married   2000       White     143.3 48.7           1
## 1399 67847  43 Female             1000       Black     118.6 48.6           0
## 1400 67854  80   Male   Married   1000       Asian      94.8 25.7           0
## 1401 67855  58   Male   Married   9000       Asian      88.0 25.5           0
## 1402 67861  60   Male    Single   5400       White     116.9 33.2           0
## 1403 67863  50 Female   Married   9000       White      88.2 21.1           0
## 1404 67870  20 Female    Single   9000       Asian      72.3 23.0           0
## 1405 67872  78 Female   Married   1600    Hispanic      97.9 28.0           1
## 1406 67874  69   Male   Married   6200       White     102.5 27.2           0
## 1407 67877  79 Female   Widowed   9000       White      86.5 24.5           0
## 1408 67885  80 Female   Widowed    300       Black      95.5 27.4           2
## 1409 67887  67 Female   Married   8200       Asian      80.8 23.0           1
## 1410 67889  42 Female    Single   1600       White      98.2 30.7           0
## 1411 67891  29 Female    Single   5400       Asian      73.0 22.5           0
## 1412 67893  34   Male    Single   8200       White     101.8 26.7           0
## 1413 67894  80   Male   Married   2500       Other     116.0 31.1           1
## 1414 67902  21   Male Separated   2000 MexAmerican      95.9 27.3           0
## 1415 67912  65   Male   Married   9000    Hispanic     110.2 29.7           0
## 1416 67915  24   Male    Single   2000       Asian      80.9 21.5           0
## 1417 67916  39 Female   Married   4500    Hispanic     101.2 27.4           0
## 1418 67917  27   Male    Single   2500       White      93.3 26.9           0
## 1419 67919  59 Female  Divorced   1000       White      97.6 26.6           0
## 1420 67925  51 Female  Divorced   3500       Black     117.7 42.7           0
## 1421 67930  59   Male   Married   6200 MexAmerican     110.6 31.0           0
## 1422 67938  27 Female    Single   8200       Asian      68.5 21.9           0
## 1423 67939  72   Male   Married   9000       White      93.5 24.7           0
## 1424 67940  66   Male   Married   4500       White     103.9 26.5           0
## 1425 67941  26 Female Separated   2500       White      89.6   NA           0
## 1426 67947  79   Male   Married   1500       Black     108.0 28.3           0
## 1427 67952  65 Female    Single    800    Hispanic     102.3 30.1           1
## 1428 67962  40 Female   Widowed   9000       Black      94.2 29.2           0
## 1429 67964  31 Female  Divorced   1000       White     170.5 56.8           1
## 1430 67966  20   Male    Single   9000       White      77.4 19.8           0
## 1431 67970  72   Male   Married     NA       White     109.8 32.7           1
## 1432 67972  30   Male    Single   1600       White     105.3 30.5           0
## 1433 67975  76 Female   Married   1600       White      89.0 23.4           0
## 1434 67978  60 Female  Divorced    300       White      94.2 24.6           0
## 1435 67986  63 Female   Widowed   5400       Black      80.6 24.1           0
## 1436 68000  65   Male   Married   6200       White      84.5 22.9           0
## 1437 68004  33 Female   Married   9000 MexAmerican      76.6 21.6           0
## 1438 68011  27 Female   Married   2500       White     120.1 43.6           0
## 1439 68012  70 Female   Married     NA       Black     115.4   NA           2
## 1440 68013  60 Female    Single   4500    Hispanic      95.9 28.2           0
## 1441 68017  68 Female   Married   6200 MexAmerican     102.4 29.5           0
## 1442 68022  58   Male   Married   9000 MexAmerican     105.8 31.7           0
## 1443 68027  41 Female   Married   4500       Black     100.3 33.1           0
## 1444 68028  66 Female   Married   5400       Black      96.2 30.5           1
## 1445 68032  80 Female   Married   2500       White      94.8 33.1           0
## 1446 68038  68   Male  Divorced   9000       Black     104.6 29.5           0
## 1447 68052  39   Male    Single   1600       White     118.5 32.3           0
## 1448 68058  50   Male   Married   4500       White     113.6 30.6           0
## 1449 68061  35 Female   Married   9000       Asian      78.0 20.5           0
## 1450 68063  51   Male  Divorced    300       White      74.6 20.7           0
## 1451 68064  80 Female   Widowed    800 MexAmerican     123.3 39.3           0
## 1452 68065  20 Female    Single   1000       White      82.5 25.3           0
## 1453 68066  63 Female   Married   8200       Black     129.9 38.8           0
## 1454 68068  79 Female   Married   9000       White      79.7 22.5           0
## 1455 68069  66 Female    Single    800    Hispanic     128.3 41.8           0
## 1456 68073  58   Male             1600       Black      94.3 26.6           0
## 1457 68091  74 Female   Widowed   1500 MexAmerican     115.3 37.7           0
## 1458 68095  41 Female   Married   1600       White      92.6 25.9           0
## 1459 68102  75   Male   Married   1000    Hispanic     114.8 33.5           0
## 1460 68109  45   Male   Married   4500       Black      93.1 27.1           0
## 1461 68110  60   Male   Married   6200       White      88.3 22.6           0
## 1462 68115  80 Female   Widowed   2000       White      84.8 25.7           0
## 1463 68121  70   Male   Married   9000       White      97.4 24.8           0
## 1464 68127  50 Female   Married   4500       Asian      78.7 23.3           0
## 1465 68128  58   Male    Single   1000       White     110.5 26.1           0
## 1466 68133  44   Male   Married   3500    Hispanic     103.0 28.0           0
## 1467 68140  30   Male    Single    300       Black      77.3 24.9           0
## 1468 68143  80 Female Separated   2500    Hispanic     105.6 29.7           0
## 1469 68154  56   Male   Married   9000       Black     102.7 30.6           0
## 1470 68155  40 Female   Married   6200       Black      98.4 28.4           0
## 1471 68159  66   Male   Married   2500       Asian     112.5 33.3           0
## 1472 68169  23 Female   Married   2000       White      90.4 26.4           0
## 1473 68170  37   Male   Married   8200       Black     129.5 37.8           0
## 1474 68171  58 Female Separated    300 MexAmerican     115.0 40.5           0
## 1475 68173  38   Male             1600       White     103.0 31.3           0
## 1476 68176  58 Female    Single   2500       Black     105.4 32.4           0
## 1477 68180  31   Male   Married   8200       Black      76.3 25.3           0
## 1478 68183  28 Female    Single   3500       Black     115.2 38.8           0
## 1479 68191  56 Female  Divorced   1000       White     101.2 27.5           0
## 1480 68197  59   Male   Married   8200       White     111.2 31.9           0
## 1481 68199  30 Female Separated   8200    Hispanic     104.4 39.1           0
## 1482 68203  78 Female   Married   1600       Other     111.4 31.7           0
## 1483 68206  35 Female   Married   6200       Asian     105.4 33.3           0
## 1484 68213  41 Female Separated   2000 MexAmerican      81.2 23.2           1
## 1485 68226  38 Female   Married   9000       Asian      85.9 24.4           0
## 1486 68227  56 Female   Widowed    800       Black      98.2 31.8           0
## 1487 68236  41 Female    Single   1600       Other     132.3 47.2           0
## 1488 68237  63   Male   Married   4500       White     102.5 29.6           0
## 1489 68247  80 Female   Married     NA       Asian      56.2 13.4           0
## 1490 68249  60   Male   Married   5400       White     104.3 27.6           0
## 1491 68256  46 Female   Married   6200       Black        NA 62.8           0
## 1492 68263  63 Female   Married   6200       White      92.0 24.1           0
## 1493 68270  48 Female             5400    Hispanic     112.5 34.0           0
## 1494 68273  31   Male   Married   2000       White     100.9 27.8           0
## 1495 68275  71   Male   Married   8200       Black     106.1 32.5           0
## 1496 68285  49 Female   Married   5400       White     101.9 41.0           0
## 1497 68293  54   Male   Married   2500       White      99.2 28.2           0
## 1498 68296  69 Female   Married   1000       White        NA 36.4           1
## 1499 68301  59   Male  Divorced    800       White     121.3 32.6           0
## 1500 68309  57   Male   Married   3500       Asian      87.8 23.4           0
## 1501 68314  31   Male   Married   2500       Black     111.5 36.6           0
## 1502 68319  43 Female   Married   9000       White     101.3 30.6           0
## 1503 68324  27 Female   Married   8200       White      99.4 29.8           0
## 1504 68327  80   Male   Married   2500       White      91.7 25.3           1
## 1505 68330  69 Female   Married   2500       White      95.5 29.6           0
## 1506 68331  66   Male   Married   8200 MexAmerican     114.9 32.9           0
## 1507 68334  38 Female    Single   1000       Black     108.3 32.5           0
## 1508 68337  36   Male   Married   6200 MexAmerican     137.8 37.6           0
## 1509 68341  64 Female   Married   6200    Hispanic      93.0 24.0           0
## 1510 68342  59   Male             1600       Asian      73.5 21.3           0
## 1511 68353  36   Male   Married   8200       White      95.3 26.8           0
## 1512 68354  45   Male   Married   1600       Asian      94.8 25.5           0
## 1513 68356  73 Female  Divorced   3500       Black     107.2 27.8           1
## 1514 68367  78   Male   Married   4500       Black     116.8 31.7           1
## 1515 68377  74   Male Separated   1000       White      95.5 23.6           1
## 1516 68384  23 Female    Single    800       White     114.5 34.3           0
## 1517 68393  20 Female    Single    300       Black      81.6 28.7           0
## 1518 68394  58 Female    Single   8200       White      96.2 27.7           0
## 1519 68401  43   Male    Single    800 MexAmerican      86.2 23.9           0
## 1520 68404  65 Female    Single   1000       Black     106.1 32.5           0
## 1521 68412  32   Male Separated   2000       White      71.8 18.8           0
## 1522 68416  63   Male   Married   1000       Asian      89.5 22.3           0
## 1523 68423  42 Female   Married   9000       White      80.0 22.3           0
## 1524 68424  72   Male   Married   8200       Asian      92.8 26.8           0
## 1525 68428  44 Female Separated   1000       White     123.5 41.1           1
## 1526 68432  80   Male   Married   1000    Hispanic      92.7 23.3           2
## 1527 68440  46   Male   Married     NA       White      96.2 25.5           0
## 1528 68445  70   Male   Married   1700    Hispanic     101.7 30.4           0
## 1529 68446  68 Female   Married   3500       Asian      76.8 18.9           0
## 1530 68447  68 Female  Divorced    800       White     130.5 41.2           0
## 1531 68450  47 Female  Divorced   3500       Asian      71.8 20.4           0
## 1532 68451  24   Male    Single   3500       Black      81.8 24.4           0
## 1533 68452  69 Female  Divorced   1600    Hispanic     102.5 31.9           0
## 1534 68453  79 Female   Married   3500       White     103.2 32.0           0
## 1535 68462  49   Male  Divorced   1600       White      85.9 22.4           0
## 1536 68468  61   Male   Married   2500    Hispanic      85.4 22.8           0
## 1537 68469  25   Male    Single   1000       White     107.6 32.3           0
## 1538 68474  35   Male   Married   8200       White      96.5 26.5           0
## 1539 68478  41   Male   Married   6200       White     104.7 30.5           0
## 1540 68485  64 Female  Divorced   2500       White     107.8 30.3           0
## 1541 68488  58 Female    Single   1600       Black     104.0 29.4           1
## 1542 68491  80   Male   Married   3500       White     109.6 29.2           0
## 1543 68493  29   Male   Married   2000       Asian      82.1 21.7           0
## 1544 68494  38 Female   Widowed    300       White      83.6 24.8           0
## 1545 68495  78 Female   Widowed    800       White     114.9 33.3           0
## 1546 68499  58   Male   Married   9000       White      94.1 24.1           0
## 1547 68501  52   Male   Married   4500       White     106.5 29.2           0
## 1548 68502  27   Male    Single   1600       Black      99.2 28.9           0
## 1549 68506  77 Female   Married   1600       White     119.8 36.9           0
## 1550 68512  57 Female   Married     NA    Hispanic      85.6 23.3           0
## 1551 68513  69 Female   Married   2500       White      81.0 24.7           0
## 1552 68516  30   Male    Single   3500       Black      82.4 25.5           0
## 1553 68525  39 Female   Married   2000 MexAmerican     102.0 34.4           0
## 1554 68529  80 Female   Widowed   2000       White      79.8 18.9           0
## 1555 68531  60   Male   Married   9000       Black     105.2 27.3           0
## 1556 68538  72   Male   Married   1700       Black     102.5 28.0           0
## 1557 68549  67   Male   Married   1000    Hispanic      95.4 24.9           0
## 1558 68551  80 Female   Widowed   1600       Black        NA 42.2           2
## 1559 68553  61 Female  Divorced   2500       White     111.2 35.2           1
## 1560 68557  71   Male  Divorced   1000       White     117.1 34.1           0
## 1561 68560  28 Female    Single   2500 MexAmerican     140.6 48.8           0
## 1562 68565  65 Female   Married   9000       Asian      84.7 22.0           0
## 1563 68569  56 Female Separated    300       Black        NA 37.6           1
## 1564 68570  49   Male  Divorced   1000       White      87.2 23.2           0
## 1565 68571  53   Male   Married   2000       Asian     103.0 25.3           0
## 1566 68572  42   Male   Married   5400       White      98.8 26.7           0
## 1567 68573  64   Male   Married   5400       Asian      84.9 21.0           0
## 1568 68574  20   Male    Single   3500 MexAmerican      88.9 23.9           0
## 1569 68575  42 Female   Married   8200    Hispanic      89.7 26.5           0
## 1570 68581  43   Male   Married   9000       Black      93.4 27.0           0
## 1571 68582  42 Female    Single   5400       Black     102.5 32.0           0
## 1572 68591  67   Male   Married   8200       Black     110.8 32.0           0
## 1573 68593  63 Female    Single   6200       Asian      76.6 21.8           0
## 1574 68594  80   Male   Widowed   1000       White     103.2 25.4           0
## 1575 68601  26   Male   Married   2000       Asian      84.2 22.0           0
## 1576 68602  36   Male   Married   2500 MexAmerican      95.7 29.3           0
## 1577 68605  46 Female   Widowed    300       Black        NA 34.1           0
## 1578 68622  70 Female   Married   3500       White        NA 24.6           0
## 1579 68623  28   Male   Married   9000       Asian      93.3 24.5           1
## 1580 68626  70 Female   Married   6200       White     115.8 32.6           0
## 1581 68627  70 Female   Married     NA       White      86.3 23.7           0
## 1582 68645  75 Female  Divorced   2500       White     107.4 25.4           1
## 1583 68646  45 Female  Divorced   1600 MexAmerican      74.7 22.7           0
## 1584 68648  30 Female   Married   8200       White      81.1 20.4           0
## 1585 68651  32 Female    Single   9000       White      98.5 27.9           1
## 1586 68652  34   Male             6200       White     120.5 35.3           0
## 1587 68661  64 Female   Married   9000       Black     105.5 32.6           0
## 1588 68675  73 Female   Married   6200       Asian      81.3 24.0           0
## 1589 68676  51 Female Separated   1600       Black     105.1 35.0           1
## 1590 68680  22 Female              800       White      89.5 28.8           0
## 1591 68682  79 Female   Married   2000       White     100.0 25.4           2
## 1592 68686  25 Female    Single   3500       Asian      66.0 19.1           0
## 1593 68689  70 Female   Married   2000    Hispanic      98.3 33.7           0
## 1594 68693  28   Male    Single   9000       White      89.0 25.8           0
## 1595 68694  57   Male   Married   9000       Black     102.6 30.5           0
## 1596 68696  44   Male  Divorced   1000    Hispanic     103.4 30.1           1
## 1597 68701  27 Female             1500 MexAmerican      99.9 32.9           0
## 1598 68702  56   Male  Divorced   2500       Black      88.8 23.3           0
## 1599 68703  63   Male  Divorced   9000 MexAmerican     105.2 28.2           1
## 1600 68706  26   Male             2000       Black      76.0 23.6           0
## 1601 68707  54   Male   Married   9000       White     123.2 39.7           0
## 1602 68711  26   Male    Single   5400       Asian      82.6 26.7           0
## 1603 68714  55 Female    Single   5400       Black      75.7 21.5           0
## 1604 68717  80   Male   Widowed   6200       Black     116.8 33.9           0
## 1605 68720  53 Female   Married   2500       White      88.4 24.0           0
## 1606 68721  39 Female    Single   1000       Black      90.0 25.9           0
## 1607 68724  27 Female   Married   2000 MexAmerican      70.1 17.4           0
## 1608 68733  54   Male   Married   9000 MexAmerican     148.1 45.9           0
## 1609 68738  22   Male    Single   2500       White      86.8 22.9           0
## 1610 68744  33   Male   Married   2000       White     127.9 37.6           0
## 1611 68748  70   Male   Married   3500       Asian      99.0 26.7           0
## 1612 68749  21 Female    Single   1000       Black     106.0 37.6           0
## 1613 68751  39   Male   Married   8200       White     116.0 32.1           0
## 1614 68752  45   Male   Married   4500 MexAmerican     105.1 30.3           0
## 1615 68753  43 Female   Married   9000       White      73.1 19.2           0
## 1616 68760  24   Male    Single    300       White      84.5 22.3           0
## 1617 68762  34 Female  Divorced   8200       White      80.3 24.4           0
## 1618 68765  25   Male              300 MexAmerican      81.0 20.1           0
## 1619 68767  68 Female    Single     NA       Black      90.2 27.5           0
## 1620 68769  56 Female   Married   9000       Asian      80.5 23.0           0
## 1621 68771  24 Female   Married   9000       Other      83.4 24.9           0
## 1622 68780  78   Male   Married   6200       Asian      94.6 27.5           1
## 1623 68781  34   Male    Single   2500       Asian      78.1 21.6           0
## 1624 68787  65   Male   Married   2500       White     106.4 27.5           0
## 1625 68794  74   Male   Married   8200       White     133.6 39.4           1
## 1626 68797  27   Male             2500       Black      71.9 20.1           0
## 1627 68799  70   Male  Divorced     NA       White     104.7 27.2           1
## 1628 68808  58   Male  Divorced    300       Black      93.4 24.5           0
## 1629 68810  80   Male    Single    800       White     147.8 47.8           0
## 1630 68818  62   Male  Divorced   2500       Black     125.4 34.9           0
## 1631 68824  80 Female   Married   2500    Hispanic      77.0 23.3           1
## 1632 68825  51   Male Separated    800       Asian      77.2 19.5           0
## 1633 68827  43   Male   Married   5400       Asian      90.3 24.6           0
## 1634 68830  39 Female   Married     NA       Asian      92.7 26.0           0
## 1635 68833  41   Male    Single   1600    Hispanic      88.4 25.5           0
## 1636 68837  35 Female Separated   6200       Black      76.7 21.1           0
## 1637 68840  31   Male    Single   3500       Black      91.0 26.5           0
## 1638 68845  75 Female   Widowed   1000       White     113.8 37.2           0
## 1639 68847  21   Male    Single   5400 MexAmerican     116.7 35.0           0
## 1640 68853  37 Female    Single    800       White     124.5 44.0           0
## 1641 68855  70   Male   Married   2500       White     101.5 26.6           0
## 1642 68859  39 Female   Married   8200       White      98.0 27.9           0
## 1643 68860  34   Male   Married   3500       White      86.0 23.5           0
## 1644 68864  57 Female   Married   1000    Hispanic     112.3 41.1           0
## 1645 68866  22   Male             2500    Hispanic        NA 27.8           0
## 1646 68868  80 Female   Married   6200       White      72.0 16.9           1
## 1647 68873  24 Female    Single    800       Asian     147.6 47.5           0
## 1648 68874  55   Male  Divorced   6200    Hispanic     100.6 27.7           0
## 1649 68876  78 Female   Married   9000       White        NA 27.1           0
## 1650 68884  54 Female    Single   1000       Black     115.6 34.5           0
## 1651 68892  75   Male   Married   6200       White     137.8 40.9           0
## 1652 68899  48   Male    Single   8200       Black     104.7 28.6           0
## 1653 68902  78 Female   Widowed     NA       Black      96.6 26.7           1
## 1654 68907  26 Female   Married   2500       White      96.0 32.0           0
## 1655 68908  59 Female   Married   5400       Black     101.1 32.8           0
## 1656 68912  80 Female   Widowed   8200       Asian      76.9 17.6           0
## 1657 68916  56   Male   Married   2000 MexAmerican      90.2 23.4           0
## 1658 68917  33   Male   Married   8200       White     117.8 35.7           0
## 1659 68919  37 Female   Married   3500       White      90.7 27.0           0
## 1660 68920  48 Female    Single   1700       Black     122.1 41.2           0
## 1661 68922  74 Female   Married   8200       White     108.2 35.1           0
## 1662 68933  72   Male   Married   8200       Black      93.8 28.3           0
## 1663 68935  46   Male   Married   1600 MexAmerican      80.6 25.8           0
## 1664 68937  31   Male    Single   6200       Black      77.5 24.2           0
## 1665 68944  79 Female  Divorced    800    Hispanic      97.0 25.5           0
## 1666 68946  64 Female   Married   9000       White      80.3 24.3           0
## 1667 68947  65 Female   Widowed   1500       Black      90.2 24.7           0
## 1668 68948  36 Female   Married   3500       White      93.8 26.8           0
## 1669 68949  63   Male   Married   2000 MexAmerican     102.3 26.9           0
## 1670 68952  80 Female   Widowed   3500       White      86.8 23.2           0
## 1671 68961  64 Female   Married   9000       White      88.4 24.2           0
## 1672 68964  20   Male    Single   2500       Black     119.9 35.5           0
## 1673 68966  63 Female    Single    300       Black     102.1 29.5           0
## 1674 68971  21 Female             1600    Hispanic      83.4 22.3           0
## 1675 68972  60 Female   Married   5400    Hispanic     106.0 28.9           0
## 1676 68978  39   Male   Married   9000       White     112.2 36.1           0
## 1677 68979  36 Female   Married   8200       White      89.0 24.3           0
## 1678 68981  80 Female  Divorced   9000       White      90.1 24.7           0
## 1679 68982  27 Female   Married   9000       Asian      91.5 24.1           0
## 1680 68983  67   Male  Divorced   2500    Hispanic     100.0 24.7           0
## 1681 68992  53 Female   Married   1000       Black     114.2 33.2           1
## 1682 68993  34 Female   Married    800       Asian      92.7 26.0           0
## 1683 68998  43 Female   Married   9000       Black      97.1 30.9           0
## 1684 69005  77 Female   Married   8200       White     104.0 31.1           0
## 1685 69007  55   Male Separated   1000    Hispanic     151.0 48.4           2
## 1686 69011  59 Female   Married   9000       White      98.8 31.4           0
## 1687 69014  78   Male   Married   6200       White     130.0 36.2           0
## 1688 69018  39   Male              800       Black      74.8 19.4           0
## 1689 69019  44 Female   Married   1500       White      91.9 27.3           0
## 1690 69022  48 Female   Married   1600       White      99.8 35.2           0
## 1691 69025  60   Male   Married   2000 MexAmerican     108.1 32.2           0
## 1692 69027  37   Male   Married   9000       White      99.0 28.4           0
## 1693 69031  22   Male    Single   2500       Asian      74.5 19.8           0
## 1694 69034  33   Male             1600    Hispanic      93.8 27.8           0
## 1695 69036  76   Male   Married     NA       Black     122.1 35.1           0
## 1696 69037  41   Male   Married   9000 MexAmerican      93.2 27.7           0
## 1697 69047  61 Female   Married   9000       White     115.3 33.8           0
## 1698 69054  43   Male   Married   2000       White     120.6 32.1           0
## 1699 69055  28 Female   Married   3500    Hispanic      74.1 19.6           0
## 1700 69066  74   Male   Married   5400       White      81.3 22.6           0
## 1701 69077  58 Female  Divorced   2500 MexAmerican     144.2 52.6           0
## 1702 69079  32   Male    Single   1600       White        NA 20.7           0
## 1703 69081  23 Female    Single   9000       Black      66.3 20.2           0
## 1704 69086  25 Female   Married   6200       White      96.2 28.7           0
## 1705 69088  67 Female   Married   1600    Hispanic     116.5 38.2           0
## 1706 69091  52   Male  Divorced   4500       White     100.1 28.9           0
## 1707 69097  31   Male   Married   1000    Hispanic      95.6 28.7           0
## 1708 69101  58   Male Separated   2500    Hispanic      99.9 27.0           0
## 1709 69105  55   Male    Single   2000    Hispanic      91.9 26.5           0
## 1710 69107  69   Male  Divorced   1600       Black     103.7 28.4           0
## 1711 69114  37 Female   Married     NA       White     115.7 32.0           0
## 1712 69137  56   Male   Married   9000       Black      95.6 28.1           0
## 1713 69140  80   Male   Married   3500       White     112.5 28.7           1
## 1714 69141  80   Male   Married   2500       Black     108.4 28.3           1
## 1715 69151  57   Male   Married   9000       White      95.6 26.3           0
## 1716 69152  21   Male    Single   1000       Black      73.9 22.0           0
## 1717 69159  22 Female    Single   1000    Hispanic      88.7 27.0           0
## 1718 69161  20   Male              800       White      75.8 19.4           0
## 1719 69164  80 Female   Widowed   3500       White      99.8 26.1           0
## 1720 69168  75   Male Separated   9000       Black      91.9 22.0           1
## 1721 69171  40 Female    Single   3500    Hispanic      89.3 26.8           0
## 1722 69176  57 Female             2000       Black     111.0 31.4           0
## 1723 69177  66   Male   Married   4500       White     108.2 30.7           0
## 1724 69184  56   Male   Married   1600       White     109.5 31.2           0
## 1725 69200  34   Male   Married   9000       Asian      95.5 26.1           0
## 1726 69201  44 Female   Married   9000       Asian      97.4 31.3           0
## 1727 69203  66 Female  Divorced   5400       Black     103.0 33.3           0
## 1728 69205  47 Female   Married   3500       Asian     101.4 29.5           0
## 1729 69220  21 Female              300       Other      82.0 18.2           0
## 1730 69227  62 Female    Single   9000       Black      86.2 25.2           0
## 1731 69229  43   Male   Married   4500       White     111.3 35.5           0
## 1732 69236  33   Male   Married   1600       White     105.1 31.9           0
## 1733 69237  49 Female   Married   9000    Hispanic      95.7 33.3           0
## 1734 69243  45 Female   Married   9000       White      81.0 22.5           0
## 1735 69245  29 Female    Single   4500       Black      97.6 31.2           0
## 1736 69256  56   Male   Married   1000       Other     126.0 40.0           0
## 1737 69259  30   Male    Single   2500       Other      84.2 22.6           0
## 1738 69261  51 Female    Single     NA       White     127.4   NA           1
## 1739 69264  69   Male   Married   9000       Black     124.5 37.7           0
## 1740 69266  27   Male             1600       Black      96.9 27.4           0
## 1741 69272  43 Female             1600    Hispanic      90.2 28.1           0
## 1742 69274  21 Female    Single   1600       Black      89.0 26.1           0
## 1743 69277  24   Male    Single   2500       Asian      89.6 24.8           0
## 1744 69278  78 Female  Divorced   2500       Black      94.2 28.4           0
## 1745 69279  58 Female   Married   9000       White     105.8 27.7           0
## 1746 69284  53   Male  Divorced   1000    Hispanic      98.4 28.4           0
## 1747 69285  26 Female    Single   2000       White        NA   NA           0
## 1748 69286  39   Male    Single   9000       Asian      98.0 25.9           0
## 1749 69288  69 Female   Married   1000       Black      90.3 22.6           1
## 1750 69301  64 Female   Married   4500       White      97.4 26.2           0
## 1751 69307  58   Male  Divorced   2000       Black      74.0 17.9           0
## 1752 69314  50   Male   Married   3500       Black      97.2 28.6           0
## 1753 69320  58 Female   Married   1000 MexAmerican      97.7 30.5           0
## 1754 69324  42   Male   Married   9000       White     102.6 25.5           0
## 1755 69325  36 Female             9000       Asian      95.2 31.7           0
## 1756 69329  50 Female  Divorced    800       White     104.2 31.1           0
## 1757 69336  30   Male  Divorced   2500       White     147.0 45.8           0
## 1758 69339  22   Male             4500 MexAmerican      91.3 24.6           0
## 1759 69343  20   Male    Single   9000       White      95.1 27.2           0
## 1760 69347  49   Male   Married   2500       White     110.8 30.1           0
## 1761 69349  74   Male   Married   8200       White     104.0 25.2           0
## 1762 69351  31 Female   Married   3500       White      86.5 25.2           0
## 1763 69361  66   Male   Married   2500       Black     106.7 31.2           0
## 1764 69363  22 Female    Single   1000 MexAmerican     113.6 36.5           0
## 1765 69365  59 Female    Single   1600       White     109.0 34.6           0
## 1766 69379  30   Male              300       White      92.0 25.6           0
## 1767 69380  20   Male    Single    300    Hispanic     102.9 32.8           1
## 1768 69386  52   Male    Single   1000       Other     112.8 31.2           0
## 1769 69387  25   Male    Single   4500       White      92.1 25.6           0
## 1770 69388  61   Male   Married   1600 MexAmerican        NA 37.4           1
## 1771 69391  52 Female             6200 MexAmerican     106.9 29.8           0
## 1772 69393  33   Male   Married   8200       Black      93.7 29.6           0
## 1773 69395  25   Male    Single   2500       Black      86.1 23.5           0
## 1774 69402  59 Female    Single   8200       Asian      98.2 26.2           0
## 1775 69403  61   Male  Divorced   2500       White     129.8 39.7           0
## 1776 69409  50 Female    Single   8200       Black      82.5 22.6           0
## 1777 69410  46 Female   Married   9000       Black      99.9 30.3           0
## 1778 69411  75   Male   Married   3500       White     116.9 38.7           0
## 1779 69413  50 Female  Divorced   2000       Black     110.8 35.0           0
## 1780 69418  71   Male   Married   9000       White      93.0 24.7           0
## 1781 69422  37 Female  Divorced   9000       Black      95.3 31.4           0
## 1782 69427  44   Male             1000       Black     105.0 28.0           0
## 1783 69428  42 Female   Married   3500       White     131.0 47.0           0
## 1784 69430  67 Female   Married   1600       Asian     103.1 25.7           0
## 1785 69431  79 Female   Married   5400       Black      84.8 22.3           0
## 1786 69433  53   Male   Married   3500 MexAmerican     125.5 36.2           1
## 1787 69434  43 Female   Married   1600 MexAmerican     113.3 37.7           0
## 1788 69446  25   Male    Single   2000 MexAmerican     107.4 30.5           0
## 1789 69450  39 Female   Married   9000       White      80.0 21.2           0
## 1790 69452  56 Female   Married   9000       White     110.0 38.4           0
## 1791 69457  80   Male   Married   1000       White        NA 38.2           0
## 1792 69460  50   Male   Married   6200    Hispanic     110.5 29.4           0
## 1793 69463  20   Male             1600       White      93.4 29.0           0
## 1794 69468  69   Male   Married   2500       Black      86.5 21.0           0
## 1795 69472  38   Male   Married   8200       Black      88.2 23.4           0
## 1796 69473  79   Male   Widowed   3500       Black     104.2 25.1           2
## 1797 69474  66 Female    Single   3500    Hispanic      84.3 22.4           0
## 1798 69486  67 Female  Divorced   4500       Black     122.2 42.6           1
## 1799 69488  65 Female  Divorced   2000       White      96.6 29.1           0
## 1800 69494  37 Female   Married   4500       White      80.2 22.0           0
## 1801 69495  22 Female    Single   1000       Asian      69.9 20.1           0
## 1802 69499  42 Female   Married   9000       White      86.8 21.4           0
## 1803 69502  50 Female    Single   4500       White     102.6 28.9           0
## 1804 69504  54   Male   Married   9000       Asian      78.7 21.5           0
## 1805 69506  80   Male   Married   1600       White     130.8 39.9           1
## 1806 69511  65 Female Separated   1600       Black      91.0 25.2           0
## 1807 69513  46   Male   Married   9000       Black      97.1 24.0           0
## 1808 69514  57   Male   Married   8200       Black     100.0 27.1           0
## 1809 69516  74   Male   Married   5400       White     109.9 28.4           0
## 1810 69520  22   Male    Single   9000       White      79.5 20.2           0
## 1811 69523  56   Male  Divorced   4500       White     121.0 34.1           0
## 1812 69528  80   Male   Married   9000 MexAmerican     112.7 32.5           2
## 1813 69532  47 Female   Married   2500       Asian      93.6 26.0           0
## 1814 69534  29 Female             6200       Black      97.0 31.0           0
## 1815 69536  57 Female   Married   4500       White     100.0 28.6           0
## 1816 69537  49   Male   Married   9000       White     110.8 29.8           0
## 1817 69542  40 Female    Single   1000       White     116.0 31.9           1
## 1818 69546  26   Male    Single   2500       Asian      71.2 17.3           0
## 1819 69547  73   Male   Widowed   8200       Black     109.4 30.2           1
## 1820 69550  58   Male             2500       Black     176.0 55.7           0
## 1821 69553  70 Female   Married   1700    Hispanic      95.7 27.3           0
## 1822 69560  26   Male    Single   2000    Hispanic      88.9 24.4           0
## 1823 69562  80   Male   Married     NA       White     119.3 33.2           0
## 1824 69569  61 Female   Married   2500       Asian      72.2 21.1           0
## 1825 69574  48 Female   Married   8200       White      87.2 23.2           0
## 1826 69577  52   Male Separated   1000       Black     111.5 33.1           0
## 1827 69581  23   Male    Single   9000       Black      91.2 27.5           0
## 1828 69594  31   Male   Married   2500       White      80.0 20.3           0
## 1829 69596  64   Male   Married   6200       Black      90.3 24.4           1
## 1830 69599  21   Male    Single   1600 MexAmerican      97.0 30.1           0
## 1831 69603  26   Male   Married   1600 MexAmerican      82.6 24.2           0
## 1832 69607  40   Male  Divorced    800       Other      90.7 24.4           0
## 1833 69608  75   Male  Divorced   1600       Black      93.2 26.0           1
## 1834 69613  27 Female   Married   9000       Asian      78.3 23.5           0
## 1835 69617  25 Female  Divorced   2500       White      91.7 26.3           0
## 1836 69619  41 Female Separated   2500       Black      97.4 29.3           0
## 1837 69622  58   Male   Married   2000       White     151.8 51.5           1
## 1838 69624  67   Male   Married     NA       Asian      66.3 16.2           0
## 1839 69626  53   Male   Married   8200       White     109.8 34.1           0
## 1840 69630  23   Male             3500 MexAmerican      84.0 28.0           0
## 1841 69633  38   Male   Married   9000 MexAmerican      99.8 30.8           0
## 1842 69637  58 Female  Divorced   2500       White     103.0 32.5           0
## 1843 69640  23 Female    Single   2000       Black     116.5 38.5           1
## 1844 69644  64 Female   Married   4500       Asian      91.6 28.6           0
## 1845 69645  71 Female   Married     NA       White      84.5 23.8           0
## 1846 69647  36   Male             8200       White     102.5 29.4           0
## 1847 69649  27   Male    Single   2000       Asian     113.7 35.2           0
## 1848 69650  48   Male    Single    800       White      82.3 20.8           0
## 1849 69653  28   Male   Married   5400       White      96.4 28.3           1
## 1850 69658  73   Male   Married   8200       Black     132.3 40.0           0
## 1851 69666  70 Female   Married   4500       White      98.5 39.8           0
## 1852 69667  63 Female   Married   4500       White      97.0 27.2           0
## 1853 69668  61   Male   Married   9000       White      94.7 25.1           1
## 1854 69669  66 Female   Widowed   9000       Black      95.9 26.3           0
## 1855 69674  60   Male             4500       Black     101.8 26.7           0
## 1856 69679  26   Male   Married   4500       Black      90.8 28.1           0
## 1857 69680  37   Male             1000       Black      90.2 24.2           0
## 1858 69684  65   Male  Divorced   1000    Hispanic     116.4 32.1           1
## 1859 69687  47 Female   Married   9000       White      80.2 23.3           0
## 1860 69695  80   Male  Divorced   1600       Black     100.0 24.8           1
## 1861 69697  22 Female    Single    800       Black      85.0 26.5           0
## 1862 69698  49   Male  Divorced    800       Black     103.0 34.5           0
## 1863 69700  27 Female    Single    800    Hispanic      90.0 25.6           0
## 1864 69701  52   Male    Single   2500       Black      95.4 24.4           0
## 1865 69702  42   Male               NA       White      97.0 26.9           0
## 1866 69704  30   Male   Married   1000       White      86.9 23.4           0
## 1867 69710  28 Female   Married   1000       White      82.0 20.6           0
## 1868 69711  51 Female   Married   4500       Black     103.0 31.8           0
## 1869 69715  43 Female Separated   1600       Black      95.0 28.0           1
## 1870 69721  22 Female    Single   6200       Black      78.0 23.7           0
## 1871 69732  33   Male   Married   2000       Asian      94.5 28.3           0
## 1872 69740  66 Female   Married   8200       White      96.5 28.8           0
## 1873 69747  34 Female  Divorced   2000       Black     118.4 34.7           0
## 1874 69753  63 Female   Married   2000 MexAmerican     102.4 30.1           0
## 1875 69755  65 Female   Married   8200       White      99.1 28.8           0
## 1876 69764  22 Female    Single   8200       Black      80.5 23.6           0
## 1877 69770  24 Female               NA       Black      75.5 22.1           0
## 1878 69774  54   Male   Married   3500    Hispanic     102.7 29.6           0
## 1879 69777  60 Female   Married   6200 MexAmerican     108.6 36.0           0
## 1880 69778  42   Male             5400 MexAmerican     104.4 29.8           0
## 1881 69783  66 Female    Single    800       Asian      67.5 20.4           0
## 1882 69789  53 Female  Divorced     NA       Black      80.7 23.4           0
## 1883 69793  35   Male   Married    800       Asian      88.8 27.3           0
## 1884 69797  31 Female   Married   8200       White      98.3 26.7           0
## 1885 69798  21 Female    Single    800       White      74.0 19.8           1
## 1886 69803  44   Male   Married   9000       Asian      85.1 21.8           0
## 1887 69813  30 Female    Single   5400       Black     102.0 35.1           0
## 1888 69815  70 Female   Widowed   3500       Black     123.1 33.6           1
## 1889 69816  20 Female    Single   1700       Black     104.7 34.8           1
## 1890 69823  55 Female  Divorced    300       Black      96.4 28.6           0
## 1891 69824  64   Male   Married   2500       Asian      78.2 22.0           0
## 1892 69827  30   Male Separated     NA    Hispanic     101.3 27.5           0
## 1893 69831  80 Female   Widowed    800       Asian      82.4 22.6           0
## 1894 69848  70   Male   Married   1000       Black     115.5 34.1           0
## 1895 69854  65   Male   Married   6200       Other     138.0 41.4           1
## 1896 69858  65   Male   Married   5400       Black      94.6 28.1           0
## 1897 69861  73 Female   Widowed   2500       Black      84.0 25.2           0
## 1898 69862  35 Female   Married   9000       White      95.0 28.6           0
## 1899 69863  43   Male   Married   8200       White     111.2 32.3           0
## 1900 69864  52   Male               NA       Black      92.8 28.7           0
## 1901 69867  50 Female    Single   1700       Black     105.8 27.9           0
## 1902 69869  36 Female             2000    Hispanic      82.6 24.0           0
## 1903 69870  68   Male   Married   9000       White     108.0 27.2           0
## 1904 69872  39   Male   Married   6200       White     101.6 27.1           0
## 1905 69875  45 Female   Married   9000       Asian      82.7 23.3           0
## 1906 69880  34 Female             8200       White      87.7 25.2           0
## 1907 69884  56   Male   Married   4500       Asian      90.1 27.6           1
## 1908 69885  42 Female  Divorced   5400       Black     106.9 33.7           0
## 1909 69887  23 Female    Single   1000       Black     105.2 31.6           0
## 1910 69893  22   Male    Single   1600       White      94.9 26.2           0
## 1911 69896  49   Male    Single   2500       White      98.5 23.8           0
## 1912 69898  71   Male   Married   2500       White     104.0 27.7           0
## 1913 69899  33 Female             2000       Black     110.4 37.9           1
## 1914 69910  20   Male    Single   2500       White      73.6 20.5           0
## 1915 69911  80 Female   Widowed   4500    Hispanic        NA 28.2           0
## 1916 69916  22 Female    Single   6200    Hispanic      83.0 22.0           1
## 1917 69917  33 Female   Married   9000       White     106.5 33.8           0
## 1918 69921  75   Male   Married   2500       Black     115.0 30.2           1
## 1919 69924  80   Male   Married   1000       White      75.0 15.7           0
## 1920 69925  80 Female    Single   1000 MexAmerican     111.9 35.3           0
## 1921 69930  27 Female   Married   5400       White     110.5 30.0           0
## 1922 69931  28 Female   Married   9000       White      97.0 29.6           0
## 1923 69941  52 Female   Married   8200       Asian      93.1 29.7           0
## 1924 69943  40   Male   Married   9000       White      91.0 28.5           0
## 1925 69948  45   Male             1000       White     120.1 33.7           0
## 1926 69962  69   Male   Married   1600 MexAmerican     108.0 32.0           0
## 1927 69963  20 Female    Single   1600       Black      72.1 23.4           0
## 1928 69964  75 Female   Married   2500       Other     129.7 44.0           1
## 1929 69973  55 Female  Divorced   3500       White     106.0 33.0           0
## 1930 69976  61   Male   Married   1700    Hispanic      98.6 31.9           0
## 1931 69983  38   Male  Divorced   1000       White      97.0 25.1           0
## 1932 69989  75 Female             1600    Hispanic      95.5 28.9           0
## 1933 69990  23 Female    Single    800       Black     106.2 31.0           0
## 1934 69991  56 Female  Divorced   1000       White      90.5 29.4           0
## 1935 69994  21 Female    Single   6200       Other      64.2 18.2           0
## 1936 69999  29 Female    Single   2000       Black      80.4 25.2           0
## 1937 70005  80   Male   Married   2000       White        NA 30.6           0
## 1938 70006  29   Male    Single     NA    Hispanic      95.0 28.9           0
## 1939 70008  55 Female  Divorced   2500       White      96.0 26.0           0
## 1940 70014  32   Male    Single   9000       White     103.2 28.6           0
## 1941 70016  72 Female   Married   9000       White        NA 29.2           0
## 1942 70032  80   Male   Married     NA       Asian      82.8 20.0           1
## 1943 70033  53 Female   Married   1700       White     103.1 32.3           0
## 1944 70046  55   Male Separated   1000       White      85.7 22.4           0
## 1945 70049  41   Male   Married   5400       Asian     106.1 32.8           0
## 1946 70052  28 Female    Single   2000       Asian      68.5 17.9           0
## 1947 70058  38   Male   Married   3500       Asian      74.8 20.8           0
## 1948 70059  74 Female   Widowed   1000       White     101.4 27.7           0
## 1949 70072  53   Male  Divorced   3500       Black     122.0 35.2           0
## 1950 70075  31 Female   Married   2000       Asian      80.5 24.0           0
## 1951 70082  29 Female    Single   4500       Black      90.4 27.5           0
## 1952 70094  36 Female   Married   9000       White     112.0 36.9           1
## 1953 70101  45 Female  Divorced   3500       Black      87.4 25.2           0
## 1954 70102  68   Male   Widowed   2500       White     111.7 31.9           0
## 1955 70109  57   Male   Married   9000    Hispanic     111.6 30.3           0
## 1956 70111  56   Male   Married     NA       Black      74.5 17.0           0
## 1957 70115  36 Female Separated    800 MexAmerican      83.0 20.6           0
## 1958 70118  80 Female   Widowed   2000       White      80.5 20.5           0
## 1959 70122  37 Female   Married   6200       White     128.3 43.6           0
## 1960 70123  45 Female   Married     NA       Asian      91.2 26.3           0
## 1961 70125  30   Male    Single   1600       Black     122.5 39.3           0
## 1962 70127  26 Female    Single   1600       White     103.2 29.5           0
## 1963 70130  42   Male   Married   3500       Black     102.9 31.2           0
## 1964 70136  39   Male   Married   9000       Asian        NA 25.0           0
## 1965 70143  40 Female   Married   8200       Asian      74.0 19.0           0
## 1966 70151  80 Female   Widowed   2500       White      97.7 30.7           0
## 1967 70160  61 Female   Married   2500    Hispanic      87.2 24.1           0
## 1968 70161  34   Male   Married   3500 MexAmerican     137.0 44.9           1
## 1969 70163  53 Female   Married   9000       White     102.0 34.3           0
## 1970 70168  73   Male   Married   9000       White     100.0 27.7           0
## 1971 70169  23 Female             2500       Other      94.0 23.3           0
## 1972 70175  62 Female  Divorced   3500       Black     100.6 34.9           0
## 1973 70176  23 Female    Single    300 MexAmerican      81.2 21.9           0
## 1974 70191  52 Female  Divorced   2000    Hispanic      88.3 26.2           1
## 1975 70192  22 Female    Single   3500       Asian      75.4 20.9           0
## 1976 70196  37   Male    Single   2000 MexAmerican     106.9 30.9           0
## 1977 70202  22   Male    Single   2000       Asian      94.0 27.0           0
## 1978 70204  20 Female    Single   3500       Black     122.2 40.8           0
## 1979 70206  34 Female   Married   9000       Asian      80.4 22.5           0
## 1980 70210  47   Male   Widowed   2000 MexAmerican     105.7 30.2           1
## 1981 70212  40 Female   Married   2000       White      94.3 27.8           0
## 1982 70213  35   Male   Married   8200       White      96.5 28.2           0
## 1983 70217  40   Male   Married   9000       Asian      80.8 20.7           0
## 1984 70219  69 Female   Widowed   2500       Other     102.5 29.9           0
## 1985 70220  31 Female   Married   6200 MexAmerican      90.0 27.5           2
## 1986 70223  47   Male  Divorced    800       White     109.0 31.1           0
## 1987 70225  25   Male   Married   6200       White     108.8 33.9           0
## 1988 70227  46 Female   Married   9000       Asian      94.0 28.4           0
## 1989 70230  24   Male    Single   3500       Asian      75.5 19.2           0
## 1990 70231  37 Female   Married   9000       Asian     100.5 31.8           0
## 1991 70238  25 Female  Divorced   3500 MexAmerican      81.6 23.7           1
## 1992 70244  80   Male   Married     NA       White     109.5 28.9           0
## 1993 70248  67 Female   Married   1000    Hispanic      91.1 24.3           0
## 1994 70254  42 Female   Married   8200       White      96.6 31.2           0
## 1995 70255  38 Female             1500 MexAmerican      90.4 27.9           0
## 1996 70261  24   Male             1600       White     129.9 41.0           0
## 1997 70264  23 Female    Single     NA       Asian      72.0 18.7           0
## 1998 70265  46 Female   Widowed   2000       White      97.0 27.6           0
## 1999 70267  32   Male    Single   8200       White      81.2 24.1           0
## 2000 70281  30 Female    Single   3500       Asian      89.9 25.1           0
## 2001 70282  24   Male    Single   3500 MexAmerican      92.8 28.4           0
## 2002 70288  37 Female   Married   2500       White      97.5 29.7           0
## 2003 70290  60   Male   Married   5400       Black      87.0 22.1           1
## 2004 70291  25 Female    Single   2500       White     130.4 40.5           0
## 2005 70292  48 Female   Married   6200       Black      97.8 31.0           0
## 2006 70295  47   Male   Married   9000       Black     106.5 33.7           0
## 2007 70297  73   Male   Married   3500       White      94.7 24.7           0
## 2008 70300  46   Male    Single    800       White     103.0 28.7           0
## 2009 70301  51 Female  Divorced    300       Black      96.5 27.8           0
## 2010 70303  56   Male  Divorced   9000    Hispanic     107.8 32.4           0
## 2011 70306  20   Male    Single   2500       Black      66.1 17.9           1
## 2012 70317  51   Male   Married   3500       Asian      94.7 27.2           2
## 2013 70326  35   Male             2000       Other     126.7 39.5           0
## 2014 70328  27   Male   Married    300 MexAmerican     109.4 31.8           0
## 2015 70329  60 Female   Married   1000    Hispanic      91.8 26.1           0
## 2016 70330  77   Male   Married   3500       Asian     104.9 29.5           1
## 2017 70331  52   Male   Married   1600 MexAmerican     114.1 32.4           0
## 2018 70332  80   Male  Divorced   1600       White     124.2 34.2           1
## 2019 70333  20 Female    Single   9000 MexAmerican      72.7 18.0           0
## 2020 70335  53 Female  Divorced   1000       White     109.5 36.5           1
## 2021 70339  55 Female   Married   1600       White        NA   NA           0
## 2022 70341  62   Male   Married   8200       Asian      98.6 28.2           0
## 2023 70347  70   Male   Married   9000       Black        NA   NA           0
## 2024 70349  80 Female   Widowed   1600       Black      93.3 25.8           2
## 2025 70351  80 Female   Widowed   2500       White      93.1 23.2           1
## 2026 70357  43 Female   Married   9000       Asian      80.5 24.6           0
## 2027 70359  80   Male   Married   8200       White      99.8 26.2           0
## 2028 70368  55   Male   Married   9000       Black     134.9 42.5           2
## 2029 70378  53   Male   Married   3500       Black      85.0 20.6           0
## 2030 70381  24   Male             2500       Other     126.1 38.4           0
## 2031 70387  60 Female             3500 MexAmerican     107.8 33.8           0
## 2032 70389  56 Female Separated     NA    Hispanic        NA 35.9           0
## 2033 70394  47   Male    Single   9000       Asian     100.0 26.9           0
## 2034 70398  57 Female Separated   2500    Hispanic      83.3 27.3           0
## 2035 70399  24   Male    Single   1000       Asian      89.2 24.3           0
## 2036 70401  47   Male   Married   9000       Asian      83.4 22.3           0
## 2037 70405  61 Female   Married   9000       White     111.6 32.7           0
## 2038 70408  33   Male    Single   8200       Black     116.9 30.9           0
## 2039 70409  44   Male  Divorced   2500       White     105.1 29.2           0
## 2040 70413  51   Male   Married   6200       Asian      86.8 26.4           0
## 2041 70415  80 Female   Widowed   1700       White      89.8 23.8           0
## 2042 70417  80   Male  Divorced   1600 MexAmerican      86.6 21.6           0
## 2043 70421  51 Female  Divorced   4500    Hispanic     116.0 36.8           0
## 2044 70425  77   Male   Married   4500       White     105.1 23.9           2
## 2045 70427  36 Female   Married   9000       White      69.7 22.7           1
## 2046 70430  37 Female   Married   8200       White      69.9 19.9           0
## 2047 70437  43   Male   Married   3500 MexAmerican      95.8 29.8           0
## 2048 70439  24 Female   Married   9000       White      78.0 22.8           0
## 2049 70443  52 Female   Married   4500    Hispanic     110.0 36.9           0
## 2050 70445  71 Female   Married   1700       White     103.6 24.0           0
## 2051 70448  29   Male Separated   2500 MexAmerican      95.9 29.3           0
## 2052 70464  60 Female    Single   1600       Black      93.6 26.1           0
## 2053 70470  43 Female   Married   9000       Asian      98.9 32.9           0
## 2054 70473  50 Female   Married   6200       White      93.5 30.9           0
## 2055 70476  30   Male   Married   3500       White      93.5 28.6           0
## 2056 70478  34 Female   Married   9000       Asian        NA 21.9           0
## 2057 70481  24   Male   Married   1000       White     127.2 39.8           0
## 2058 70483  20   Male    Single   6200       Asian     123.5 38.9           0
## 2059 70485  34   Male    Single   8200       Asian      76.8 20.6           0
## 2060 70489  40   Male   Married   3500    Hispanic     105.8 30.3           0
## 2061 70493  52   Male    Single    800       Other      96.0 29.7           0
## 2062 70494  25   Male    Single   3500 MexAmerican     120.6 37.1           0
## 2063 70498  63 Female    Single   6200       White     113.3 39.0           0
## 2064 70514  22 Female              300       White     111.5 33.3           0
## 2065 70523  31   Male   Married   8200       White      94.6 31.6           0
## 2066 70525  63   Male  Divorced    800       Black     100.8 27.9           0
## 2067 70529  49   Male   Married   1000       White     100.0 27.8           0
## 2068 70534  48 Female               NA MexAmerican      95.3 27.6           0
## 2069 70536  30   Male    Single   2500       Other      86.2 24.7           0
## 2070 70543  78 Female   Married   2500       Black        NA 40.2           1
## 2071 70544  77   Male   Married   2500       Black      92.0 23.3           2
## 2072 70545  31   Male  Divorced   3500 MexAmerican      85.1 23.7           0
## 2073 70547  39 Female    Single   1000       White      85.0 23.5           0
## 2074 70548  34   Male Separated   3500 MexAmerican      86.2 24.5           0
## 2075 70550  76   Male   Married   8200       Black     103.0 29.1           0
## 2076 70561  42   Male   Married   8200       Black      84.8 24.7           0
## 2077 70562  52   Male              300       White     103.5 24.9           0
## 2078 70565  76 Female  Divorced   3500       Asian      92.6 25.6           0
## 2079 70566  31 Female    Single    800       Black      87.2 29.4           0
## 2080 70567  80   Male   Married   1500       White     101.4 25.1           1
## 2081 70573  24   Male    Single   3500 MexAmerican     110.3 34.0           0
## 2082 70575  69 Female  Divorced   5400       White      85.1 24.9           0
## 2083 70580  58   Male   Married   2500       Black      95.8 25.2           0
## 2084 70587  50 Female    Single   2500    Hispanic      90.0 26.2           0
## 2085 70590  51 Female  Divorced   5400    Hispanic      98.9 31.9           0
## 2086 70593  80   Male   Widowed   2000       Black     100.5 26.9           0
## 2087 70595  60 Female  Divorced     NA    Hispanic        NA 29.9           0
## 2088 70596  33 Female   Married   9000       White      85.7 23.9           0
## 2089 70597  49 Female    Single   2500       Other      99.0 26.3           0
## 2090 70599  54   Male   Married   2500       White      97.5 25.5           0
## 2091 70604  39   Male   Married   9000       Asian      76.9 21.3           0
## 2092 70605  56   Male   Married   9000       Black      97.8 27.3           0
## 2093 70617  45 Female             2000       White     102.2 28.1           0
## 2094 70626  33   Male   Married   2000       White     105.7 29.3           0
## 2095 70627  52 Female Separated   8200       Black      84.1 24.3           0
## 2096 70633  56   Male   Married   9000       White     128.9 36.7           0
## 2097 70635  68 Female   Married   1700       White     110.0 36.1           0
## 2098 70639  34 Female             3500 MexAmerican     109.4 32.5           1
## 2099 70641  63   Male    Single    800       Black      85.4 22.3           0
## 2100 70644  41   Male   Married   5400       White      97.4 28.7           0
## 2101 70649  63   Male   Married   9000    Hispanic     112.2 33.3           0
## 2102 70653  43   Male    Single   8200       White     109.7 31.0           0
## 2103 70661  65 Female   Married   9000    Hispanic      78.2 22.5           1
## 2104 70663  29 Female  Divorced   2500       Black      77.2 24.9           0
## 2105 70664  70 Female   Married   1600       White     106.8 33.1           0
## 2106 70670  56 Female   Married   6200    Hispanic     108.8 34.1           0
## 2107 70675  65   Male   Married   8200       Asian     102.3 29.5           0
## 2108 70676  75 Female  Divorced   6200       White      93.8 23.0           0
## 2109 70678  21   Male    Single   2500    Hispanic      89.1 26.4           0
## 2110 70682  22 Female    Single   6200       Black     100.8 30.3           0
## 2111 70684  58   Male   Married     NA       Asian      86.7 22.8           0
## 2112 70686  48 Female    Single   9000       Black     114.9 45.5           0
## 2113 70704  35 Female   Married   8200    Hispanic     122.0 41.8           0
## 2114 70710  57 Female  Divorced   1000    Hispanic      99.5 31.7           0
## 2115 70716  43 Female   Married   9000       White      75.7 19.4           0
## 2116 70718  75   Male  Divorced   1600       White     111.2 30.2           1
## 2117 70721  79 Female   Married   5400    Hispanic     107.5 35.0           0
## 2118 70725  60 Female   Married   6200       Black     101.0 40.5           1
## 2119 70727  44 Female   Married   9000       Black     105.5 36.0           0
## 2120 70737  28   Male    Single    300    Hispanic      89.7 28.4           0
## 2121 70741  21 Female    Single   3500       Black      73.8 22.2           0
## 2122 70747  80   Male   Widowed   1000       White        NA 35.7           1
## 2123 70748  32 Female   Married   3500       White      84.0 23.9           0
## 2124 70751  27   Male Separated   1000 MexAmerican      87.4 25.9           0
## 2125 70753  30   Male             2500 MexAmerican     117.0 33.2           1
## 2126 70755  56   Male   Married   6200       White     100.8 23.7           0
## 2127 70758  21   Male    Single   2000    Hispanic      78.4 21.2           0
## 2128 70761  46   Male   Married   4500 MexAmerican     118.5 34.7           1
## 2129 70772  71   Male   Married   9000       White        NA   NA           0
## 2130 70774  49 Female    Single   1000       Black     114.4 32.9           0
## 2131 70775  60   Male   Married     NA    Hispanic      85.6 23.2           0
## 2132 70776  60   Male   Married   9000       Asian      71.0 18.6           0
## 2133 70785  41 Female   Married    300       Black     155.0 57.1           0
## 2134 70788  34   Male   Married   8200       Asian      84.5 23.6           0
## 2135 70804  53 Female   Married   9000       Black     101.4 30.1           0
## 2136 70806  42 Female  Divorced   5400       White      96.1 27.0           0
## 2137 70807  22 Female    Single   8200 MexAmerican      91.6 29.0           0
## 2138 70812  25   Male    Single   8200       Black     114.5 33.6           2
## 2139 70821  63   Male   Married   8200       White     118.4 30.3           0
## 2140 70825  47   Male  Divorced   9000       White      92.4 25.8           0
## 2141 70832  31 Female   Married   2000       White      87.8 23.2           0
## 2142 70833  35 Female             2000       Black      85.3 25.5           0
## 2143 70837  60   Male   Married   2000 MexAmerican     101.8 29.8           0
## 2144 70842  32   Male    Single     NA       Asian      71.4 17.8           1
## 2145 70845  21 Female    Single   1700       Black      85.7 20.8           0
## 2146 70850  28 Female   Married   8200       Asian      69.0 16.9           0
## 2147 70860  44 Female   Married   3500       Black     114.3 35.8           0
## 2148 70862  75   Male   Married   1600       Asian        NA 24.3           1
## 2149 70863  77 Female  Divorced    800       Asian      80.0 24.3           1
## 2150 70868  46   Male   Married   1600       White      80.0 21.1           0
## 2151 70871  39   Male   Married   2500       White     110.5 34.2           0
## 2152 70890  59 Female             3500       Black      98.8 33.5           0
## 2153 70894  70   Male   Married   4500       White     120.8 36.1           0
## 2154 70898  71   Male   Married   1500    Hispanic      92.2 26.8           0
## 2155 70900  59   Male    Single    800       Black     141.2 50.9           2
## 2156 70906  39   Male   Married   8200       White     123.5 33.8           0
## 2157 70908  25   Male    Single   3500       White      83.3 22.4           0
## 2158 70912  67   Male   Widowed   6200    Hispanic     140.1 38.1           0
## 2159 70914  40   Male    Single    300       Black      68.1 17.6           2
## 2160 70916  78 Female   Widowed   1000    Hispanic      91.6 25.8           2
## 2161 70920  46 Female   Married   3500       Asian      86.7 23.8           0
## 2162 70929  29 Female             8200       Asian      82.8 23.2           0
## 2163 70932  43 Female   Married   9000       Asian      73.6 18.4           1
## 2164 70933  46 Female   Married   9000       Asian      99.3 29.0           0
## 2165 70935  46 Female   Married   9000       Black      91.8 24.5           0
## 2166 70938  49   Male  Divorced   4500 MexAmerican      97.3 28.5           0
## 2167 70941  45   Male   Married   6200       White      92.0 27.0           0
## 2168 70949  68 Female   Married   9000       White      86.3 23.8           0
## 2169 70950  50   Male   Married    800    Hispanic      87.2 23.5           0
## 2170 70959  55 Female              300       White     110.0 39.7           0
## 2171 70961  74 Female    Single   5400       White      85.2 21.4           0
## 2172 70966  20   Male             1000       Asian      76.0 20.6           0
## 2173 70967  25   Male    Single     NA       Black     113.5 33.3           0
## 2174 70969  45   Male   Married   1000 MexAmerican      93.7 27.4           0
## 2175 70972  61   Male  Divorced     NA       Black     106.3 30.5           0
## 2176 70973  39   Male  Divorced   3500       White      84.3 22.4           0
## 2177 70974  49   Male   Married   2000       White     129.4 39.3           0
## 2178 70975  22 Female   Married   1600       White      92.3 31.9           0
## 2179 70979  46   Male   Married   9000       Asian     109.3 32.3           1
## 2180 70980  32   Male   Married   4500       White      97.0 27.4           0
## 2181 70982  44   Male   Married   1600    Hispanic     102.3 28.7           0
## 2182 70987  22 Female    Single   9000       White      78.9 23.6           0
## 2183 70991  80 Female   Widowed   1000       White      93.1 26.2           1
## 2184 70995  34 Female   Married   1600       White     144.0 45.5           1
## 2185 70996  41   Male   Married   9000    Hispanic      84.8 23.8           0
## 2186 70999  50 Female   Married   8200       White      74.0 20.2           0
## 2187 71005  64 Female   Married   4500       Black      99.9 36.2           0
## 2188 71037  52 Female   Married   9000       Black      78.0 23.4           0
## 2189 71038  60   Male   Married    300    Hispanic     101.0 29.1           1
## 2190 71042  38   Male   Married   2000       Asian      86.7 22.3           0
## 2191 71046  52   Male   Married   8200       White     117.9 33.8           0
## 2192 71048  52 Female Separated    300 MexAmerican      72.6 18.9           0
## 2193 71051  78   Male   Married   9000       White        NA 27.7           0
## 2194 71059  53   Male   Married   1000       White     113.8 29.9           0
## 2195 71060  31 Female   Widowed    300       White     115.8 33.8           0
## 2196 71061  54   Male   Married   5400 MexAmerican     103.5 30.4           0
## 2197 71062  52   Male  Divorced   1000       White     114.2 33.4           2
## 2198 71064  26 Female    Single   2000       Asian     138.2 44.5           0
## 2199 71065  51 Female   Married   2500       White      66.4 17.5           0
## 2200 71066  71 Female    Single   2500    Hispanic      84.4 20.7           0
## 2201 71069  62 Female   Married   2500       White      99.4 29.9           0
## 2202 71071  36 Female   Married   4500       Asian      89.0 28.7           0
## 2203 71072  50 Female Separated   2500    Hispanic     105.5 37.0           0
## 2204 71076  63 Female   Married   8200       Other      88.2 27.4           0
## 2205 71084  55   Male Separated   2000       White     103.7 27.5           0
## 2206 71087  65 Female   Widowed   1600 MexAmerican     122.8 38.4           1
## 2207 71089  32 Female Separated     NA MexAmerican      96.0 32.3           0
## 2208 71091  39 Female             5400    Hispanic      93.5 32.3           0
## 2209 71097  21   Male    Single    300       Black      75.2 23.7           0
## 2210 71101  51   Male    Single    800       White     118.0 33.4           0
## 2211 71103  57 Female  Divorced   2500       White     125.0 37.8           0
## 2212 71107  34 Female  Divorced   6200       White      79.9 22.3           0
## 2213 71108  20 Female    Single    300       Black     112.4 41.0           0
## 2214 71111  75 Female   Widowed    800       White        NA 42.9           1
## 2215 71114  20 Female    Single    300       White      77.6 20.5           1
## 2216 71117  32 Female    Single    800       Black      77.7 20.6           0
## 2217 71119  36   Male   Married   9000       White      95.4 25.2           0
## 2218 71122  63   Male   Married   9000       White     104.2 26.3           0
## 2219 71132  68 Female   Married   6200       White      82.7 25.2           0
## 2220 71133  36 Female    Single   3500       White      72.2 18.1           0
## 2221 71135  76 Female   Married   1000       White      99.8 28.6           1
## 2222 71136  21   Male    Single   2000       Asian      85.5 24.4           0
## 2223 71141  78 Female   Widowed   4500       Black      87.3 25.0           0
## 2224 71144  30 Female   Married   3500       White        NA 36.4           1
## 2225 71155  41   Male    Single   8200       White      99.4 27.1           0
## 2226 71157  26 Female   Married   2500       Black     105.7 35.7           0
## 2227 71159  37 Female   Married   9000       White      80.3 20.8           0
## 2228 71164  48   Male   Married   8200       White     103.9 31.1           0
## 2229 71172  42 Female   Married   2000       Black      85.2 22.6           0
## 2230 71185  29   Male   Married   3500 MexAmerican      90.9 22.8           0
## 2231 71189  51   Male   Married   9000       White      95.0 25.6           0
## 2232 71197  36   Male   Married   2000       White     138.5 44.7           0
## 2233 71204  27 Female   Married   8200 MexAmerican      89.0 26.4           0
## 2234 71206  29   Male   Married   2500       Asian      78.0 22.2           0
## 2235 71208  32   Male   Married   6200       White      75.1 21.0           0
## 2236 71213  38 Female               NA       White      80.6 20.8           0
## 2237 71215  60   Male    Single     NA       White      77.7 19.2           0
## 2238 71217  28   Male    Single   3500 MexAmerican      93.3 24.9           0
## 2239 71218  33   Male    Single   9000       White     101.1 27.7           0
## 2240 71222  55 Female             6200       White     103.5 29.0           0
## 2241 71231  52   Male Separated    800       Black     100.9 30.2           0
## 2242 71234  47 Female    Single   3500       White      99.6 30.8           0
## 2243 71237  43 Female  Divorced   1500       White     101.2 27.9           0
## 2244 71238  53 Female   Widowed   1500       White      95.3 28.6           0
## 2245 71239  48   Male   Widowed   2000       White      92.6 22.3           0
## 2246 71240  80   Male   Widowed    800       White     107.5 28.8           1
## 2247 71242  48   Male    Single   5400       White      97.4 23.5           0
## 2248 71244  64 Female  Divorced   9000       White      90.9 25.5           0
## 2249 71249  24   Male    Single   1000       Black     116.0 38.7           0
## 2250 71250  39   Male              300       White      96.6 23.6           0
## 2251 71259  23 Female    Single    300       Asian      77.1 20.6           0
## 2252 71267  41 Female   Married   4500       Asian      80.5 23.4           0
## 2253 71271  57   Male   Married   2500 MexAmerican      78.3 18.5           0
## 2254 71272  30   Male   Married   4500       White      80.5 25.6           0
## 2255 71278  69   Male   Married     NA       Black      87.5 22.7           0
## 2256 71279  40   Male   Married   2500       White     100.0 25.1           0
## 2257 71284  64 Female    Single    800       Black     109.2 39.3           0
## 2258 71302  56 Female Separated   1600       Black     102.1 29.1           0
## 2259 71306  52 Female   Married   9000       Asian      90.8 26.4           0
## 2260 71307  58   Male  Divorced   2000       White     112.4 32.9           0
## 2261 71308  69 Female   Married   3500       Asian      81.5 22.9           0
## 2262 71310  67 Female   Widowed   2500       Black     124.2 41.8           0
## 2263 71315  44   Male   Married   2500       White     147.2 40.4           0
## 2264 71316  57   Male   Married   6200       Other      91.6 24.7           0
## 2265 71321  54 Female Separated   8200       Black     101.7 34.5           1
## 2266 71324  35   Male   Married   5400    Hispanic     100.1 29.8           0
## 2267 71328  54 Female  Divorced   3500    Hispanic      81.0 25.8           0
## 2268 71336  45   Male   Married   9000       Asian      79.0 21.0           0
## 2269 71340  36 Female  Divorced   2000       White     112.4 40.8           0
## 2270 71348  56   Male   Married   2500 MexAmerican     114.1 29.9           0
## 2271 71353  76 Female   Widowed   1000       White      99.0 34.1           0
## 2272 71359  41   Male   Married    300    Hispanic     100.0 27.8           0
## 2273 71360  25 Female   Married   1600 MexAmerican      77.5 22.2           0
## 2274 71363  30 Female    Single     NA       Asian      80.8 20.8           0
## 2275 71365  22   Male    Single   1600       Other      91.2 29.7           0
## 2276 71368  35   Male   Married   8200       White      81.5 20.6           0
## 2277 71371  63 Female   Married   3500       Other     113.6 34.1           0
## 2278 71372  37   Male             1000 MexAmerican     115.9 32.5           0
## 2279 71379  60 Female    Single    800       White      96.5 27.7           0
## 2280 71381  48   Male   Married   8200       Asian      92.3 25.0           0
## 2281 71388  42   Male   Married   3500 MexAmerican     127.7 36.7           1
## 2282 71393  27   Male  Divorced   3500       White      86.4 25.7           0
## 2283 71395  30   Male Separated   3500    Hispanic      88.3 23.4           0
## 2284 71413  40   Male             1000    Hispanic      98.6 28.7           0
## 2285 71417  64   Male   Married   2500       Black     129.0 41.2           0
## 2286 71419  37 Female   Married   9000       White      85.0 22.1           0
## 2287 71420  54 Female   Married   1700 MexAmerican      98.0 32.5           0
## 2288 71422  37 Female   Married   8200       White      83.3 23.1           0
## 2289 71428  35   Male   Married   2500       White     145.8 45.3           0
## 2290 71430  65 Female   Widowed   3500       Black      94.2 29.5           1
## 2291 71433  33   Male             2500       Black      89.0 24.5           0
## 2292 71438  70 Female   Married   1700       Black     108.0 34.6           1
## 2293 71450  34 Female   Married   3500       White      75.0 21.2           0
## 2294 71455  70   Male    Single   1000       White      99.0 24.4           0
## 2295 71460  47 Female   Married   9000       Black      89.9 28.3           0
## 2296 71467  48   Male  Divorced   4500       White      92.2 24.9           0
## 2297 71470  80 Female   Married   4500       White     105.0 31.4           0
## 2298 71472  32   Male   Married   1000       Black      75.2 22.7           0
## 2299 71473  38 Female    Single   6200       Black     100.4 29.5           0
## 2300 71474  25   Male    Single    800       Black     127.0 38.0           0
## 2301 71476  49 Female   Married   4500       White     111.0 30.9           0
## 2302 71477  80 Female   Married   1500       Black        NA 21.9           0
## 2303 71478  43   Male             3500 MexAmerican     103.3 29.3           0
## 2304 71483  80 Female   Married   3500       White      88.5 26.6           0
## 2305 71497  71 Female  Divorced    800       White     107.2 29.3           1
## 2306 71509  60 Female   Widowed     NA       Asian      82.2 23.4           0
## 2307 71511  64   Male   Married     NA       Asian     105.1 27.5           1
## 2308 71522  63 Female   Married   2000       White     109.5 32.8           0
## 2309 71527  54 Female  Divorced   1600       White     114.0 37.1           1
## 2310 71528  30 Female    Single   9000       Black      80.2 22.6           0
## 2311 71529  33   Male   Married   6200       Black      92.1 27.6           0
## 2312 71531  35   Male    Single    800       White      79.8 22.4           0
## 2313 71533  38 Female  Divorced    300       Black        NA   NA           0
## 2314 71536  44 Female  Divorced   1000       White      92.4 24.2           0
## 2315 71542  67 Female   Married   9000       White     125.0 33.7           0
## 2316 71559  51 Female    Single    800    Hispanic     101.1 28.9           0
## 2317 71561  40 Female   Married   9000       Asian      83.5 23.0           0
## 2318 71571  60   Male   Married   8200       Black     130.2 39.8           1
## 2319 71578  41   Male   Married   4500       White      95.6 30.6           0
## 2320 71580  50 Female   Married   4500    Hispanic      91.6 27.0           0
## 2321 71582  29   Male             1600 MexAmerican      99.7 32.4           0
## 2322 71584  58 Female   Married   9000       Black     104.0 35.9           0
## 2323 71593  45   Male   Widowed   3500       Black        NA   NA           0
## 2324 71605  38 Female             2000       White      86.2 26.4           0
## 2325 71620  65   Male   Married     NA       Asian      83.1 20.9           1
## 2326 71633  64 Female   Married   1000       Asian      87.3 23.4           0
## 2327 71634  21 Female    Single   2000       Other      80.7 21.6           1
## 2328 71640  51 Female   Married   8200       Black      98.3 31.0           0
## 2329 71644  80 Female   Married   3500       White        NA 22.5           0
## 2330 71656  58   Male   Married   9000       White      96.5 23.8           0
## 2331 71657  49 Female   Married   4500    Hispanic      90.0 29.4           0
## 2332 71658  25   Male              300 MexAmerican     108.4 32.0           0
## 2333 71660  35 Female Separated   1600       White     112.5 36.4           0
## 2334 71666  61   Male              300       Black      86.5 22.3           0
## 2335 71675  73 Female   Married   3500       White      96.7 28.3           0
## 2336 71676  80   Male   Married   4500       White     106.2 27.0           0
## 2337 71691  76 Female   Married   6200       White     107.4 30.1           0
## 2338 71697  74   Male   Married   1600       White      99.6 28.6           0
## 2339 71698  46 Female   Married   8200       White      91.2 24.3           0
## 2340 71702  70 Female   Widowed     NA       Black      94.2 26.0           1
## 2341 71704  77   Male   Married   1600       White     105.4 28.1           0
## 2342 71705  67   Male   Married   1000 MexAmerican     125.5 38.5           0
## 2343 71706  30 Female Separated    800       White      77.0 23.9           0
## 2344 71709  45 Female   Married   1000       White     111.4 33.0           1
## 2345 71710  68   Male   Married   9000       Black      94.5 23.5           0
## 2346 71722  48 Female Separated   1000       Black     114.7 38.8           0
## 2347 71724  54   Male  Divorced   1000    Hispanic      97.0 26.8           0
## 2348 71730  40 Female  Divorced     NA    Hispanic      87.1 25.4           0
## 2349 71739  80   Male   Married   1600       White      91.5 25.9           1
## 2350 71740  20 Female    Single   1000       Black      71.4 20.4           0
## 2351 71745  21 Female    Single   9000       White      84.1 27.8           0
## 2352 71748  36 Female              300 MexAmerican     101.4 31.2           0
## 2353 71750  80 Female   Widowed   1600       White      72.3 20.8           0
## 2354 71751  42 Female   Married   8200       White      74.5 20.1           0
## 2355 71756  63   Male   Married   5400       White      97.6 23.7           0
## 2356 71757  23   Male    Single   4500       Asian      86.3 22.0           0
## 2357 71758  24 Female             2500    Hispanic      91.4 26.4           0
## 2358 71763  40   Male   Married   8200       White      89.4 20.9           0
## 2359 71767  38   Male  Divorced   4500 MexAmerican      94.5 26.6           0
## 2360 71769  24   Male    Single   4500    Hispanic      78.4 21.3           0
## 2361 71777  77 Female   Married   2000       Black      91.7 24.8           1
## 2362 71778  20   Male    Single   1000    Hispanic      74.0 23.8           0
## 2363 71781  52 Female    Single   1700       Black     120.5 42.6           0
## 2364 71784  24 Female   Married   2500       White      70.2 19.3           0
## 2365 71785  64   Male  Divorced     NA       Black     102.1 28.4           0
## 2366 71787  50 Female    Single   1500       Black     142.6 48.0           1
## 2367 71789  50 Female   Married   9000       Other      93.3 32.1           0
## 2368 71799  59   Male    Single    300       White        NA 22.5           0
## 2369 71802  53   Male             1000       White     117.7 31.3           1
## 2370 71803  52 Female  Divorced   1600       Black     107.2 34.8           0
## 2371 71810  33   Male   Married   1600    Hispanic      97.8 30.0           0
## 2372 71813  36   Male   Married   9000       Asian     104.0 31.5           0
## 2373 71825  53 Female   Married   6200       White      91.0 22.7           0
## 2374 71826  77 Female   Widowed    300       White     110.2 32.4           1
## 2375 71828  49 Female   Married   3500 MexAmerican     115.5 37.5           0
## 2376 71829  57   Male Separated    800 MexAmerican      87.3 22.9           0
## 2377 71830  34 Female             1000 MexAmerican     109.0 36.5           0
## 2378 71832  49 Female  Divorced   2000 MexAmerican      91.2 28.3           0
## 2379 71836  65   Male   Married   9000       Black     116.3 32.4           0
## 2380 71839  57 Female    Single   2500       White     142.7 42.4           0
## 2381 71841  45   Male   Married   8200    Hispanic     112.1 33.3           0
## 2382 71849  56 Female Separated   1000    Hispanic      91.2 32.1           0
## 2383 71856  32 Female   Married   6200       Asian      69.5 18.6           0
## 2384 71863  38   Male   Married   9000       White     117.8 36.0           0
## 2385 71866  32   Male  Divorced     NA MexAmerican      89.3 27.3           0
## 2386 71867  26 Female    Single   6200       Asian      72.0 18.3           0
## 2387 71868  43   Male   Married   5400 MexAmerican      96.4 28.4           0
## 2388 71869  69   Male   Married   4500       White     131.4 37.8           0
## 2389 71874  24   Male    Single   1600       Asian      80.1 23.6           0
## 2390 71877  72   Male   Married     NA    Hispanic     101.6 25.4           1
## 2391 71885  35   Male             1600 MexAmerican      92.6 25.1           0
## 2392 71886  61   Male    Single   2500       Black      98.2 26.8           0
## 2393 71887  68 Female   Married   1600    Hispanic      95.8 28.9           0
## 2394 71891  54 Female   Married   5400 MexAmerican      96.0 28.4           0
## 2395 71895  31   Male   Married   2500       Asian      74.0 20.6           0
## 2396 71898  65 Female   Married   5400 MexAmerican      98.5 29.4           0
## 2397 71901  48 Female   Married   1000       Other        NA 59.7           0
## 2398 71904  30 Female    Single   2000       Asian        NA 18.0           0
## 2399 71909  28   Male    Single    800 MexAmerican     100.8 29.4           0
## 2400 71911  27   Male   Married   8200 MexAmerican     106.6 31.3           0
## 2401 71915  60   Male    Single   6200       White     106.6 27.5           0
##      UrAlbCr UricAcid BloodGlucose HDL Triglycerides MetabolicSyndrome
## 1       3.88      4.9           92  41            84                 0
## 2       8.55      4.5           82  28            56                 0
## 3       5.07      5.4          107  43            78                 0
## 4       5.22      5.0          104  73           141                 0
## 5       8.13      5.0           95  43           126                 0
## 6       9.79      4.8          105  47           100                 0
## 7       9.21      5.4           87  61            40                 0
## 8       8.78      6.7           83  48            91                 0
## 9      45.67      5.4           96  35            75                 0
## 10      2.21      6.7           94  46            86                 0
## 11      4.16      6.0          100  35            98                 1
## 12     62.14      6.7           94  58           182                 0
## 13      7.24      8.8          101  40           129                 1
## 14      5.53      4.5           91  46            62                 0
## 15      2.33      3.6          138  31           565                 1
## 16     21.43      4.8           90  54            44                 0
## 17      8.38      3.9          161  52            79                 1
## 18    187.41      4.2          178  46           107                 1
## 19     16.63      5.6          102  36           162                 1
## 20      7.39      4.5           84  56           121                 0
## 21      6.94      4.2          111  37           105                 0
## 22      4.71      6.5          204  33           192                 1
## 23      4.84      5.7           99  59           122                 0
## 24      2.34      5.3          102  39           135                 1
## 25      5.33      4.1           90  42            68                 0
## 26     31.46      6.3          106  30           326                 1
## 27      5.89      5.0          101  50            98                 0
## 28     25.97      6.4          130  55           138                 1
## 29    120.73      4.1          258  39           223                 1
## 30    172.13      6.7           92  56            91                 0
## 31      5.44      4.6           97  48           118                 0
## 32     13.41      4.2           84  72            75                 0
## 33      6.72      3.2           91  85            88                 0
## 34      9.39      7.5          108  29           194                 1
## 35      6.09      4.9           95  53            63                 0
## 36      5.57      4.6          103  43            54                 0
## 37    821.71      9.3          125  40           286                 1
## 38     10.39      7.0           94  57           177                 0
## 39     58.06      5.1          223  51            93                 1
## 40      3.65      5.3           85  38            89                 0
## 41     20.97      5.6           98  59           146                 0
## 42      6.67      4.9          105  52           125                 0
## 43      8.83      8.0          112  43           178                 1
## 44      3.50      6.6           96  49           126                 0
## 45      3.60      4.9           96  49            88                 0
## 46      7.82      4.2           95  57           117                 0
## 47      4.36      5.1          117  44           121                 1
## 48     10.52      5.8          222  39            68                 1
## 49      3.41      4.8           82  44           128                 0
## 50      5.24      4.8           89  45           192                 1
## 51   3267.57      4.7          135  44            75                 0
## 52     10.63      7.9          107  41           190                 0
## 53      5.24      4.1           99  52            82                 0
## 54     10.00      4.7          121  50           108                 1
## 55     14.76      8.6           80  33            76                 1
## 56      4.17      6.2          103  44           344                 1
## 57      4.03      4.8          112  47           155                 1
## 58     10.67      3.4           98  54            67                 0
## 59      1.73      6.3           94  45            86                 0
## 60      7.09      4.8          144  45           148                 1
## 61      3.11      5.1          136  60           174                 1
## 62      2.84      9.5          107  45           163                 0
## 63    195.65      5.7           73  72           105                 0
## 64     12.63      5.3           96  34           109                 1
## 65      8.73      9.3           70  63           169                 1
## 66    319.15      7.6          112  37           212                 1
## 67      6.70      6.0          105  65            65                 1
## 68      2.11      7.2           94  61            98                 0
## 69      3.89      6.0           94  43           109                 0
## 70     21.41      7.5           97  39            95                 0
## 71      5.29      4.8           81  54            53                 0
## 72      2.41      5.1           89  45           125                 0
## 73      7.82      4.2          103  71            65                 0
## 74      5.20      6.8           95  51           122                 0
## 75      7.89      4.4           99  37           134                 0
## 76      2.34      6.3           96  68            96                 0
## 77      8.72      2.6           95  51            62                 0
## 78     30.21     11.2          134  53           167                 1
## 79      2.65      6.0           84  51            61                 0
## 80      4.87      4.5           98  44            90                 0
## 81      9.00      5.7          119  32           154                 1
## 82      4.83      6.2          110  50           169                 1
## 83      5.52      3.5           88  46            40                 0
## 84      7.23      4.5           85  47           122                 0
## 85     22.86      5.2          109  47           174                 1
## 86      2.75      5.3          101  44           184                 0
## 87      3.42      7.7           93  42           218                 0
## 88      9.21      4.5          100  51            71                 0
## 89      3.16      7.2          101  62           111                 0
## 90      5.33      5.0           92  43           134                 0
## 91     10.77      7.7          108  53           149                 1
## 92     12.76      5.4           84  48            63                 0
## 93      4.43      6.4          128  56           128                 0
## 94      5.07      6.5          124  93            95                 1
## 95      6.91      6.0           89  39            78                 0
## 96      4.18      5.0           97  49           112                 0
## 97      9.04      7.4          128  54            62                 0
## 98      3.29      5.7          101  43           207                 0
## 99     10.85      5.0          106  48            55                 1
## 100    56.22      5.9          116  65            58                 1
## 101    18.69      4.7           97  49           153                 0
## 102    15.49      6.5          100  53            57                 1
## 103     6.29      3.8          105  44           129                 0
## 104     3.23      5.4           95  70            60                 0
## 105     4.07      5.5           92  40           120                 1
## 106    13.83      4.8           86  57            80                 0
## 107     6.13      5.4           85  68            72                 0
## 108    68.26      6.7           75  45           125                 0
## 109     2.35      3.1           93  53            83                 0
## 110    50.42      4.7           88  59           130                 0
## 111     4.40      5.0          126  61            71                 0
## 112    14.90      5.1          103  53           151                 1
## 113     7.67      7.1          103  53            95                 0
## 114    11.48      6.7           94  41            89                 0
## 115     2.47      6.2           95  71           118                 0
## 116     5.57      3.5          147  48            79                 1
## 117    15.76      4.7          113  55            36                 0
## 118    69.46      4.9          107  57           124                 0
## 119     4.73      7.2          122  30           199                 1
## 120     9.77      6.1          109  51           218                 1
## 121     5.50      6.1          118  44           283                 1
## 122     4.45      5.2          101  41           354                 1
## 123     4.84      5.5           93  45           289                 0
## 124     9.41      7.3          104  64            66                 0
## 125     8.08      7.3          158  29           589                 1
## 126     4.88      3.2           98  77            64                 0
## 127     8.63      3.2           92  48            46                 0
## 128    15.29      5.4          118  50            77                 0
## 129    10.00      4.2          103  33           260                 1
## 130     4.40      4.4           91  54            80                 0
## 131     6.54      6.1          122  41            94                 1
## 132     2.68      5.1           90  57            42                 0
## 133     3.52      4.4           90  63            68                 0
## 134     1.97      6.7           99  46            49                 0
## 135     4.85      3.4          105  64           115                 0
## 136     6.02      4.9          100  62           132                 0
## 137    11.22      5.8          107  47           112                 0
## 138     5.94      4.3           98  73            34                 0
## 139     5.07      5.9           84  46           141                 0
## 140     5.81      5.5          107  48            75                 0
## 141  3284.62      7.8          132  65           130                 1
## 142    10.75      5.0          102  61           129                 1
## 143     4.67      6.0           88  44            69                 0
## 144     4.85      3.9           97  68            68                 0
## 145    38.45      6.6           87  35           270                 0
## 146     4.93      5.6           87  44            81                 0
## 147     3.92      2.8           88  61            43                 0
## 148   173.75      3.9           96  49           157                 1
## 149     4.20      5.1           98  34           668                 1
## 150     2.72      4.4           97  46            96                 0
## 151     4.60      7.9          101  80            81                 0
## 152     9.59      4.6          101  52           109                 1
## 153     7.88      4.2           85  66            54                 0
## 154    97.01      3.3           91  80            98                 0
## 155   106.95      5.9           82  30            49                 0
## 156     6.14      4.1           96  52            86                 0
## 157     9.46      8.5           99  92            45                 0
## 158     7.92      3.8           94  54            49                 0
## 159     7.50      4.7           99  49           117                 0
## 160     3.23      6.6           97  67            91                 0
## 161     6.40      7.3          111  50            89                 0
## 162     7.67      4.5          123  59           111                 0
## 163   114.55      5.0          109  67           105                 0
## 164     6.30      6.9           98  62            76                 0
## 165     4.19      5.8          107  73            88                 0
## 166    13.72      5.2          223  46            48                 0
## 167     5.87      4.2           86  71            60                 0
## 168     6.22      5.2          102  46            75                 1
## 169     4.04      7.1          105  38           336                 1
## 170    20.69      5.6          107  49            61                 1
## 171    88.80      7.4           82  53           138                 0
## 172     3.49      6.2           99  48            83                 0
## 173    21.22      6.2           99  57            65                 0
## 174     9.80      5.2           92  50            62                 0
## 175    33.47      4.5          157  76            61                 0
## 176     8.67      6.7          104  48           351                 1
## 177     7.13      7.1          112  58           367                 1
## 178    13.75      5.9          102  30           384                 1
## 179     3.96      9.1          118  43           214                 1
## 180    12.71      5.1          107  75            93                 1
## 181    25.31      5.7           93  65            91                 0
## 182     4.63      7.0          103  47            93                 0
## 183     6.17      4.7          103  53            81                 0
## 184   244.57      4.8           99  38           275                 1
## 185    24.69      3.1           88  69            50                 0
## 186     6.67      5.4          115  56           181                 1
## 187     4.14      4.4           89  44           202                 0
## 188    15.47      5.3           87  49           128                 0
## 189     5.84      3.2           78  72            56                 0
## 190     4.62      7.5           86  43           121                 0
## 191    22.99      6.9          251  46           127                 1
## 192    97.65      6.9          104  48           135                 0
## 193     3.26      5.2          102  58            75                 0
## 194     1.76      3.7           81  70            52                 0
## 195     6.96      5.4          140  48           140                 1
## 196    22.91      5.5           83 119            46                 0
## 197     3.44      5.0          180  47           107                 0
## 198    11.10      5.4           82  43           123                 0
## 199    17.00      3.4           92  77            67                 0
## 200    31.03      5.3          103  49           158                 1
## 201     7.37      6.8          117  50            86                 0
## 202     7.54      5.3           90  52           119                 0
## 203     9.11      6.0          104  40            85                 1
## 204    10.12      4.8          237  62           262                 1
## 205    10.59      6.2           90  33           205                 1
## 206     8.10      4.3           94  83           107                 0
## 207    16.51      3.8          180  56           104                 0
## 208     3.81      6.9          108  51            99                 1
## 209     5.56      5.3           97  62            92                 0
## 210     9.29      5.5          107  52            89                 0
## 211    14.92      5.2           85  47            35                 0
## 212     2.37      7.8           88  40            89                 0
## 213  1777.05      7.2          104  37           111                 1
## 214    10.86      3.2          107  62            90                 0
## 215     5.47      5.2           90  65            97                 0
## 216    28.00      4.2          100  47            93                 0
## 217     3.21      5.7           90  38            78                 0
## 218     5.38      5.7           97  40           121                 0
## 219     6.50      4.0           94  56            62                 0
## 220     3.61      6.0           85  43            65                 0
## 221    37.26      7.1          105 150            74                 0
## 222     3.93      5.5          105  60            57                 0
## 223    31.62      4.5          104  42            78                 0
## 224     4.11      5.8           91  53            82                 0
## 225    40.59      6.8          105  54           192                 1
## 226     3.98      8.4          105  38           117                 0
## 227     5.05      6.1           97  61           147                 0
## 228     8.11      5.4          149  54           101                 1
## 229     3.32      5.6          107  38           194                 1
## 230    11.45      6.5           95  50            92                 0
## 231     5.89      3.5          101  63            82                 0
## 232     2.07      5.6           96  54           323                 0
## 233     4.53      7.2          107  45            80                 1
## 234    16.05      4.6           69  88            79                 0
## 235    12.81      8.0          101  41           323                 1
## 236     3.42      4.9           85  47           117                 0
## 237    49.32      5.2          144  51           258                 1
## 238     4.70      4.7          102  49           169                 1
## 239     9.91      5.7           93  49           191                 0
## 240     4.21      7.4           96  45           302                 0
## 241     9.23      5.8          100  41            86                 0
## 242     5.89      5.2          187  45            97                 0
## 243    24.44      7.1           83  36            98                 0
## 244     5.39      4.0           96  63            74                 0
## 245     5.76      4.9           96  42            88                 0
## 246    12.92      6.5          111  30           263                 1
## 247  2750.00      5.7          127  80            92                 0
## 248     4.55      5.6           86  46            98                 0
## 249    10.00      4.2          105  90            94                 0
## 250     6.27      4.4          105  89           138                 1
## 251     6.79     11.3           96  37           163                 1
## 252     3.00      7.2          100  38           126                 0
## 253     8.64      3.8          102  65           103                 0
## 254     2.22      4.7          107  44           169                 0
## 255     4.50      5.8           96  41           131                 0
## 256     8.90      3.4          113  55            94                 0
## 257   169.26      8.0          130  52           108                 0
## 258     3.23      3.1          103  69            55                 0
## 259     6.54      5.1           97  45           179                 1
## 260     4.05      5.4          104  41           129                 0
## 261    47.53      6.7          217  35           419                 1
## 262     8.67      4.8           83  55            94                 0
## 263     2.03      7.6           97  48           102                 0
## 264    18.47      3.3          140  53           198                 1
## 265     4.48      5.3          103  49           103                 0
## 266     4.68      6.4          108  51           126                 0
## 267     5.00      5.1          102  54            90                 0
## 268     9.50      5.9           86  43            68                 0
## 269     2.43      6.3           90  49            69                 0
## 270     4.70      4.4           84  53           116                 0
## 271     3.82      6.9          124  47           152                 0
## 272     8.45      2.8          268  39           174                 1
## 273     6.89      3.8           93  52           105                 0
## 274   355.56      6.0          116  43           115                 1
## 275    11.50      3.5          105  72            89                 0
## 276     6.33      5.8          158  47           147                 1
## 277    11.11      3.6           93  90            92                 0
## 278     4.18      7.3          131  40           142                 1
## 279    24.16      4.2           96  88            76                 0
## 280     2.58      8.1          110  34           187                 1
## 281    14.41      6.3          116  42           174                 1
## 282     6.80      5.5          108  41           105                 0
## 283    34.20      6.7           99  54            97                 0
## 284   535.85      7.8          244  53           126                 1
## 285     3.13      7.9           96  49            78                 0
## 286     7.50      2.7           97  85            72                 0
## 287     6.43      3.8          121  51            71                 0
## 288     5.95      6.0           88  74            73                 0
## 289     7.34      4.6           96  64            69                 0
## 290     6.36      7.1           89  61           151                 0
## 291     2.86      6.3          102  49            79                 0
## 292     1.98      4.7           90  44            75                 0
## 293    45.83      4.5          105  60           118                 0
## 294     6.88      4.0           87  67            29                 0
## 295     7.36      6.0           86  75           167                 0
## 296     6.81      6.2          111  32           163                 1
## 297    15.64      5.1           86  62            97                 0
## 298    52.09      6.2           89  66            40                 0
## 299    11.24      5.1          192  21           265                 1
## 300     1.74      4.4           85  49            37                 0
## 301     4.68      5.4           92  39           118                 0
## 302     5.87      6.0          101  43           175                 1
## 303     5.85      4.3           91  39           139                 1
## 304     5.15      4.0           96  52           137                 0
## 305     4.38      5.1           90 100            61                 0
## 306    46.53      5.0          204  43            93                 0
## 307     2.64      5.4           95  44           229                 1
## 308    18.72      5.8           96  52           173                 0
## 309    13.54      6.9           99  46            96                 0
## 310    11.84      4.8           95  56            89                 0
## 311     3.60      3.9          101  49            80                 1
## 312     3.98      4.8           91  48           140                 0
## 313  2238.10      7.1          291  34           248                 1
## 314     3.16      6.7           90  41            79                 0
## 315     5.56      3.4          102  87            77                 1
## 316    15.22      6.1           86  56            41                 0
## 317     9.30      4.3          103  83            74                 0
## 318     8.99      5.4          100  55           103                 1
## 319    44.29      6.4           90  70            62                 0
## 320    17.99      3.7          115  59            76                 1
## 321   684.00      5.9           91  82            64                 0
## 322   589.61      6.5           85  49           151                 0
## 323     5.92      5.4          102  51           128                 0
## 324   141.62      7.4           93  97            63                 0
## 325  2403.85      6.6          100  53           166                 1
## 326    30.53      5.5           89  42           105                 0
## 327     5.00      4.3          109  69            65                 0
## 328     4.17      6.2          111  65            82                 0
## 329     4.77      3.9           90  52            81                 0
## 330    53.20      6.8          160  54            81                 0
## 331     1.87      4.5          278  42           192                 1
## 332     3.56      3.4           85  65            70                 0
## 333     5.43      4.2           95  51           127                 0
## 334     5.51      7.1          105  37           156                 1
## 335     3.02      6.8           96  41           168                 0
## 336    22.52      7.0          228  47           410                 1
## 337     7.31      2.8          270  23           179                 1
## 338    47.04      4.3          112  51            97                 0
## 339     3.88      5.8          120  47           143                 1
## 340    27.27      5.8          104  62           119                 0
## 341     8.75      3.1           89  62           168                 0
## 342    20.00      5.7           96  42            41                 0
## 343     2.00      5.2           98  69            60                 0
## 344     4.00      7.5           96  47            94                 1
## 345     6.41      4.0          312  50            57                 0
## 346     8.62      8.7           91  42            53                 0
## 347    58.00      3.9          254  37            91                 1
## 348     2.08      4.2          102  60           118                 0
## 349    45.08      5.1           85  51            95                 0
## 350    22.68      5.5           94  61            75                 0
## 351     6.18      5.4          116  63            91                 1
## 352     8.34      5.8           94  51           123                 0
## 353     2.99      5.3          100  33           354                 1
## 354     5.53      8.8           96  38           175                 1
## 355     5.18      4.9           85  46            78                 0
## 356    13.91      5.5          175  40           109                 1
## 357   814.58      5.8          116  53           188                 1
## 358     4.41      4.4          102  59            66                 0
## 359     8.53      4.5           77  51            97                 0
## 360     7.74      3.6           89  58            53                 0
## 361     2.45      5.2          104  34           347                 1
## 362   195.65      4.7          181  70            69                 0
## 363    36.27      7.5          190  50           118                 0
## 364    12.08      6.0           92  51            98                 0
## 365    12.81      4.6          275  60           236                 1
## 366     5.75      7.0           87  42            99                 0
## 367     2.87      6.4          107  41           105                 0
## 368     3.66      5.2           96  43            69                 0
## 369     5.38      7.2          107  42           117                 1
## 370     4.35      4.7           97  69            93                 0
## 371   134.36      3.9           95  62            44                 0
## 372     4.00      4.7           90  70            42                 0
## 373   920.35      6.5          117  58            78                 0
## 374   250.00      4.8          317  37            70                 1
## 375   109.43      7.4          225  36           131                 0
## 376    33.88      3.4           81  33            93                 0
## 377     9.25      6.6           97  50           154                 0
## 378     4.97      6.6           96  56            81                 0
## 379     5.74      5.5           99  38            94                 0
## 380     5.61      7.2           99  42            98                 0
## 381     5.71      3.7          103  51           173                 1
## 382     8.43      6.1           99  46            95                 0
## 383    10.53      3.1           98  72            54                 0
## 384    26.05      4.9          304  58           205                 1
## 385   381.25      7.1          111  51           172                 1
## 386     2.81      8.3           89  42            64                 0
## 387    10.31      5.8          103  69            91                 1
## 388    12.42      5.3          108  58            80                 1
## 389     8.23      3.1           97  50           124                 0
## 390     9.14      4.3          102  58           140                 0
## 391     7.27      3.2           97  51           138                 0
## 392     2.76      3.8           86  52            56                 0
## 393     2.47      6.4           94  37            26                 0
## 394     7.78      3.6           97  59            61                 0
## 395    81.20      5.3           71  43            68                 0
## 396    20.63      7.0           90  34           287                 1
## 397    93.53      3.3          112  57            71                 1
## 398     8.70      5.0          115  50            58                 0
## 399     5.32      4.1          106  51            79                 0
## 400    30.91      8.4          151  41           190                 1
## 401    14.43      4.5          344  46           268                 0
## 402    22.11      6.3          116  39           129                 1
## 403    26.83      4.9          320  49            77                 1
## 404     3.49      5.6           99 106            89                 0
## 405    10.09      4.8           88  66            41                 0
## 406    11.66      3.4           83  82            32                 0
## 407     8.49      5.6          109  36           124                 0
## 408     6.43      6.7          107  42           133                 0
## 409     4.69      5.8           96  44           120                 0
## 410     5.56      4.3           89  48            65                 0
## 411     5.63      3.5          171  66            69                 0
## 412    36.82      9.4          107  31            99                 0
## 413    63.22      5.4           97  34           208                 0
## 414     3.01      7.1          108  43           182                 1
## 415     6.26      3.8           92  44           154                 1
## 416    10.61      3.8          105  44           177                 1
## 417     5.11      3.9           92  59            60                 0
## 418     5.14      4.9          111  45            53                 0
## 419  1817.31      6.7           99  64            93                 0
## 420     9.14      4.8          103  52            52                 0
## 421     9.12      6.2          129  36           158                 1
## 422    48.42      5.3          156  59            46                 0
## 423     3.78      5.7          101  57           109                 0
## 424     4.95      5.0           87  61           167                 0
## 425     7.64      5.7          105  87            64                 0
## 426     6.67      4.5           86  60            75                 0
## 427     6.22      5.8          102  40           256                 1
## 428     8.43      8.4          109  45           184                 1
## 429    13.49      5.2          111  53           195                 1
## 430     2.42      5.2          100  44           119                 0
## 431    36.36      7.7          137  43            92                 1
## 432     5.38      6.7           76  31           134                 0
## 433    35.24      4.3           94  71            60                 0
## 434    52.86      3.4           85  67            65                 0
## 435     6.31      3.4           71  52           130                 0
## 436     4.72      7.3           89  48           110                 0
## 437     3.64      5.2          118  61            80                 0
## 438     3.22      4.1           96  57            80                 0
## 439    51.35      3.8           85  72            30                 0
## 440   338.54      6.3          153  46           102                 0
## 441    11.38      4.7          243  44           371                 1
## 442    60.19      3.7           95  49            45                 1
## 443     4.31      6.1          108  56            45                 0
## 444     4.10      5.2          129  60           119                 1
## 445     6.75      5.9          171  35           254                 1
## 446    10.21      5.7          308  34           103                 1
## 447     7.42      3.9           91  84            76                 0
## 448    32.12      4.8           95  32           206                 1
## 449     5.13      4.0           86  51           176                 0
## 450     3.40      5.5          129  41           151                 1
## 451     6.97      5.7          110  62            81                 0
## 452    18.82      3.7           90  51            90                 0
## 453     6.53      4.1           94  72            74                 0
## 454     6.52      8.7          105  32           150                 1
## 455     9.63      5.4           91  46           122                 0
## 456     2.95      5.9           99  37           335                 1
## 457     5.64      5.3           98  82            83                 0
## 458    25.25      6.1          101  36           224                 1
## 459     6.58      5.0          149  47           170                 1
## 460     6.63      2.1           89  32           336                 1
## 461     1.58      6.5          108  42            64                 0
## 462     9.83      5.0          100  51            88                 1
## 463     5.44      5.2           90  72            69                 0
## 464     6.27      3.3           79  51            54                 0
## 465     4.32      4.1          103  35           246                 1
## 466     4.81      6.4           94  38           222                 0
## 467     3.23      6.7           94  52            91                 0
## 468     5.66      2.4          102  58            89                 0
## 469     3.18      3.7           80  61            99                 0
## 470    33.50      8.6          162  36           241                 1
## 471     5.61      4.2           95  54            64                 0
## 472     7.17      4.2           84  63            68                 0
## 473     1.70      5.6          101  47            84                 0
## 474     6.97      6.9          160  54            84                 1
## 475     5.00      4.5          108  44           148                 1
## 476     3.44      4.7           88  72            58                 0
## 477     3.44      7.7           80  58            74                 0
## 478     5.75      8.1          108  49           123                 0
## 479     4.70      6.2           94  37           123                 0
## 480   806.58      7.2          106  71           144                 0
## 481    62.50      7.8          110  49           142                 1
## 482     6.58      5.5           94  44           125                 0
## 483     5.92      8.4           92  36           197                 0
## 484   689.47      6.2           88  36           197                 1
## 485    10.72      5.1           91  52            65                 0
## 486    44.24      7.5          118  54           241                 1
## 487     4.53      4.9          101  54           152                 1
## 488     4.58      4.6          103  55            70                 1
## 489    17.53      6.8          109  58            86                 0
## 490     8.23      4.1          105  53           119                 0
## 491    30.60      2.7          107  53           135                 1
## 492    11.60      4.0          101  74            87                 0
## 493     5.06      4.5          108  77            46                 1
## 494     2.88      5.2           91  47           148                 0
## 495     3.49      4.6          106  42            78                 1
## 496    33.16      5.6          137  55           187                 1
## 497     4.37      8.1          107  33           111                 1
## 498    13.83      7.3          174  40           121                 1
## 499     3.12      9.1          103  33            83                 0
## 500   572.46      6.2          111  39           130                 1
## 501    10.26      5.0           82  59           141                 0
## 502     4.94      3.6           91  45            67                 0
## 503     3.73      2.8           81  52            75                 0
## 504    15.18      7.0          103  68            97                 0
## 505     5.89      3.4          108  95            64                 0
## 506     5.71      7.1           97  57            90                 0
## 507    85.22      4.2          109  52            85                 0
## 508    13.49      6.4          109  71            55                 1
## 509    10.18      7.0           88  41           233                 0
## 510    11.40      5.0          249  42           309                 1
## 511    16.25      3.9           87  65            75                 0
## 512     4.92      5.3          165  31           333                 1
## 513     3.23      3.4           81  79            77                 0
## 514     5.99      4.1          111  49            87                 1
## 515     3.93      5.7          100  30           624                 1
## 516    11.78      4.1          112  64            54                 0
## 517     5.00      6.6          117  46            84                 1
## 518     5.26      4.5           97  68            49                 0
## 519    28.32      7.2          106  44           104                 0
## 520     5.25      7.5           97  47           139                 0
## 521    29.52      4.8          258  40           373                 1
## 522    11.96      6.1          253  47           112                 0
## 523    14.38      8.8           91  47            66                 0
## 524    75.22      4.7          109  36           144                 1
## 525     4.89      3.2           92  67            50                 0
## 526    11.06      6.8          101  42           114                 0
## 527    16.29      5.1          101  73            65                 0
## 528    13.49      3.6           93  70           149                 0
## 529     3.52      4.3          104  42           115                 0
## 530     3.92      3.5           99  62           111                 0
## 531     4.66      5.2          100  45            65                 0
## 532    60.70      6.2           91  54           172                 0
## 533     6.19      6.0          102  43           127                 1
## 534     8.75      3.8           78  66            97                 0
## 535    15.38      6.1          110  58            46                 1
## 536     4.86      7.0           91  65           100                 0
## 537    24.20      3.7           86  71            35                 0
## 538    11.63      4.2          110  44           146                 1
## 539     5.26      6.4           96  44           166                 0
## 540     8.41      5.5           96  57           124                 0
## 541     4.15      6.2          111  51           122                 1
## 542    47.79      5.8           93  63            45                 0
## 543    22.18      5.2           95  62            62                 0
## 544    21.78      5.3          101  48            46                 1
## 545     2.05      3.8          102  59           174                 0
## 546     5.89      2.9           94  43           130                 0
## 547     5.81      6.8           88  42            78                 0
## 548     5.12      5.0          100  45           174                 1
## 549     2.48      5.3          104  50            81                 0
## 550     6.27      3.6           90  62            37                 0
## 551    46.87      4.2          111  83            73                 0
## 552     5.00      6.6           96  44           136                 0
## 553    18.91      5.3          269  40            65                 1
## 554     4.58      4.2           97  55            90                 0
## 555     3.59      4.5           99  37            91                 0
## 556     3.43      3.5           85  78            75                 0
## 557    43.33      5.6           86  60            72                 0
## 558     3.98      5.5           92  59            94                 0
## 559     1.92      5.7           94  37           197                 1
## 560     8.15      3.2           98  45           120                 1
## 561     1.46      4.2           88  64            43                 0
## 562     5.81      3.1           86  47            76                 1
## 563     4.84      5.4          103  77            91                 0
## 564    13.18      7.0           95  46            92                 0
## 565     7.64      4.9           96  55            58                 0
## 566     4.69      6.5          125  52           162                 1
## 567     2.50      6.5           96  57            64                 0
## 568     6.28      4.9          104  47            74                 0
## 569     9.17      4.8           91  54           158                 0
## 570     4.30      6.1           88  48            55                 0
## 571     8.49      7.6          101  41           363                 0
## 572     2.86      6.0           91  54           158                 0
## 573     3.73      4.3           94  41           168                 0
## 574     4.44      7.6          104  21           485                 1
## 575    32.36      7.3          166  49            78                 1
## 576    19.90      5.5           98  65            80                 0
## 577     9.63      3.8           90  78            54                 0
## 578     4.45      8.0          113  57            67                 0
## 579     9.77      4.7           95  56           117                 0
## 580     3.25      4.6          155  51            75                 0
## 581     8.59      3.1           90  54            90                 0
## 582     2.69      3.9          114  34           146                 1
## 583    13.81      5.0           94  65            58                 0
## 584     7.55      3.0          117  36            44                 1
## 585     6.26      6.9          115  51           284                 1
## 586     6.98      2.6           93  77            69                 0
## 587    18.42      3.8          285  39           454                 1
## 588     3.67      3.0           96  87            62                 0
## 589    10.80      5.8           86  64            83                 0
## 590     4.36      5.7          101  42           119                 0
## 591     4.03      3.1           92  57           100                 0
## 592    10.68      3.8          112  40           176                 1
## 593     2.60      4.6           95  56            61                 0
## 594    36.90      5.3          127  51           136                 1
## 595     4.79      5.7          104  52           105                 0
## 596     4.02      4.0           75  50           138                 0
## 597     6.04      4.4           99  43            58                 0
## 598    10.91      9.7          203  36           190                 1
## 599     6.25      6.4          104  40           170                 1
## 600     3.41      7.3           99  63            85                 0
## 601     8.18      7.5          110  48            59                 0
## 602     7.11      4.6          104  36           141                 1
## 603     5.96      6.2          111  43           101                 0
## 604     4.62      4.4           93  54           240                 0
## 605     6.40      3.7           88  67            80                 0
## 606     9.70      2.9          163  40           272                 1
## 607     8.57      5.0          128  63           148                 0
## 608     4.39      7.4          123  42           109                 0
## 609    21.04      5.4          100  46            68                 0
## 610   507.39      4.0          142  97           180                 0
## 611     7.64      5.5           90  44           193                 1
## 612    20.92      4.0          133  52            78                 0
## 613     3.13      7.2           95  39            73                 1
## 614     8.94      6.8          135  41           139                 0
## 615     5.56      6.5          143  39           348                 1
## 616    76.84      6.2          100  34           127                 1
## 617     6.18      4.2           93  58            67                 0
## 618     6.22      6.8          108  38            76                 1
## 619     7.12      4.6           87  45            75                 0
## 620    15.91      3.8           93  51            67                 0
## 621    13.61      4.6           97  86            71                 0
## 622    11.37      2.7           84  14            57                 0
## 623     5.00      4.5           83  72            78                 0
## 624    11.44      4.5           83  59            62                 0
## 625     5.68      6.4           93  42           192                 1
## 626     2.86      5.4          109  48            91                 0
## 627     4.55      2.7           96  52           145                 0
## 628    15.71      3.4           93  49            52                 0
## 629     4.31      3.5           92  62            47                 0
## 630    10.83      4.6           86  45            65                 1
## 631    26.42      3.6          343  36           168                 1
## 632    61.68      5.8          247  40           110                 1
## 633    11.54      3.4           97  44            60                 0
## 634     7.68      4.6           81  60            74                 0
## 635     3.38      6.2           99  63            89                 0
## 636     7.68      3.9          121  57           141                 1
## 637     2.94      3.9           98  63            59                 0
## 638     7.46      5.7          124  38            77                 1
## 639     3.32      5.6           97  43           127                 0
## 640     9.81      7.3          105  40           222                 1
## 641    18.41      7.2           99  38           227                 1
## 642     3.95      6.5           89  58            85                 0
## 643     4.94      6.3           86  39            65                 0
## 644    17.14      6.7          113  40            93                 1
## 645     7.14      5.8           96  35            95                 0
## 646     6.23      3.4          105  48            78                 1
## 647     7.50      2.8          115  41           177                 0
## 648     3.38      7.0          127  52            94                 1
## 649    10.27      3.9           97  49            61                 0
## 650     3.25      5.2           90  75            45                 0
## 651     8.66      6.8          108  27           626                 1
## 652    44.55      7.1          116  59            91                 1
## 653     6.14      5.7           90  58            74                 0
## 654     4.55      5.7           97  43           104                 0
## 655     5.04      6.1          228  48           146                 1
## 656    14.75      4.5          327  26           302                 1
## 657    11.27      3.2           91  78           111                 0
## 658     8.31      4.9          110  62            72                 0
## 659    24.80      5.8           96  60           138                 0
## 660    12.43      2.5           92  65            99                 0
## 661     2.73      5.8          135  37           200                 1
## 662     8.41      4.3          102  47           107                 1
## 663    16.88      7.3          176  47           171                 1
## 664     5.97      8.8           88  40           160                 1
## 665    12.79      4.3          108  56           116                 0
## 666     5.85      4.5          106  61            71                 0
## 667    22.86      3.5          100  54            73                 0
## 668     3.15      5.8           85  61            75                 0
## 669     2.37      4.7          105  72            58                 0
## 670    26.39      6.3          114  39           135                 1
## 671     3.20      4.8          103  74            83                 1
## 672     1.80      5.0           88  57            51                 0
## 673    11.05      3.0           90  58            73                 0
## 674     7.37      4.9           91  63            29                 0
## 675     7.86      4.6          103  36            86                 1
## 676    27.98      4.7           90  91            78                 0
## 677     8.72      3.6          111  58            89                 0
## 678    21.03      4.4           87  46           136                 0
## 679     2.63      6.1           99  70            53                 0
## 680    11.09      3.7          114  58            54                 1
## 681    15.80      4.2           87  74            48                 0
## 682   454.74      7.6          140  21           681                 1
## 683   903.64      6.4          122  31           318                 1
## 684    12.12      6.6           86  46            78                 0
## 685     4.95      7.2          114  60            88                 0
## 686     2.16      6.3          101  41           174                 0
## 687     4.03      5.6           87  97            79                 0
## 688     7.14      4.9           88  84            96                 0
## 689    11.25      6.7           88  62            43                 0
## 690     6.28      8.1           97  53            77                 0
## 691    12.84      4.9          103  69            50                 0
## 692     1.65      5.7           93  53           118                 0
## 693     7.78      8.3          157  38           144                 0
## 694     5.56      4.4          102  47           163                 1
## 695     5.63      5.2          111  49           120                 1
## 696     9.74      5.0          110  33           264                 1
## 697     3.09      4.8          107  65           114                 0
## 698    14.25      6.8          118  38           107                 1
## 699     4.44      6.1           96  58            79                 0
## 700     6.40      5.2          113  78            61                 0
## 701     3.85      5.2           98  50           104                 0
## 702    22.13      4.7           98  58           452                 0
## 703     4.97      4.4          126  79            59                 1
## 704    27.91      9.9          123  34           246                 1
## 705     8.31      4.0           96  74           169                 0
## 706     8.82      4.8          154  66            71                 0
## 707    26.90      5.5          102  57           110                 0
## 708    16.50      3.9           90  55            84                 0
## 709     6.55      5.4          193  44            91                 0
## 710     4.15      6.0           98  44           119                 0
## 711    34.58      7.5           94  55            99                 0
## 712    10.84      5.2           98  43           187                 0
## 713    21.13      5.2           91  62           148                 0
## 714    28.98      7.8          115  40           119                 1
## 715     3.14      4.2           78  88           181                 0
## 716     5.74      4.3           82  53            84                 0
## 717    26.17      4.7          176  44           200                 0
## 718    31.45      6.4          136  35           102                 1
## 719     7.48      5.8          107  51           153                 0
## 720     3.53      6.0          135  40           246                 1
## 721     5.38      4.1           89  53            67                 0
## 722     7.44      5.1           96  48           223                 1
## 723     4.09      5.1           88  39           119                 0
## 724    15.11      3.8           81  61           218                 0
## 725     2.32      6.2          118  68            31                 1
## 726     9.26      2.5           81  57            52                 0
## 727     3.76      6.1           76  53           155                 0
## 728    10.97      7.3          114  39           584                 1
## 729     9.58      4.3           86  63            45                 0
## 730     9.08      4.3           83  65            94                 0
## 731    11.09      6.9          143  48           171                 1
## 732     3.74      5.9           95  55            59                 0
## 733     2.93      6.4          112  44           120                 0
## 734     5.23      4.9           97  66            71                 0
## 735     3.22      6.9           96  57            46                 0
## 736     6.15      5.8           90  56           116                 0
## 737    11.85      5.4          157  44            96                 1
## 738     4.00      6.0          118  34           180                 1
## 739     3.10      6.3           92  50           128                 0
## 740     3.68      5.6           92  40           279                 0
## 741    44.66      7.0          219  41           409                 1
## 742    59.33      4.7          237  39           465                 1
## 743     9.05      3.5           94  65            75                 0
## 744     3.26      5.7           92  56            94                 0
## 745     3.33      5.9          121  55           101                 1
## 746    11.51      4.3           96  75            37                 0
## 747    11.65      4.9           99  97            56                 0
## 748     3.58      5.5           94  51           117                 0
## 749    14.14      5.7          108  53           122                 0
## 750    10.00      2.7          103  48            85                 1
## 751    11.18      3.6           90  61            73                 0
## 752     5.70      6.6          101  47           110                 0
## 753     6.03      3.8          219  49           123                 0
## 754     1.62      5.3           83  42            73                 0
## 755     3.36      5.7           93  53           165                 0
## 756     3.50      3.5           77  60            46                 0
## 757    10.86      4.0           87  69           100                 0
## 758    56.46      4.7           98  44           130                 0
## 759     7.14      4.8           94  66            81                 0
## 760     6.21      6.8           95  46           162                 0
## 761     9.60      4.1           98  55            62                 0
## 762     2.12      6.6          103  47            59                 0
## 763     2.57      6.8           88  61           137                 0
## 764     7.20      5.2           94  31           124                 0
## 765   425.37      4.9          333  45           323                 0
## 766     7.76      7.1           81  58           394                 0
## 767     5.04      3.4           94  66           103                 0
## 768    11.52      5.5          131  48           125                 1
## 769    39.38      8.6           94  46           111                 0
## 770    18.47      6.5          125  62           113                 0
## 771     3.53      5.6           94  52            51                 0
## 772     7.50      5.1          113  44            68                 0
## 773     5.79      3.0           94  66            65                 0
## 774    10.77      8.5          101  32           162                 1
## 775     3.33      7.2           95  44           120                 0
## 776    62.50      4.4          153  45           106                 1
## 777    17.78      4.8          100  57            69                 1
## 778   777.03      4.6          111  46           205                 1
## 779     6.24      7.1           98  46            65                 0
## 780    10.09      6.1           85  45           172                 0
## 781    84.78      8.7          113  37           124                 1
## 782     5.12      5.8          105  50           195                 0
## 783     8.75      4.5           84  91           107                 0
## 784    12.92      6.2          122  38           117                 0
## 785    10.71      6.9          141  53           106                 0
## 786     7.19      2.7          102  66            55                 0
## 787    11.06      6.3          108  47           122                 1
## 788     2.50      5.8           98  49            38                 0
## 789     9.42      4.4           93  32           179                 1
## 790    32.05      5.2          181  51           268                 1
## 791     3.17      3.2          103  95           101                 0
## 792    50.40      5.7          116  83            86                 0
## 793     3.73      4.9           97  68            72                 0
## 794    12.63      7.5          117  28           220                 1
## 795    18.33      5.1           80  55           117                 0
## 796    11.43      7.6          134  45           133                 1
## 797     3.57      5.4          106  57            65                 0
## 798    21.33      4.9          141  28           125                 0
## 799     5.22      5.7           88 108            77                 0
## 800     4.29      6.7           84  52           122                 0
## 801     8.18      4.2           90  54            64                 0
## 802     6.96      5.4           86  60           144                 0
## 803     4.88      6.2           93  36           108                 0
## 804     5.92      5.9           91  81            70                 0
## 805    10.46      5.2          106  38           195                 1
## 806     9.03      6.4          116  69            93                 1
## 807     7.25      4.6          196  61            75                 0
## 808    18.74      5.0          115  73            76                 0
## 809    28.47      6.9          105  41           217                 1
## 810     2.61      5.3           97  39            92                 0
## 811     6.67      6.9          145  46           207                 1
## 812    32.51      6.1           93  66           137                 0
## 813    40.47      3.9          111  46            90                 0
## 814     6.27      4.8           86  40            83                 0
## 815    14.12      5.4          101  45           439                 1
## 816     3.32      5.0          103  53            50                 0
## 817    39.64      8.0          101  39           291                 1
## 818     7.78      5.9          111  42           279                 1
## 819     3.09      4.5           94  59            37                 0
## 820    32.37      6.0          111  36           155                 1
## 821    12.00      5.2          107  67           145                 0
## 822     6.73      5.5          105  40            82                 1
## 823     6.37      6.8           92  52            88                 0
## 824     4.14      3.9           82  65            55                 0
## 825    15.00      3.5          103  62            84                 0
## 826     9.34      4.7           99  42           145                 0
## 827    10.68      3.9           92  48            44                 0
## 828    12.45      5.6          144  30           191                 1
## 829     5.28      5.2          144  59           160                 0
## 830   844.83      4.2          335  35           979                 1
## 831    13.82      7.0           93  45            98                 0
## 832     4.02      4.3           98  58           116                 0
## 833     3.94      7.9           90  39           330                 1
## 834     4.21      3.8           94  52            63                 0
## 835     3.77      7.6          103  49            93                 0
## 836     6.60      5.2           98  56            63                 0
## 837     5.00      8.0          107  64            90                 0
## 838     4.54      6.7          117  42           174                 1
## 839    58.90      6.3          107  43            87                 0
## 840     7.83      2.5           87  48            62                 0
## 841     8.09      4.6           88  65            58                 0
## 842    10.00      5.5          104  48            44                 1
## 843     5.60      7.6          130  46           198                 1
## 844     8.21      5.3           94  50           125                 0
## 845     3.06      4.6          132  58            96                 1
## 846     6.17      5.3           95  75            89                 0
## 847     6.79      4.4           89  80            55                 0
## 848     1.95      4.0           89  56            67                 0
## 849    10.00      6.8          105  35           115                 1
## 850    14.10      4.4           90  64            73                 0
## 851    31.29      8.5          110  81           238                 1
## 852     4.72      8.4          139  44            88                 1
## 853     7.75      5.0          243  44           205                 1
## 854    14.92      4.7           95  26           135                 0
## 855     5.09      5.8          120  46           170                 1
## 856    15.92      2.8          138  51            80                 0
## 857    15.04      5.6           96  56            74                 0
## 858     9.34      4.6          181  86            89                 0
## 859    14.64      6.9           75  53           114                 0
## 860     9.75      7.0          129  46           135                 0
## 861    19.22      6.1          105  34           131                 1
## 862     6.48      9.9          118  31           332                 1
## 863     3.66      4.6           92 104            37                 0
## 864    28.99      2.8           94  81           114                 0
## 865     4.95      4.6           92  50            82                 0
## 866    39.75      6.3           92  51           174                 0
## 867     6.05      4.8          110  52           124                 0
## 868    32.89      5.9          163  40           166                 1
## 869    99.57      4.5           97  57            64                 0
## 870   657.41      8.0          117  43           178                 1
## 871     6.25      4.8           97  39           170                 0
## 872     4.44      4.9           98  65           117                 0
## 873  1276.60      8.1           47  60           159                 1
## 874     3.37      6.0          164  46            92                 0
## 875   301.05      5.9          109  42           120                 0
## 876     4.31      4.8          101  59           144                 0
## 877     6.16      6.3          121  44           115                 0
## 878     7.14      5.1          107  43           225                 1
## 879     5.42      5.5          100  34           149                 1
## 880     4.44      5.4           99  60            55                 0
## 881     1.41      6.4           98  35           167                 1
## 882     3.35      3.3           91  71           167                 0
## 883     2.88      7.1           95  40           109                 0
## 884    50.11      5.1          254  69            60                 0
## 885     5.08      5.4          123  41           275                 1
## 886     2.97      5.5           98  53            72                 0
## 887     3.71      3.8           92  48            56                 0
## 888     6.77      5.8           96  40           173                 1
## 889    34.73      4.2           93  41           140                 1
## 890    32.67      5.2          144  54           105                 0
## 891    27.44      4.9           96  46           262                 1
## 892  1511.11      6.2          250  47            80                 1
## 893     2.77      6.7          109  30           274                 1
## 894    10.38      6.9          130  39           160                 1
## 895     6.82      5.8          115  38           106                 1
## 896     3.42      7.2           79  48            57                 0
## 897     4.77      5.7           89  54           153                 0
## 898     3.81      4.7          101  48            71                 0
## 899     3.75      4.4           98  55            92                 0
## 900    11.21      6.1          107  64            85                 0
## 901     5.19      4.8           98  53           175                 1
## 902     2.62      6.5           93  41           274                 1
## 903     2.07      5.5          119  51            96                 0
## 904    12.20      6.7          105  67            66                 0
## 905     7.50      4.2           97  42            74                 0
## 906     5.69      4.8          106  46           108                 0
## 907     3.41      5.5           96  43           178                 1
## 908   100.79      7.6          171  40           130                 1
## 909    17.13      6.7          134  49           181                 1
## 910     4.68      5.6          116  51           177                 1
## 911  3666.67      8.8          211  48           188                 0
## 912     6.94      3.6           74  97           107                 0
## 913    51.95      6.0          100  50            77                 0
## 914    20.45      4.9           94  66            94                 0
## 915     3.73      5.3           77  62           231                 0
## 916    12.57      7.2          117  44            92                 1
## 917    12.38      4.5           92  58           162                 0
## 918   755.00      8.9          100  54           148                 1
## 919    10.17      4.2           96  36           111                 0
## 920     4.22      3.6           94  72            44                 0
## 921    23.82      3.6          110  27           185                 1
## 922     3.60      6.2          110  40            97                 1
## 923    58.10      6.3          103  63            81                 1
## 924     8.28      2.9           85  58           112                 0
## 925     9.41      5.2           99  41           329                 0
## 926    47.61      8.5          112  51            82                 1
## 927    90.48      4.1          237  37           215                 1
## 928    11.42      3.8           91  69            44                 0
## 929     4.80      4.4           80  63           166                 0
## 930     6.08      6.4           86  56            75                 0
## 931     8.60      4.7          105  64           147                 0
## 932     4.65      5.5           93  42            61                 0
## 933     4.04      5.2           97  33           398                 0
## 934     3.90      5.7           99  44           116                 0
## 935     5.40      2.8           94  62           125                 0
## 936     6.67      6.8           83  82            68                 0
## 937    15.40      4.5          100  63            99                 1
## 938    11.54      5.2           95  62            92                 0
## 939     3.91      3.6           87  70            42                 0
## 940    15.45      4.8          101  80            76                 1
## 941    37.73      7.0          115  32           148                 1
## 942     3.26      5.5           85  63            66                 0
## 943    10.24      3.0           87  59            90                 0
## 944    10.59      6.2          107  44           113                 1
## 945    38.00      9.4          133  34           271                 1
## 946     6.79      5.8           86  84            72                 0
## 947     6.17      3.0           88  80            44                 0
## 948     3.47      6.3          103  56            70                 0
## 949     8.00      5.7          106  36           183                 1
## 950    12.97      3.3           97  71            84                 0
## 951     4.10      6.5          110  52           123                 1
## 952     4.16      5.6           99  35           212                 0
## 953    32.31      6.2           99  65           116                 0
## 954     5.00      4.7           96  66           143                 0
## 955    23.67      3.7           82  55           119                 0
## 956     5.95      6.1          104  59           172                 1
## 957    44.55      7.7          105  45           224                 1
## 958    20.00      6.8          121  45           377                 1
## 959    12.16      3.3           94  49            94                 0
## 960     6.52      3.4           93 138            54                 0
## 961     5.63      5.7          112  54           189                 1
## 962    18.93      8.1           97  41           152                 1
## 963   289.72      9.6          138  56           157                 1
## 964     6.81      7.2          133  57           130                 1
## 965    61.17      6.0          107  36            88                 1
## 966     2.66      5.9           95  31            86                 0
## 967     7.14      5.0           90  44            98                 0
## 968     7.42      4.0          101  50            76                 1
## 969     4.84      5.6          223  37           202                 1
## 970     2.75      7.2           98  52            76                 0
## 971     7.50      6.1          104  65           144                 0
## 972     7.36      5.5           84  55            43                 0
## 973     3.28      8.4           99  46           158                 0
## 974     8.72      1.9           86  30            91                 0
## 975     6.11      6.1          114  39            86                 1
## 976     6.26      5.9          108  41           114                 1
## 977     3.98      4.0           94  51            56                 0
## 978     7.11      5.6          107  44           148                 1
## 979    12.29      4.5           98  52           105                 0
## 980     5.64      3.2          101  44           162                 1
## 981     4.05      7.1           83  38           112                 0
## 982     7.73      4.4           84  52            92                 0
## 983     3.06      5.2          148  52            70                 1
## 984    14.38      5.2          101  53            55                 0
## 985    56.33      6.0          124  51           109                 1
## 986     1.66      6.0           87  61            76                 0
## 987     8.75      5.8           87  58            53                 0
## 988     6.18      3.9          102  54            59                 0
## 989    10.55      4.2           72  70            64                 0
## 990     3.30      3.8           91  51            58                 0
## 991    10.48      3.9          102  51           125                 1
## 992     8.91      3.7          112  77            75                 0
## 993     7.15      8.6          116  36           146                 0
## 994     8.81      3.4          106  43           113                 0
## 995   232.56      7.7          121  40           150                 1
## 996    27.41      7.2           92  39           109                 0
## 997    90.38      4.8          111  55           196                 1
## 998     4.22      5.7          102  88            61                 0
## 999    93.33      3.2           99  64            96                 0
## 1000    5.95      6.0           99  54            87                 0
## 1001   18.06      5.9           88  53           157                 1
## 1002    7.12      3.0           86  67           127                 0
## 1003    5.51      5.6          100  49            80                 0
## 1004   10.17      4.7          109  45           115                 0
## 1005    4.77      5.8          109  50           147                 0
## 1006    2.84      6.7           95  59           167                 1
## 1007    3.78      5.7          102  56           141                 0
## 1008    6.29      4.6          123  49           154                 1
## 1009    4.97      4.6           91  65            63                 0
## 1010    5.20      6.5          114  46           126                 0
## 1011    2.96      5.4          100  52           103                 0
## 1012   19.14      4.0           89  82            73                 0
## 1013   15.46      4.8          142  42           125                 1
## 1014    7.19      4.9          148  49           127                 1
## 1015    2.02      5.6          102  69            67                 0
## 1016    6.96      5.7           95  48           192                 0
## 1017    7.65      4.9          126  28          1311                 1
## 1018   55.00      7.8          132  41           231                 1
## 1019  511.72      7.2          100  57            89                 0
## 1020    3.04      5.7          103  39           119                 1
## 1021   67.24      4.9          108  76           119                 0
## 1022    3.61      6.1          138  49           125                 1
## 1023    4.74      6.8           99  43           105                 0
## 1024    5.67      3.4           84  62            63                 0
## 1025    3.47      4.4          101  54            61                 0
## 1026   16.02      3.9           97  59           151                 0
## 1027   17.82      6.2           94  63            67                 0
## 1028   54.47      4.3           83  68            77                 0
## 1029   20.30      4.6           92  62            87                 0
## 1030  391.57      8.2          133  42            98                 0
## 1031    5.00      6.0           94  48           123                 0
## 1032    2.19      4.6          103  55            33                 0
## 1033   18.91      4.8           96  63           162                 1
## 1034   21.18      4.4          131  54           186                 0
## 1035    4.28      3.4           77  59            36                 0
## 1036    5.13      7.8           90  50            63                 0
## 1037    8.52      4.3          121  61            92                 0
## 1038    3.28      6.5          116  54            91                 1
## 1039    8.35      6.9           88  53           205                 0
## 1040    6.46      4.5           85  54            42                 0
## 1041    6.22      5.5          105  48            85                 0
## 1042    4.40      4.1          108  48           201                 1
## 1043    7.56      7.0          102  52            90                 1
## 1044   15.05      5.5          114  47           123                 0
## 1045    7.07      4.6          116  48           125                 1
## 1046    8.97      7.0          147  33           308                 1
## 1047   25.59      3.6           78  60           115                 0
## 1048   17.78      4.4          365  40           306                 1
## 1049    6.58      5.8           91  61           102                 0
## 1050   18.86      4.2          103  42           109                 1
## 1051    8.08      4.8           97  57           115                 0
## 1052    4.49      6.6           90  32           337                 1
## 1053    6.57      5.7          100  48           118                 0
## 1054   13.37      3.8          101  65            61                 0
## 1055   29.38      3.8          200  34           172                 1
## 1056    7.35      7.0          143  52           158                 1
## 1057  285.71      5.2          114  67           150                 1
## 1058    6.82      4.3           96  55           106                 0
## 1059    6.40      5.8          122  49           120                 1
## 1060   18.85      4.8           93  57            87                 0
## 1061   10.32      6.7          105  39           188                 1
## 1062    6.36      8.2          107  45           176                 1
## 1063    6.82      3.8          103  86            52                 1
## 1064  130.77      4.0          123  50           226                 1
## 1065   11.50      4.1          241  66            87                 0
## 1066   12.97      4.7          133  37            44                 0
## 1067    3.08      4.0           95  48            77                 0
## 1068   14.71      7.2           93  56            95                 0
## 1069  142.62      5.0          113  43           124                 1
## 1070    5.63      7.0          102  54            76                 0
## 1071   11.55      6.7          101  65            76                 1
## 1072    5.28      4.9           97  32           233                 0
## 1073    4.25      6.7          105  51           243                 1
## 1074    3.73      8.7          109  50           192                 1
## 1075    4.31      9.4           95  27           306                 1
## 1076    5.56      6.3          103  46           164                 1
## 1077    2.50      3.8           96  47            62                 0
## 1078   24.46      7.4          101  57            93                 0
## 1079   41.20      7.2          201  56           163                 1
## 1080   13.75      4.8           91  64           116                 0
## 1081   35.81      5.6           92  45            98                 0
## 1082    7.00      4.6           98  83            73                 0
## 1083   18.28      4.9           88  62            75                 0
## 1084    7.57      6.1           93  36           154                 1
## 1085   21.79      4.2          106  50           118                 0
## 1086    4.34      7.4           92  31            95                 0
## 1087 1024.31      5.1          180  46            85                 1
## 1088    6.06      5.0           90  33            90                 0
## 1089    3.70      6.5           99  29            98                 0
## 1090    4.88      4.3           96  54            89                 0
## 1091   10.34      4.8           95  42           158                 1
## 1092   10.25      6.1          109  76            54                 1
## 1093    7.25      3.2           94  45            64                 0
## 1094  207.32      6.8          130  37           153                 1
## 1095    5.27      6.9           99  88            63                 0
## 1096    3.51      5.5           89  52            83                 0
## 1097    4.10      5.8          108  62            84                 0
## 1098    3.92      7.5          102  43           125                 1
## 1099   33.85      5.3          155  37           151                 1
## 1100  155.43      7.2          107  45           103                 1
## 1101    6.40      4.1          101  46           235                 1
## 1102    7.43      5.0           92  62           136                 0
## 1103    3.80      6.3          100  83            72                 0
## 1104   26.61      3.9          248  43           193                 0
## 1105   12.29      7.4          142  35           222                 1
## 1106    6.79      4.0           99  46           114                 0
## 1107    4.04      6.4           95  34            80                 0
## 1108   13.29      4.5           98  52           101                 0
## 1109    9.25      5.7           96  55           241                 0
## 1110    2.96      5.8          101  59           127                 0
## 1111    4.18      4.2          103  62           226                 1
## 1112    4.74      5.5          103  41           428                 1
## 1113    2.86      6.2           97  33           144                 0
## 1114    6.00      4.7          108  70            89                 0
## 1115    4.36      5.3          102  43            93                 0
## 1116   10.50      6.9          119  25           560                 1
## 1117    2.74      7.9           91  44           177                 1
## 1118   13.73      7.9          125  35           124                 1
## 1119    5.09      6.6           96  89            78                 0
## 1120    5.94      5.6          124  37           178                 1
## 1121    4.31      5.4          125  35           119                 0
## 1122   13.51      3.1           87  65            65                 0
## 1123   11.53      3.5           93  81            35                 0
## 1124    4.18      8.2          107  39           104                 0
## 1125    6.92      3.8           86  46           108                 0
## 1126    2.96      5.6           79  44            87                 0
## 1127  584.75      7.9          133  42           191                 1
## 1128    2.19      7.0           93  40           118                 0
## 1129    8.78      4.7          109  50           146                 1
## 1130    3.87      6.5          147  78           112                 1
## 1131   13.67      4.1          202  56            69                 1
## 1132    6.67      5.0           93  47           101                 0
## 1133    7.88      5.9           96  38           121                 1
## 1134   26.40      5.5           90  46            94                 0
## 1135   12.29      4.6          172  29           374                 1
## 1136    5.31      6.3          154  44           136                 1
## 1137   13.33      5.1           89  66           107                 0
## 1138    3.33      4.0          106  56            60                 0
## 1139    3.67      1.8           88  78            79                 0
## 1140   10.30      9.8           97  40           213                 1
## 1141   10.14      4.7           75  61           101                 0
## 1142   10.97      5.4          117  39           212                 1
## 1143    6.74      5.1           95  62            93                 0
## 1144    9.13      4.3           87  65            87                 0
## 1145    6.44      6.3           99  55           230                 0
## 1146    6.27      6.5           98  52           134                 0
## 1147    3.96      7.8           99  40           127                 0
## 1148   19.80      4.6          114  53           229                 1
## 1149    5.71      3.6           89  52            89                 0
## 1150    6.75      4.2           93  78            47                 0
## 1151    7.09      5.3          103  64            80                 0
## 1152    6.39      6.7           93  47            75                 0
## 1153   10.91      4.8           92  63           102                 0
## 1154    9.65      6.4          103  43           139                 1
## 1155   20.00      3.1           91  68            59                 0
## 1156    8.35      4.5           99  44            93                 0
## 1157    7.96      6.8           90  97            62                 0
## 1158   16.67      4.4          101  70            90                 0
## 1159   11.11      7.3          180  43           250                 0
## 1160    9.47      6.7          231  40           155                 1
## 1161    3.91      8.3          102  62            70                 0
## 1162   31.39      3.4           86  52            72                 0
## 1163    3.02      4.0           73  80            39                 0
## 1164    8.60      4.9           78  52            85                 0
## 1165    3.33      5.0           84  49            77                 0
## 1166   10.63      5.4           83  72            58                 0
## 1167   24.51      6.1          103  46           108                 1
## 1168    7.88      4.9           73  58            85                 0
## 1169    5.63      3.3          100  85            62                 0
## 1170   10.32      7.0          200  50           146                 1
## 1171    2.81      6.7          107  22           319                 1
## 1172    7.93      5.0           89  87           113                 0
## 1173    3.87      6.6           90  39            62                 1
## 1174    8.93      4.2          114  42            89                 1
## 1175    5.42      5.1           93  55            56                 0
## 1176    3.49      6.4           80  57           138                 0
## 1177   11.75     10.9          132  43           129                 1
## 1178   10.09      5.3           98  36           267                 1
## 1179   14.68      3.5           89  58           150                 0
## 1180   21.93      4.3          103  35           171                 1
## 1181    5.56      6.9          112  50           136                 1
## 1182   25.98      6.1           88  65            64                 0
## 1183    9.37      7.1          100  44           263                 0
## 1184    3.58      5.6          111  39           160                 1
## 1185   13.40      6.7          115  35           182                 1
## 1186    4.95      6.4           87  69            90                 0
## 1187    5.26      4.6           77  55            61                 0
## 1188    9.03      7.5          110  61            91                 0
## 1189    6.85      5.5          103  78            43                 1
## 1190   20.00      4.3           92  75            83                 0
## 1191    8.71      6.1           91  48           228                 1
## 1192  145.05      5.1          120  44           195                 1
## 1193    5.81      6.5          114  45           326                 1
## 1194   27.09      3.3           86  61            39                 0
## 1195   10.37      5.6          104  43           134                 1
## 1196    6.33      3.2           82  59            50                 0
## 1197    3.63      3.9           93  51            78                 0
## 1198    4.81      6.0           93  75           320                 1
## 1199    5.71      4.3          105  51           132                 1
## 1200    3.97      5.6           98  34           177                 0
## 1201   12.10      6.1           75  44            72                 0
## 1202    5.61      3.1           89  75            98                 0
## 1203    3.84      6.2           87  58           143                 0
## 1204    2.96      6.5           92  26           151                 0
## 1205    8.89      5.2          101  72           112                 0
## 1206    7.66      3.4          100  62            63                 0
## 1207   16.91      6.3           96  74            65                 0
## 1208    7.93      8.2           87  58            95                 0
## 1209   21.75      3.0           99  66            54                 0
## 1210    2.29      5.4          102  36            54                 0
## 1211    4.44      5.5           94  63            68                 0
## 1212    8.93      3.6           94  56           100                 0
## 1213    5.38      6.5          113  50            99                 1
## 1214    6.34      3.4           97  64            91                 0
## 1215    3.29      9.1          105  39           234                 1
## 1216    3.47      3.8           87  78            86                 0
## 1217    2.35      5.3           88  64            52                 0
## 1218    5.08      6.0           85  57           138                 0
## 1219    5.48      5.7           84  62            53                 0
## 1220    7.90      6.0          138  40            84                 0
## 1221    2.50      8.5           97  42           256                 1
## 1222    3.42      6.4           96  50           102                 0
## 1223    4.34      5.4           99  52            90                 0
## 1224    3.21      5.5          102  66            97                 1
## 1225   17.41      4.2           93  70           198                 1
## 1226   10.51      3.9           95  48            76                 1
## 1227    4.04      4.0           94  48           135                 0
## 1228    3.85      6.3           83  94           112                 0
## 1229    4.06      4.4          102  65           185                 1
## 1230    4.33      6.4          107  42            58                 0
## 1231    3.36      5.2           95  50            64                 0
## 1232  106.67      6.7          137  85            82                 0
## 1233    3.73      4.8           88  54           208                 0
## 1234    4.78      6.3          105  40           238                 1
## 1235   46.10      3.5          119  88           159                 1
## 1236   13.00      7.4          112  53           163                 0
## 1237   29.31      4.5           98  52           223                 1
## 1238    5.51      2.9          236  80            39                 0
## 1239    2.36      6.1          114  59           101                 0
## 1240    5.91      5.6           98  76           186                 0
## 1241   10.35      5.3           97  40           194                 1
## 1242  245.61      4.9          118  57           121                 1
## 1243    4.58      3.7           91  59            53                 0
## 1244   16.05      5.0          109  49            85                 1
## 1245    5.12      5.3          129  63            96                 1
## 1246    5.45      4.9          106  52           182                 1
## 1247   19.83      5.6          111  46           136                 1
## 1248    5.38      9.4          114  40           218                 1
## 1249    7.65      5.5           96  53           113                 0
## 1250    6.01      4.8           88  52            50                 0
## 1251   12.38      4.8          201  45           208                 1
## 1252   17.20      3.7           70  57           144                 0
## 1253   19.65      4.5           88  83           106                 0
## 1254    7.39      3.2           99  55            46                 0
## 1255    3.75      6.4           89  59            69                 0
## 1256   68.09      3.1           99  48            87                 1
## 1257    6.80      5.2          103  40           111                 1
## 1258   13.42      4.7           93  52           110                 0
## 1259    5.42      7.1           93  74            62                 0
## 1260    7.60      6.2           93  42            75                 0
## 1261   10.14      7.8          100  47            76                 0
## 1262   27.41      7.0          107  48           307                 1
## 1263    4.40      3.5           93  39           158                 1
## 1264    3.39      5.7           89  44            85                 0
## 1265   11.80      4.4           94  43            67                 0
## 1266   27.08      6.8          111  57           130                 0
## 1267   15.36      6.3          119  43           125                 1
## 1268    1.43      6.4           99  38           115                 0
## 1269    5.15      3.6          126  41            90                 0
## 1270    7.16      4.4           96  44           109                 0
## 1271    3.68      5.7           91  48            96                 0
## 1272    5.45      6.3          118  58           271                 1
## 1273    4.02      6.4          301  32           510                 1
## 1274    6.93      3.8           88  43            80                 0
## 1275    5.72      3.3          130  57           117                 0
## 1276   34.21      6.0          108  48           139                 1
## 1277   12.73      3.8           99  60           152                 0
## 1278   51.59      8.8          129  59            66                 1
## 1279    3.39      5.4          111  53            50                 0
## 1280    3.70      4.5          109  73            76                 1
## 1281    3.25      5.4           95  60            66                 0
## 1282   23.60      3.9           95  84            95                 0
## 1283    1.96      6.9          100  55           113                 1
## 1284    4.19      5.4           54  58            83                 0
## 1285    6.74      4.6           83  48            55                 0
## 1286    4.40      6.7          194  52            90                 0
## 1287    7.28      5.4           87  56            85                 0
## 1288    3.92      5.4          103  69            65                 0
## 1289    3.77      5.4           99  59           149                 0
## 1290    3.05      5.5           90  65            91                 0
## 1291    2.94      6.8          101  51            67                 1
## 1292   12.78      5.8          107  51            78                 0
## 1293   40.15      4.6          103  50           106                 1
## 1294  171.24      4.3           80  71            64                 0
## 1295  138.79      7.1          108  53           146                 1
## 1296    2.96      3.2           97  60            68                 0
## 1297    3.22      3.4           79  72            38                 0
## 1298    5.29      4.1           89  61           137                 0
## 1299   10.93      8.7          110  75            74                 1
## 1300    8.35      4.2          106  78           168                 1
## 1301   16.04      6.2          107  39           181                 1
## 1302   18.39      5.1          193  40           330                 1
## 1303    3.80      7.1          102  33           139                 1
## 1304   13.95      5.0           93  46            81                 0
## 1305    2.35      6.6          108  71            68                 1
## 1306    2.05      6.5           85  45            83                 0
## 1307    6.83      4.9          105  76            76                 1
## 1308    3.72      4.6          118  66            94                 0
## 1309   16.10      2.9          112  56           120                 1
## 1310   46.49      5.4           84  56            71                 0
## 1311  151.70      7.4          108 156            64                 0
## 1312    3.97      5.0           91  62            92                 0
## 1313    4.05      6.8           97  68            81                 0
## 1314    4.39      5.4          103  55           124                 0
## 1315    4.10      5.8          103  53           162                 1
## 1316   10.81      6.6          177  28           357                 1
## 1317    6.92      4.3          105  49            81                 1
## 1318    5.69      5.1           91  56            66                 0
## 1319   16.03      5.5           97  42            64                 0
## 1320   85.80      5.6          100  81            64                 1
## 1321  204.14      7.3          144  33           157                 1
## 1322    3.64      6.7           95  34           564                 1
## 1323   10.27      5.6          113  35           107                 1
## 1324    3.26      5.9          109  53           117                 0
## 1325   21.78      6.6           97  48           122                 0
## 1326   19.59      4.0           92  80            99                 0
## 1327    2.34      5.0           75  71            59                 0
## 1328    9.16      4.4           78  42           294                 1
## 1329    5.22      3.8           91  63            56                 0
## 1330   11.93      4.7          104  51            60                 0
## 1331    5.00      5.8           91  51           125                 0
## 1332    6.79      3.8          103  86            93                 0
## 1333    8.92      4.2          108  52           220                 1
## 1334    5.41      3.9          103  80           116                 0
## 1335    3.03      4.5           92  35            79                 0
## 1336    4.37      6.2          107  45           142                 0
## 1337    6.71      5.8           91  82            72                 0
## 1338   20.52      8.4          107  42           193                 1
## 1339    7.70      2.8           81  56            58                 0
## 1340    6.45      5.4           91  40           183                 0
## 1341    6.86      7.7          138  38           240                 1
## 1342    4.28      6.1          116  54           125                 0
## 1343   37.78      7.6           97  48           110                 0
## 1344    6.19      4.1           87  57            84                 0
## 1345    3.87      5.2          117  54            63                 0
## 1346    8.58      4.0           92  34           191                 1
## 1347    6.50      4.7          116  62            56                 1
## 1348    4.52      4.6           89  47           111                 0
## 1349   11.28      9.3          113  46           102                 1
## 1350  681.12      3.5          170  38           249                 1
## 1351    1.70      6.9          111  48            86                 0
## 1352    7.66      7.0          111  38            81                 1
## 1353   21.56      4.4           99  67           114                 0
## 1354    5.47      5.1           99  90            95                 0
## 1355    7.02      7.1           98  44            42                 0
## 1356    4.23      6.8           85  53           128                 0
## 1357    6.77      3.8           92  80            78                 0
## 1358    3.50      6.8           88  40           306                 1
## 1359   13.69      5.1          126  54            69                 1
## 1360    5.34      7.4          111  52            92                 0
## 1361    5.48      7.7          111  33           268                 1
## 1362   14.00      4.5          131  67            42                 1
## 1363   10.74      6.4          108  55            98                 0
## 1364  569.08      7.1           39  69           113                 0
## 1365    5.74      4.6           98  40           122                 0
## 1366   14.87      5.1          155  39           150                 1
## 1367    5.55      4.5           83  65           194                 0
## 1368    8.14      3.3           85  56           126                 0
## 1369    8.50      4.6           90  77           113                 0
## 1370    2.00      4.3          104  42            39                 0
## 1371    1.54      6.5           80  83           215                 0
## 1372    4.79     10.0           57  47            95                 0
## 1373    6.52      5.3          101  84            70                 1
## 1374    4.77      4.6           89  61           133                 0
## 1375   29.15      6.3          100  38           333                 1
## 1376    3.47      4.9          100  38           491                 1
## 1377    9.84      6.6           82  60           148                 0
## 1378   11.48      3.2          102  59           101                 0
## 1379    4.76      3.7           98  53            31                 0
## 1380    5.08      5.6           95  36           105                 0
## 1381    7.69      6.1           99  61           102                 0
## 1382    3.93      5.4           97  56           107                 0
## 1383    5.09      6.3           96  45            45                 0
## 1384    5.80      6.0           80  74           124                 0
## 1385    5.41      5.9          101  37           553                 1
## 1386    9.13      4.1          126  45           169                 1
## 1387  394.74      3.6           98  58            62                 0
## 1388    6.48      3.8           84  59            66                 0
## 1389   23.94      6.6           97  43           119                 1
## 1390   73.25      4.2           91  47            66                 0
## 1391   14.26      4.2           94  50           113                 1
## 1392    2.88      6.6          100  50            48                 0
## 1393    3.97      5.5          104  44            97                 0
## 1394   13.95      4.5           90  58            59                 0
## 1395   28.92      8.5          136  28           138                 1
## 1396    2.64      5.7          105  38           104                 0
## 1397    8.50      7.7           91  48           187                 0
## 1398   64.04      6.4           94  34           120                 0
## 1399    6.00      3.3           99  61            38                 0
## 1400   14.00      6.3          118  68            70                 0
## 1401    3.75      5.6          113  53           109                 0
## 1402    2.91      6.8          105  44           151                 1
## 1403    9.86      4.6           96  81           140                 0
## 1404    9.28      5.2           90  86            45                 0
## 1405   31.67      3.7          108  54            71                 1
## 1406    2.67      5.5          110  64            87                 0
## 1407    7.38      5.6           87  66           127                 0
## 1408  326.44      8.5          111  46           161                 1
## 1409   32.80      5.8           93  67            57                 0
## 1410    5.07      4.1           90  60            85                 0
## 1411    8.57      2.7           94  59            60                 0
## 1412    5.40      4.8           88  47            86                 0
## 1413   32.06      6.8          107  62            61                 0
## 1414    1.97      6.1          105  51            99                 0
## 1415    5.03      4.9          104  31           236                 1
## 1416    5.25      7.4          102  53           168                 0
## 1417    5.27      4.1           87  71           100                 0
## 1418   15.57      5.9           94  59           104                 0
## 1419    4.11      4.4           90  55           122                 0
## 1420    2.99      8.9          116  69           141                 0
## 1421    8.75      6.9           79  44           201                 1
## 1422    3.62      4.3           94  69            84                 0
## 1423    2.05      4.6          118  92           105                 0
## 1424    6.49      3.0           96  57           528                 1
## 1425    7.56      5.5           60  69            67                 0
## 1426    3.07      6.7           91  60            61                 0
## 1427   64.27      8.1          118  39           186                 1
## 1428   10.92      3.4           91  63            74                 0
## 1429  180.56      7.7           94  33           176                 1
## 1430    5.93      6.3           86  48            84                 0
## 1431   57.31      6.4          172  53           118                 1
## 1432   10.28      8.3          102  44           100                 1
## 1433    9.79      3.8          108  57           102                 1
## 1434    7.00      2.8          110  38            81                 1
## 1435   20.70      3.4          102  48           108                 0
## 1436    4.62      5.8           90  80            69                 0
## 1437    5.57      3.3           88  64            77                 0
## 1438    5.44      5.2           93  41           106                 0
## 1439 2360.66      9.2           98  59           209                 1
## 1440   11.76      5.5           80  87            77                 0
## 1441    4.42      3.9          111  71           115                 1
## 1442   14.72      6.7          103  27           158                 1
## 1443    6.36      5.3           90  56           103                 0
## 1444   55.77     10.5           88  51           163                 0
## 1445    8.38      5.6          108  60           137                 0
## 1446    4.68      7.7          104  44           100                 1
## 1447    5.00      4.5          108  46           143                 1
## 1448    2.24      4.8          108  52           108                 0
## 1449    4.43      4.4           96  71            78                 0
## 1450    4.15      4.0           97  66            92                 0
## 1451    4.17      5.7          270  49           121                 1
## 1452    5.93      4.5           92  41           128                 0
## 1453    7.52      8.5          120  33            97                 1
## 1454   20.00      4.5          105 107            95                 0
## 1455    5.08      4.8           95  35           190                 1
## 1456    5.25      7.0          250  22           332                 1
## 1457   20.54      5.5          191  41           281                 1
## 1458   15.81      4.2           79  78            84                 0
## 1459   14.88      5.3          126  52            73                 1
## 1460    8.72      6.6           85  43            95                 0
## 1461    6.40      4.1          108  43            37                 0
## 1462   27.50      7.2          128  55           119                 0
## 1463    5.57      6.7           91  86           145                 0
## 1464    5.36      2.7           85  68           100                 0
## 1465    4.96      4.5          108  71            51                 0
## 1466    3.31      5.8          107  39           159                 1
## 1467    3.16      6.0          111  45           169                 0
## 1468   12.75      5.9          110  54           147                 1
## 1469    7.53      5.9          110  53            84                 1
## 1470   12.33      3.7          115  50            42                 1
## 1471   12.08      7.5          110  34           325                 1
## 1472   10.53      8.5           90  38            73                 0
## 1473    3.49      7.8           96  62            86                 0
## 1474    5.95      3.4          139  35           111                 1
## 1475    5.41      5.8          100  29           481                 1
## 1476    5.06      4.3           94  65            98                 0
## 1477    4.43      5.6          100  47            66                 0
## 1478    5.90      3.8           98  40           126                 0
## 1479    3.55      4.3           94  56            86                 0
## 1480    7.07      6.0          103  49           195                 1
## 1481    7.05      6.6           88  56            87                 0
## 1482   23.14      4.1          110  54           134                 1
## 1483   26.86      2.5           83  52            99                 0
## 1484  116.49      3.5           96  46           124                 0
## 1485    4.70      2.8           96  54           114                 0
## 1486    4.29      3.3           93  69            86                 0
## 1487    9.59      5.4           94  59           104                 0
## 1488    3.33      6.7          101  46            80                 0
## 1489   27.63      3.8          110  91           101                 0
## 1490    4.78      5.3          109  48            79                 0
## 1491    2.90      8.1          103  60           101                 0
## 1492   20.73      4.9          173  75            94                 1
## 1493    3.20      4.3           98  38           157                 1
## 1494    7.53      6.2           94  49            87                 0
## 1495    8.88      6.7          127  53            83                 0
## 1496    2.93      5.1          124  50            62                 1
## 1497    2.50      6.1           98  34           163                 0
## 1498   83.83      5.3          166  44           161                 1
## 1499   12.08      6.1          114  42           167                 1
## 1500    4.00      6.4          105  45           203                 1
## 1501    4.29      7.8           99  54           115                 0
## 1502    5.75      5.5          120  38           273                 1
## 1503    8.96      3.3           91  76            53                 0
## 1504   70.16      5.9          102  39            41                 1
## 1505    6.56      4.8          160  45           103                 1
## 1506   10.71      7.0          118  40           197                 1
## 1507    4.36      6.2          115  46           276                 1
## 1508    3.31      6.6          101  35           108                 1
## 1509   20.13      3.2           93  49           105                 1
## 1510    7.23      5.3           98  41           120                 0
## 1511    2.08      6.0           93  60            87                 0
## 1512    5.25      5.7           93  31           385                 0
## 1513   39.32      6.4           97 104            97                 0
## 1514  100.63      6.9           95  43            89                 0
## 1515   30.52      5.9          124  43           132                 0
## 1516    5.95      5.9           98  53            53                 0
## 1517    8.29      4.5           88  74            45                 0
## 1518    3.52      5.0           94  77            92                 0
## 1519   19.57      4.5          103  40           175                 1
## 1520    5.59      3.4          113  69           108                 0
## 1521    5.14      5.3           84  32           124                 0
## 1522   11.47      6.9          169  48           199                 1
## 1523    5.19      3.9           85  89            46                 0
## 1524   16.97      6.3           98  48           101                 0
## 1525   52.63      5.0           81  43            92                 0
## 1526  321.74      5.9          162  61           120                 0
## 1527    3.86      6.6           96  53           114                 0
## 1528   13.64      9.1          107  41           131                 1
## 1529   13.48      3.4           97  35           356                 1
## 1530   22.85      8.3          125  60           135                 1
## 1531   16.00      4.6           99  77            70                 0
## 1532    4.91      4.0          102  49            73                 0
## 1533   14.07      4.7           94  79            42                 0
## 1534   10.95      5.2          122  68           131                 1
## 1535    7.52      6.5           96  68           112                 0
## 1536    4.55      6.3          105  37           147                 0
## 1537    5.05      9.4           99  40           106                 0
## 1538    4.36      6.5           98  41           143                 0
## 1539    4.62      8.3          101  42           197                 1
## 1540   13.53      5.4          102  72            64                 0
## 1541   75.85      7.8          117  60           139                 0
## 1542    6.61      5.9          105  59            66                 1
## 1543    4.67      4.8           94  35            92                 0
## 1544    8.93      3.4          138  89            86                 0
## 1545   28.74      7.4          130  46           209                 1
## 1546    7.98      4.8          107  45           105                 0
## 1547    3.06      4.3           89  30            90                 1
## 1548    4.55      6.3           84  43            81                 0
## 1549    2.07      9.9          110  42           145                 1
## 1550    5.00      5.4          113  58           127                 0
## 1551   11.29      5.5           95  58            54                 0
## 1552    2.67      5.3           99  51            46                 0
## 1553   26.45      4.2          127  40           146                 1
## 1554    5.35      5.0           98  90            78                 0
## 1555    5.30      8.3          125  65            86                 1
## 1556    4.47      2.9          123  82            62                 1
## 1557    4.72      4.6          116  46           105                 0
## 1558 5928.00      8.1          120  60           169                 1
## 1559   31.09      5.2          118  53           131                 0
## 1560   10.97      8.5           99  29           206                 1
## 1561   13.99      6.1           93  36           112                 1
## 1562   10.83      4.8           81  68            78                 0
## 1563   31.01      6.0          169  45           371                 1
## 1564    8.75      5.0          124  62            75                 0
## 1565    8.62      4.8          112  52           123                 0
## 1566    9.85      7.7          100  54           217                 0
## 1567   14.18      4.2           90  56           142                 0
## 1568   11.22      6.8           99  58           112                 0
## 1569    6.82      4.4           85  74            66                 0
## 1570    2.52      7.2           92  39            88                 0
## 1571    3.92      4.0          336  43           103                 1
## 1572    5.43      6.2          124  38            96                 1
## 1573    9.19      4.8          103  92           101                 0
## 1574   10.77      5.7           95  39           123                 1
## 1575    1.40      6.1           95  39           311                 0
## 1576    2.48      4.6          110  36           115                 0
## 1577    5.90      6.4           89  34           168                 0
## 1578    4.49      5.9           94  78            77                 0
## 1579   50.09      9.1          117  52           286                 1
## 1580    8.71      5.1           92  71           114                 0
## 1581    9.06      3.5           84  82            68                 0
## 1582  175.83      7.7          107  51           107                 0
## 1583    5.07      4.9           88  75            34                 0
## 1584   14.62      5.0           91  76            51                 0
## 1585   46.03      6.2           95  60            88                 0
## 1586    8.33      6.6          105  36           102                 1
## 1587    5.60      4.6           82  79            84                 0
## 1588    5.71      4.0           90  82            75                 0
## 1589   76.40      5.0          136  66            88                 0
## 1590   13.06      4.9           91  55            59                 0
## 1591  339.61     11.0          147  34           539                 1
## 1592    4.18      3.0           92  49            54                 0
## 1593   18.84      5.4          191  43            85                 1
## 1594    5.56      6.0          100  71            41                 0
## 1595    3.80      6.6          116  43            74                 0
## 1596   73.37      5.8          173  25           610                 1
## 1597   13.83      3.6           85  39           106                 0
## 1598    4.72      5.1           95  57            83                 0
## 1599   38.35      4.1          113  50            85                 1
## 1600    5.11      5.5           95  58           114                 0
## 1601    4.92      6.0          113  28           349                 1
## 1602    2.76      5.7           92  51            70                 0
## 1603    8.06      5.8           93  79            39                 0
## 1604   20.14      8.2          154  48           148                 1
## 1605    9.38      3.5          103  50           136                 0
## 1606    3.37      4.6          102  58            56                 0
## 1607   28.92      3.5           87  86            58                 0
## 1608   11.49      5.0          127  78           148                 1
## 1609    4.06      5.6           89  61            79                 0
## 1610    7.02      7.8           99  45           119                 0
## 1611   18.64      5.5          113  45           134                 0
## 1612   23.57      4.6           85  44            38                 0
## 1613    6.27      7.0          121  41           144                 0
## 1614   27.51      6.6          108  36           114                 1
## 1615    4.93      4.0           88  77            67                 0
## 1616    3.72      4.5           86  58           233                 0
## 1617   14.03      5.9           92  95           113                 0
## 1618    8.67      4.8           98  39            30                 0
## 1619    3.13      3.8           89  55            70                 0
## 1620    8.15      3.8          100  47           101                 0
## 1621    8.57      4.3           93  46            61                 0
## 1622   34.84      4.7          107  66            60                 0
## 1623    2.68      6.6          108  63            54                 0
## 1624    5.77      6.0          126  49           143                 0
## 1625   51.14      6.1          117  35           316                 1
## 1626    2.75      5.3           63  58            71                 0
## 1627   46.50      8.6           88  47           273                 0
## 1628    2.51      7.9           91  49           340                 0
## 1629   20.47      8.0          104  33           260                 1
## 1630    5.88      4.3          153  53            49                 0
## 1631   74.51      5.4          100  63           192                 1
## 1632   18.82      6.3          101  66            56                 0
## 1633    5.47      7.4          108  55           126                 0
## 1634   10.00      4.4           97  71            70                 0
## 1635   13.14      6.8          103  53           173                 0
## 1636    9.02      3.2           86  58            26                 0
## 1637   10.70      4.8           89  53            96                 0
## 1638    6.52      4.4           99  50           154                 1
## 1639    2.76      7.4          100  37           173                 1
## 1640   13.05      4.9          112  52           158                 1
## 1641    2.83      4.0           98  53           111                 0
## 1642    5.06      5.3           92  81            75                 0
## 1643   10.45      5.3           70  68           167                 0
## 1644   11.29      5.9          133  66           180                 1
## 1645    2.69      6.2          107  35           148                 0
## 1646   93.57      5.2          106  71           182                 1
## 1647   18.70      6.9          128  34           267                 1
## 1648    7.23      7.4          115  40           201                 1
## 1649   17.14      7.2          104  43           196                 1
## 1650   22.09      6.4          114  70           129                 1
## 1651    3.67      5.5          111  37           202                 1
## 1652   23.78      6.6           93  42           145                 0
## 1653   54.49      5.9           69  65            67                 0
## 1654    7.64      5.9          100  25           473                 1
## 1655    4.53      4.9           95  84            50                 0
## 1656   10.92      5.9          115  44           120                 1
## 1657    3.73      6.6           92  56            89                 0
## 1658   15.38      6.8           94  31           136                 1
## 1659   13.81      4.0           85  64            52                 0
## 1660   11.44      7.0          148  91            76                 1
## 1661   27.00      8.6          123  49           171                 1
## 1662    5.47      7.1          101  51            66                 0
## 1663    5.73      5.2          113  41           213                 0
## 1664    7.92      6.6          106  59            65                 0
## 1665    7.27      3.4           94  55           102                 0
## 1666    9.19      3.8          100  68            91                 0
## 1667   18.30      5.2          176  59            44                 1
## 1668    5.42      4.1           91  74           130                 0
## 1669    2.83      4.4          144  48           104                 0
## 1670   22.11      8.3          102  98            91                 0
## 1671    8.83      5.1           83  95            65                 0
## 1672   11.17      9.1           97  52            58                 0
## 1673   26.23      6.6          120  46           165                 1
## 1674   11.60      3.1           90  47            98                 0
## 1675    5.94      4.4          113  44           202                 1
## 1676    3.04      5.7          101  41           137                 0
## 1677    6.49      3.3           94  57            78                 0
## 1678    5.38      4.1          112  76            50                 1
## 1679   11.38      3.0           79  75           177                 0
## 1680    6.90      5.8           97  58            98                 0
## 1681   90.47     10.2          112  77           535                 1
## 1682   15.41      2.7           88  59            81                 0
## 1683    6.83      5.2           85  71            51                 0
## 1684    7.73      4.2           92  79            59                 0
## 1685  352.94      6.4          132  21           215                 1
## 1686    9.43      5.8           92  54            60                 0
## 1687   20.75      8.1          165  29           305                 1
## 1688    8.65      5.2          108  89            35                 0
## 1689    4.12      5.1           93  38           112                 0
## 1690    4.29      6.8           93  37           128                 0
## 1691    6.28      7.2          115  39           134                 1
## 1692    4.64      7.4           77  57            94                 0
## 1693    3.38      6.9           88  56            87                 0
## 1694    2.96      6.3          100  39           383                 1
## 1695    3.33      7.5          122  49            88                 1
## 1696    5.45      5.8           91  46           139                 0
## 1697   13.07      6.8          100  55           155                 1
## 1698    4.47      4.8          110  36           113                 1
## 1699    7.37      3.7           90  62           216                 0
## 1700    8.40      5.9          102  62            53                 0
## 1701   11.06      6.2          148  54           134                 1
## 1702    3.80      5.4           87  33            72                 0
## 1703    2.54      4.6           77  67            47                 0
## 1704    3.11      4.3           97  59           113                 0
## 1705    5.19      5.7          114  42           189                 1
## 1706    7.78      6.2          107  55           167                 1
## 1707    5.13      6.0          100  58            86                 0
## 1708    3.16      4.7           98  50            73                 0
## 1709    5.25      5.0           87  42           149                 0
## 1710    9.36      5.6          126  98            54                 1
## 1711    7.25      4.4          190  33           364                 1
## 1712    4.19      5.6           87  46           119                 0
## 1713  158.33      4.6          105  48           211                 1
## 1714   99.15      5.2          142  70            83                 1
## 1715    3.70      4.8          116  63            74                 0
## 1716    2.28      4.3          102  48           104                 0
## 1717   13.79      4.4           98  60            57                 0
## 1718   11.98      7.1           83  46           115                 0
## 1719   11.56      3.4           87  76            50                 0
## 1720   65.56      8.6          100  91            81                 0
## 1721    6.09      4.0           97  53           152                 0
## 1722    4.17      3.7          100  51            55                 1
## 1723    2.83      5.8           74  40           156                 1
## 1724    3.53      6.8          104  36           188                 1
## 1725    5.37      7.8          108  55           161                 1
## 1726    8.02      5.3          112  40           325                 1
## 1727    7.65      6.1          133  61            82                 1
## 1728   14.00      6.1          144  48           208                 1
## 1729   11.77      3.3           88  47            56                 0
## 1730    4.67      5.1           96  67            83                 0
## 1731    3.67      8.0          103  35           223                 1
## 1732    3.93      5.4           92  32           198                 1
## 1733    3.81      2.7           89  51           139                 0
## 1734    4.15      4.0           75  58            61                 0
## 1735    4.81      4.4           77  42           145                 0
## 1736    7.15      6.4           92  48           169                 0
## 1737    1.47      7.9          110  71           171                 1
## 1738  252.69      9.3           94  48           289                 1
## 1739   11.94      6.2          182  27           404                 1
## 1740    2.97      6.8          103  42           130                 0
## 1741   23.25      5.0          318  32           688                 1
## 1742    3.80      4.5           96  76           111                 0
## 1743    5.21      7.3           96  43           256                 0
## 1744    3.28      5.6          103  55            67                 0
## 1745    9.22      6.1          115  64            67                 1
## 1746    4.00      5.9          129  35            84                 0
## 1747    8.52      4.8           88  62           150                 0
## 1748    4.73      4.8          106  48           151                 0
## 1749   36.49      5.7          101  73           163                 1
## 1750    4.30      8.6          107  47           153                 1
## 1751   10.48      4.4          102  69            68                 0
## 1752    5.74      7.8          100  34           105                 0
## 1753    6.67      5.3          105  38           167                 1
## 1754   20.96      7.5           99  53           226                 1
## 1755    6.96      3.6           86  50           119                 0
## 1756    4.65      5.4          108  72            75                 0
## 1757    5.41      9.3           97  43            85                 0
## 1758   10.62      5.1           98  32           128                 0
## 1759    4.26      5.2          111  39           239                 1
## 1760   11.27      6.9          112  31           309                 1
## 1761    9.50      2.8          125  63           134                 1
## 1762    6.08      3.4           83  84           108                 0
## 1763    4.54      6.2          101  41           128                 0
## 1764   20.42      4.2           97  44            89                 0
## 1765   23.83      4.2           95  59           133                 0
## 1766    2.65      5.4           92  44            63                 0
## 1767   54.17      5.6           95  48           116                 0
## 1768    5.42      4.3          105  44            75                 1
## 1769    2.96      7.5           94  55           105                 0
## 1770   61.03      5.7          129  41           103                 0
## 1771    5.22      4.5           98  78            91                 0
## 1772    5.38      6.7          100  43            93                 0
## 1773    5.89      5.2           81  68            55                 0
## 1774    4.48      6.8          128  61            87                 0
## 1775    3.86      6.1           97  63            79                 0
## 1776    6.30      4.4           77  83            52                 0
## 1777    5.96      5.1          116  68           113                 0
## 1778   13.39      5.6          162  28           559                 1
## 1779    3.92      5.2          107  70            58                 0
## 1780    9.78      6.0          100  42           151                 0
## 1781    5.68      5.1           99  48            72                 0
## 1782    2.27      5.9           93  43            44                 0
## 1783   11.15      5.9          120  51           128                 0
## 1784    8.00      6.7           84  50           110                 1
## 1785    3.65      4.6          109  64           109                 0
## 1786  245.28      6.4          204  39           129                 1
## 1787    5.12      5.8           98  40           164                 1
## 1788    4.44      5.6           95  46           129                 0
## 1789    9.09      4.1           86  59            95                 0
## 1790    3.13      5.8           91  47           134                 1
## 1791   22.88     10.0           97  32           184                 1
## 1792    6.59      5.3          100  36           186                 1
## 1793    3.58      7.6          105  41           119                 0
## 1794    2.83      6.4          103  66            59                 0
## 1795    2.41      4.9          102  75            51                 0
## 1796  420.79      6.4          111  55            72                 0
## 1797   10.39      3.1           93  71            74                 0
## 1798   33.33      7.5           74  54            60                 0
## 1799    7.02      4.6           94  50            72                 0
## 1800    9.32      2.8           98  62            66                 0
## 1801    8.62      4.4           88  48            54                 0
## 1802    3.44      4.2           97  49           109                 0
## 1803   11.80      3.4          104  63           173                 1
## 1804    2.14      6.1          103  50            93                 0
## 1805   74.12      6.1          150  41           167                 1
## 1806    7.00      6.2          162  41           149                 1
## 1807    6.27      4.8           89  46            97                 0
## 1808    5.95      7.7           84  70           163                 0
## 1809   23.69      6.1           90  47           252                 1
## 1810   10.54      5.1           95  61           107                 0
## 1811    4.29      7.3          135  35           133                 1
## 1812  929.27      7.8          118  43            72                 1
## 1813   10.84      5.6           87  40            98                 0
## 1814    3.85      6.1           98  69            61                 0
## 1815    4.56      7.1           95  47           229                 1
## 1816    2.87      6.1           99  48            59                 0
## 1817  174.90      5.1          106  35           296                 1
## 1818    2.55      5.9           87  65            62                 0
## 1819   83.90      4.4          321  40           147                 1
## 1820    2.27      6.6          106  85            64                 1
## 1821    8.62      4.9          124  52            87                 1
## 1822    3.19      5.5           97  34           163                 0
## 1823   12.47      8.2          134  36            73                 1
## 1824    5.67      5.7           92  76            99                 0
## 1825    8.29      4.4           90  64            91                 0
## 1826   22.77      7.2          114  67           128                 1
## 1827    3.92      7.3           79  68            42                 0
## 1828    7.67      5.4           89  48            66                 0
## 1829   96.41      4.8          111  59            72                 0
## 1830    4.15      5.0          100  53            43                 0
## 1831    3.10      5.1           93  44            70                 0
## 1832    2.73      5.7           96  29            73                 0
## 1833   48.99      6.1           91 101            62                 0
## 1834    5.63      4.3           83  91            71                 0
## 1835    3.44      3.0           85  55            39                 0
## 1836    2.32      4.9          101  48           124                 1
## 1837   55.13      5.8          128  29           145                 1
## 1838   11.25      4.6          108  65           114                 0
## 1839    4.46      5.6          171  46            85                 0
## 1840    4.81      7.3           86  66            68                 0
## 1841    6.19      5.0           88  52           154                 0
## 1842    9.30      5.9          104  64           139                 0
## 1843   78.06      6.0           98  40            77                 0
## 1844   29.09      6.3          109  50            79                 1
## 1845    5.00      4.8           99  75           109                 0
## 1846    5.58      4.9          106  48           102                 1
## 1847    2.19      5.7           92  38           319                 1
## 1848    9.03      4.7           99  45           144                 0
## 1849   34.70      7.7           97  30           362                 0
## 1850    3.63      7.0          109  53            57                 0
## 1851    7.31      5.1           97  58            75                 0
## 1852    8.37      3.2           99  61           184                 1
## 1853   87.12      7.2          110 108            52                 0
## 1854    7.13      5.3          102  68            52                 0
## 1855    3.09      6.6           96  50            53                 0
## 1856    3.16      4.9           89  48            67                 0
## 1857   20.37      5.0           85  60           136                 0
## 1858   90.34      5.1          240  34           244                 1
## 1859    7.70      5.0           95  59            76                 0
## 1860   44.91      9.2          156  31           110                 1
## 1861   15.97      5.1           92  69            39                 0
## 1862    6.47      6.0          241  44           132                 1
## 1863    6.17      3.7          100  43            59                 1
## 1864    4.46      7.1           97  83           114                 0
## 1865    6.23      6.3           99  39           208                 0
## 1866   13.91      6.4          107  54           126                 0
## 1867   12.78      3.6           80  50            58                 0
## 1868    4.27      5.0          112  62            87                 1
## 1869  104.55      3.8           98  57            39                 0
## 1870    3.32      5.4           85  48            53                 0
## 1871    4.88      6.4          110  63           141                 0
## 1872    6.95      4.6           97  60           105                 0
## 1873    3.95      3.8           97  49            44                 0
## 1874    3.80      4.8          107  45           140                 1
## 1875   23.33      6.2          109  51           235                 1
## 1876   20.53      5.1           79  67            30                 0
## 1877    8.69      4.7           89  36            52                 0
## 1878    4.25      6.4          104  37           291                 1
## 1879    5.15      7.0          105  51           180                 1
## 1880    2.50      2.3          106  41           179                 1
## 1881    4.96      4.8           99  92            82                 0
## 1882    4.85      3.4           91  96            96                 0
## 1883    2.92      6.3           96  26           150                 1
## 1884   12.61      4.2           78  65           242                 0
## 1885   76.55      6.2           87  56            80                 0
## 1886    3.19      4.3           82  44            71                 0
## 1887    8.57      2.8           93  39            64                 0
## 1888  108.33      5.8          111  57           124                 1
## 1889   30.49      4.7           88  40            85                 0
## 1890    6.28      3.8           99  67            51                 0
## 1891   16.57      4.4          112  62            54                 0
## 1892    7.82      5.6          120  55           180                 0
## 1893    8.09      6.3          104  94           101                 0
## 1894   12.50      5.6          155  43           136                 0
## 1895   46.98      8.1          130  39           216                 1
## 1896    5.32      6.5          116  53           121                 0
## 1897    6.60      4.7           71  71            68                 0
## 1898    4.21      4.6           88  58           174                 0
## 1899    5.13      4.2          101  39           101                 1
## 1900    7.79      6.9          105  62           106                 0
## 1901   10.83      7.9          115  45           258                 1
## 1902    7.61      3.8           85  71            42                 0
## 1903    4.50      6.2           90  53            56                 0
## 1904    7.43      6.9          112  47           147                 0
## 1905   14.15      4.5           93  94            89                 0
## 1906    4.05      3.9           98  53           102                 0
## 1907   78.70      6.1          125  33           127                 0
## 1908    6.94      4.7           80  65            86                 0
## 1909    4.58      5.8           90  43            58                 0
## 1910    3.19      5.3          103  52            34                 0
## 1911    4.12      3.9          113  38           481                 1
## 1912    8.40      6.3          139  50           203                 1
## 1913  151.28      5.6          115  35           129                 1
## 1914    7.60      6.1           89  66            52                 0
## 1915    7.14      4.3          147  60           102                 0
## 1916   35.33      3.6           90  40            59                 0
## 1917    7.22      4.7           83  75            46                 0
## 1918   44.69      5.6          109  43           166                 1
## 1919   28.20      4.9          106  59           131                 0
## 1920   11.39      4.6           83  61            97                 0
## 1921   14.58      5.2           84  53           274                 0
## 1922    5.56      3.3           91  65            93                 0
## 1923    4.81      4.6          156  43           117                 1
## 1924    2.63      5.0           83  68            65                 0
## 1925   12.47      4.3          277  31           172                 1
## 1926    7.76      5.2          103  52           169                 1
## 1927    6.00      3.3           93  66            60                 0
## 1928   55.56      5.4          224  46           220                 1
## 1929   11.94      3.9           98  50           164                 1
## 1930    5.00      4.9           92  40           167                 1
## 1931   16.57      6.8          116  45           210                 1
## 1932   23.96      5.1          125  61            85                 1
## 1933    5.38      3.2           99  47            40                 0
## 1934    3.45      4.5           94  57           112                 0
## 1935   26.45      3.6           94  61            71                 0
## 1936    4.24      3.5           90  44            95                 0
## 1937    8.36      5.2          104  54            59                 0
## 1938    2.90      4.6           94  44            64                 0
## 1939    5.09      5.1           99  54           167                 0
## 1940    3.84      5.8          102  45           133                 0
## 1941    8.63      5.9           96  47           235                 0
## 1942   37.20      3.6          101  74            60                 0
## 1943    8.93      5.8          102  46           113                 1
## 1944    3.91      6.1          108  52           175                 1
## 1945    3.75      6.5          105  33           320                 1
## 1946   22.22      3.8           94  65            84                 0
## 1947    3.08      5.7          107  57            77                 0
## 1948    4.41      5.9          128  42           285                 1
## 1949    9.18      5.3          172  38           144                 1
## 1950    7.44      4.2           94  56            67                 0
## 1951    3.81      4.6           83  88            26                 0
## 1952   37.98      4.1           80  90           217                 0
## 1953    3.56      3.3           72  61            48                 0
## 1954    7.89      7.2          120  46           241                 1
## 1955   21.05      5.9          119  50           189                 1
## 1956   10.00      4.3           98  57            55                 0
## 1957   22.03      3.5           94  54            74                 0
## 1958   26.00      3.9          102  68            89                 0
## 1959    8.15      5.0          102  72           114                 0
## 1960    8.47      5.2          115  56           120                 1
## 1961    6.72      4.9           92  76            40                 0
## 1962    5.32      4.0           89  45            99                 0
## 1963    3.29      7.7           98  49           219                 0
## 1964    3.48      5.6           80  35           462                 0
## 1965   11.30      4.3          102  61            85                 0
## 1966    8.06      5.8          113  69           102                 0
## 1967    4.05      3.9          100  56           231                 0
## 1968   58.16      6.9          106  46           103                 0
## 1969    4.29      5.5          106  67            58                 0
## 1970    7.48      6.7           93  46           122                 0
## 1971   17.12      4.0           89  38            65                 0
## 1972    3.43      5.9           91  68            44                 0
## 1973   11.11      5.2           92  61           101                 0
## 1974   50.00      4.6          108  60           109                 0
## 1975   11.35      4.5          101  73            63                 0
## 1976    5.71      5.7          109  40           272                 1
## 1977    7.41      8.3          111  36           382                 1
## 1978   10.00      5.0          104  36           103                 1
## 1979    2.62      3.8           89  50            80                 0
## 1980   47.09      3.9          219  32           666                 1
## 1981    6.97      4.4           93  40            94                 0
## 1982    2.69      5.7          105  53            55                 0
## 1983    4.09      6.6           98  41           226                 0
## 1984    8.55      3.0           98  52           145                 0
## 1985  305.59      4.0          100  42           188                 1
## 1986   29.82      7.2           93  47           138                 0
## 1987    2.10      8.9          100  36           210                 1
## 1988   12.25      4.6           97  53            44                 0
## 1989    4.64      4.5           94  46            62                 0
## 1990    7.18      3.8           95  32           170                 1
## 1991   44.12      4.4           98  62            64                 0
## 1992    8.06      6.2          109  48            87                 1
## 1993    7.71      2.5          103  69            91                 1
## 1994    4.27      4.6          104  57            94                 0
## 1995    7.54      4.5          123  56           114                 0
## 1996    4.33      8.6          106  30           307                 1
## 1997    6.11      4.0           93  71            47                 0
## 1998    4.29      5.3           82  65           113                 0
## 1999    4.55      5.2           90  46            89                 0
## 2000   17.10      5.0          105  78            98                 0
## 2001    8.83      6.3           96  44            83                 0
## 2002    4.43      5.0           95  31           118                 0
## 2003  100.57      9.5          105  73           180                 1
## 2004    3.54      5.7           93  34           149                 0
## 2005    5.95      5.9          111  53           173                 1
## 2006    4.35      5.7          104  51           350                 1
## 2007    2.99      6.8           88  63            62                 0
## 2008    8.18      5.3          107  33           345                 1
## 2009    4.69      6.3           83  62           180                 1
## 2010    5.29      6.7          100  45           134                 0
## 2011  140.89      5.5          101  59            42                 0
## 2012  348.74      7.3          146  83           222                 0
## 2013   16.49      8.5          145  30           180                 1
## 2014    4.56      6.4          107  42           274                 1
## 2015    5.92      3.8           99  48           168                 1
## 2016   99.07      9.9          126  33           124                 1
## 2017    5.38      6.9          135  38           228                 1
## 2018   32.09      8.0          195  31           245                 1
## 2019   10.87      2.9           90  89           106                 0
## 2020   37.17      5.6           81  69           185                 1
## 2021    9.32      7.9           84 108           239                 0
## 2022    3.97      6.6           99  55            86                 0
## 2023    2.63      7.4          105  42           117                 0
## 2024 2047.17      8.4          126  63            95                 1
## 2025   33.78      6.0          107  85           112                 0
## 2026    7.73      3.4           90  43           111                 0
## 2027   10.78      6.7           95  69           146                 0
## 2028 2403.85      8.1          159  35           105                 1
## 2029    5.16      6.5          120  41           139                 0
## 2030    4.34      6.6          141  45           110                 0
## 2031    4.55      4.7          108  52           157                 1
## 2032    4.58      4.9          104  53           115                 0
## 2033    2.27      5.9           82  45           140                 0
## 2034   11.54      4.4           98  80            60                 0
## 2035    7.21      5.5          101  49            64                 0
## 2036   12.12      5.7           88  97           103                 0
## 2037    4.36      4.5           88  53           141                 0
## 2038    3.27      6.0           92  43           141                 0
## 2039   10.52      5.8           96  43           275                 0
## 2040    3.42      5.9           92  61            58                 0
## 2041   13.70      4.0          109  65            76                 1
## 2042   14.53      5.8          162  57            43                 0
## 2043    5.81      5.1          102  44           145                 1
## 2044  560.87      5.1          134  39            67                 1
## 2045   49.12      3.6           99  83            45                 0
## 2046   26.41      4.3           91  69            45                 0
## 2047    6.42      7.2          104  42           222                 1
## 2048    9.20      4.5           88  65            55                 0
## 2049    7.38      4.9          122  30            79                 1
## 2050    6.80      4.6          111  69           149                 0
## 2051    8.44      3.9          102  45           147                 0
## 2052    8.59      5.1          110  62           108                 1
## 2053   19.27      5.8          103  73            71                 0
## 2054    2.44      4.7          109  62           156                 1
## 2055    2.00      6.4           88  30           127                 0
## 2056    7.56      5.1          100  63            85                 0
## 2057    5.17      9.9          103  31           259                 1
## 2058   10.34     10.0          108  44            78                 1
## 2059    6.78      5.1           98  51           196                 0
## 2060    3.24      5.5          103  55            75                 1
## 2061    8.62      5.0          223  51            85                 0
## 2062    6.34      8.0          127  36           174                 1
## 2063    8.17      5.0          127  46           145                 1
## 2064    7.40      6.5          115  37            99                 1
## 2065    3.78      6.1           96  42            90                 0
## 2066   10.06      5.5          119  40           189                 1
## 2067    3.41      6.5          144  24           526                 1
## 2068    6.18      4.4          107  53           106                 0
## 2069    4.12      4.4           84  63            41                 0
## 2070  108.33      7.9          225  53           151                 0
## 2071 4462.81      7.4          110  79            91                 0
## 2072    6.64      7.0          100  50            58                 0
## 2073   26.01      4.0           87  64           102                 0
## 2074   16.14      6.1          114  83            60                 0
## 2075   11.09      3.4           96  54            63                 0
## 2076    7.02      4.6          124  48            75                 0
## 2077    3.00      5.4           91  52           700                 0
## 2078    6.88      5.6          106  56           250                 1
## 2079    4.72      4.0           91  75            57                 0
## 2080   47.95      6.6           93  41           123                 0
## 2081    4.05      6.5           93  43            95                 0
## 2082    9.78      5.9          105  42           159                 1
## 2083    3.02      7.8          116  48           269                 1
## 2084    4.19      3.6           89  42           107                 0
## 2085    9.66      5.0           86 125            62                 0
## 2086   17.73      5.1           98  53            82                 0
## 2087    8.29      4.2           89  65           107                 0
## 2088    6.89      3.7           91  36           165                 0
## 2089   11.68      2.9           89  43           162                 1
## 2090   23.25      4.7          130  54           115                 0
## 2091    4.14      6.9           93  80            77                 0
## 2092    6.76      5.8           91  83            55                 0
## 2093   23.28      6.5           75  27          1562                 1
## 2094    3.10      5.6           98  42           208                 0
## 2095    9.19      4.2           87  72           112                 0
## 2096    6.16      7.0          142  41           336                 1
## 2097    9.88      5.7          110  58           149                 0
## 2098   45.75      3.8           92  54           151                 0
## 2099   26.31      8.0          220  43           116                 0
## 2100    3.14      6.7          111  34           265                 1
## 2101   11.43      6.8          109  50            66                 0
## 2102    8.06      4.9          112  37           145                 1
## 2103   35.87      5.0           97  54           115                 0
## 2104    6.00      3.5           87  90            31                 0
## 2105    6.55      5.3          244  38           127                 1
## 2106   25.24      4.8          172  51           124                 1
## 2107    3.25      5.4           95  38           166                 1
## 2108   25.76      6.2           97  48           108                 1
## 2109    4.14      5.2           94  60            93                 0
## 2110    8.09      4.4           99  42           108                 0
## 2111   15.18      3.3          141  51           117                 0
## 2112    3.51      6.1           91  65            52                 0
## 2113    3.28      5.1           90  54            55                 0
## 2114    3.59      4.6          102  49           106                 1
## 2115   10.30      4.2           86  94            57                 0
## 2116   49.28      8.9          115  36            87                 1
## 2117   10.86      4.6          160  59           159                 1
## 2118   44.42      5.6          111  68            54                 1
## 2119    6.16      6.6           99  70            73                 0
## 2120    4.26      4.0           91  51           180                 0
## 2121   13.47      3.8           87  55            71                 0
## 2122   30.27      6.8           96  37           106                 0
## 2123    5.00      5.3           92  35           288                 1
## 2124    8.57      5.2          102  44           138                 0
## 2125  153.85      5.9          133  42           157                 1
## 2126    5.36      4.7          102  52           140                 0
## 2127    7.07      5.3          102  58            86                 0
## 2128   80.00      4.0          293  33           476                 1
## 2129   26.54      8.9           91  57            92                 0
## 2130    4.06      5.5          122  34           101                 1
## 2131    3.82      3.1          106  56            80                 0
## 2132    7.33      5.3           98  80            89                 0
## 2133    6.64      5.5          147  47            78                 1
## 2134    6.41      7.3          102  48           149                 0
## 2135    3.71      6.3           94  52            92                 0
## 2136   10.00      3.5           94  54            92                 0
## 2137    2.16      5.6           92  50            76                 0
## 2138 1016.67      4.9          102  48           114                 1
## 2139    4.74      7.3          110  42           511                 1
## 2140    1.80      6.5          111  39            80                 0
## 2141    6.90      3.2           83  61            38                 0
## 2142    3.08      5.0          112  61            91                 0
## 2143    3.43      6.5          119  39           120                 1
## 2144   58.62      8.2           84  38            95                 0
## 2145    8.57      3.4           80  95           106                 0
## 2146    6.91      4.1           84  55            91                 0
## 2147    2.83      3.3          108  47            89                 1
## 2148   36.46      6.3          102  77            45                 0
## 2149   49.63      4.1          107  61            85                 0
## 2150    4.00      5.9          104  55            63                 0
## 2151    4.58      5.9          116  34           439                 1
## 2152    4.53      5.8           98  64           125                 0
## 2153    4.56      5.6          121  44           138                 0
## 2154    6.45      6.7           97  39            76                 0
## 2155  359.09      7.1          113  61            69                 1
## 2156    4.76      9.2          122  46           166                 1
## 2157    9.39      5.8           80  58            87                 0
## 2158   11.57      5.9          101  45           146                 1
## 2159  716.51      5.5           87 121            55                 0
## 2160  531.48      6.5           88  69           117                 0
## 2161   10.00      6.1           97  64            94                 0
## 2162    5.06      4.4           85  52            67                 0
## 2163   36.46      4.4          101  70            65                 0
## 2164    5.15      6.9           93  59           149                 0
## 2165    3.82      3.8           92  63            87                 0
## 2166    6.35      5.6           91  40           461                 0
## 2167    2.16      5.7           99  47            76                 0
## 2168    3.33      4.1          104  76           131                 0
## 2169    3.01      6.2           99  48            84                 0
## 2170    3.42      4.5          100  51           142                 0
## 2171   16.25      5.0           91  91            58                 0
## 2172    6.02      5.2           97  49            88                 0
## 2173   15.00      5.8           84  44           213                 1
## 2174    8.27      7.8          114  43           153                 1
## 2175    2.08      6.7           98  38           118                 0
## 2176   28.22      9.5          110  85            94                 0
## 2177    5.91      8.4          101  40           167                 1
## 2178    8.04      5.6           93  50           104                 0
## 2179   32.72      6.7          105  21           244                 1
## 2180    4.53      5.1          108  55            70                 0
## 2181    4.14      5.8          100  50            93                 0
## 2182    4.62      6.2           87  61           129                 0
## 2183  118.82      5.0          100  53            87                 1
## 2184   64.17      5.8          118  37            70                 1
## 2185    5.26      6.2           98  47           100                 0
## 2186    5.12      3.6           93  73            92                 0
## 2187    2.97      5.5           98  78            50                 0
## 2188    8.09      4.6          103  98            78                 0
## 2189   52.59      8.0          115  30           295                 1
## 2190    6.10      7.6          101  40            97                 0
## 2191    6.37      7.8          102  45           135                 0
## 2192   16.64      3.0           89  62            77                 0
## 2193    8.55      6.3          108  38           180                 1
## 2194   21.30      5.3          130  26           190                 1
## 2195   10.58      5.8           90  46           105                 0
## 2196    3.17      6.4           98  39           164                 1
## 2197 3500.00      8.1          128  29           814                 1
## 2198   13.43      7.3          107  47           112                 1
## 2199   14.19      2.1           99  53            69                 0
## 2200    6.62      4.1          100  63           138                 0
## 2201    4.24      7.1          109  83            94                 1
## 2202    6.86      4.4          106  50           152                 1
## 2203    5.26      6.2          132  47           109                 1
## 2204    8.05      4.6           97  77            84                 0
## 2205   16.67      5.4          115  53           133                 1
## 2206   32.36      3.4          297  38           303                 1
## 2207    8.73      5.2           99  41            81                 0
## 2208    3.73      5.3           91  57            83                 0
## 2209   13.28      4.4           92  60            78                 0
## 2210    3.33      7.7           95  44           277                 1
## 2211    9.95      3.2          169  53            99                 0
## 2212   17.50      4.3           86  52            71                 0
## 2213    5.43      5.2          100  54            95                 0
## 2214   72.50      7.5          141  42           134                 1
## 2215   33.97      4.6           97  66           130                 0
## 2216   12.70      3.4           97  50            32                 0
## 2217    3.03      5.7           98  53            37                 0
## 2218    4.63      3.7           98  46            70                 0
## 2219   12.73      3.0           99  84            82                 0
## 2220   12.08      3.4           81  65           134                 0
## 2221   97.88      2.9          382  42           490                 1
## 2222    5.84      6.0           96  51            75                 0
## 2223   11.85      5.1           97  99            61                 0
## 2224  112.06      6.2           83  35           240                 0
## 2225    2.18      7.3          105  53            92                 0
## 2226    6.81      4.7           84  68            98                 0
## 2227    5.00      6.0           85  90            42                 0
## 2228    2.83      5.2          100  77            72                 0
## 2229    6.24      5.0           83  55            41                 0
## 2230    3.74      5.2          109  62           119                 0
## 2231    3.14      5.4          102  49           111                 0
## 2232    4.15      7.8           90  41           191                 1
## 2233    2.78      5.4           86  60            71                 0
## 2234    3.40      5.7           94  71            44                 0
## 2235    3.63      7.5           89  54            82                 0
## 2236   12.34      5.4           93  47           125                 0
## 2237    5.00      5.5           98  68            39                 0
## 2238    3.67      6.6           99  47           135                 0
## 2239    2.94      4.9          100  48           106                 0
## 2240    7.58      4.9          102  69            98                 0
## 2241    8.59      5.8           81  56           126                 0
## 2242    5.68      4.8          106  63           126                 0
## 2243    4.44      3.4          102  64            47                 0
## 2244    5.83      3.3           98  67            95                 0
## 2245    6.09      5.2           93  34           137                 0
## 2246   30.25      7.8          112  53            70                 0
## 2247   12.99      3.4           89  30           200                 0
## 2248    6.60      4.3          107  64           101                 0
## 2249    2.42      5.7           94  39           229                 1
## 2250    4.90      5.3           97  41            75                 0
## 2251    3.07      5.2           81  59           106                 0
## 2252    8.55      3.7           94  64            55                 0
## 2253    4.76      3.9           91  64            76                 0
## 2254    3.04      6.2           85  46            62                 0
## 2255   20.00      5.0          123  49            55                 0
## 2256    6.67      6.0           91  31           309                 1
## 2257    8.40      5.5          128  50            71                 1
## 2258    6.67      5.2          109  52           102                 1
## 2259    3.97      5.3           94  50           138                 0
## 2260    3.51      6.3          100  40           104                 1
## 2261    5.91      5.3           97  65            67                 0
## 2262    7.41      5.6          145  59            84                 0
## 2263    4.03      6.6          107  40           141                 1
## 2264    5.93      5.7          108  44           114                 0
## 2265   48.89      5.3          100  51           118                 1
## 2266    6.67      6.0           97  48            82                 0
## 2267   16.36      5.1           96  53           179                 0
## 2268    2.69      5.8          105  65            55                 0
## 2269   22.92      4.8           95  34           156                 1
## 2270   22.54      6.1          101  40           182                 1
## 2271    8.26      5.7           98  48           153                 1
## 2272    2.65      7.5           97  35           267                 0
## 2273    4.13      4.9           89  52            86                 0
## 2274    5.79      4.3          103  52           129                 0
## 2275    7.55      5.4          104  27           101                 0
## 2276    4.64      4.8          100  50            76                 0
## 2277   14.69      5.1          102  56           156                 1
## 2278    2.73      5.9          106  52           100                 1
## 2279   13.51      6.2           92  72           131                 0
## 2280    5.82      5.4          109  36           156                 1
## 2281   31.03      6.4          287  41           147                 1
## 2282    4.20      4.8           95  61            47                 0
## 2283   10.55      8.7           99  42            86                 0
## 2284    2.88      5.6          102  48           181                 0
## 2285    7.44      9.0          104  65            60                 0
## 2286    5.14      4.5           85  52            67                 0
## 2287    7.20      4.4          105  74            34                 0
## 2288    3.24      4.5           88  72            45                 0
## 2289    4.83      6.7           97  38           489                 1
## 2290  146.81      5.6           93  95            41                 0
## 2291    3.01      6.9           66  79            50                 0
## 2292  224.32      6.3          123  67           192                 1
## 2293    4.71      4.0           90  58            83                 0
## 2294    4.58      4.4           89  49           140                 0
## 2295    3.19      4.5          101  57            53                 0
## 2296    2.99      5.2           96  42           148                 0
## 2297   10.00      7.4          103  52           138                 1
## 2298    4.83      5.2           90  56            31                 0
## 2299    8.78      4.9          141  62           101                 1
## 2300    4.02      8.5           94  42            77                 0
## 2301   28.24      5.5           97  62           146                 0
## 2302    9.86      5.2          182  64            93                 0
## 2303    5.42      5.4          104  51            90                 0
## 2304    7.88      4.4           98  84           152                 0
## 2305  167.74      5.1           88  54            78                 0
## 2306   20.84      6.3          102  56           182                 1
## 2307  152.24      6.6          121  58           151                 1
## 2308    5.44      6.9          208  37           231                 1
## 2309   30.00      3.8          128  42           139                 1
## 2310    4.26      4.3           72  77            52                 0
## 2311    1.76      6.3           86  53            59                 0
## 2312   15.68      5.3           94  94           163                 0
## 2313    5.36      2.9           92  72            46                 0
## 2314    3.44      4.4           86 104           133                 0
## 2315    5.06      6.0          130  44           107                 1
## 2316    2.82      5.6          131  53           109                 1
## 2317    7.32      4.5           88  70            76                 0
## 2318   44.95      8.8          115  52            79                 1
## 2319    2.73      6.7           95  51            68                 0
## 2320    3.48      3.7           95  62            69                 0
## 2321    2.60      7.0           98  44           147                 0
## 2322   10.56      5.1          102  75            42                 1
## 2323   11.05      5.4           95  63           267                 0
## 2324    3.37      5.5           85  47           144                 0
## 2325  117.65      5.5           96  55            63                 0
## 2326   21.40      3.5          366  65           117                 0
## 2327   31.19      3.9           90  54            55                 0
## 2328    1.67      4.0           86  59            64                 0
## 2329   21.79      4.7           97  72            98                 0
## 2330    6.22      5.4           90  47           157                 0
## 2331    8.11      4.4           86  77            67                 0
## 2332    3.96      7.1          101  31           400                 1
## 2333    6.31      5.8           84  51            88                 0
## 2334    3.42      5.8          106 114            75                 0
## 2335    7.31      7.6          107  51            94                 1
## 2336    4.68      7.0          107  63            84                 0
## 2337   10.04      8.0          106  74           117                 1
## 2338    4.13      4.6           99  49            80                 0
## 2339    5.86      5.0          106  80            35                 0
## 2340   34.41      6.4          126  93            59                 1
## 2341    9.40      6.4          105  38            98                 1
## 2342    4.18      4.7           98  39           147                 1
## 2343    4.69      4.0           87  73           101                 0
## 2344   44.75      5.4          142  26           607                 1
## 2345    4.47      8.2          106  39            92                 1
## 2346   20.12      2.5           75  51            99                 0
## 2347    3.11      6.3           96  40            87                 0
## 2348    6.02      3.4           87  53           107                 0
## 2349   56.76      5.9          121  33           133                 1
## 2350   14.81      3.3           89  61            53                 0
## 2351    5.33      5.0           97  53           174                 0
## 2352   12.73      3.9          309  37           175                 1
## 2353   18.00      2.2          100  83            60                 0
## 2354   20.67      5.1           85  62           198                 0
## 2355    7.88      7.3           92  73            73                 0
## 2356    2.63      7.0          100  37           216                 1
## 2357    4.57      4.1           96  59            62                 0
## 2358    5.00      5.8           85  76            82                 0
## 2359    4.20      6.1           94  39           123                 0
## 2360    8.92      6.4           95  43           100                 0
## 2361   76.63      5.0          121  66            52                 1
## 2362    4.41      3.5           92  51            46                 0
## 2363    4.48      6.7          106  44            72                 1
## 2364    7.94      4.4           86  52            70                 0
## 2365    6.06      6.0          100  43            70                 1
## 2366   59.70      6.5          276  42           298                 1
## 2367    6.65      6.4          124  53           195                 1
## 2368    3.70      4.9           93  74            56                 0
## 2369  181.82      8.4          129  42           196                 1
## 2370   21.54      4.7           84  51            94                 0
## 2371    5.75      6.6           96  37           215                 0
## 2372    4.39      8.3          101  40           111                 1
## 2373    7.98      6.1          112  52           229                 1
## 2374   33.75      5.0          117  57           109                 1
## 2375   10.12      4.6          110  48            91                 1
## 2376    4.21      6.0           93  78            64                 0
## 2377    9.75      4.1          100  44           162                 1
## 2378   12.22      4.1          106  44           182                 1
## 2379    4.87      5.5          103  42            74                 1
## 2380    3.63      5.0          292  31           373                 1
## 2381    2.40      7.3          107  56           104                 1
## 2382    9.29      3.9           95  75            30                 0
## 2383    5.50      4.1           92  60            89                 0
## 2384    9.81      7.8           94  50            95                 0
## 2385    7.76      5.8           98  53            86                 0
## 2386    5.17      4.0           88  60            35                 0
## 2387    3.08      4.6          112  47            52                 0
## 2388    3.83      7.3          105  34           144                 1
## 2389    3.61      6.7           91  34           101                 0
## 2390   71.84      6.0          135  39           105                 1
## 2391    3.03      6.5          111  48           105                 0
## 2392    2.91      5.3           95  61            51                 0
## 2393    5.15      5.6           96  60            75                 0
## 2394    5.39      3.2           96  65           144                 0
## 2395    2.00      6.7           95  64            81                 0
## 2396    5.51      6.7          114  49           165                 1
## 2397   22.11      5.8          152  57           107                 0
## 2398    2.90      7.9           91  90            91                 0
## 2399    2.78      6.2           99  47            84                 0
## 2400    4.15      6.2          100  41           124                 1
## 2401   12.82      5.2           91  36           226                 1
#Checking the missing values
col_missing <- colSums(is.na(df))
col_missing
##              seqn               Age               Sex           Marital 
##                 0                 0                 0                 0 
##            Income              Race         WaistCirc               BMI 
##               117                 0                85                26 
##       Albuminuria           UrAlbCr          UricAcid      BloodGlucose 
##                 0                 0                 0                 0 
##               HDL     Triglycerides MetabolicSyndrome 
##                 0                 0                 0
#Dropping Un-necessary columns
Metabolic_Syndrome<-select(df, -c(WaistCirc, Albuminuria, UrAlbCr, Marital, Triglycerides, Income))
head(Metabolic_Syndrome)
##    seqn Age    Sex  Race  BMI UricAcid BloodGlucose HDL MetabolicSyndrome
## 1 62161  22   Male White 23.3      4.9           92  41                 0
## 2 62164  44 Female White 23.2      4.5           82  28                 0
## 3 62169  21   Male Asian 20.1      5.4          107  43                 0
## 4 62172  43 Female Black 33.3      5.0          104  73                 0
## 5 62177  51   Male Asian 20.1      5.0           95  43                 0
## 6 62178  80   Male White 28.5      4.8          105  47                 0
summary(Metabolic_Syndrome)
##       seqn            Age            Sex                Race          
##  Min.   :62161   Min.   :20.00   Length:2401        Length:2401       
##  1st Qu.:64591   1st Qu.:34.00   Class :character   Class :character  
##  Median :67059   Median :48.00   Mode  :character   Mode  :character  
##  Mean   :67031   Mean   :48.69                                        
##  3rd Qu.:69495   3rd Qu.:63.00                                        
##  Max.   :71915   Max.   :80.00                                        
##                                                                       
##       BMI          UricAcid       BloodGlucose        HDL        
##  Min.   :13.4   Min.   : 1.800   Min.   : 39.0   Min.   : 14.00  
##  1st Qu.:24.0   1st Qu.: 4.500   1st Qu.: 92.0   1st Qu.: 43.00  
##  Median :27.7   Median : 5.400   Median : 99.0   Median : 51.00  
##  Mean   :28.7   Mean   : 5.489   Mean   :108.2   Mean   : 53.37  
##  3rd Qu.:32.1   3rd Qu.: 6.400   3rd Qu.:110.0   3rd Qu.: 62.00  
##  Max.   :68.7   Max.   :11.300   Max.   :382.0   Max.   :156.00  
##  NA's   :26                                                      
##  MetabolicSyndrome
##  Min.   :0.0000   
##  1st Qu.:0.0000   
##  Median :0.0000   
##  Mean   :0.3424   
##  3rd Qu.:1.0000   
##  Max.   :1.0000   
## 
#PREPROCESSING (Only BMI has 26 null values)
Metabolic_Syndrome <- Metabolic_Syndrome[!is.na(Metabolic_Syndrome$BMI), ]
summary(Metabolic_Syndrome)
##       seqn            Age            Sex                Race          
##  Min.   :62161   Min.   :20.00   Length:2375        Length:2375       
##  1st Qu.:64563   1st Qu.:34.00   Class :character   Class :character  
##  Median :67058   Median :48.00   Mode  :character   Mode  :character  
##  Mean   :67028   Mean   :48.67                                        
##  3rd Qu.:69501   3rd Qu.:63.00                                        
##  Max.   :71915   Max.   :80.00                                        
##       BMI          UricAcid       BloodGlucose        HDL        
##  Min.   :13.4   Min.   : 1.800   Min.   : 39.0   Min.   : 14.00  
##  1st Qu.:24.0   1st Qu.: 4.500   1st Qu.: 92.0   1st Qu.: 43.00  
##  Median :27.7   Median : 5.400   Median :100.0   Median : 51.00  
##  Mean   :28.7   Mean   : 5.481   Mean   :108.3   Mean   : 53.36  
##  3rd Qu.:32.1   3rd Qu.: 6.400   3rd Qu.:110.0   3rd Qu.: 62.00  
##  Max.   :68.7   Max.   :11.300   Max.   :382.0   Max.   :156.00  
##  MetabolicSyndrome
##  Min.   :0.000    
##  1st Qu.:0.000    
##  Median :0.000    
##  Mean   :0.344    
##  3rd Qu.:1.000    
##  Max.   :1.000
#COUNT OF NUMBER OF ROWS
nrow(Metabolic_Syndrome)
## [1] 2375
#TYPE OF DATA
str(Metabolic_Syndrome)
## 'data.frame':    2375 obs. of  9 variables:
##  $ seqn             : int  62161 62164 62169 62172 62177 62178 62184 62189 62195 62199 ...
##  $ Age              : int  22 44 21 43 51 80 26 30 35 57 ...
##  $ Sex              : chr  "Male" "Female" "Male" "Female" ...
##  $ Race             : chr  "White" "White" "Asian" "Black" ...
##  $ BMI              : num  23.3 23.2 20.1 33.3 20.1 28.5 22.1 22.4 28.2 28 ...
##  $ UricAcid         : num  4.9 4.5 5.4 5 5 4.8 5.4 6.7 6.7 6 ...
##  $ BloodGlucose     : int  92 82 107 104 95 105 87 83 94 100 ...
##  $ HDL              : int  41 28 43 73 43 47 61 48 46 35 ...
##  $ MetabolicSyndrome: int  0 0 0 0 0 0 0 0 0 1 ...
# Assuming 'Metabolic_Syndrome' is the name of your dataset

# Boxplot for Age
boxplot(Metabolic_Syndrome$Age,
        main = "Boxplot of Age",
        ylab = "Age",
        col = "lightblue",
        border = "black"
)
 
# Boxplot for Blood Glucose Level
boxplot(Metabolic_Syndrome$BloodGlucose,
        main = "Boxplot of Blood Glucose",
        ylab = "Blood Glucose ",
        col = "lightgreen",
        border = "black"
)
 
# Boxplot for BMI
boxplot(Metabolic_Syndrome$BMI,
        main = "Boxplot of BMI",
        ylab = "BMI",
        col = "lightpink",
        border = "black"
)
 
boxplot(Metabolic_Syndrome$HDL,
        main = "Boxplot of HDL",
        ylab = "HDL",
        col = "yellow",
        border = "black"
)
 
boxplot(Metabolic_Syndrome$UricAcid,
        main = "Boxplot of UricAcid",
        ylab = "Uric Acid ",
        col = "purple",
        border ="black")
 
# Counting the number of outliers
count_outliers <- function(data, column_name) {
  # Calculate the first and third quartiles
  q1 <- quantile(data[[column_name]], 0.25)
  q3 <- quantile(data[[column_name]], 0.75)
  
  # Calculate the interquartile range (IQR)
  iqr <- q3 - q1
  
  # Define the lower and upper bounds for outliers
  lower_bound <- q1 - 1.5 * iqr
  upper_bound <- q3 + 1.5 * iqr
  
  # Identify outliers
  outliers <- data[[column_name]] < lower_bound | data[[column_name]] > upper_bound
  
  # Count the number of outliers
  num_outliers <- sum(outliers)
  
  # Return the count of outliers
  return(num_outliers)
}


# Count outliers for BMI
num_outliers_bmi <- count_outliers(Metabolic_Syndrome, "BMI")
cat("Number of outliers for BMI:", num_outliers_bmi, "\n")
## Number of outliers for BMI: 67
# Count outliers for Blood Glucose Level
num_outliers_bg <- count_outliers(Metabolic_Syndrome, "BloodGlucose")
cat("Number of outliers for Blood Glucose Level:", num_outliers_bg, "\n")
## Number of outliers for Blood Glucose Level: 218
num_outliers_hdl <- count_outliers(Metabolic_Syndrome, "HDL")
cat("Number of outliers for HDL:", num_outliers_hdl, "\n")
## Number of outliers for HDL: 53
num_outliers_bg <- count_outliers(Metabolic_Syndrome, "UricAcid")
cat("Number of outliers for UricAcid:", num_outliers_bg, "\n")
## Number of outliers for UricAcid: 29
#Capping outliers for required columns.
# Function to cap outliers for specified columns
cap_outliers <- function(data, columns) {
  for (col in columns) {
    # Calculate the first and third quartiles
    q1 <- quantile(data[[col]], 0.25)
    q3 <- quantile(data[[col]], 0.75)
  
    # Calculate the interquartile range (IQR)
    iqr <- q3 - q1
  
    # Define the lower and upper bounds for outliers
    lower_bound <- q1 - 1.5 * iqr
    upper_bound <- q3 + 1.5 * iqr
  
    # Cap outliers
    data[[col]][data[[col]] < lower_bound] <- lower_bound
    data[[col]][data[[col]] > upper_bound] <- upper_bound
  }
  
  # Return the updated dataset
  return(data)
}

# Columns to cap outliers for (e.g., "BMI" and "BloodGlucoseLevel")
columns <- c("BMI", "BloodGlucose", "HDL", "UricAcid")

# Cap outliers for specified columns
Metabolic_Syndrome_final <- cap_outliers(Metabolic_Syndrome, columns)

# View the updated dataset
head(Metabolic_Syndrome_final)
##    seqn Age    Sex  Race  BMI UricAcid BloodGlucose HDL MetabolicSyndrome
## 1 62161  22   Male White 23.3      4.9           92  41                 0
## 2 62164  44 Female White 23.2      4.5           82  28                 0
## 3 62169  21   Male Asian 20.1      5.4          107  43                 0
## 4 62172  43 Female Black 33.3      5.0          104  73                 0
## 5 62177  51   Male Asian 20.1      5.0           95  43                 0
## 6 62178  80   Male White 28.5      4.8          105  47                 0
#boxplot after capping
boxplot(Metabolic_Syndrome_final$BMI,
        main = "Boxplot of BMI",
        ylab = "BMI",
        col = "lightgreen",
        border = "black"
)
 
boxplot(Metabolic_Syndrome_final$BloodGlucose,
        main = "Boxplot of BloodGlucose",
        ylab = "BloodGlucose",
        col = "lightpink",
        border = "black"
)
 
boxplot(Metabolic_Syndrome_final$HDL,
        main = "Boxplot of HDL",
        ylab = "HDL",
        col = "yellow",
        border = "black"
)
 
boxplot(Metabolic_Syndrome_final$UricAcid,
        main = "Boxplot of UricAcid",
        ylab = "Uric Acid ",
        col = "purple",
        border ="black")
 
#contigency table for categorical variables
addmargins(table(Sex = Metabolic_Syndrome_final$Sex , Metabolicsyndrome= Metabolic_Syndrome_final$MetabolicSyndrome))
##         Metabolicsyndrome
## Sex         0    1  Sum
##   Female  797  400 1197
##   Male    761  417 1178
##   Sum    1558  817 2375
addmargins(table(Race = Metabolic_Syndrome_final$Race , Metabolicsyndrome= Metabolic_Syndrome_final$MetabolicSyndrome))
##              Metabolicsyndrome
## Race             0    1  Sum
##   Asian        264   81  345
##   Black        363  179  542
##   Hispanic     153  102  255
##   MexAmerican  146  103  249
##   Other         44   17   61
##   White        588  335  923
##   Sum         1558  817 2375
#Visualisations
#Distribution of Age
library(ggplot2)
ggplot(data = Metabolic_Syndrome_final, aes(x = Age)) +
  geom_histogram(binwidth = 5, fill = "skyblue", color = "black") +
  labs(title = "Distribution of Age", x = "Age", y = "Frequency")
 
library(ggplot2)

# Define the intervals or values you want to display on the x-axis
custom_breaks <- c(80, 85, 90, 95, 100, 105, 110, 115, 120)

# Create a ggplot bar plot with custom x-axis breaks and space between intervals
ggplot(data = Metabolic_Syndrome_final, aes(x = factor(BloodGlucose))) +
  geom_bar(fill = "lightcoral") +
  labs(title = "Distribution of Blood Glucose Levels", x = "Blood Glucose Level", y = "Count") +
  scale_x_discrete(breaks = custom_breaks) +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 90, vjust = 0.5, hjust = 1))
 
ggplot(data = Metabolic_Syndrome_final, aes(x = factor(MetabolicSyndrome), y = HDL, fill = factor(MetabolicSyndrome))) +
  geom_violin(trim = FALSE) +
  labs(title = "Distribution of HDL by Metabolic Syndrome", x = "Metabolic Syndrome", y = "HDL") +
  scale_fill_manual(values = c("0" = "lightblue", "1" = "lightgreen")) +
  theme_minimal()
 
library(ggplot2)

sex_counts <- table(Metabolic_Syndrome_final$Sex)
sex_data <- data.frame(Sex = names(sex_counts), Count = as.numeric(sex_counts))

ggplot(data = sex_data, aes(x = "", y = Count, fill = Sex)) +
  geom_bar(width = 1, stat = "identity") +
  coord_polar("y", start = 0) +
  labs(title = "Distribution by Sex", fill = "Sex") +
  theme_void() +
  scale_fill_manual(values = c("Female" = "pink", "Male" = "skyblue"))
 
ggplot(data = Metabolic_Syndrome_final, aes(x = Race, fill = factor(MetabolicSyndrome))) +
  geom_bar(position = "dodge", width = 0.7) +
  labs(title = "Distribution of Metabolic Syndrome by Race", x = "Race", y = "Count") +
  scale_fill_manual(values = c("0" = "lightblue", "1" = "lightgreen"), name = "Metabolic Syndrome") +
  theme_minimal()
 
# Box plot for BMI vs Metabolic Syndrome
ggplot(data = df, aes(x = factor(MetabolicSyndrome), y = BMI, fill = factor(MetabolicSyndrome))) +
  geom_boxplot() +
  labs(title = "Distribution of BMI with Metabolic Syndrome",
       x = "Metabolic Syndrome", y = "BMI", fill = "Metabolic Syndrome") +
  scale_fill_manual(values = c("lightblue", "lightcoral"), labels = c("No", "Yes")) +
  theme_minimal()
## Warning: Removed 26 rows containing non-finite outside the scale range
## (`stat_boxplot()`).
 
# Scatter plot for Age vs HDL with Metabolic Syndrome
ggplot(data = df, aes(x = Age, y = HDL, color = factor(MetabolicSyndrome))) +
  geom_point() +
  labs(title = "Relationship between Age, HDL Levels, and Metabolic Syndrome",
       x = "Age", y = "HDL Level", color = "Metabolic Syndrome") +
  scale_color_manual(values = c("blue", "red"), labels = c("No", "Yes")) +
  theme_minimal()
 
library(ggplot2)

# Create a density plot for the 'UricAcid' variable
ggplot(data = df, aes(x = UricAcid, y = ..density..)) +
  geom_density(fill = "lightblue", color = "black") +
  labs(title = "Distribution of Uric Acid Levels", x = "Uric Acid Level", y = "Density") +
  theme_minimal()
## Warning: The dot-dot notation (`..density..`) was deprecated in ggplot2 3.4.0.
## ℹ Please use `after_stat(density)` instead.
## This warning is displayed once every 8 hours.
## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
## generated.
 
# Box plot for Uric Acid vs Metabolic Syndrome
ggplot(data = df, aes(x = factor(MetabolicSyndrome), y = UricAcid, fill = factor(MetabolicSyndrome))) +
  geom_boxplot() +
  labs(title = "Distribution of Uric Acid with Metabolic Syndrome",
       x = "Metabolic Syndrome", y = "Uric Acid", fill = "Metabolic Syndrome") +
  scale_fill_manual(values = c("lightblue", "lightcoral"), labels = c("No", "Yes")) +
  theme_minimal()
 
# Stacked bar plot for Race vs Metabolic Syndrome
ggplot(data = df, aes(x = Race, fill = factor(MetabolicSyndrome))) +
  geom_bar(position = "stack") +
  labs(title = "Race vs Metabolic Syndrome",
       x = "Race", y = "Count", fill = "Metabolic Syndrome") +
  scale_fill_manual(values = c("lightblue", "lightcoral"), labels = c("No", "Yes")) +
  theme_minimal()
 
# Histogram with density overlay for Blood Glucose Levels and Metabolic Syndrome
ggplot(data = df, aes(x = BloodGlucose, fill = factor(MetabolicSyndrome), color = factor(MetabolicSyndrome))) +
  geom_histogram(aes(y = ..density..), bins = 30, alpha = 0.5) +
  geom_density(alpha = 0.5) +
  labs(title = "Distribution of Blood Glucose Levels by Metabolic Syndrome",
       x = "Blood Glucose Level", y = "Density", fill = "Metabolic Syndrome", color = "Metabolic Syndrome") +
  scale_fill_manual(values = c("lightblue", "lightcoral"), labels = c("No", "Yes")) +
  scale_color_manual(values = c("lightblue", "lightcoral"), labels = c("No", "Yes")) +
  theme_minimal()
 
#STATISTICAL ANALYSIS #Exploratory data Analysis
summary(Metabolic_Syndrome_final)
##       seqn            Age            Sex                Race          
##  Min.   :62161   Min.   :20.00   Length:2375        Length:2375       
##  1st Qu.:64563   1st Qu.:34.00   Class :character   Class :character  
##  Median :67058   Median :48.00   Mode  :character   Mode  :character  
##  Mean   :67028   Mean   :48.67                                        
##  3rd Qu.:69501   3rd Qu.:63.00                                        
##  Max.   :71915   Max.   :80.00                                        
##       BMI           UricAcid      BloodGlucose        HDL       
##  Min.   :13.40   Min.   :1.800   Min.   : 65.0   Min.   :14.50  
##  1st Qu.:24.00   1st Qu.:4.500   1st Qu.: 92.0   1st Qu.:43.00  
##  Median :27.70   Median :5.400   Median :100.0   Median :51.00  
##  Mean   :28.55   Mean   :5.474   Mean   :102.9   Mean   :53.12  
##  3rd Qu.:32.10   3rd Qu.:6.400   3rd Qu.:110.0   3rd Qu.:62.00  
##  Max.   :44.25   Max.   :9.250   Max.   :137.0   Max.   :90.50  
##  MetabolicSyndrome
##  Min.   :0.000    
##  1st Qu.:0.000    
##  Median :0.000    
##  Mean   :0.344    
##  3rd Qu.:1.000    
##  Max.   :1.000
#Checking Normality of data
numeric_columns = Metabolic_Syndrome_final[sapply(Metabolic_Syndrome_final,is.numeric)]
normality_results = sapply(numeric_columns,function(x) {
  shapiro.test = shapiro.test(x) 
  p_value = shapiro.test$p.value
})
normality_results
##              seqn               Age               BMI          UricAcid 
##      7.679795e-27      8.851966e-26      3.886852e-23      4.517758e-13 
##      BloodGlucose               HDL MetabolicSyndrome 
##      3.090104e-33      3.288860e-23      4.070491e-59
The data is not normally distributed.
#DENSITY PLOTS
library(ggplot2)

# Convert MetabolicSyndrome to a factor if it's not already
Metabolic_Syndrome_final$MetabolicSyndrome <- factor(Metabolic_Syndrome_final$MetabolicSyndrome)

# Define color palette for each variable
color_palette <- c("Age" = "blue", "BMI" = "darkgreen", "Blood Glucose" = "red","HDL" = "brown", "UricAcid" = "purple")

# Create the plot
ggplot(data = Metabolic_Syndrome_final) +
  geom_density(aes(x = Age, color = "Age"), alpha = 0.6) +
  geom_density(aes(x = BMI, color = "BMI"), alpha = 0.6) +
  geom_density(aes(x = HDL, color = "HDL"), alpha = 0.6) +
  geom_density(aes(x = UricAcid, color = "UricAcid"), alpha = 0.6) +
  geom_density(aes(x = BloodGlucose, color = "Blood Glucose"), alpha = 0.6) +
  facet_wrap(~ Sex) +  # Facet by Sex
  scale_color_manual(values = color_palette, name = "Variables", labels = c("Age", "BMI", "Blood Glucose" , "HDL", "UricAcid")) +
  labs(title = "Density plots of Metabolic Syndrome by Age, BMI, and Blood Glucose , HDL, UricAcid", 
       x = "Variables", y = "Density") +
  theme_bw() +  # Change plot background to white
  theme(panel.grid = element_blank())  # Remove grid lines
 
FOR RQ1
#chi-square test
# Create a contingency table of Sex and Metabolic Syndrome
contingency_table <- table(Metabolic_Syndrome_final$Sex, Metabolic_Syndrome_final$MetabolicSyndrome)

# Perform chi-square test
chi_square_result <- chisq.test(contingency_table)

# Print the results
print(chi_square_result)
## 
##  Pearson's Chi-squared test with Yates' continuity correction
## 
## data:  contingency_table
## X-squared = 0.94767, df = 1, p-value = 0.3303
# Check for significance and provide interpretation
if (chi_square_result$p.value < 0.05) {
  cat("\nThere is a significant association between Sex and Metabolic Syndrome.\n")
} else {
  cat("\nThere is no significant association between Sex and Metabolic Syndrome.\n")
}
## 
## There is no significant association between Sex and Metabolic Syndrome.
# Create a contingency table of Race and Metabolic Syndrome
contingency_table_race <- table(Metabolic_Syndrome_final$Race, Metabolic_Syndrome_final$MetabolicSyndrome)

# Perform chi-square test for Race
chi_square_result_race <- chisq.test(contingency_table_race)

# Print the results for Race
print(chi_square_result_race)
## 
##  Pearson's Chi-squared test
## 
## data:  contingency_table_race
## X-squared = 30.209, df = 5, p-value = 1.342e-05
# Check for significance and provide interpretation
if (chi_square_result_race$p.value < 0.05) {
  cat("\nThere is a significant association between Race and Metabolic Syndrome.\n")
} else {
  cat("\nThere is no significant association between Race and Metabolic Syndrome.\n")
}
## 
## There is a significant association between Race and Metabolic Syndrome.
#Kruskal-Wallis test
# Perform Kruskal-Wallis test for Age
kruskal_test_age <- kruskal.test(Age ~ MetabolicSyndrome, data = Metabolic_Syndrome_final)

# Print the results for Age
print(kruskal_test_age)
## 
##  Kruskal-Wallis rank sum test
## 
## data:  Age by MetabolicSyndrome
## Kruskal-Wallis chi-squared = 155.73, df = 1, p-value < 2.2e-16
# Check for significance and provide interpretation
if (kruskal_test_age$p.value < 0.05) {
  cat("\nThere is a significant association between Age and Metabolic Syndrome.\n")
} else {
  cat("\nThere is no significant association between Age and Metabolic Syndrome.\n")
}
## 
## There is a significant association between Age and Metabolic Syndrome.
# Perform Kruskal-Wallis test for BMI
kruskal_test_bmi <- kruskal.test(BMI ~ MetabolicSyndrome, data = Metabolic_Syndrome_final)

# Print the results for BMI
print(kruskal_test_bmi)
## 
##  Kruskal-Wallis rank sum test
## 
## data:  BMI by MetabolicSyndrome
## Kruskal-Wallis chi-squared = 497.51, df = 1, p-value < 2.2e-16
# Check for significance and provide interpretation
if (kruskal_test_bmi$p.value < 0.05) {
  cat("\nThere is a significant association between BMI and Metabolic Syndrome.\n")
} else {
  cat("\nThere is no significant association between BMI and Metabolic Syndrome.\n")
}
## 
## There is a significant association between BMI and Metabolic Syndrome.
# Perform Kruskal-Wallis test for Blood Glucose
kruskal_test_glucose <- kruskal.test(BloodGlucose ~ MetabolicSyndrome, data = Metabolic_Syndrome_final)

# Print the results for Blood Glucose
print(kruskal_test_glucose)
## 
##  Kruskal-Wallis rank sum test
## 
## data:  BloodGlucose by MetabolicSyndrome
## Kruskal-Wallis chi-squared = 655.43, df = 1, p-value < 2.2e-16
# Check for significance and provide interpretation
if (kruskal_test_glucose$p.value < 0.05) {
  cat("\nThere is a significant association between Blood Glucose and Metabolic Syndrome.\n")
} else {
  cat("\nThere is no significant association between Blood Glucose and Metabolic Syndrome.\n")
}
## 
## There is a significant association between Blood Glucose and Metabolic Syndrome.
# Perform Kruskal-Wallis test for HDL
kruskal_test_HDL <- kruskal.test(HDL ~ MetabolicSyndrome, data = Metabolic_Syndrome_final)

# Print the results for Blood Glucose
print(kruskal_test_HDL)
## 
##  Kruskal-Wallis rank sum test
## 
## data:  HDL by MetabolicSyndrome
## Kruskal-Wallis chi-squared = 407.91, df = 1, p-value < 2.2e-16
# Check for significance and provide interpretation
if (kruskal_test_HDL$p.value < 0.05) {
  cat("\nThere is a significant association between HDL and Metabolic Syndrome.\n")
} else {
  cat("\nThere is no significant association between HDL and Metabolic Syndrome.\n")
}
## 
## There is a significant association between HDL and Metabolic Syndrome.
# Perform Kruskal-Wallis test for UricAcid
kruskal_test_UricAcid <- kruskal.test(UricAcid ~ MetabolicSyndrome, data = Metabolic_Syndrome_final)

# Print the results for Blood Glucose
print(kruskal_test_UricAcid)
## 
##  Kruskal-Wallis rank sum test
## 
## data:  UricAcid by MetabolicSyndrome
## Kruskal-Wallis chi-squared = 130.64, df = 1, p-value < 2.2e-16
# Check for significance and provide interpretation
if (kruskal_test_UricAcid$p.value < 0.05) {
  cat("\nThere is a significant association between HDL and Metabolic Syndrome.\n")
} else {
  cat("\nThere is no significant association between HDL and Metabolic Syndrome.\n")
}
## 
## There is a significant association between HDL and Metabolic Syndrome.
#{r}install.packages("reshape2")
#correlation
library(ggplot2)
library(reshape2)
## Warning: package 'reshape2' was built under R version 4.3.3
numerical_data <- Metabolic_Syndrome_final[, c("Age", "BMI", "BloodGlucose","HDL","UricAcid")]

correlation_matrix <- cor(numerical_data)
melted_correlation <- melt(correlation_matrix, value.name = "Correlation")

ggplot(data = melted_correlation, aes(Var1, Var2, fill = Correlation)) + 
  geom_tile() + 
  geom_text(aes(label = round(Correlation, 2)), color = "black", size = 3) + 
  scale_fill_gradient(low = "#4E79A7", high = "skyblue") + 
  labs(title = "Correlation HeatMap", x = "", y = "") + 
  theme_minimal() + 
  theme(axis.text.x = element_text(angle = 45, vjust = 1, hjust = 1))
 
#logistic regression
# Fit logistic regression model for Age
logistic_model_age <- glm(MetabolicSyndrome ~ Age, data = Metabolic_Syndrome_final, family = binomial)

# Summary of the model for Age
summary(logistic_model_age)
## 
## Call:
## glm(formula = MetabolicSyndrome ~ Age, family = binomial, data = Metabolic_Syndrome_final)
## 
## Coefficients:
##             Estimate Std. Error z value Pr(>|z|)    
## (Intercept) -2.20847    0.14105  -15.66   <2e-16 ***
## Age          0.03119    0.00260   12.00   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 3057.4  on 2374  degrees of freedom
## Residual deviance: 2904.1  on 2373  degrees of freedom
## AIC: 2908.1
## 
## Number of Fisher Scoring iterations: 4
# Extract odds ratio for Age
odds_ratio_age <- exp(coef(logistic_model_age)["Age"])

# Print the odds ratio with interpretation for Age
cat("Odds Ratio for Age:", odds_ratio_age, "\n")
## Odds Ratio for Age: 1.031683
# Interpretation for Age
cat("For every one year increase in age, the odds of having metabolic syndrome increase by a factor of", round(odds_ratio_age, 2), "times, holding all other variables constant.\n")
## For every one year increase in age, the odds of having metabolic syndrome increase by a factor of 1.03 times, holding all other variables constant.
# Fit logistic regression model
logistic_model <- glm(MetabolicSyndrome ~ BMI, data = Metabolic_Syndrome_final, family = binomial)

# Summary of the model
summary(logistic_model)
## 
## Call:
## glm(formula = MetabolicSyndrome ~ BMI, family = binomial, data = Metabolic_Syndrome_final)
## 
## Coefficients:
##              Estimate Std. Error z value Pr(>|z|)    
## (Intercept) -5.682010   0.268580  -21.16   <2e-16 ***
## BMI          0.172429   0.008945   19.28   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 3057.4  on 2374  degrees of freedom
## Residual deviance: 2570.8  on 2373  degrees of freedom
## AIC: 2574.8
## 
## Number of Fisher Scoring iterations: 4
# Extract odds ratio
odds_ratio <- exp(coef(logistic_model)["BMI"])

# Print the odds ratio with interpretation
cat("Odds Ratio for BMI:", odds_ratio, "\n")
## Odds Ratio for BMI: 1.188187
# Interpretation
cat("For every one unit increase in BMI, the odds of having metabolic syndrome increase by a factor of", round(odds_ratio, 2), "times, holding all other variables constant.")
## For every one unit increase in BMI, the odds of having metabolic syndrome increase by a factor of 1.19 times, holding all other variables constant.
# Fit logistic regression model for Blood Glucose
logistic_model_glucose <- glm(MetabolicSyndrome ~ BloodGlucose, data = Metabolic_Syndrome_final, family = binomial)

# Summary of the model for Blood Glucose
summary(logistic_model_glucose)
## 
## Call:
## glm(formula = MetabolicSyndrome ~ BloodGlucose, family = binomial, 
##     data = Metabolic_Syndrome_final)
## 
## Coefficients:
##               Estimate Std. Error z value Pr(>|z|)    
## (Intercept)  -8.858154   0.396141  -22.36   <2e-16 ***
## BloodGlucose  0.078647   0.003759   20.92   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 3057.4  on 2374  degrees of freedom
## Residual deviance: 2434.1  on 2373  degrees of freedom
## AIC: 2438.1
## 
## Number of Fisher Scoring iterations: 4
# Extract odds ratio for Blood Glucose
odds_ratio_glucose <- exp(coef(logistic_model_glucose)["BloodGlucose"])

# Print the odds ratio with interpretation for Blood Glucose
cat("Odds Ratio for Blood Glucose:", odds_ratio_glucose, "\n")
## Odds Ratio for Blood Glucose: 1.081822
# Interpretation for Blood Glucose
cat("For every one unit increase in blood glucose level, the odds of having metabolic syndrome increase by a factor of", round(odds_ratio_glucose, 2), "times, holding all other variables constant.\n")
## For every one unit increase in blood glucose level, the odds of having metabolic syndrome increase by a factor of 1.08 times, holding all other variables constant.
# Fit logistic regression model for HDL
logistic_model_HDL <- glm(MetabolicSyndrome ~ HDL, data = Metabolic_Syndrome_final, family = binomial)

# Summary of the model for HDL
summary(logistic_model_HDL)
## 
## Call:
## glm(formula = MetabolicSyndrome ~ HDL, family = binomial, data = Metabolic_Syndrome_final)
## 
## Coefficients:
##              Estimate Std. Error z value Pr(>|z|)    
## (Intercept)  3.126841   0.215954   14.48   <2e-16 ***
## HDL         -0.074356   0.004325  -17.19   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 3057.4  on 2374  degrees of freedom
## Residual deviance: 2653.2  on 2373  degrees of freedom
## AIC: 2657.2
## 
## Number of Fisher Scoring iterations: 4
# Extract odds ratio for HDL
odds_ratio_HDL <- exp(coef(logistic_model_HDL)["HDL"])

# Print the odds ratio with interpretation for HDL
cat("Odds Ratio for HDL:", odds_ratio_HDL, "\n")
## Odds Ratio for HDL: 0.9283408
# Interpretation for HDL
cat("For every one unit increase in HDL, the odds of having metabolic syndrome increase by a factor of", round(odds_ratio_HDL, 2), "times, holding all other variables constant.\n")
## For every one unit increase in HDL, the odds of having metabolic syndrome increase by a factor of 0.93 times, holding all other variables constant.
# Fit logistic regression model for UricAcid
logistic_model_UricAcid <- glm(MetabolicSyndrome ~ HDL, data = Metabolic_Syndrome_final, family = binomial)

# Summary of the model for UricAcid
summary(logistic_model_UricAcid)
## 
## Call:
## glm(formula = MetabolicSyndrome ~ HDL, family = binomial, data = Metabolic_Syndrome_final)
## 
## Coefficients:
##              Estimate Std. Error z value Pr(>|z|)    
## (Intercept)  3.126841   0.215954   14.48   <2e-16 ***
## HDL         -0.074356   0.004325  -17.19   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 3057.4  on 2374  degrees of freedom
## Residual deviance: 2653.2  on 2373  degrees of freedom
## AIC: 2657.2
## 
## Number of Fisher Scoring iterations: 4
# Extract odds ratio for HDL
odds_ratio_UricAcid <- exp(coef(logistic_model_UricAcid)["UricAcid"])

# Print the odds ratio with interpretation for UricAcid
cat("Odds Ratio for UricAcid:", odds_ratio_UricAcid, "\n")
## Odds Ratio for UricAcid: NA
# Interpretation for UricAcid
cat("For every one unit increase in UricAcid, the odds of having metabolic syndrome increase by a factor of", round(odds_ratio_UricAcid, 2), "times, holding all other variables constant.\n")
## For every one unit increase in UricAcid, the odds of having metabolic syndrome increase by a factor of NA times, holding all other variables constant.
FOR RQ2:
Which demographic or health factor has the highest impact on the prevalence of metabolic syndrome among individuals with certain risk factors?
Null Hypothesis (H0): There is no significant difference in the prevalence of metabolic syndrome among individuals with certain risk factors based on demographic or health factors. Alternate Hypothesis (H1): At least one demographic or health factor has a significant impact on the prevalence of metabolic syndrome among individuals with certain risk factors.
# Load necessary libraries
library(dplyr)   # For data manipulation
library(tidyr)   # For data tidying
## Warning: package 'tidyr' was built under R version 4.3.3
## 
## Attaching package: 'tidyr'
## The following object is masked from 'package:reshape2':
## 
##     smiths
library(broom)   # For tidying model results
## Warning: package 'broom' was built under R version 4.3.3
# Select relevant variables for analysis
#variables <- c("BMI", "UricAcid", "BloodGlucose", "HDL")
variables1 <- c("Age", "Sex","Race")

# Define outcome variable
outcome_var1 <- "MetabolicSyndrome"

# Fit logistic regression model
logit_model1 <- glm(as.formula(paste(outcome_var1, "~", paste(variables1, collapse = " + "))),
                   data = Metabolic_Syndrome_final,
                   family = binomial)

# Tidy up the model results
tidy_results1 <- tidy(logit_model1)

# Print coefficient estimates
print(tidy_results1)
## # A tibble: 8 × 5
##   term            estimate std.error statistic  p.value
##   <chr>              <dbl>     <dbl>     <dbl>    <dbl>
## 1 (Intercept)      -2.71     0.191     -14.2   1.19e-45
## 2 Age               0.0313   0.00265    11.8   2.55e-32
## 3 SexMale           0.0811   0.0900      0.902 3.67e- 1
## 4 RaceBlack         0.399    0.161       2.48  1.31e- 2
## 5 RaceHispanic      0.667    0.186       3.59  3.25e- 4
## 6 RaceMexAmerican   0.899    0.186       4.83  1.37e- 6
## 7 RaceOther         0.287    0.322       0.890 3.74e- 1
## 8 RaceWhite         0.463    0.149       3.11  1.89e- 3
# Visualize coefficient estimates
plot(tidy_results1, main = "Coefficient Estimates")
 
# Check statistical significance of coefficients
summary(logit_model1)
## 
## Call:
## glm(formula = as.formula(paste(outcome_var1, "~", paste(variables1, 
##     collapse = " + "))), family = binomial, data = Metabolic_Syndrome_final)
## 
## Coefficients:
##                  Estimate Std. Error z value Pr(>|z|)    
## (Intercept)     -2.709339   0.191045 -14.182  < 2e-16 ***
## Age              0.031309   0.002645  11.836  < 2e-16 ***
## SexMale          0.081120   0.089967   0.902 0.367236    
## RaceBlack        0.399407   0.161006   2.481 0.013113 *  
## RaceHispanic     0.667227   0.185622   3.595 0.000325 ***
## RaceMexAmerican  0.898895   0.186159   4.829 1.37e-06 ***
## RaceOther        0.286902   0.322467   0.890 0.373622    
## RaceWhite        0.462566   0.148862   3.107 0.001888 ** 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 3057.4  on 2374  degrees of freedom
## Residual deviance: 2876.0  on 2367  degrees of freedom
## AIC: 2892
## 
## Number of Fisher Scoring iterations: 4
# Assuming you have already fitted a logistic regression model named logit_model

# Get summary of the model
summary_logit <- summary(logit_model1)

# Extract coefficient estimates and p-values
coefficients <- coef(logit_model1)
p_values <- summary_logit$coefficients[, 4]

# Exclude intercept (if present)
if ("(Intercept)" %in% names(coefficients)) {
  coefficients <- coefficients[-1]
  p_values <- p_values[-1]
}

# Calculate absolute coefficients
abs_coefficients <- abs(coefficients)

# Find the index of the variable with the highest absolute coefficient
highest_impact_index <- which.max(abs_coefficients)

# Print the variable with the highest impact and its coefficient
cat("Variable with the highest impact: ", names(coefficients)[highest_impact_index], "\n")
## Variable with the highest impact:  RaceMexAmerican
cat("Coefficient estimate: ", coefficients[highest_impact_index], "\n")
## Coefficient estimate:  0.8988951
cat("P-value: ", p_values[highest_impact_index], "\n")
## P-value:  1.37472e-06
# Load necessary libraries
library(dplyr)   # For data manipulation
library(tidyr)   # For data tidying
library(broom)   # For tidying model results



# Select relevant variables for analysis
variables2 <- c("BMI", "UricAcid", "BloodGlucose", "HDL")


# Define outcome variable
outcome_var2 <- "MetabolicSyndrome"

# Fit logistic regression model
logit_model2 <- glm(as.formula(paste(outcome_var2, "~", paste(variables2, collapse = " + "))),
                   data = Metabolic_Syndrome_final,
                   family = binomial)

# Tidy up the model results
tidy_results2 <- tidy(logit_model2)

# Print coefficient estimates
print(tidy_results2)
## # A tibble: 5 × 5
##   term         estimate std.error statistic  p.value
##   <chr>           <dbl>     <dbl>     <dbl>    <dbl>
## 1 (Intercept)   -9.47     0.625      -15.2  6.32e-52
## 2 BMI            0.134    0.0104      12.9  5.10e-38
## 3 UricAcid       0.0868   0.0424       2.05 4.04e- 2
## 4 BloodGlucose   0.0698   0.00417     16.7  1.07e-62
## 5 HDL           -0.0573   0.00512    -11.2  4.33e-29
# Visualize coefficient estimates
plot(tidy_results2, main = "Coefficient Estimates")
 
# Check statistical significance of coefficients
summary(logit_model2)
## 
## Call:
## glm(formula = as.formula(paste(outcome_var2, "~", paste(variables2, 
##     collapse = " + "))), family = binomial, data = Metabolic_Syndrome_final)
## 
## Coefficients:
##               Estimate Std. Error z value Pr(>|z|)    
## (Intercept)  -9.469499   0.624559  -15.16   <2e-16 ***
## BMI           0.134302   0.010419   12.89   <2e-16 ***
## UricAcid      0.086849   0.042366    2.05   0.0404 *  
## BloodGlucose  0.069759   0.004174   16.71   <2e-16 ***
## HDL          -0.057337   0.005122  -11.20   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 3057.4  on 2374  degrees of freedom
## Residual deviance: 1966.3  on 2370  degrees of freedom
## AIC: 1976.3
## 
## Number of Fisher Scoring iterations: 5
# Get summary of the model
summary_logit2 <- summary(logit_model2)

# Extract coefficient estimates and p-values
coefficients2 <- coef(logit_model2)
p_values2 <- summary_logit2$coefficients2[, 4]

# Exclude intercept (if present)
if ("(Intercept)" %in% names(coefficients2)) {
  coefficients2 <- coefficients2[-1]
  p_values2 <- p_values2[-1]
}

# Calculate absolute coefficients
abs_coefficients2 <- abs(coefficients2)

# Find the index of the variable with the highest absolute coefficient
highest_impact_index2 <- which.max(abs_coefficients2)

# Print the variable with the highest impact and its coefficient
cat("Variable with the highest impact: ", names(coefficients2)[highest_impact_index2], "\n")
## Variable with the highest impact:  BMI
cat("Coefficient estimate: ", coefficients2[highest_impact_index2], "\n")
## Coefficient estimate:  0.1343017
cat("P-value: ", p_values2[highest_impact_index2], "\n")
## P-value:
# Install and load the pROC package
if (!requireNamespace("pROC", quietly = TRUE)) {
    install.packages("pROC")
}
library(pROC)
## Warning: package 'pROC' was built under R version 4.3.3
## Type 'citation("pROC")' for a citation.
## 
## Attaching package: 'pROC'
## The following objects are masked from 'package:stats':
## 
##     cov, smooth, var
# Plot ROC curve and calculate AUC
roc_response <- roc(response = as.numeric(as.character(Metabolic_Syndrome_final$MetabolicSyndrome)) - 1, 
                    predictor = fitted(logit_model2))
## Setting levels: control = -1, case = 0
## Setting direction: controls < cases
plot(roc_response)
 
auc(roc_response)
## Area under the curve: 0.8778
