[toc]


1. 进入bin所在的父目录下。shift+鼠标右键 -> 打开git bash shell
2. 逐行输入
```
    export DEBUG=dss*

    set DEBUG=dss*

    npm install

    npm start
```


- 注意：
	- windows和linux下使用时，注意，要从原始压缩包开始重新进行npm install，只有这样运行npm start时才会成功，因为在不同平台下执行npm install 加载的包不一样

```

  dss:boot online @ 3001 +0ms
  dss GET /data/PC 404 - - 2.325 ms +0ms
  dss GET /data/PC 404 - - 0.512 ms +426ms
  dss GET /data/PC 404 - - 0.446 ms +529ms
  dss GET /data/PC 404 - - 0.075 ms +474ms
  dss GET /data/PC 404 - - 0.054 ms +515ms
  dss GET /data/PC 404 - - 0.065 ms +480ms
  dss GET /data/PC 404 - - 0.052 ms +525ms
  dss GET /data/UNITY 404 - - 0.059 ms +276ms
  dss GET /data/PC 404 - - 0.054 ms +239ms
  dss GET /data/UNITY 404 - - 0.053 ms +136ms
  dss GET /data/PC 404 - - 0.052 ms +344ms
  dss GET /data/UNITY 404 - - 0.070 ms +160ms
  dss GET /data/PC 404 - - 0.052 ms +365ms
  dss GET /data/UNITY 404 - - 0.428 ms +161ms
  dss GET /data/PC 404 - - 0.058 ms +319ms
  dss GET /data/UNITY 404 - - 0.182 ms +161ms
  dss GET /data/PC 404 - - 0.057 ms +354ms
  dss GET /data/UNITY 404 - - 0.052 ms +206ms
  dss GET /data/PC 404 - - 0.063 ms +319ms
  dss:body {"MessageType":3,"Data":"candidate:1153648606 1 udp 2122197247 2409:8970:10e1:4383:ddaa:9c45:dba0:2810 61309 typ host generation 0 ufrag Xxeh network-id 3 network-cost 10|1|1","IceDataSeparator":"|"} +0ms
  dss POST /data/UNITY 200 - - 2.046 ms +138ms
  dss:body {"MessageType":3,"Data":"candidate:375418661 1 udp 2122262783 2409:8970:10e1:4383:904f:1941:89ca:1dc3 61308 typ host generation 0 ufrag Xxeh network-id 2 network-cost 10|1|1","IceDataSeparator":"|"} +2ms
  dss POST /data/UNITY 200 - - 0.542 ms +3ms
  dss:body {"MessageType":3,"Data":"candidate:1153648606 1 udp 2122197247 2409:8970:10e1:4383:ddaa:9c45:dba0:2810 61306 typ host generation 0 ufrag Xxeh network-id 3 network-cost 10|0|0","IceDataSeparator":"|"} +5ms
  dss POST /data/UNITY 200 - - 4.689 ms +4ms
  dss:body {"MessageType":3,"Data":"candidate:375418661 1 udp 2122262783 2409:8970:10e1:4383:904f:1941:89ca:1dc3 61305 typ host generation 0 ufrag Xxeh network-id 2 network-cost 10|0|0","IceDataSeparator":"|"} +16ms
  dss POST /data/UNITY 200 - - 15.720 ms +16ms
  dss:body {"MessageType":3,"Data":"candidate:583039341 1 udp 2122129151 192.168.43.187 61307 typ host generation 0 ufrag Xxeh network-id 1 network-cost 10|0|0","IceDataSeparator":"|"} +7ms
  dss POST /data/UNITY 200 - - 0.286 ms +8ms
  dss:body {"MessageType":3,"Data":"candidate:583039341 1 udp 2122129151 192.168.43.187 61310 typ host generation 0 ufrag Xxeh network-id 1 network-cost 10|1|1","IceDataSeparator":"|"} +6ms
  dss POST /data/UNITY 200 - - 0.207 ms +5ms
  dss:body {"MessageType":3,"Data":"candidate:1491309525 1 tcp 1518283007 2409:8970:10e1:4383:904f:1941:89ca:1dc3 49292 typ host tcptype passive generation 0 ufrag Xxeh network-id 2 network-cost 10|0|0","IceDataSeparator":"|"} +2ms
  dss POST /data/UNITY 200 - - 5.079 ms +2ms
  dss GET /data/UNITY 200 - - 0.072 ms +2ms
  dss:body {"MessageType":3,"Data":"candidate:172014382 1 tcp 1518217471 2409:8970:10e1:4383:ddaa:9c45:dba0:2810 49293 typ host tcptype passive generation 0 ufrag Xxeh network-id 3 network-cost 10|0|0","IceDataSeparator":"|"} +30ms
  dss POST /data/UNITY 200 - - 5.176 ms +29ms
  dss:body {"MessageType":3,"Data":"candidate:1816364445 1 tcp 1518149375 192.168.43.187 49297 typ host tcptype passive generation 0 ufrag Xxeh network-id 1 network-cost 10|1|1","IceDataSeparator":"|"} +5ms
  dss POST /data/UNITY 200 - - 0.171 ms +4ms
  dss:body {"MessageType":3,"Data":"candidate:172014382 1 tcp 1518217471 2409:8970:10e1:4383:ddaa:9c45:dba0:2810 49296 typ host tcptype passive generation 0 ufrag Xxeh network-id 3 network-cost 10|1|1","IceDataSeparator":"|"} +1ms
  dss POST /data/UNITY 200 - - 5.339 ms +1ms
  dss:body {"MessageType":3,"Data":"candidate:1491309525 1 tcp 1518283007 2409:8970:10e1:4383:904f:1941:89ca:1dc3 49295 typ host tcptype passive generation 0 ufrag Xxeh network-id 2 network-cost 10|1|1","IceDataSeparator":"|"} +8ms
  dss POST /data/UNITY 200 - - 0.157 ms +8ms
  dss:body {"MessageType":3,"Data":"candidate:1816364445 1 tcp 1518149375 192.168.43.187 49294 typ host tcptype passive generation 0 ufrag Xxeh network-id 1 network-cost 10|0|0","IceDataSeparator":"|"} +0ms
  dss POST /data/UNITY 200 - - 0.280 ms +0ms
  dss:body {"MessageType":1,"Data":"v=0\r\no=- 633218473215359903 2 IN IP4 127.0.0.1\r\ns=-\r\nt=0 0\r\na=group:BUNDLE 0 1\r\na=msid-semantic: WMS\r\nm=audio 9 UDP/TLS/RTP/SAVPF 111 103 104 9 102 0 8 106 105 13 110 112 113 126\r\nc=IN IP4 0.0.0.0\r\na=rtcp:9 IN IP4 0.0.0.0\r\na=ice-ufrag:Xxeh\r\na=ice-pwd:2xJy0RTPddXIVVcO5jl4mDi/\r\na=ice-options:trickle\r\na=fingerprint:sha-256 27:76:BC:6E:74:1E:00:6C:19:B8:E2:04:49:C4:37:05:91:44:AF:60:CB:D5:B8:8E:B6:7C:FE:02:CB:1F:3B:BA\r\na=setup:actpass\r\na=mid:0\r\na=extmap:1 urn:ietf:params:rtp-hdrext:ssrc-audio-level\r\na=extmap:9 urn:ietf:params:rtp-hdrext:sdes:mid\r\na=sendrecv\r\na=msid:- 55e0ff04-9874-49f6-becd-23da69e4c9e8\r\na=rtcp-mux\r\na=rtpmap:111 opus/48000/2\r\na=rtcp-fb:111 transport-cc\r\na=fmtp:111 minptime=10;useinbandfec=1\r\na=rtpmap:103 ISAC/16000\r\na=rtpmap:104 ISAC/32000\r\na=rtpmap:9 G722/8000\r\na=rtpmap:102 ILBC/8000\r\na=rtpmap:0 PCMU/8000\r\na=rtpmap:8 PCMA/8000\r\na=rtpmap:106 CN/32000\r\na=rtpmap:105 CN/16000\r\na=rtpmap:13 CN/8000\r\na=rtpmap:110 telephone-event/48000\r\na=rtpmap:112 telephone-event/32000\r\na=rtpmap:113 telephone-event/16000\r\na=rtpmap:126 telephone-event/8000\r\na=ssrc:3854352483 cname:TZwGz9qJaMhd20x4\r\na=ssrc:3854352483 msid: 55e0ff04-9874-49f6-becd-23da69e4c9e8\r\na=ssrc:3854352483 mslabel:\r\na=ssrc:3854352483 label:55e0ff04-9874-49f6-becd-23da69e4c9e8\r\nm=video 9 UDP/TLS/RTP/SAVPF 96 97 98 99 100 101 127 124 125\r\nc=IN IP4 0.0.0.0\r\na=rtcp:9 IN IP4 0.0.0.0\r\na=ice-ufrag:Xxeh\r\na=ice-pwd:2xJy0RTPddXIVVcO5jl4mDi/\r\na=ice-options:trickle\r\na=fingerprint:sha-256 27:76:BC:6E:74:1E:00:6C:19:B8:E2:04:49:C4:37:05:91:44:AF:60:CB:D5:B8:8E:B6:7C:FE:02:CB:1F:3B:BA\r\na=setup:actpass\r\na=mid:1\r\na=extmap:2 urn:ietf:params:rtp-hdrext:toffset\r\na=extmap:3 http://www.webrtc.org/experiments/rtp-hdrext/abs-send-time\r\na=extmap:4 urn:3gpp:video-orientation\r\na=extmap:5 http://www.ietf.org/id/draft-holmer-rmcat-transport-wide-cc-extensions-01\r\na=extmap:6 http://www.webrtc.org/experiments/rtp-hdrext/playout-delay\r\na=extmap:7 http://www.webrtc.org/experiments/rtp-hdrext/video-content-type\r\na=extmap:8 http://www.webrtc.org/experiments/rtp-hdrext/video-timing\r\na=extmap:10 http://tools.ietf.org/html/draft-ietf-avtext-framemarking-07\r\na=extmap:9 urn:ietf:params:rtp-hdrext:sdes:mid\r\na=sendrecv\r\na=msid:- 2c7a0b7f-ac56-4fc6-81da-2973d2e3e94f\r\na=rtcp-mux\r\na=rtcp-rsize\r\na=rtpmap:96 VP8/90000\r\na=rtcp-fb:96 goog-remb\r\na=rtcp-fb:96 transport-cc\r\na=rtcp-fb:96 ccm fir\r\na=rtcp-fb:96 nack\r\na=rtcp-fb:96 nack pli\r\na=rtpmap:97 rtx/90000\r\na=fmtp:97 apt=96\r\na=rtpmap:98 VP9/90000\r\na=rtcp-fb:98 goog-remb\r\na=rtcp-fb:98 transport-cc\r\na=rtcp-fb:98 ccm fir\r\na=rtcp-fb:98 nack\r\na=rtcp-fb:98 nack pli\r\na=fmtp:98 x-google-profile-id=0\r\na=rtpmap:99 rtx/90000\r\na=fmtp:99 apt=98\r\na=rtpmap:100 multiplex/90000\r\na=rtcp-fb:100 goog-remb\r\na=rtcp-fb:100 transport-cc\r\na=rtcp-fb:100 ccm fir\r\na=rtcp-fb:100 nack\r\na=rtcp-fb:100 nack pli\r\na=fmtp:100 acn=VP9;x-google-profile-id=0\r\na=rtpmap:101 rtx/90000\r\na=fmtp:101 apt=100\r\na=rtpmap:127 red/90000\r\na=rtpmap:124 rtx/90000\r\na=fmtp:124 apt=127\r\na=rtpmap:125 ulpfec/90000\r\na=ssrc-group:FID 2475663826 879813117\r\na=ssrc:2475663826 cname:TZwGz9qJaMhd20x4\r\na=ssrc:2475663826 msid: 2c7a0b7f-ac56-4fc6-81da-2973d2e3e94f\r\na=ssrc:2475663826 mslabel:\r\na=ssrc:2475663826 label:2c7a0b7f-ac56-4fc6-81da-2973d2e3e94f\r\na=ssrc:879813117 cname:TZwGz9qJaMhd20x4\r\na=ssrc:879813117 msid: 2c7a0b7f-ac56-4fc6-81da-2973d2e3e94f\r\na=ssrc:879813117 mslabel:\r\na=ssrc:879813117 label:2c7a0b7f-ac56-4fc6-81da-2973d2e3e94f\r\n","IceDataSeparator":""} +46ms
  dss POST /data/UNITY 200 - - 104.750 ms +46ms
  dss GET /data/UNITY 200 - - 0.079 ms +10ms
  dss GET /data/UNITY 200 - - 0.057 ms +81ms
  dss GET /data/PC 404 - - 0.054 ms +123ms
  dss GET /data/UNITY 200 - - 0.037 ms +0ms
  dss GET /data/UNITY 200 - - 0.062 ms +111ms
  dss GET /data/UNITY 200 - - 0.059 ms +130ms
  dss GET /data/UNITY 200 - - 0.088 ms +101ms
  dss GET /data/UNITY 200 - - 0.065 ms +99ms
  dss GET /data/PC 404 - - 0.061 ms +89ms
  dss GET /data/UNITY 200 - - 0.244 ms +1ms
  dss GET /data/UNITY 200 - - 0.421 ms +110ms
  dss GET /data/UNITY 200 - - 0.108 ms +115ms
  dss GET /data/UNITY 200 - - 0.063 ms +80ms
  dss GET /data/UNITY 200 - - 0.070 ms +130ms
  dss GET /data/PC 404 - - 0.054 ms +74ms
  dss GET /data/UNITY 404 - - 0.054 ms +91ms
  dss:body {"MessageType":3,"Data":"candidate:1378922506 1 udp 2122197247 2409:8970:10e1:4383:9147:d1db:b81b:8109 55777 typ host generation 0 ufrag uX9W network-id 3 network-cost 10|0|0","IceDataSeparator":"|"} +2s
  dss POST /data/PC 200 - - 4.802 ms +236ms
  dss:body {"MessageType":2,"Data":"v=0\r\no=- 7940498730907357895 2 IN IP4 127.0.0.1\r\ns=-\r\nt=0 0\r\na=group:BUNDLE 0 1\r\na=msid-semantic: WMS\r\nm=audio 9 UDP/TLS/RTP/SAVPF 111 103 104 9 102 0 8 106 105 13 110 112 113 126\r\nc=IN IP4 0.0.0.0\r\na=rtcp:9 IN IP4 0.0.0.0\r\na=ice-ufrag:uX9W\r\na=ice-pwd:Lp5a2h9I6xS6aKIP+BELM6zz\r\na=ice-options:trickle\r\na=fingerprint:sha-256 74:A7:BE:F4:28:EB:55:01:6F:1E:A1:67:1C:12:70:39:83:3F:D0:4E:C0:82:31:CE:A0:1B:0F:4E:82:7E:1E:B5\r\na=setup:active\r\na=mid:0\r\na=extmap:1 urn:ietf:params:rtp-hdrext:ssrc-audio-level\r\na=extmap:9 urn:ietf:params:rtp-hdrext:sdes:mid\r\na=sendrecv\r\na=msid:- c6f2c48c-d84e-49dc-a6f0-d67329a89d88\r\na=rtcp-mux\r\na=rtpmap:111 opus/48000/2\r\na=rtcp-fb:111 transport-cc\r\na=fmtp:111 minptime=10;useinbandfec=1\r\na=rtpmap:103 ISAC/16000\r\na=rtpmap:104 ISAC/32000\r\na=rtpmap:9 G722/8000\r\na=rtpmap:102 ILBC/8000\r\na=rtpmap:0 PCMU/8000\r\na=rtpmap:8 PCMA/8000\r\na=rtpmap:106 CN/32000\r\na=rtpmap:105 CN/16000\r\na=rtpmap:13 CN/8000\r\na=rtpmap:110 telephone-event/48000\r\na=rtpmap:112 telephone-event/32000\r\na=rtpmap:113 telephone-event/16000\r\na=rtpmap:126 telephone-event/8000\r\na=ssrc:2608653346 cname:zeInPLsNDZzACA3g\r\nm=video 9 UDP/TLS/RTP/SAVPF 96 97 98 99 100 101 127 124 125\r\nc=IN IP4 0.0.0.0\r\na=rtcp:9 IN IP4 0.0.0.0\r\na=ice-ufrag:uX9W\r\na=ice-pwd:Lp5a2h9I6xS6aKIP+BELM6zz\r\na=ice-options:trickle\r\na=fingerprint:sha-256 74:A7:BE:F4:28:EB:55:01:6F:1E:A1:67:1C:12:70:39:83:3F:D0:4E:C0:82:31:CE:A0:1B:0F:4E:82:7E:1E:B5\r\na=setup:active\r\na=mid:1\r\na=extmap:2 urn:ietf:params:rtp-hdrext:toffset\r\na=extmap:3 http://www.webrtc.org/experiments/rtp-hdrext/abs-send-time\r\na=extmap:4 urn:3gpp:video-orientation\r\na=extmap:5 http://www.ietf.org/id/draft-holmer-rmcat-transport-wide-cc-extensions-01\r\na=extmap:6 http://www.webrtc.org/experiments/rtp-hdrext/playout-delay\r\na=extmap:7 http://www.webrtc.org/experiments/rtp-hdrext/video-content-type\r\na=extmap:8 http://www.webrtc.org/experiments/rtp-hdrext/video-timing\r\na=extmap:10 http://tools.ietf.org/html/draft-ietf-avtext-framemarking-07\r\na=extmap:9 urn:ietf:params:rtp-hdrext:sdes:mid\r\na=sendrecv\r\na=msid:- eab3e3fe-4869-4c83-a65c-0bac35414754\r\na=rtcp-mux\r\na=rtcp-rsize\r\na=rtpmap:96 VP8/90000\r\na=rtcp-fb:96 goog-remb\r\na=rtcp-fb:96 transport-cc\r\na=rtcp-fb:96 ccm fir\r\na=rtcp-fb:96 nack\r\na=rtcp-fb:96 nack pli\r\na=rtpmap:97 rtx/90000\r\na=fmtp:97 apt=96\r\na=rtpmap:98 VP9/90000\r\na=rtcp-fb:98 goog-remb\r\na=rtcp-fb:98 transport-cc\r\na=rtcp-fb:98 ccm fir\r\na=rtcp-fb:98 nack\r\na=rtcp-fb:98 nack pli\r\na=fmtp:98 x-google-profile-id=0\r\na=rtpmap:99 rtx/90000\r\na=fmtp:99 apt=98\r\na=rtpmap:100 multiplex/90000\r\na=rtcp-fb:100 goog-remb\r\na=rtcp-fb:100 transport-cc\r\na=rtcp-fb:100 ccm fir\r\na=rtcp-fb:100 nack\r\na=rtcp-fb:100 nack pli\r\na=fmtp:100 acn=VP9;x-google-profile-id=0\r\na=rtpmap:101 rtx/90000\r\na=fmtp:101 apt=100\r\na=rtpmap:127 red/90000\r\na=rtpmap:124 rtx/90000\r\na=fmtp:124 apt=127\r\na=rtpmap:125 ulpfec/90000\r\na=ssrc-group:FID 1636970736 2908761298\r\na=ssrc:1636970736 cname:zeInPLsNDZzACA3g\r\na=ssrc:2908761298 cname:zeInPLsNDZzACA3g\r\n","IceDataSeparator":""} +24ms
  dss POST /data/PC 200 - - 111.260 ms +25ms
  dss:body {"MessageType":3,"Data":"candidate:1971277814 1 udp 2122262783 2409:8970:10e1:4383:2ce6:8:b237:6731 55776 typ host generation 0 ufrag uX9W network-id 2 network-cost 10|0|0","IceDataSeparator":"|"} +5ms
  dss POST /data/PC 200 - - 4.945 ms +4ms
  dss:body {"MessageType":3,"Data":"candidate:3099195943 1 udp 2122129151 192.168.43.105 55778 typ host generation 0 ufrag uX9W network-id 1 network-cost 10|0|0","IceDataSeparator":"|"} +4ms
  dss POST /data/PC 200 - - 4.158 ms +4ms
  dss:body {"MessageType":3,"Data":"candidate:481512698 1 tcp 1518217471 2409:8970:10e1:4383:9147:d1db:b81b:8109 58684 typ host tcptype passive generation 0 ufrag uX9W network-id 3 network-cost 10|0|0","IceDataSeparator":"|"} +15ms
  dss POST /data/PC 200 - - 14.745 ms +15ms
  dss:body {"MessageType":3,"Data":"candidate:1006416646 1 tcp 1518283007 2409:8970:10e1:4383:2ce6:8:b237:6731 58683 typ host tcptype passive generation 0 ufrag uX9W network-id 2 network-cost 10|0|0","IceDataSeparator":"|"} +6ms
  dss POST /data/PC 200 - - 4.601 ms +6ms
  dss:body {"MessageType":3,"Data":"candidate:4130997975 1 tcp 1518149375 192.168.43.105 58685 typ host tcptype passive generation 0 ufrag uX9W network-id 1 network-cost 10|0|0","IceDataSeparator":"|"} +21ms
  dss POST /data/PC 200 - - 0.298 ms +21ms
  dss GET /data/PC 200 - - 0.069 ms +63ms
  dss GET /data/PC 200 - - 0.564 ms +80ms
```