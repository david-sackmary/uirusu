# uirusu

uirusu is an [Virustotal](http://www.virustotal.com) automation and convenience tool for hash, file and URL submission.

The current version is 0.0.6.

## Requirements

* ruby 1.9+
* json
* rest-client
* **public api key from [virustotal.com](http://www.virustotal.com)**

## Installation

	% gem install uirusu
	% uirusu [options]

## Setup is fairly easy

### Create your configuration file
	% uirusu --create-config

### Edit your configuration file with API key
	% $EDITOR ~/.uirusu

## Usage

### Searching a file of hashes

	% uirusu -f <file_with_hashes_one_per_line>

### Searching a single hash

	% uirusu -h FD287794107630FA3116800E617466A9

### Searching a file of hashes and outputting to XML
	% uirusu -f <file_with_hashes_one_per_line> -x

### Upload a file to Virustotal and wait for analysis
	% uirusu -u </path/to/file>

### Search for a single URL
	% uirusu -s "http://www.google.com"

### Saving results to a file
	% uirusu -s "http://www.google.com" --yaml-output > file.yaml

### Scan a directory and have them searched and save the results as json
	% uirusu -d /bin/ --json-output > file.json

## API Usage
```ruby
#First you need to include the correct require files
require 'rubygems'
require 'uirusu'

APT_KEY = "YOUR API KEY HERE"

hash = "FD287794107630FA3116800E617466A9" #Hash for a version of Poison Ivy
url = "http://www.google.com"
comment = "Hey this is Poison Ivy, anyone have a copy of this binary?"

#To query a hash(sha1/sha256/md5)
results = Uirusu::VTFile.query_report(APT_KEY, hash)
result = Uirusu::VTResult.new(hash, results)
print result.to_stdout if result != nil

#To scan for a url
results = Uirusu::VTUrl.query_report(APT_KEY, url)
result = Uirusu::VTResult.new(url, results)
print result.to_stdout if result != nil

#To post a comment to a resource(url/hash/scan_id)
results = Uirusu::VTComment.post_comment(APT_KEY, hash, comment)
print results if results != nil
```

##License

Uirusu is licensed under the BSD license see the `LICENSE` file for the full license.

## Contact
You can reach the team at uirusu[@]arxopia[dot]com or http://www.arxopia.com
