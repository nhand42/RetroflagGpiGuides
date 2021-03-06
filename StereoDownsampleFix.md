![Banner Image](https://sinisterspatula.github.io/RetroflagGpiGuides/images/GuidesBanner.png)

[Back to Index](https://sinisterspatula.github.io/RetroflagGpiGuides/)


# Stereo Downsample Fix guide

  > If your Retroflag Gpi is missing some sounds (you only hear sounds destined for the Right speaker of the stereo audio), it may be due to the fact that it's outputing audio in a stereo format, but only has a mono speaker.  This fix will downsample the stereo audio into mono audio.

  * [SSH into your Pi](https://www.youtube.com/watch?v=aEJoQZBSlSs)
  * Enter the command `sudo nano /etc/asound.conf`

  * Paste the following code:

```
# convert stereo to mono output

# internal speaker only plays RIGHT channel
# headphone jack plays BOTH channels
# 50% volume per channel to prevent clipping
pcm.monocard{
  slave.pcm "hw:0"
  slave.channels 2
  type route
  ttable {
    # Copy both input channels to output channel 1 (Right).
    0.1 0.5
    1.1 0.5
    # Copy both input channels to output channel 0 (Left).
    0.0 0.5
    1.0 0.5
  }
}

pcm.!default monocard
```

  * [Ctrl+O] (to save) [Enter] and [Ctrl+X] (to exit)
  * Use Command `sudo reboot` to restart

## Support Thread
[Go here for help](https://www.facebook.com/groups/401660300458844/)

[Back to Index](https://sinisterspatula.github.io/RetroflagGpiGuides/)

###### Head back to our [Facebook Group](https://www.facebook.com/groups/401660300458844/)


