# subpop-results
Results from the latest Rapid7 Sonar FDNS processed by subpop for use with tools

## things you should know

I usually do this on an m4 instance on AWS, you'll need a disk with around 200GB of space for the data. Also running the python script with pypy offers a massive speed improvment, I could have scaled up to a bigger CPU instance which would have increased processing time by a bit but meh.
Once you've downloaded your data and processed it, you'll end up with some artifacts similar to below.

```
root@subpop:/mnt/data/dnspop/code# ls -lah
total 193G
drwxr-xr-x 2 admin admin 4.0K Dec  5 05:33 .
drwxr-xr-x 5 admin admin 4.0K Dec  4 08:55 ..
-rw-r--r-- 1 admin admin  98G Feb  1  2017 20170128_dnsrecords_all
-rw-r--r-- 1 root  root   30G Dec  5 05:07 20170128_domains_without_tld
-rw-r--r-- 1 root  root   36G Dec  5 02:47 20170128_domains_with_tld
-rw-r--r-- 1 root  root   18G Dec  5 05:58 20170128_subdomains_popular
-rw-r--r-- 1 root  root   13G Dec  5 05:33 20170128_subdomains_raw
-rw-r--r-- 1 root  root  196K Dec  5 00:41 public_suffix_list.dat
-rwxr-xr-x 1 admin admin 2.4K Dec  5 02:13 subpop.sh
-rwxr-xr-x 1 admin admin 1.9K Dec  5 02:14 suffix_strip.py
```

To cut your subdomains lists up just head it out into files, then use sed to remove counts for making lists to be used with tools like glugger or subbrute.
Maybe I'll automate this next time.

```
root@subpop:/mnt/data/dnspop/code# head -1000 20170128_subdomains_popular > 20170128_subdomains_popular_1000_with_count.txt
[...]
root@subpop:/mnt/data/dnspop/code# cat 20170128_subdomains_popular_1000_with_count.txt | sed 's/.*[0-9] //' > 20170128_subdomains_popular_1000.txt
[rinse and repeat for different sizes]
```


