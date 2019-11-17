# Dojo Rally Words List

Took https://raw.githubusercontent.com/dwyl/english-words/master/words_alpha.txt, shuffle it and recreate it as 1 commits per words.

* To sort the file use: `cat DRW.txt | sort -n`
* To sort by words lenght: `cat DRW.txt | awk '{ print length, $0 }' | sort -n | cut -d" " -f2-`

## Script for the commits

```
#!/usr/bin/env bash
rm DRW.txt || true
touch DRW.txt
rm -rf .git
git init
git add DRW.txt
git commit "[INIT] Dojo Rally Words"
while IFS="" read -r p || [ -n "$p" ]
do
  printf '%s\n' "$p"
  echo "$p" >> DRW.txt
  git add DRW.txt
  git commit -m "[ADD] $p"
done < words.txt | shuf
```
