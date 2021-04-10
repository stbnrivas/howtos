# extract trac from cue


```bash
sudo apt-get install cuetools shntool flac

sudo dnf install cuetools shntool flac
```

```bash
cuebreakpoints file.cue | shnsplit -o flac file.flac
```
