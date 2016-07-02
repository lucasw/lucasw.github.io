---
title: Logitech Webcams with ROS
layout: post
---

# Ubuntu 16.04 Kinetic

## C930e

```

[  374.906012] usb 3-6: new high-speed USB device number 2 using xhci_hcd
[  376.143343] usb 3-6: New USB device found, idVendor=046d, idProduct=0843
[  376.143346] usb 3-6: New USB device strings: Mfr=0, Product=2, SerialNumber=1
[  376.143348] usb 3-6: Product: Logitech Webcam C930e
[  376.143349] usb 3-6: SerialNumber: 7B1F226E
[  376.143846] uvcvideo: Found UVC 1.00 device Logitech Webcam C930e (046d:0843)
[  376.144175] input: Logitech Webcam C930e as /devices/pci0000:00/0000:00:14.0/usb3/3-6/3-6:1.0/input/input18
[  376.611638] usbcore: registered new interface driver snd-usb-audio
```

    Bus 003 Device 002: ID 046d:0843 Logitech, Inc. Webcam C930e


cheese works

```

$ uvcdynctrl -l
Listing available devices:
  video1   Logitech Webcam C930e
    Media controller device: /dev/media1
ERROR: Unable to open media controller device '/dev/media1': Permission denied (Error: 13)
ERROR: Unable to list device entities: Invalid device or device cannot be opened. (Code: 5)
```

pavucontrol shows the microphone as working


guvcview doesn't work

```
guvcview -d /dev/video1
V4L2_CORE: (UVCIOC_CTRL_MAP) Error: No such file or directory
V4L2_CORE: (UVCIOC_CTRL_MAP) Error: No such file or directory
V4L2_CORE: (UVCIOC_CTRL_MAP) Error: No such file or directory
V4L2_CORE: (UVCIOC_CTRL_MAP) Error: No such file or directory
V4L2_CORE: (UVCIOC_CTRL_MAP) Error: No such file or directory
V4L2_CORE: (UVCIOC_CTRL_MAP) Error: No such file or directory
V4L2_CORE: (UVCIOC_CTRL_MAP) Error: No such file or directory
V4L2_CORE: (UVCIOC_CTRL_MAP) Error: No such file or directory
V4L2_CORE: (UVCIOC_CTRL_MAP) Error: No such file or directory
ALSA lib pcm_dsnoop.c:606:(snd_pcm_dsnoop_open) unable to open slave
ALSA lib pcm_dmix.c:1029:(snd_pcm_dmix_open) unable to open slave
ALSA lib pcm.c:2266:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.rear
ALSA lib pcm.c:2266:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.center_lfe
ALSA lib pcm.c:2266:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.side
ALSA lib pcm_dmix.c:1029:(snd_pcm_dmix_open) unable to open slave
Cannot connect to server socket err = No such file or directory
Cannot connect to server request channel
jack server is not running or cannot be started
JackShmReadWritePtr::~JackShmReadWritePtr - Init not done for 4294967295, skipping unlock
JackShmReadWritePtr::~JackShmReadWritePtr - Init not done for 4294967295, skipping unlock
libv4l2: error setting pixformat: Device or resource busy
V4L2_CORE: (VIDIOC_S_FORMAT) Unable to set format: Device or resource busy
GUCVIEW: could not set the defined stream format
GUCVIEW: trying first listed stream format
libv4l2: error setting pixformat: Device or resource busy
V4L2_CORE: (VIDIOC_S_FORMAT) Unable to set format: Device or resource busy
GUCVIEW: also could not set the first listed stream format
GUVCVIEW: Video capture failed
Gtk-Message: GtkDialog mapped without a transient parent. This is discouraged.
V4L2_CORE: (VIDIOC_S_PARM) error: Device or resource busy
V4L2_CORE: Unable to set 1/2 fps
```

But this was because another process was using the device?
Kill some processes and now guvcview works.

## usb cam on ros


sudo apt-get install libv4l-dev

```
git clone https://github.com/lucasw/v4l2ucp.git
git clone https://github.com/lucasw/vimjay.git
git clone https://github.com/bosch-ros-pkg/usb_cam.git
```

```
[ WARN] [/usb_cam] [/home/lucasw/catkin_ws/src/usb_cam/src/usb_cam.cpp]:[1206] [sh: 1: v4l2-ctl: not found
]
[mjpeg @ 0x1bd2240] Changeing bps to 8
[mjpeg @ 0x1bd2240] overread 8
[mjpeg @ 0x1bd2240] EOI missing, emulating

[swscaler @ 0x1fd6a60] deprecated pixel format used, make sure you did set range correctly
```

But still works.
