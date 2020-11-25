./tracker <my_tracker_ip>:<my_tracker_port> <other_tracker_ip>:<other_tracker_port> <seederlist_file> <log_file>
./tracker 127.0.0.1:8001 127.0.0.2:8002 seeder_tracker log_tracker

client 1
./client 127.0.0.3:8005 127.0.0.1:8001 127.0.0.2:8002 log_8005

client 2
./client 127.0.0.3:8006 127.0.0.1:8001 127.0.0.2:8002 log_8006

share <local_file_path> <filename>.<file_extension>.mtorrent
share mTorrent/ sample.mp4.mtorrent

get <path_to_.mtorrent_file> <destination_path>
get sample.mp4 mTorrent/d.mp4


# Mini Bit Torrent

A mini p2p file sharing system.

## Prerequisites
We need following to generate SHA1 hash of the files.
```
sudo apt-get install openssl
sudo apt-get install libssl-dev
```

## Compiling 
* Code is divided in folders: client and tracker
* Both folders have corresponding Makefile. Use "make" in both folders to compile

## Running
* Run tracker
```
./tracker_2018201103 <my_tracker_ip>:<my_tracker_port> <other_tracker_ip>:<other_tracker_port> <seederlist_file> <log_file>
```
* Run client
```
./client_2018201103 <CLIENT_IP>:<UPLOAD_PORT> <TRACKER_IP_1>:<TRACKER_PORT_1> <TRACKER_IP_2>:<TRACKER_PORT_2> <log_file>
```
log_file(s) can be used to check the activities

## Commands for client
* Share a file
```
share <local_file_path> <filename>.<file_extension>.mtorrent
```
It generates an mtorrent file and shares the information with tracker so that tracker can add the peer to seederlist

* Download a file
```
get <path_to_.mtorrent_file> <destination_path>
```
Gets data about the peers sharing the required file and starts downloading the file in destination_path

* Stop sharing a file
```
remove <filename.mtorrent>
```
Deletes mtorrent file and remove information about the peer from the tracker

* Show downloads
```
show downloads
```
show downloaded and downloading files

* Close the peer
```
exit
```
Remove information from the tracker and closes the client program

## Assumptions
* Spaces in file name should be escaped by \
* Relative and absolute paths are supported
* Only one tracker is implemented
* Downloading occurs only from one peer (first peer from seederlist) in chunks of 512KB
* All the mTorrent files should be present in client/mTorrent folder
