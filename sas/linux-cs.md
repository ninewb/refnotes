## General

List comma separated items

    id | tr ',' '\n' | grep -i value

## Searching

Find words (OR)

    grep -rni -E "ERROR|Heap" .

Find words (AND)

    grep -rni -E "ERROR.*Heap" .

## Logging

Move logs with a specific time/date

    for i in `ls -lrt | grep "May 12" | awk '{print $9}' `; do mv $i* /tmp/May; done

#### variable

Remove file extension

    name=$(echo "${filename}" | cut -f 1 -d '.')


