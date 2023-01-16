
<div  align="center"  style="background-color: #111; padding: 100;">
<a  href="https://github.com/xteve-project/xTeVe"><img  width="880"  height="200"  src="https://github.com/xteve-project/xTeVe/raw/master/html/img/logo_b_880x200.jpg"  alt="xTeVe"  /></a>
</div>
<br>

# Unoffical NVIDIA® CUDA® enabled container for xTeVe

### M3U Proxy for Plex DVR and Emby Live TV.

Documentation for setup and configuration of xTeVe is [here](https://github.com/xteve-project/xTeVe-Documentation/blob/master/en/configuration.md).

---

## Features

#### CUDA Enabled ffmpeg

* Use hardware transcoding
* User hardware deinterlacing
* Other hardware related things I guess?
* Python3 installed for scripting

---

## Hardware GPU

#### Using your NVIDIA GPU

I use the below as the settings for the ffmpeg encoder (obviously with ffmpeg selected)

**H.265 / HEVC Encoding**

```text

-hide_banner -loglevel error -hwaccel cuda -hwaccel_output_format nv12 -i [URL] -c:v hevc_nvenc -pix_fmt yuv420p -preset llhp -tune ull -rc cbr -multipass disabled -movflags +faststart -zerolatency 1 -tag:v hvc1 -c:a aac -c:s copy -f mpegts pipe:1

```

You can also add deinterlacing etc to your pipeline should you wish

*CUDA® name and the CUDA logo are a registered trademarks of Nvidia Corporation*
*NVIDIA® name and the NVIDIA logo are a registered trademarks of Nvidia Corporation*
