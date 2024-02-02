# electric-panda-json-server

![LGTM](https://i.lgtm.fun/2oph.png)

### RUN
```sh
$ npx json-server db.json

JSON Server started on PORT :3000
Press CTRL-C to stop
Watching db.json...

(˶ᵔ ᵕ ᵔ˶)

Index:
http://localhost:3000/

Static files:
Serving ./public directory if it exists

Endpoints:
http://localhost:3000/posts
http://localhost:3000/comments
http://localhost:3000/profile
```
### DEPOY
```sh
$ fly deploy
```
### fly.io install
1. branch 및 pr 생성 0.1.0/fly
2. Dockerfile 생성

```
FROM node:20.11

WORKDIR /app
 
RUN npm install -g npm

RUN npm install -g json-server
 
COPY ./db.json /app
 
CMD ["json-server", "-p", "80", "-w", "/app/db.json"]
```
 
3. https://fly.io/ 가입 - (주의! hobby plan 가입)
4. 무료 플랜 : https://fly.io/docs/about/pricing/#free-allowances
5. install cmd - https://fly.io/docs/hands-on/install-flyctl/
 
```sh
$ tail -n 3 ~/.zshrc
# fly
export FLYCTL_INSTALL="~/.fly"
export PATH="$FLYCTL_INSTALL/bin:$PATH"
 
$ source ~/.zshrc
```
 
7. flyctl auth login
8. flyctl launch 후 y 해서 용량을 256MB로 변경해야함. 그다음도 y하기.
```sh
flyctl launch
Scanning source code
Detected a Dockerfile app
Creating app in /home/awya5/code/electric-panda-json-server
We're about to launch your app on Fly.io. Here's what you're getting:

Organization: Yong Yong                  (fly launch defaults to the personal org)
Name:         electric-panda-json-server (derived from your directory name)
Region:       Tokyo, Japan               (this is the fastest region for you)
App Machines: shared-cpu-1x, 1GB RAM     (most apps need about 1GB of RAM)
Postgres:     <none>                     (not requested)
Redis:        <none>                     (not requested)

⚠️ ? Do you want to tweak these settings before proceeding? Yes
failed opening browser. Copy the url (https://fly.io/cli/launch/2861240a57dd0996bcaa8ec0df568345) into a browser and continue
Waiting for launch data... Done
Created app 'electric-panda-json-server' in organization 'personal'
Admin URL: https://fly.io/apps/electric-panda-json-server
Hostname: electric-panda-json-server.fly.dev
? Create .dockerignore from 1 .gitignore files? Yes
Created /home/awya5/code/electric-panda-json-server/.dockerignore from 1 .gitignore files.
Wrote config file fly.toml
Validating /home/awya5/code/electric-panda-json-server/fly.toml
Platform: machines
✓ Configuration is valid
==> Building image
```
9. cat fly.toml | grep internal
   internal_port = 80
10. flyctl deploy
 
```
.
.
.
https://electric-panda-json-server.fly.dev/
```


### FROM
- https://www.npmjs.com/package/json-server?activeTab=readme

