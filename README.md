# DOAX3 Girls (doax3-girls)

Infos about the girls

## Install the dependencies
```bash
npm install
```

### Start the app in development mode (hot-code reloading, error reporting, etc.)
```bash
quasar dev
```

### Lint the files
```bash
npm run lint
```

### Build the app for production
```bash
quasar build
```

### Customize the configuration
See [Configuring quasar.conf.js](https://quasar.dev/quasar-cli/quasar-conf-js).


### Icons

```bash
svgexport src/assets/heart-logo.svg src/assets/heart-logo.png 1000:1000 pad
icongenie generate -i src/assets/heart-logo.png
```

### Parse site

```
(.+?)( ?([±*]+))?$
{ item: items['$1'], degree: '$3' },
```

### Convert to APK

```bash
rm doax3girls.apks; \
  java -jar ~/Downloads/bundletool-all-1.8.2.jar \
    build-apks --mode=universal \
    --bundle=src-cordova/platforms/android/app/build/outputs/bundle/release/app-release.aab \
    --output=doax3girls.apks; \
  unzip doax3girls.apks universal.apk
```
