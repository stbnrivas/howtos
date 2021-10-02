# csv cli tooling

```bash
cat temp.csv

1,2,3,4,5,6,7,8,9,10
1,2,3,4,5,6,7,8,9,10
1,2,3,4,5,6,7,8,9,10
1,2,3,4,5,6,7,8,9,10
1,2,3,4,5,6,7,8,9,10
1,2,3,4,5,6,7,8,9,10
1_10,2_10,3_10,4_10,5_10,6_10,7_10,8_10,9_10,10_10
```



## take N first lines from start or end

```
head -n 2 $input > $output

1,2,3,4,5,6,7,8,9,10
1,2,3,4,5,6,7,8,9,10



tail-n 2 $input > $output

1,2,3,4,5,6,7,8,9,10
1_10,2_10,3_10,4_10,5_10,6_10,7_10,8_10,9_10,10_10
```


## split by selected columns only


```bash
cut --delimiter=, -f1              input.csv > output.csv

1
1
1
1
1
1
1_10



cut --delimiter=, -f1,3              input.csv > output.csv

1,3
1,3
1,3
1,3
1,3
1,3
1_10,3_10



cut -d,           -f1,3 --complement input.csv > output.csv

2,4,5,6,7,8,9,10
2,4,5,6,7,8,9,10
2,4,5,6,7,8,9,10
2,4,5,6,7,8,9,10
2,4,5,6,7,8,9,10
2,4,5,6,7,8,9,10
2_10,4_10,5_10,6_10,7_10,8_10,9_10,10_10
```


## csv validation (go implentation)


set iscsv = `awk ' BEGIN{FS=","}!n{n=NF}n!=NF{failed=1;exit}END{print !failed}' file.csv`



go https://github.com/Clever/csvlint

download from https://github.com/Clever/csvlint/releases/tag/v0.3.0