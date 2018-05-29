# librtmp

Fork from http://git.ffmpeg.org/rtmpdump integrated with srs.

Compare the code we modified: 

* [All commit](https://github.com/ossrs/librtmp/compare/master...feature/srsid)
* [Parse ip/pid/cid from SRS](https://github.com/ossrs/librtmp/commit/0e90e5dfa37e8b3e18944e76cf223d61e421f8cd)

Strongly recommend to use the [srs-librtmp](https://github.com/ossrs/srs-librtmp), which is stable
and more readable.

Winlin



## build 

> mkdir build && cd build && cmake -DCMAKE_BUILD_TYPE=Debug ../ && make

