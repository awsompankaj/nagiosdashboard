
# Configure checkmk Livestatus with nagios

 
 ## Install dependencies:

```bash
 apt-get install -y librrd-dev make gcc-c++ wget libboost1.58-all-dev
```
## Download mk livestatus:

```bash
 cd /tmp && wget https://checkmk.com/support/1.4.0p37/mk-livestatus-1.4.0p37.tar.gz
```
## Extract package:

```bash
tar -xzvf mk-livestatus-1.4.0p37.tar.gz
```
## Install:

```bash
cd mk-livestatus-1.4.0p37/ && ./configure
make && make install
```
## Create new directory with correct permissions:

```bash
mkdir /usr/lib/nagios/mk-livestatus && chown nagios:apache /usr/lib/nagios/mk-livestatus
```
## Edit /etc/nagios/nagios.cfg :

```bash
broker_module=/usr/local/lib/mk-livestatus/livestatus.o /usr/lib/nagios/mk-livestatus/live
```

## Restart Nagios:

```bash
service nagios restart
```
## Try command line:

```bash
echo 'GET hosts' | unixcat /usr/lib/nagios/mk-livestatus/live
```

