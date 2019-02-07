# filebeat-6.6.0-armv7
Cross compiled filebeat-6.6.0 for ARMv7
Elastic does not provide Filebeat binaries for ARMv7
Filebeat can easily be cross-compiled with:
```
# ----- Instantiate an immutable Go container for cross-compilation ----- #
mkdir build && cd $_
docker run -it --rm -v `pwd`:/build golang:1.11 /bin/bash

# ----- Inside Go container ----- #
go get github.com/elastic/beats
cd /go/src/github.com/elastic/beats/filebeat/
git checkout v6.6.0
GOARCH=arm go build
cp filebeat /build
exit

# ----- Verify the output file ----- #
file filebeat
#filebeat: ELF 32-bit LSB executable, ARM, EABI5 version 1 (SYSV), statically linked, not stripped
```
This proyect contains the newly built filebeat binary substituted in the official filebeat 6.6.0 linux package
https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-6.6.0-linux-x86_64.tar.gz
