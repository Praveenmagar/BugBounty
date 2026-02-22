# Finding sensitive data from JavaScript
- ### Step 1: At first try to find as many as possible link of JavaScript
- It is best to do manual research but sometime automation is also ok
- List of some automate tools are
	```
    katana
    ```
	```
    subjs
    ```
- Lets start with `subjs`
	```
    https://github.com/lc/subjs
    ```
	- Installation from binary release
		```
        wget https://github.com/lc/subjs/releases/download/v1.0.1/subjs_1.0.1_linux_amd64.tar.gz
        ```
    - to unzip it
		```
        tar -xvf subjs_file.tar
        ```
		```
        mv subjs /usr/bin
        ```
		```
        subjs -h
        ```
    - to run subjs 
		```
        cat file.txt | subjs
        ```
		```
        cat file.txt | subjs > file.txt
        ```
- For `katana`
	```
    https://github.com/projectdiscovery/katana
    ```
	```
    katana -u https://tesla.com -d 5 -headless -no-sandbox -xhr -jc
    ```
	```
    katana -u https://tesla.com -d 5 -headless -no-sandbox -xhr -jc | grep ".js$"
    ```
	```
    katana -list teslafile.txt -d 5 -headless -no-sandbox -xhr -jc -v| grep ".js$" | uniq | sort > savefile.txt
    ```
	```
    katana -list teslafile.txt -d 5 -headless -no-sandbox -xhr -jc -o savefile.txt| grep ".js$"
    ```
- to move content from teslafile.txt to newteslafile.txt with `.js` extension
	```cat teslafile.txt | grep ".js$" > newteslafile.txt
    ```
- to move content of `first.txt` and `second.txt` to `third.txt`
	```
    cat first.txt second.txt > third.txt
    ```
	```
    sort file.txt | uniq | wc -l
    ```

- To check unique
	- `cat file.txt | uniq | wc -l`
- To create file with unique content
	- `sort file.txt |uniq > sortedfile.txt`

- ### Step 2: Finding sensitive data inside that JavaScript file
	- Using `SecretFinder` to find sensitive data
	- Installing ways
		- `python3 -m venv .venv
		- `source .venv/bin/activate`
		- `sed -i 's/requests_file/requests-file/g' requirements.txt`
		- `python -m pip install --upgrade pip setuptools wheel`
		- `sudo apt update && sudo apt install -y python3-dev libxml2-dev libxslt1-dev zlib1g-dev build-essential`
		- `pip install -r requirements.txt`

- To find secret 
	- `cat sortedfile.txt | while read url; do python3 SecretFinder/SecretFinder.py -i $url -o cli > secrets.txt; done`
	- `cat sortedfile.txt | while read url; do python3 SecretFinder/SecretFinder.py -i $url -o cli; done`
	
- We can also find secret data using grep
	- `cat teslakatanasorted.txt| grep -r -E aws_access_key`
	
- ***Next we can also find using `nuclei` `github.com/projectdiscovery/nuclei`
	- `nuclei -l teslakatanasorted.txt -t /root/nuclei-templates/file/keys/ -file`
	- `nuclei -l teslakatanasorted.txt -t /root/nuclei-templates/javascript  -file`

- Next interesting tool is `mantra` `https://github.com/brosck/mantra`
	- `cat teslakatanasorted.txt | mantra `