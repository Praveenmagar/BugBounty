# Now we know how to find subdomains
- Using 
```
subfinder
```
`subfinder -d samsung.com -all -silent -o samsung.txt`
- ***Now we need to find subdomain of subdomain
	- Firstly, we can use `ffuf`
		- `ffuf -c -u https://FUZZ.samsung.com -w n0kovo_subdomains_medium.txt -mc 200 -rate 100 -v`
		- `ffuf -c -u https://FUZZ.samsung.com -w n0kovo_subdomains_medium.txt -mc 200 -rate 100 -v -o file.txt`
	- Use tool `Oneforall`
		- `https://github.com/shmilylty/OneForAll/blob/master/docs/en-us/README.md
		- For this tool i have use virtual environment in Parrot OS
			- `cd /home/praveen/OneForAll`
			- `python3 -m venv myenv
			- `source myenv/bin/activate
			- `deactivate`
			- `python3 oneforall.py --help`
			- `python3 oneforall.py --target example.com run`
- ***Tool to find subdomain of subdomain
	- Use shuffledns 
		- `https://github.com/projectdiscovery/shuffledns`
	- But shuffledns is part of massdns. So to run this we need massdns to install first
		- `https://github.com/blechschmidt/massdns`
	- After installing both lets work on shuffledns
		- `shuffledns -d samsung.com -w 2m-subdomains.txt -r resolvers.txt -o samsungshuffle.txt -v -mode resolve<<< "samsung.com"`
		- One best wordlist for this shuffledns is `https://wordlists.assetnote.io`
		- Now click on download and you will redirect to that wordlist page. To download copy URL and go to Linux terminal and  type 
			- `wget https://wordlists-cdn.assetnote.io/data/manual/2m-subdomains.txt`. 
			- This will download that file
		- Now next we need resolver file so to download that file go to
			- `https://github.com/blechschmidt/massdns/blob/master/lists/resolvers.txt`
			- There are many other places to download this resolvers

- To check numbers of domain
	- `cat samsung.txt | wc -l`
- To keep only unique value
	- `sort samsung.txt| uniq > samsungsorted.txt`


- ### Running httpx to check http server (Which are live)
	- `cat samsungsorted.txt | httpx-toolkit > samsunglive.txt`
- Note: If there is problem with `httpx-toolkit` you can go with `httprobe`

***To merge two files
- `cat file1.txt file2.txt > newmerge.txt`

- ### After finding live now lets do screenshot
	- `cat teslafinal.txt | aquatone -out Aquatone`


- ### Now lets perform directory bruteforce
	- We have lots of tools for this
		- `ffuf`
		- `dirsearch`
		- `dirbuster`
		- `gobuster`
	- Now lets use `dirsearch`
```text
dirsearch -l samsunglive.txt -e php,asp,http,aspx,js -i 200,400 -t 100
```