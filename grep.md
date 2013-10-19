# Using grep (and other tools)

[grep_is_good.png]

## tool list

### shell kit
* head, tail
* cat
* wc (especially `wc -l`!)
* time

### scientist's kit
* grep: string matching
* egrep: regular expressions
* cut: slice and dice on fields, characters
* sort: ascii sort (or `-g` for numeric sort)
* uniq: given a sorted list, give only a single item of each. can also count.

### Downloading
* wget, curl
* scp, rsync

### compressed files
* tar for tgz or .tar.gz extensions (`tar -zxvf` and `tar -czvf`)
* gzip, gunzip for .gz extensions (and .Z, which is rare)
* zcat, zgrep, zegrep (use `gunzip -c` for gz on OSX)
* bzip for .bzip2
* zip for .zip

### scary others
* perl: regex ftw
* awk: quick summation and processing
* sed: regex substitutions

### connectors
* pipe: `|`
* redirect: `>`
* append: `>>`

## Examples

### wikipedia stats

[Using pagecount files](http://dumps.wikimedia.org/other/pagecounts-raw/) from Wikimedia, we can extract information fairly easily.

#### Popular pages in this hour, by language

    time egrep "^\w\w .*\d\d{3,} \d+$" pagecounts-20121101-080001 | cut -d ' ' -f 1 | uniq -c | sort -g | tail

#### Count of pages with hits, by language

    time egrep --only-matching "^\w\w " pagecounts-20121101-080001 | cut -d ' ' -f 1 | sort | uniq -c | sort -g | tail

(why `sort` twice? apparently results aren't fully sorted by language)

### "apache style" access logs

#### Histogram of hits in a logfile

    zgrep -v Pingdom burner.log-20130928.gz | egrep --only-matching "2013-09-2.*\" 200.*" | cut -c 9-13 | sort | uniq -c

### "i before e except after c" rulebreakers

    grep cie /usr/share/dict/words




