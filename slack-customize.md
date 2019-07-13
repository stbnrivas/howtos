# slack change to dark mode

```bash
wget http://neckcode.com/slack/ssb-interop.js.zip
```



```bash
cd /var/lib/flatpak/app/com.slack.Slack/
cd x86_64/stable/810ae703189dd439c5a7059accf33af495d415e2d46545a3bfcccf445ab7c092/files/extra/lib/slack/resources/
cd  app.asar.unpacked/src/static/

mv ssb-interop.js ssb-interop.js.ori
curl https://raw.githubusercontent.com/caiceA/slack-black-theme/master/ssb-interop.js --output ssb-interop.js


```
