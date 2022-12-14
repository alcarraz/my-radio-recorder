# Recording an online radio show
Some years ago, when I moved from my beloved country Uruguay, I wanted to listen to some radio shows to keep myself informed.

I chose a show called **No toquen nada**, at first I listened to it as a podcast, but pretty soon I started to want to hear it in real-time. The thing is, my OCD wouldn't allow me not to start listening from the beginning. And it started too early in my time zone.

## What I want
Even if I wake up early, I want to be able to pause it at any time and retake it at a faster pace, to synchronize myself afterward. But also I want to be able to listen to it after it started, and then listen at a fast pace, and obviously fast- forward the commercial breaks, to synchronize with it.

Also, it would be great to be able to perform all of those on any device, with access to the local network of course. I don't have a server on the cloud or with public IP.

## What I've done so far

My first attempt was simply to schedule a script with cron in my Raspberry Pi, which I use mainly as a media server, to record the show using `curl`:

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
https://github.com/alcarraz/my-radio-recorder/blob/3a815c4b06550e34109982fc23d7d513af4e9c4d/record-stream#L12-L27

## What I'm missing

With [`smplayer`](https://www.smplayer.info/) I am able to almost do what I want, I can listen at some multiplier velocity, but when it reaches the end I have to manually set the velocity at `1x`. But this only works on the PC, I couldn't find an app for my cellphone that can do that. VLC stops at some point when it reaches the size the file had when I opened it.

What I achieved so far is a good enough solution for me, with so little effort. But since now I have the time I can explore more sophisticated tools, including writing my own, for example my own app or a local web server with a basic UI that allows me to do what I want.

If you reached this point, and you have a need like mine, I hope this basic approach can be of some use to you. And if you know something that can resolve what is pending for my use case, please point me to some app or code I can use to build on top. I would really appreciate it.

