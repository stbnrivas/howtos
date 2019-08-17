# slack change to dark mode 4.0

```bash
npm install -g asar

# mac
mkdir -p ~/tmp/slack
cp /Applications/Slack.app/Contents/Resources/app.asar ~/tmp/slack
cp -r /Applications/Slack.app/Contents/Resources/app.asar.unpacked ~/tmp/slack


# linux
cp /var/lib/flatpak/app/com.slack.Slack/current/active/files/extra/lib/slack/resources/app.asar /tmp/slack
cp -r /var/lib/flatpak/app/com.slack.Slack/current/active/files/extra/lib/slack/resources/app.asar.unpacked /tmp/slack

cd ~/tmp/slack
asar extract app.asar app

vim app/dist/ssb-interop.bundle.js
```

```js
//ssb-interop.bundle.js

document.addEventListener('DOMContentLoaded', function() {

  fetch('https://cdn.rawgit.com/laCour/slack-night-mode/master/css/raw/black.css')

  .then(function(response) {

    return response.text();

  })

  .then(function(css) {

    const style = document.createElement('style'); 

    style.innerHTML = css;

    document.head.appendChild(style);

  });

});



// ssb-interop.bundle.js

document.addEventListener('DOMContentLoaded', function() {

  $.ajax({

    url: 'https://cdn.rawgit.com/laCour/slack-night-mode/master/css/raw/black.css',

    success: function(css) {

      $("<style></style>").appendTo('head').html(css);

    }

  });

});
```

https://qiita.com/shoken/items/4f0bbba9b5d911657b5a


https://cdn.rawgit.com/laCour/slack-night-mode/master/css/raw/variants/black-monospaced.css

https://cdn.rawgit.com/laCour/slack-night-mode/master/css/raw/variants/aubergine.css

https://cdn.rawgit.com/laCour/slack-night-mode/master/css/raw/variants/aubergine-monospaced.css

https://cdn.rawgit.com/laCour/slack-night-mode/master/css/raw/variants/arc-dark.css

https://cdn.rawgit.com/laCour/slack-night-mode/master/css/raw/variants/midnight-blue.css

https://cdn.rawgit.com/laCour/slack-night-mode/master/css/raw/variants/midnight-blue-monospaced.css

https://cdn.rawgit.com/laCour/slack-night-mode/master/css/raw/variants/solarized-dark.css

https://cdn.rawgit.com/laCour/slack-night-mode/master/css/raw/variants/solarized-light.css


https://cdn.rawgit.com/laCour/slack-night-mode/master/css/raw/black.css


```bash
asar pack app app.asar

cp app.asar /var/lib/flatpak/app/com.slack.Slack/current/active/files/extra/lib/slack/resources/
cp -r /var/lib/flatpak/app/com.slack.Slack/current/active/files/extra/lib/slack/resources/ .

cp app.asar /var/lib/flatpak/app/com.slack.Slack/current/active/files/extra/lib/slack/resources

sudo cp app.asar /Applications/Slack.app/Contents/Resources
sudo cp app.asar /Applications/Slack.app/Contents/Resources
```



# slack change to dark mode previous 4.0

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
