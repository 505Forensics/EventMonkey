# EventMonkey
A Windows Event Processing Utility

View more information on the [wiki](https://github.com/devgc/EventMonkey/wiki)!

## Ingest
Three types of files are currently supported:
- Native evt
- Native evtx
- EvtXtract's json recovered records file

If you are using [EVTXtract](https://github.com/williballenthin/EVTXtract) output, just stick the .json files in the path specified with -p

## Usage

```
usage: EventMonkey.py [-h] -n EVIDENCENAME -p EVENTS_PATH -o OUTPUT_PATH
                      [--threads THREADS_TO_USE] [--esconfig ESCONFIG]
                      [--esurl ESURL] [--eshost ESHOST] [--esuser ESUSER]
                      [--espass ESPASS]

EventMonkey (A Windows Event Parsing Utility)

optional arguments:
  -h, --help            show this help message and exit
  -n EVIDENCENAME, --evidencename EVIDENCENAME
                        Path to Event Files
  -p EVENTS_PATH, --path EVENTS_PATH
                        Path to Event Files
  -o OUTPUT_PATH, --output_path OUTPUT_PATH
                        Output Path
  --threads THREADS_TO_USE
                        Number of threads to use (default is all [8])
  --esconfig ESCONFIG   Elastic YAML Config File
  --esurl ESURL         Elastic RFC-1738 URL
  --eshost ESHOST       Elastic Host IP
  --esuser ESUSER       Elastic Host User
  --espass ESPASS       Elastic Password [if not supplied, will prompt]
```

## Creating Descriptions and Tags
Description files are located in the etc/descriptions folder. The name of the file is the same as an event's 'System.Channel.#text' field (with a .yml extention).

Example from etc/descriptions/Security.yml:
```
4608:
  description: "Windows is starting up"
  tags:
    - "Startup"
4609:
  description: "Windows is shutting down"
  tags: 
    - "Shutdown"
```

If an event is from channel Security, it will then look for the EventID number to load the description and tags.

## Elastic YAML Config File
You can now use a config file to connect to elastic. This way you can add in SSL certs if needed. Follow the structure of the elasticsearch py api: https://elasticsearch-py.readthedocs.io/en/master/api.html#elasticsearch

```
elastic_config:
  hosts:
    - host: '127.0.0.1'
  http_auth: ['user','password']
```

## Dependencies
* libevt and libevtx
 * Get the compiled binaries:<br/>
https://github.com/log2timeline/l2tbinaries
 * Source code:<br/>
https://github.com/libyal/libevtx<br/>
https://github.com/libyal/libevt<br/>

- PyYAML
 - Get the compiled binaries:<br/>
http://pyyaml.org/wiki/PyYAML

- lxml
 - `pip install lxml`

- bs4 (beautifulsoup4)
 - `pip install bs4`
 - Project Info:<br/>
https://pypi.python.org/pypi/beautifulsoup4

- progressbar2
 - `pip install progressbar2`

## Do Things Like:
Easier viewing and filtering using customizable tags and descriptions
![Security Descriptions and Tagging](https://github.com/devgc/EventMonkey/blob/master/examples/DescriptionsAndTags.png)

Search records recovered by EVTXtract
![Ingest EVTXtract records](https://github.com/devgc/EventMonkey/blob/master/examples/Ingest_EVTXtract_records.png)

Search for a devices' serial number
![Image of Device Serial Number Search](https://github.com/devgc/EventMonkey/blob/master/examples/SearchDeviceSerial.png)
