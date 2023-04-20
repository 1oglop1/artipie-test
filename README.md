# Reproduce Artipie NPM not working

`asdf install`

export NPM_TOKEN=$(curl -X POST -d '{"name": "admin", "pass": "admin"}' -H 'Content-type: application/json' "http://localhost:8086/api/v1/oauth/token" | jq -j .token)

cd npm-project && npm publish . --registry http://localhost:8086/npm
