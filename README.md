# Reproduce Artipie NPM not working

`asdf install`


Artipie steps

1. `docker-compose up` and start another terminal
2. generate JWT token
    ```
    export ARTIPIE_NPM_TOKEN=$(curl -X POST -d '{"name": "admin", "pass": "admin"}' -H 'Content-type: application/json' "http://localhost:8086/api/v1/oauth/token" | jq -j .token)
    ```
3. `cd npm-package`
4. `npm publish . --registry http://localhost:8086/npm/`

observe error
```
npm info using npm@9.6.5
npm info using node@v18.14.2
npm verb title npm publish .
npm verb argv "publish" "." "--registry" "http://localhost:8086/npm/"
npm verb logfile logs-max:0 dir:/Users/user/.npm/_logs/2023-05-04T20_13_24_443Z-
npm verb logfile no logfile created
npm verb publish [ '.' ]
npm sill logfile done cleaning log files
npm notice 
npm notice 📦  @1oglop1/npm-package@1.0.8
npm notice === Tarball Contents === 
npm notice 284B package.json
npm notice === Tarball Details === 
npm notice name:          @1oglop1/npm-package                    
npm notice version:       1.0.8                                   
npm notice filename:      1oglop1-npm-package-1.0.8.tgz           
npm notice package size:  272 B                                   
npm notice unpacked size: 284 B                                   
npm notice shasum:        08ce01859fd0ff37402cb4db50270b880eee2dc3
npm notice integrity:     sha512-E9OKVd9kLhcr7[...]FKM/smU9I4Suw==
npm notice total files:   1                                       
npm notice 
npm notice Publishing to http://localhost:8086/npm/ with tag latest and public access
npm http fetch PUT 404 http://localhost:8086/npm/@1oglop1%2fnpm-package 52ms
npm verb stack HttpErrorGeneral: 404 Not Found - PUT http://localhost:8086/npm/@1oglop1%2fnpm-package
npm verb stack     at /Users/user/.asdf/installs/nodejs/18.14.2/.npm/lib/node_modules/npm/node_modules/npm-registry-fetch/lib/check-response.js:95:15
npm verb stack     at process.processTicksAndRejections (node:internal/process/task_queues:95:5)
npm verb stack     at async publish (/Users/user/.asdf/installs/nodejs/18.14.2/.npm/lib/node_modules/npm/node_modules/libnpmpublish/lib/publish.js:48:12)
npm verb stack     at async otplease (/Users/user/.asdf/installs/nodejs/18.14.2/.npm/lib/node_modules/npm/lib/utils/otplease.js:4:12)
npm verb stack     at async Publish.exec (/Users/user/.asdf/installs/nodejs/18.14.2/.npm/lib/node_modules/npm/lib/commands/publish.js:128:7)
npm verb stack     at async module.exports (/Users/user/.asdf/installs/nodejs/18.14.2/.npm/lib/node_modules/npm/lib/cli.js:89:5)
npm verb statusCode 404
npm verb pkgid @1oglop1/npm-package@1.0.8
npm verb cwd /Users/user/work/stekz/tmp/artipie/npm-package
npm verb Darwin 22.4.0
npm verb node v18.14.2
npm verb npm  v9.6.5
npm ERR! code E404
npm ERR! 404 Not Found - PUT http://localhost:8086/npm/@1oglop1%2fnpm-package
npm ERR! 404 
npm ERR! 404  '@1oglop1/npm-package@1.0.8' is not in this registry.
npm ERR! 404 
npm ERR! 404 Note that you can also install from a
npm ERR! 404 tarball, folder, http url, or git url.
npm verb exit 1
npm verb code 1

npm ERR! Log files were not written due to the config logs-max=0
```

NPM steps

1. Go to https://www.npmjs.com/settings/<your nickname>/tokens
2. generate granular Access token
3. Then in your CLI
    ```
    export NPM_PAT_TOKEN=<your token>
    ```

Observe success
```
npm info using npm@9.6.5
npm info using node@v18.14.2
npm verb title npm publish .
npm verb argv "publish" "."
npm verb logfile logs-max:0 dir:/Users/<user>/.npm/_logs/2023-05-04T20_12_26_258Z-
npm verb logfile no logfile created
npm verb publish [ '.' ]
npm sill logfile done cleaning log files
npm notice 
npm notice 📦  @1oglop1/npm-package@1.0.8
npm notice === Tarball Contents === 
npm notice 284B package.json
npm notice === Tarball Details === 
npm notice name:          @1oglop1/npm-package                    
npm notice version:       1.0.8                                   
npm notice filename:      1oglop1-npm-package-1.0.8.tgz           
npm notice package size:  272 B                                   
npm notice unpacked size: 284 B                                   
npm notice shasum:        08ce01859fd0ff37402cb4db50270b880eee2dc3
npm notice integrity:     sha512-E9OKVd9kLhcr7[...]FKM/smU9I4Suw==
npm notice total files:   1                                       
npm notice 
npm notice Publishing to https://registry.npmjs.org/ with tag latest and public access
npm http fetch PUT 200 https://registry.npmjs.org/@1oglop1%2fnpm-package 1981ms
+ @1oglop1/npm-package@1.0.8
npm verb exit 0
npm info ok 
```
