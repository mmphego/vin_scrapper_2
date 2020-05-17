
# VIN Scrapper

[![Python](https://img.shields.io/badge/Python-3.6%2B-red.svg)](https://www.python.org/downloads/)

Web scrapping tool for retrieving VIN number by licence and location from URL: https://www.vehiclehistory.com

# Installation

```python
    pip install -r requirements.txt
```

# Usage

```bash
usage: vin_scrapper.py [-h] --licence-number LICENCE_NUMBER --state STATE [--proxy-host HOST] [--proxy-port PORT] [--proxy-username USERNAME] [--proxy-password PASSWORD]
                       [--spoof-cloudflare]

Web scrapping tool for Vehicle information from URL: https://www.vehiclehistory.com

optional arguments:
  -h, --help            show this help message and exit
  --licence-number LICENCE_NUMBER
                        Vehicle licence number.
  --state STATE         A state where licence is registered.
                          Example: --state CA [i.e. California].
  --proxy-host HOST     Proxy address. [Optional]
  --proxy-port PORT     Proxy port. [Optional]
  --proxy-username USERNAME
                        Username to access proxy. [Optional]
  --proxy-password PASSWORD
                        Password to access proxy. [Optional]
  --spoof-cloudflare    Node.js version 10 or above is required to interpret Cloudflare's obfuscated JavaScript challenge.
                        Your machine may already have Node installed (check with node -v).
                        If not, you can install it with apt-get install nodejs on Ubuntu >= 18.04 and Debian >= 9 and brew install node on macOS.
```

Example:

**No Proxy**
```
python3 vin_scrapper.py \
--licence-number 33878M1 \
--location CA
```

**With Proxy Auth**
```
python3 vin_scrapper.py \
--licence-number 33878M1 \
--location CA \
--proxy-host 23.229.37.50 \
--proxy-port 34223 \
--proxy-username netkingz9 \
--proxy-password test123
```

**With Proxy Auth and CloudFlare spoofing**
```
python3 vin_scrapper.py \
--licence-number 33878M1 \
--state CA \
--proxy-host 23.229.37.50 \
--proxy-port 34223 \
--proxy-username netkingz9 \
--proxy-password test123 \
--spoof-cloudflare
```

## Multiple licence and rotating proxies

```bash
LICENCE_NUMBERS="license1 license2 license3"
STATE="state"
PROXY_HOSTS="host1 host2 host3"
for licence in $LICENCE_NUMBERS; do
  for proxy_host in $PROXY_HOSTS; do
    echo $licence >> vin_number.txt
    python3 vin_scrapper.py \
      --licence-number $licence \
      --state $STATE \
      --proxy-host $proxy_host \
      --proxy-port 34223 \
      --proxy-username netkingz9 \
      --proxy-password test123 \
      --spoof-cloudflare >> vin_numbers.txt
    echo "=================================" >> vin_numbers.txt
  done;
done;
```

# Demo
![Peek 2020-05-17 23-43](https://user-images.githubusercontent.com/7910856/82160844-57942900-9898-11ea-9109-1e6f96fd21ee.gif)
