# Installation
To install the script, you need to get a free virtustotal api key. You can generate it on [VirtusTotal Webstie](https://www.virustotal.com/)
## Using docker
```
git clone https://github.com/gregxsunday/automated-recon
cd automated-recon
docker build -t autorecon --build-arg VIRUSTOTAL_KEY=$VIRUSTOTAL_KEY .
```
## manual installation
### 1. Set VirtusTotal API key as an environment variable
```
EXPORT VIRUSTOTAL_KEY=****
```
### 2. Install amass
download binary from https://github.com/OWASP/Amass/releases and add to `$PATH`

### 3. Install dig
* On Ubuntu:
```
sudo apt install dnsutils
```
* On Alpine Linux:
```
RUN apk add bind-tools
RUN apk add git
```

### 4. Install dnsgen
```
git clone https://github.com/ProjectAnte/dnsgen
cd dnsgen
pip install -r requirements.txt
sudo python setup.py install
```
make sure it;s in the `$PATH`


# Usage

## Example usage:
```
docker run autorecon -m s -d example.com,example.pl -o example
```
```
python automated_recon.py -m s -d example.com,example.pl -o example
```
* -m s -  search for subdomains
* -d example.com,example.pl - scan domains example.com and example.pl
* -o example - save results into example directory  

The output will have a file subdomains.txt wich all found subdomains and there will be folder aquatone.d, which has screenshots of found subdomains.

## Full usage:

```
usage: automated_recon.py [-h] (-d DOMAIN [DOMAIN ...] | -dl DOMAIN_LIST)
                          [-o OUT] [-m METHOD]

Automated recon

optional arguments:
  -h, --help            show this help message and exit
  -d DOMAIN [DOMAIN ...], --domain DOMAIN [DOMAIN ...]
                        target domain or domains separated by spaces
  -dl DOMAIN_LIST, --domain_list DOMAIN_LIST
                        file with target domains in separate lines
  -o OUT, --out OUT     output directory, ./recon by default
  -m METHOD, --method METHOD
                        recon method, available: [i]pspace, [p]orts,
                        [s]ubdomains, [d]irectories, [a]l
```