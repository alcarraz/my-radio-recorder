# Recording a radio show
Some years ago, when I moved from my beloved country Uruguay, I wanted to listen to some radio shows to keep myself informed.

I chose a show called **No toquen nada**, at first I listened to it as a podcast, but pretty soon I started to wonted to hear it in real time. Thing is, my TOC wouldn't allow me to not start listening from the beginning. And it started to early in my time zone.

## What I want
Even if I wake up early, I want to be able to pause it at any time and retake it at a faster pace, to synchronize myself afterwards. But also I want to be able to listen to it after it started, and then listen at a fast pace, and obviously fast forward the commercial breaks, to synchronize with it.

Also, it would be great to be able to perform all of those in any device, with access to the local network of course. I don't have a server on the cloud or with public IP.

## What I've done so far

My first attempt, was simply to schedule a script with cron in my Raspberry PI, which I use mainly as a media server, to record the show using `curl`:

```bash
#!/bin/bash
# URL of the stream
url=$1

# How long to record in seconds
length=$2

# Where to store the recording
file=$3

curl -s  $url --retry 10 --retry-max-time 60 --max-time $length >> $file 
```

Pretty soon, just letting run `curl` for the duration of the show proved not to be good enough, if for some reason, the `curl` program hangs, the rest of the program isn't recorded.

So I ended up with the following script: 
https://github.com/alcarraz/my-radio-recorder/blob/3a815c4b06550e34109982fc23d7d513af4e9c4d/record-stream