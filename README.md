# PushResults2ELK
Many times we feel the need to push CodeCoverage, test results and/or other build artifacts from Jenkins to ElasticSearch for analysis and reporting but it is not an easy path.
One solution is to use Logstash plugin to push console logs to ELK. The issues with this approach are :
- Specify how many lines (tail of the logs) you want to push to ELK
- Lot of information stored in ELK is not useful
- Fills up ELK storage pretty quickly
- Difficult to create indexes and end up in one gaint index

The approach I have taken is to use
- Logstash as data shipper
- Jenkins Rest APIs to fetch the latest build/test data as json
- Powershell or Bash to POST data to Logstash on port 5400
- Logstash in turn will filter any data/event if needed
- Logstash will POST the data to ES endpoint

I will elaborate each point in detail:

