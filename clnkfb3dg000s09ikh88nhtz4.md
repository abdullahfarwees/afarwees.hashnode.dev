---
title: "Troubleshooting RTSP Playback Issues in VMS for specific IP Cameras - Interesting journey of solving the problem"
datePublished: Tue Oct 10 2023 14:34:35 GMT+0000 (Coordinated Universal Time)
cuid: clnkfb3dg000s09ikh88nhtz4
slug: troubleshooting-rtsp-playback-issues-in-vms-for-specific-ip-cameras-interesting-journey-of-solving-the-problem
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696948387016/ffeff4df-a8da-49df-947a-481886b3f433.jpeg
tags: streaming, rtsp, ip-camera, vms

---

**Introduction:**

In the world of video management software, ensuring seamless playback and livestreaming is a fundamental requirement. However, users often encounter challenges when dealing with different camera vendors. In this article, we dive into a specific issue that plagued our video management system (VMS) – the inability to playback and livestream from AXIS cameras via RTSP (Real-Time Streaming Protocol). It is a regression bug !.

**The Challenge:**

Live and playback video were accessible in 3rd party video players such as VLC using RTSP URLs for most camera vendors. Unfortunately, selective vendors, notably AXIS, presented a significant challenge. Our initial attempts at streaming AXIS camera footage from our Live555 media server were met with failure. It was clear that something needed to be done to resolve this issue.

**RTSP Validation:**

To pinpoint the problem, we embarked on a validation process. We selected recorded files from AXIS cameras stored in our VMS and experimented with RTSP streaming using our server. What we found was that Live555 did not support AVI file streaming. This raised a crucial point – the compatibility of file formats with our media server. We explored the list of supported formats by Live555, and AVI was conspicuously absent.

**Testing and Experimentation:**

Our next step was to record H.264 video directly from AXIS cameras and attempt to stream it directly from the Live555 media server. This experiment aimed to isolate the issue further. However, VMS records H.264 data in AVI file containers. When streaming RTSP, it reads H.264 frames from AVI files and sends individual frames to the Live555 media server. This was our first clue that the format might be the culprit.

**Working on the RTSP Streaming Experiment:**

We systematically tested various scenarios. First, we attempted to set up the VIMS (Video Management System) with AXIS, Arecont, and Wisenet cameras. While Arecont and Wisenet RTSP URLs played in VLC, AXIS did not cooperate.

We then tinkered with the camera's internal settings and managed to stream RTSP successfully with AXIS cameras. However, we faced issues when fetching and recording frames in H.264 with MKV and MP4 containers. Live555 media server couldn't stream these files, nor could it stream the ".264" files directly.

Moreover, even other camera vendors like Arecont, Vivotek, Panasonic, and more struggled to provide RTSP streams that could be captured by external frame grabbers like FFmpeg.

**Root Cause Identified:**

After thorough investigation, we found the root cause of the problem – unsupported profile streams in H.264 AXIS frames. This lack of support rendered RTSP playback impossible in AXIS cameras within our applications.

Two crucial experiments confirmed this problem. First, we played H.264 recorded files from different cameras in FFPLAY. AXIS camera files produced errors, while others played seamlessly.

Second, we used a media server to stream the H.264 files, with VLC as the client. The result was the same – AXIS files failed to broadcast.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696948230973/b06b2512-58fa-409c-9139-5a00a29a8ddd.png align="center")

**The Missing SPS and PPS Parameters:**

Upon deeper analysis, we discovered that the absence of Sequence Parameter Set (SPS) and Picture Parameter Set (PPS) parameters in AXIS data was **the primary issue**. These parameters are critical for the media server to function correctly. Other camera models provided the necessary structure for SPS and PPS, but AXIS did not.

**The Solution:**

To address this problem, we made code changes and conducted extensive testing. By adding PPS and SPS variables and making minor adjustments in the source code.

In the old code, certain frame types and position values led to issues in frame recognition by the media server. The new code preserved the starting index for header values, enabling proper recognition and streaming by the media server and VLC player.

* When the program encounters a frame with the type "H.264\_PictureParameterSet," it checks if `_ppsPacket` already exists and releases it if it does. Then, it creates a new `_ppsPacket` buffer and writes data from the incoming buffer into it, essentially saving the PPS header information.
    
* If `isSavePpsHeader` is `true` (which means we're dealing with a PPS header), it writes the `_startCode` data into the `_currentPacket` buffer at the current position, effectively adding the start code to the packet. This appears to be a necessary step for proper handling of the frame.
    

**Conclusion:**

Troubleshooting RTSP playback issues in AXIS cameras was a challenging journey. However, by identifying the root cause and making necessary code adjustments, we were able to overcome these hurdles and ensure seamless playback and livestreaming in our video management system. This experience highlights the importance of understanding the intricacies of video formats and the critical role of parameters like SPS and PPS in ensuring smooth RTSP streaming. Very few lines of code but huge effects !. This reminds the famous quote…😎

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696948272878/1f903a83-e9c8-4299-8dbc-e8dee452b42f.png align="center")