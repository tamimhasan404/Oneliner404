![text (1)](https://user-images.githubusercontent.com/78614799/207514371-2c964af2-4306-4e80-9c36-6d0b9b7c733d.gif)

![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat) <a href="https://twitter.com/tamimhasan404">
    <img src="https://img.shields.io/badge/author-@tamimhasan404-orange.svg?style=square&logo=twitter">
  </a>
  
## Uncover
- [ ] Description: Oneliner for run your targets all domain on uncover ( very useful when you have list of wildcard domains)
```  
while read -r line; do uncover -q "$line" -e fofa,censys | uniq; done < all-domains.txt > all-domains-ips-uncover.txt
```

## FFUF
- [ ] Description: Run ffuf on all of your targets domain and save only find in a txt file
```
for url in $(cat targets.txt); do ffuf -ac -fc 404,403 -w wordlist.txt -u $url/FUZZ >> results.txt; done && sort -u results.txt | grep -E '^https?://' > results.txt
```
## Httpx grep only ips
- [ ] Description: Graping only Ips and filter out domains and save them on a txt file
```
cat live-domain.txt | httpx -ip -silent -timeout 10 | grep -o '[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}' | tee domains-ips.txt
```

## Httpx only Cname gather
- [ ] Description: Graping only cname and filter out other stuff and save them on a txt file

```
cat domains.txt | httpx -cname -timeout 13 | cut -f2 | awk '{print $2}' | uniq | unfurl -u domains > cname.txt
```

## Html DEV comments grep
- [ ] Description: Sometimes developer #Html comments can be useful while doing bug bounty or security assessments .

```
cat target-domain.txt | xargs -I@ sh -c 'curl -v --stderr - @ | grep "<\!--" && echo @' > target-domains-html-comments.txt
```
## Greather all panel stuff from Gau/wayback urls
- [ ] Description: Greather all panel stuff from Gau/wayback urls that may help to find vulnabilty like defult password, sqli on admin panel, singup option, unrestricted/weakly secure admin panel etc.

```
cat gau-urls.txt | grep -i "login\|singup\|admin\|dashboard\|wp-admin\|singin\|adminer\|dana-na\|login/?next/=" | sort | uniq > gau-panel.txt
```
🛠 Post-Mortem your Gau/Wayback result with [Gau-Expose](https://github.com/tamimhasan404/Gau-Expose) tool

### Regex for bug bounty

- [ ] Description: Remove http/s from your target list very useful when your tool dosen't work with http/s like nabbu

```
cat targets.txt | sed 's/^http\(\|s\):\/\///g' > without-http.txt
```
- [ ] Description: adding https:// or any word like admin,ftp infront of your domains.
```
awk '$0="https://"$0' domains.txt > add-done-domain.txt
```

- [ ] Description: Remove garbage from gospider/wayback urls

```
cat gospider.txt | sed -e 's/\.gif\|.html\|.rss\|.cfm\|.htm\|.jpg\|.mp4\|.css\|.jpeg\|.png\|.svg\|.ico\|.mp3\|.mp4//' > filter-gospider-urls.txt
```
- [ ] Description: `Grep only ips from a txt file`.Hidden ips may revel internal admin panel page, help in ssrf , may find interesting thing after port scan etc.

```
grep -E '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}' text-file.txt
```
