# Video-STT-Search
Video Speech-to-Text and Search Samples

![Screenshot Video STT Search](https://raw.githubusercontent.com/AzureMediaCognitiveDemos/Video-STT-Search-Python/master/img/screenshot-video-stt-demo.jpg)

Demo: [http://aka.ms/amcdemo_videostt](http://aka.ms/amcdemo_videostt)


## 1. Preparation

### 1-1. Configurations for Azure Services
You have to create the following Azure services accounts and configure the files for each service:

| Azure Services                | Config file    |
|-------------------------------|----------------|
| Azure Media Services          | ams.conf       |
| Azure Search                  | search.conf    |

### 1-2. Create Azure Search Index for STT text search
You have to create index schema to index digital text that were generated from Speech-to-Text processing of the video by Azure Media Indexer2. There is a scritp for creating index schema.

```
# run this if text is English
./create_stt_schema_en.sh
```

### 1-3. Setup Azure Media Processors Modules
Please install maven and git if not yet installed on your environment
```
# for Ubuntu,Debian
sudo apt-get install git
sudo apt-get install maven

# for CentOS,Fedora,Oracle Linux,Red Hat Enterprise Linux
sudo yum install git
sudo yum install maven
```

Also you need Java compiler, so please install JDK if not yet installed on your environment
```
# for Ubuntu,Debian
sudo apt-get install openjdk-7-jdk   (JDK7)
sudo apt-get install openjdk-8-jdk   (JDK8)

# for CentOS,Fedora,Oracle Linux,Red Hat Enterprise Linux
sudo yum install java-1.7.0-openjdk  (JDK7)
sudo yum install java-1.8.0-openjdk  (JDK8)
```

Finall Check out github repo and build the module in order to make it ready for batch execution
```
cd mediaprocessors
./setup.sh
```


## 2. Batch execution

### run-batch command Usages
```
usage: ./run-batch [WORKFLOW] [VIDEO_FILE] [BATCH_NAME] [BATCH_WORK_DIR]
This program generates webvtt file from your video leveraging Azure Media 
Services Media Indexer and upload all dataset of extracted text and their 
appearing times into Azure search to make them searchable

WORKFLOW : ALL|GEN_CC|SEARCH_UPLOAD
```

### Example1: Run all workflows
```
./run-batch ALL ../demo/build2016breakout/video/Python_and_node.js.mp4  build2016breakout ../demo/build2016breakout
```

### Example2: Run each workflow one by one

```
# (1) Extract text from Video by Azure Media Indexer2
# Azure Media Indexer generates Webvtt file output as a result
./run-batch GEN_CC ../demo/build2016breakout/video/Python_and_node.js.mp4  build2016breakout ../demo/build2016breakout

# (2) Parse and extract text from the webvtt file obtained in (2) and upload them onto Azure Search
./run-batch SEARCH_UPLOAD ../demo/build2016breakout/video/Python_and_node.js.mp4  build2016breakout ../demo/build2016breakout
```

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/AzureMediaCognitiveDemos/Video-STT-Search-Python.
