# Audio Recognition Python SDK

## Overview
  [ACRCloud](https://www.acrcloud.com/) provides cloud [Automatic Content Recognition](https://www.acrcloud.com/docs/introduction/automatic-content-recognition/) services for [Audio Fingerprinting](https://www.acrcloud.com/docs/introduction/audio-fingerprinting/) based applications such as **[Audio Recognition](https://www.acrcloud.com/music-recognition)** (supports music, video, ads for both online and offline), **[Broadcast Monitoring](https://www.acrcloud.com/broadcast-monitoring)**, **[Second Screen](https://www.acrcloud.com/second-screen-synchronization)**, **[Copyright Protection](https://www.acrcloud.com/copyright-protection-de-duplication)** and etc.<br>
  
  This **audio recognition python SDK** support most of audio / video files. 

>>Audio: mp3, wav, m4a, flac, aac, amr, ape, ogg ...<br>
>>Video: mp4, mkv, wmv, flv, ts, avi ...

## Requirements
Follow one of the tutorials to create a project and get your host, access_key and access_secret.

 * [How to identify songs by sound](https://www.acrcloud.com/docs/tutorials/identify-music-by-sound/)
 
 * [How to detect custom audio content by sound](https://www.acrcloud.com/docs/tutorials/identify-audio-custom-content/)

## Install
sudo python setup.py install

## Windows Runtime Library 
**If you run the SDK on Windows, you must install this library.**<br>
X86: [download and install Library(windows/vcredist_x86.exe)](https://www.microsoft.com/en-us/download/details.aspx?id=5555)<br>
x64: [download and install Library(windows/vcredist_x64.exe)](https://www.microsoft.com/en-us/download/details.aspx?id=14632)

## Note
1. If you run the SDK on Windows, you must install library(vcredist).

## Functions
Introduction all API.
### recognizer.py
```python
class ACRCloudRecognizer:
    def recognize_by_file(self, file_path, start_seconds):
      #@param file_path : query file path
      #@param start_seconds : skip (start_seconds) seconds from from the beginning of (filePath)
      #@return result metainfos
      
    def recognize_by_filebuffer(self, file_buffer, start_seconds):
      #@param file_buffer : file_path query buffer
      #@param start_seconds : skip (start_seconds) seconds from from the beginning of (filePath)
      #@return result metainfos
      
    def recognize(self, wav_audio_buffer):
      #@param wav_audio_buffer : query buffer(RIFF (little-endian) data, WAVE audio, Microsoft PCM, 16 bit, mono 8000 Hz)
      #@return result metainfos
```
### Module acrcloud_extr_tool
```python
def create_fingerprint_by_file(file_name, start_time_seconds, audio_len_seconds, is_db_fingerprint):
      #file_name: Path of input file; 
      #start_time_seconds: Start time of input file, default is 0; 
      #audio_len_seconds: Length of audio data you need. if you create recogize frigerprint, default is 12 seconds, if you create db frigerprint, it is not usefully; 
      #is_db_fingerprint: If it is True, it will create db frigerprint; 

def create_fingerprint_by_filebuffer(data_buffer, start_time_seconds, audio_len_seconds, is_db_fingerprint):
      #data_buffer: data buffer of input file; 
      #start_time_seconds: Start time of input file, default is 0; 
      #audio_len_seconds: Length of audio data you need. if you create recogize frigerprint, default is 12 seconds, if you create db frigerprint, it is not usefully; 
      #is_db_fingerprint: If it is True, it will create db frigerprint; 

def create_fingerprint(data_buffer, is_db_fingerprint):
      #data_buffer: audio data buffer(RIFF (little-endian) data, WAVE audio, Microsoft PCM, 16 bit, mono 8000 Hz); 
      #is_db_fingerprint: If it is True, it will create db frigerprint; 

def decode_audio_by_file(file_name, start_time_seconds, audio_len_seconds):
      #It will return the audio data(RIFF (little-endian) data, WAVE audio, Microsoft PCM, 16 bit, mono 8000 Hz); 
      #file_name: Path of input file; 
      #start_time_seconds: Start time of input file, default is 0; 
      #audio_len_seconds: Length of audio data you need, if it is 0, will decode all the audio; 

def decode_audio_by_filebuffer(data_buffer, start_time_seconds, audio_len_seconds):
      #It will return the audio data(RIFF (little-endian) data, WAVE audio, Microsoft PCM, 16 bit, mono 8000 Hz); 
      #data_buffer: data buffer of input file; 
      #start_time_seconds: Start time of input file, default is 0; 
      #audio_len_seconds: Length of audio data you need, if it is 0, will decode all the audio; 

def version() 
      #return the version of this module
```
## Example
run Test: python test.py test.mp3
```python
#!/usr/bin/env python
#-*- coding:utf-8 -*-

import os, sys
from acrcloud.recognizer import ACRCloudRecognizer

if __name__ == '__main__':
    config = {
        #Replace "xxxxxxxx" below with your project's host, access_key and access_secret.
        'host':'XXXXXXXX',
        'access_key':'XXXXXXXX', 
        'access_secret':'XXXXXXXX',
        'timeout':10 # seconds
    }

    '''This module can recognize ACRCloud by most of audio/video file. 
        Audio: mp3, wav, m4a, flac, aac, amr, ape, ogg ...
        Video: mp4, mkv, wmv, flv, ts, avi ...'''
    re = ACRCloudRecognizer(config)

    #recognize by file path, and skip 0 seconds from from the beginning of sys.argv[1].
    print re.recognize_by_file(sys.argv[1], 0)

    buf = open(sys.argv[1], 'rb').read()
    #recognize by file_audio_buffer that read from file path, and skip 0 seconds from from the beginning of sys.argv[1].
    print re.recognize_by_filebuffer(buf, 0)
```
