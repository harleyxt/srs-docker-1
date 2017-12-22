# SRS 2.0 Docker Image

This repository includes a demo of `Dockerfile` to build a docker image contains [SRS Media Server Verson 2](https://github.com/ossrs/srs/tree/2.0release) on Cent OS.  

If you want to use the image directly,you can push a ready-made image([See it on Docker Hub](https://hub.docker.com/r/zhouweitong/srs-docker/)).Feel free to try it!  

### Feature:
Support RTMP,RTSP,HTTP-FLV,HTTP-AAC,HLS,HDS and many other streaming protols.  
It can also transcoding rhe live stream,and built-in HTTP Server can be used to deliver player sites.  
You can build a RTMP or HTTP-FLV cluster easily as well.

### Notice:
1. HTML5 Player temporarily unsupported.  
2. Some of the configurations are untested.Please take then at your own risk. 

### Pull command:  

`docker pull zhouweitong/srs-docker:v2`

### Docker command sample:  
  
```
docker run -d \
		-p 554:554 \
		-p 1935:1935 \
		-p 1985:1985 \
		-p 2037:2037 \
		-p 2038:2038 \
		-p 2039:2039 \
		-p 2040:2040 \
		-p 8080:8080 \
		-p 8081:8081 \
		-p 8936:8936 \
		-p 50000-51000:50000-51000 \
		-p 57000-58000:57200-57300 \
		zhouweitong/srs-docker:v2
```  
It automatically runs `/bin/bash -c /root/start.sh` and starts the SRS server. 

### Customize settings:
If you want to customize the settings of the media server,you should run the continer using `docker run -it` ,and add `bash` or `/bin/bash -c "while 1;do sleep 1;done"` parameter at the end of the command.

### Port Settings:
 
Alternative HTTP Server port:`80`  
RTSP main port:`554`  
RTMP:`1935`  
HTTP API:`1985`  
RTMP Control API using go-oryx:`2037`  
HTTP Server Control API using go-oryx:`2038`  
HTTP API Control API using go-oryx:`2039`  
Go-oryx Worker Control API using go-oryx:`2040`  
HTTP Server:`8080`  
Websocket Server:`8081`  
HTTP-Flv Pushing:`8936`  
RTSP using go-oryx:`50000-51000`  
RTSP using SRS:`57000-58000` 

### Link Details: 

RTMP:`rtmp://<ip>/<app>/<stream>`  
HLS:`http://<ip>:8080/hls/<app>/<stream>.m3u8`  
HTTP Server:`http://<ip>:8080/`  
HTTP Flv:`http://<ip>:8080/http/<app>/<stream>.flv`  
Admin Consle:`http://<ip>:8080/srs-console/index.html`  
Other links and settings,please refer to the config file.

### File settings:
`/root/start.sh` is a soft link of `/root/shell/start_srs.sh` ,which is a sample starting script using srs itself.  
`/root/stop.sh` is a soft link of `/root/shell/stop.sh` ,which is a sample stoping script.  
Other shell scripts for launching single program are included in the `/root/shell` folder.  
You can change them according to your own condition.  

### Volume setting:  
`/root/software` is the folder for the program files.  
The two sub folders `go-oryx/conf` and `srs/trunk/conf` are the configuration files folder,which are mounted by default.  
`/root/logs` is the folder for all the log files,and is mounted by default.  
`/root/sample_conf` is the folder for sample configuration files,and it's mounted by default.  
`/root/shell` is the folder for the sample starting&stoping scripts,and it's mounted by default.
