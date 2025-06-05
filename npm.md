
Npm sometimes takes too long
By default it tries 10 times and takes around 33 seconds to fix it run
```ts
npm install --fetch-timeout=5000 --fetch-retries=2 --loglevel=info
```

Or set as default
```ts
npm set fetch-timeout 5000
npm set fetch-retries 2
```

