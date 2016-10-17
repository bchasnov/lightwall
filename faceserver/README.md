# Face Server

This server runs [OpenFace](https://cmusatyalab.github.io/openface/) to classify known faces from a database.

Connect to FaceServer through websocket port 9000. Lists of supported messages are shown below.

## About OpenFace
OpenFace operates a pre-trained deep convolutional neural network based on [FaceNet](http://www.cv-foundation.org/openaccess/content_cvpr_2015/app/1A_089.pdf), implemented in Python and Torch.

## Requirements

- An Ubuntu server with a strong CPU
- docker installed on the Ubuntu server

## Getting Started *(unsupported)*

1. Make sure you are in the root folder folder `$ cd faceserver`
2. Pull the pre-built OpenFace docker build using `$ docker pull bamos/openface`
3. Run the docker build with the mounted folder ```$ docker run --name faceserver -v ./faceserver:/root/openface/faceserver -d -p 9000:9000 -p 8000:8000 -t -i bamos/openface /bin/bash```
 * `-d` runs  the container in the background
 * port 8000 is the http server and 9000 is websocket server
 * [ ] TODO: do not run in detached mode.
4. Attach to the docker  `$ docker attach faceserver --detach-keys="ctrl-x"`
5. Run faceserver inside docker `$ /bin/bash -l -c /root/openface/faceserver/start-faceserver.sh`
6. Detach docker by sending `ctrl-x`

### Docker Cheatsheet
View the docker process by `$ docker ps`

Start, stop, remove by running comands `$ docker [start/stop/rm] faceserver`

## Messages

### Sending image and receiving transparent bounding box overlay, and lists of persons
client-to-server:
```
dataURL = canvas.toDataURL('image/jpeg', 0.6)
msg = { 
    type: 'FRAME',
    dataURL: dataURL,
    identity: ?
}
```
Reply:
```
content = 'data:image/png;base64,' + \
urllib.quote(base64.b64encode(imgdata.buf))
msg = {
    type: 'FRAMEOVERLAY',
    content: content,
    personsn: 2,
    persons: ['name1','name2'],
    personsid: [1234, 2345],
    personsprob: [0.93, 0.84]
}
```
### Re-classify
client-to-server:
```
msg = {
    type: "RECLASSIFY",
}
```
### Server Status
``` 
msg = {
    type: "REQUEST_STATUS"
}
```

```
msg = {
    type: "STATUS",
    timesinceclassification: time,
    numberofpeople: n
}
```

### Polling
Since the FaceServer need to have low latency and high bandwidth (streaming camera 24/7), it should be located on the local network behind a firewall. However, user images are stored in the cloud.

To access the updated user images, FaceServer polls the cloud (AWS EC2) to see whether or not there is an updated list of photos. This happens 10 times a minute, every 12 seconds.

faceserver-to-cloud
```
msg = {
    type: "IS_UPDATED"
}
```

cloud-to-faceserver
```
msg = {
    type: "NEEDS_UPDATING",
    content: FALSE/TRUE
}
```

## TODOs
 - [ ] move to GPU processing
