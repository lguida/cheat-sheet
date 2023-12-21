# cheat-sheet

## Node

### List available node versions 
```
nvm ls
```
### Switch node version
```
nvm use 20
```
### Remove node_modules
```
rm -rf node_modules
```
### Clear npm cache
```
npm cache clean --force
```
### Which arch is node using
```
node -p 'process.arch'
```

## Git

### Branch off of currently checked out branch
```
git checkout -b new-branch-name
```

### Merge in branch and rebase
```
git pull remote-name remote-branch-name --rebase
```
### Reset git action(s)
View a log of all past git actions across all branches. Grab the index from that list and then you can use the second command to reset the git history to that action
```
git reflog
git reset HEAD@{index}
```
### Squash all commits in a branch into one commit
```
git log <branch-name>
git rebase -i HEAD~3 #This rebases the last 3 branches
type `i` to get the editor to work
#then in the editor, change all but the first one to say ‘squash’ instead of ‘pick’
#then esc :wq for this screen and the next
git push origin <branch-name> --force
```
### Update remote url
```
git remote set-url <remote_name> <remote_url>
```
### Rename git remote
```
git remote rename old-name new-name
```
### initialize and install submodules
```
git submodule update --init
```

## Kubernetes

### List namespaces with your current NS highlighted
```
kubens
```
### Move to a given namespace
```
kubens namespace-name
```
### Get the Pod names in the current namespace
```
kubectl get pods
```
### Get All pods in all namespaces
```
kubectl get pods -A
```
### Get all pods in a namespace without moving to that namespace
```
kubectl get pods -n NAMESPACE-NAME
```
### set config to mmt-nonprod
```
export KUBECONFIG=~/.kube/conf-file-name.conf
```
### Restart a server
```
kubectl rollout restart deployment POD-NAME
```
### get logs:
use `kubectx` to get to the config file
then `kubens` to pick the namespace
```
# get the pods
kubectl get pods

# get logs
kubectl logs POD-NAME | pino-pretty

# or get pods with labels
kubectl get pods --show-labels

# get logs from label (may have different envs in it)
kubectl logs -l app=POD_LABEL | pino-pretty

# spit it into a file
kubectl logs POD-NAME | pino-pretty > ~/workspace/kubelogs/logs.txt

# Get the last 50 logs of the live pod
kubectl logs -f --tail 50 POD-NAME | pino-pretty
```

## AWS
### Configure Aws creds
```
aws configure
```

## Homebrew
See brew installed packages
```
brew list
```
or
```
brew list --cask
```

## Docker commands

## login to pull docker image from private github
```
echo $GITHUB_TOKEN | docker login ghcr.io -u github-username --password-stdin
```
## build docker image (note the period at the end!)
```
docker build -t <repo-name> .
```
## run security scan for docker image
```
trivy image --severity HIGH,CRITICAL <container-name>
```
## run docker build on a port with an env file
```
docker run -p 8000:8000 --env-file .env container-name
```
## clean docker cache
```
docker builder prune -a
```
## if running into invalid certificate found:
```
docker image prune
docker container prune
```

## Android:

### install apk to a specific device
```
# first cd to the location of the apk

adb devices

adb -s SERIAL install APK_FILENAME
```
## Get logs for Log tag:
```
adb logcat | grep LogTag
```
## get ip address for android localhost
```
ifconfig | grep 'inet '
```
## get app fingerprint
```
keytool -printcert -jarfile ./android/app/build/outputs/apk/dev/debug/apk-name.apk | grep SHA256
```

## React Native

### fix for Invariant Violation: Failed to call into JavaScript module method AppRegistry.runApplication().
```
npm start -- --reset-cache
```
## fix for Cocoapods incompatible versions
```
git checkout main ios/Podfile.lock
```

## Redis:

https://redis.io/docs/getting-started/installation/install-redis-on-mac-os/

### Start redis in foreground:
```
redis-server
# ^C to stop
```
### Start redis in the background:
```
brew services start redis

brew services info redis

brew services stop redis
```
### Test redis connection:
```
redis-cli
```

## zsh Permissions commands

### error that shows up:
```
zsh: permission denied:
```
### Show file permissions in current directory
note that there is a space after -l
```
ls -l 
```
### modify permissions
```
chmod a+x filename.sh //add execute to all users
chmod u-w filename.sh //remove write for current user
chmod g+r filename.sh //add write permissions for "group"
```

## Javascript

### print JSON formatted:
```
JSON.stringify(jsonVar, null, 2)
```
### Switch case alternative pattern:
```
 return (
      {
        ACCOUNT_ALERT: 'fcbe34454728e110c33ce738436d43e6',
        CARD_REPLACEMENT: 'a3cdfcc14728e110c33ce738436d4333',
        CLOSE_ACCOUNT: '8b1e38054728e110c33ce738436d431e',
        DIRECT_DEPOSIT: '384e78054728e110c33ce738436d43a0',
        DISPUTE_TRANSACTION: '345e7c054728e110c33ce738436d4306',
        FEEDBACK: '24aeb0454728e110c33ce738436d439e',
        FUNDING: '096ebc054728e110c33ce738436d4356',
        GENERAL: '472d34c14728e110c33ce738436d439c',
        SAVINGS: 'b47e3c054728e110c33ce738436d430c',
        TRANSFERS: '577e3c054728e110c33ce738436d43a1',
        WELLNESS_FEATURES: '699e70454728e110c33ce738436d43aa',
      }[topic] ?? ''
    );
```
### Function to escape wildcards
```
function escapeWildcards(input: string): string {
  const wildcardRegex = /[%_[\]^-]/g;
  if (wildcardRegex.test(input)) {
    return input.replace(wildcardRegex, (x: string): string => `\\${x}`);
  }
  return input;
}
```

## Python

### Pip install package globally
```
python3 -m pip install -U pip-upgrader
```
### check python version
```
python3 --version
```
### check pip version
```
python3 -m pip --version
```

## Misc

### Vim Editor for Git
press Esc then do `:wq` (for write and quit)

### To find a process and kill it if necessary:
- `ps` -> list running processes
- `kill 2005` -> kill process on port 2005 (for example)
- `kill -9 2005` -> kill (ungracefully) process on port 2005

### Fix port forwarding error:
```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
etc..
```

fix by doing removing the lines from /var/root/.ssh/known_hosts:
```
echo "" | sudo tee /var/root/.ssh/known_hosts
```
