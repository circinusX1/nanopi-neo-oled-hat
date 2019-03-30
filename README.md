## my first and I hope my last python script 

    * For NANO PI NEO OLED HAT, after you have cloned the NanoHatOLED you can cutomize and display your text.
    * KIll all started OLED processes in /etc/rc.local

```
cd NanoHatOLED/BakeBit/Software/Python

```
    * Make a new python file there.
    * Copy following content

```

#!/usr/bin/env python

import bakebit_128_64_oled as oled
from PIL import Image
from PIL import ImageFont
from PIL import ImageDraw
import time
import sys
import subprocess
import threading
import signal
import os
import socket

global width
width=128
global height
height=64

oled.init()  			#initialze SEEED OLED display
oled.setNormalDisplay()      #Set display to normal mode (i.e non-inverse mode)
oled.setHorizontalMode()


global image
image = Image.new('1', (width, height))
global draw
draw = ImageDraw.Draw(image)
global fontb24
fontb24 = ImageFont.truetype('DejaVuSansMono-Bold.ttf', 24);
global font14 
font14 = ImageFont.truetype('DejaVuSansMono.ttf', 14);
global smartFont
smartFont = ImageFont.truetype('DejaVuSansMono-Bold.ttf', 10);
global fontb14
fontb14 = ImageFont.truetype('DejaVuSansMono-Bold.ttf', 14);
global font11
font11 = ImageFont.truetype('DejaVuSansMono.ttf', 11);


def draw_page():
    global image
    global draw
    global oled
    global font
    global font11
    global fontb14
    global fontb24
    global smartFont
    global width
    global height
    global width
    global height
    g = globals()
    l = locals();

    draw.rectangle((0,0,width,height), outline=0, fill=0)
    if  os.path.isfile("/tmp/oled"):
        s = open("/tmp/oled", 'r').read()
        parts = s.split("\n",8)
	y=0
        for line in parts:
	    draw.text((2,y),line,font=fontb14,fill=255)
	    y+=16
    oled.drawImage(image);


while True:
    draw_page()
```

    * The run
    
```
pi@NanoPi-NEO:~/oled/NanoHatOLED/BakeBit/Software/Python$ sudo python ./xxxx.py

```
    * You can start '/oled/NanoHatOLED/BakeBit/Software/Python$ sudo python ./xxxx.py' in /etc/rc.local
    * To display test echo some stirngs in /tmp/oled
    
```    
echo -e "first line \n second line \n  third line \n fourth line " > /tmp/oled
```
