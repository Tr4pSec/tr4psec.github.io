# BlueTeamLabs


Extracting hidden files with StegHide:
``` 
steghide extract -sf file.jpg -p "password" 
```

Extracting strings:
``` 
strings file.wav | awk 'length($0)>8' 
```

Python Script for extracting data from audio streams:
Ref https://medium.com/analytics-vidhya/get-secret-message-from-audio-file-8769421205c3

``` python3 ./test.py ```

```python 
import wave
import struct
wav = wave.open("file.wav", mode='rb')
frame_bytes = bytearray(list(wav.readframes(wav.getnframes())))
shorts = struct.unpack('H'*(len(frame_bytes)//2), frame_bytes)

extracted_left = shorts[::2] 
extracted_right = shorts[1::2]

extractedLSB = ""
for i in range(0, len(extracted_left)):
    extractedLSB += (str(extracted_left[i] & 1)) if i%2==0 else(str(extracted_right[i] & 1))
    
string_blocks = (extractedLSB[i:i+8] for i in range(0, len(extractedLSB), 8))
decoded = ''.join(chr(int(char, 2)) for char in string_blocks)
print(decoded[0:500])

wav.close()
```

Morse Code Decoder:
https://morsecode.world/international/decoder/audio-decoder-expert.html