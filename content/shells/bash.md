# Bash commands

Index of snippets and commands bash related.

## Process CSV files [taken from this article][1]

- Print the first column of a CSV file `awk -F, '{print $1}' file.csv`
- Print the first and third column of a CSV file `awk -F, '{print $1,$3}' file.csv`
- Print only the lines that contain a specific string `grep "string" file.csv`
- Remove the header row of a file `tail -n +2 file.csv`
- Remove duplicates based on the values of a column (ie: first) `awk '!seen[$1]++' file.csv`
- Calculate the sum of values in a column (ie: second) `awk -F, '{sum+=$2} END {print sum}' file.csv`
- Convert csv into json array `jq -R -r 'split(",") | {name:.[0],age:.[1]}' file.csv`

[1]: https://muhammadraza.me/2022/data-oneliners/