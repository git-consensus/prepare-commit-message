# Github Pre Commit Message Hooks

Let's add the Ethereum Address available in the environment file to each commit of git action.

## Installation & Pre-Requisites

Use the following website [git-scm.com/downloads](https://git-scm.com/downloads) to install git.
This installation is mandatory to pull the repositories from git and add pre committed message to the commits.

Use the below command for Linux and other related platforms :

```bash
sudo apt install git-all
```

Make sure to have .env file in the project with the Ethereum address having the below Key :
```bash
ETH_ADDRESS=0x71C7656EC7...B751B740...8976F
```

## Detailed Instructions

1. Create a below folder in the root directory of the GIT project :
```bash
mkdir git-config/hooks
```
2. Create a file with the name "prepare-commit-msg" inside the above folder location or use below command in linux.
```bash
nano git-config/hooks/prepare-commit-msg.sh
```
3. Add the below contents and change the env file location in the script according to the project.
```bash
#!/bin/bash
FILE=$1
MESSAGE=$(cat $FILE)
KEYCHECK="ETH_ADDRESS"
ADDFILE="$PWD/.env"
ADDRESS="No ETH Address"
while IFS="=" read -r key value; do
	case "$key" in
	  "$KEYCHECK") ADDRESS="$value" ;;
	esac
done < "$ADDFILE"
if [[ "$key" == "$KEYCHECK" ]]; then
  ADDRESS=$value
fi
echo "$MESSAGE $ADDRESS" > $FILE
```
4. Change the permission of the newly created file for git actions to execute.
```bash
chmod +x git-config/hooks/prepare-commit-msg
```

5. Execute the below command to change the default directory for git in the current project from the root location to execute hooks for git actions from our custom directory location.
```bash
git config core.hooksPath ./git-config/hooks
```

## Overall Process
Add the File in Custom Folder -> Execute GIT cmd to change the directory of Hooks -> Have .env file to get Address. 

## License
The code in this project is licensed under the is licensed under the [GNU General Public License v3](https://gist.github.com/kn9ts/cbe95340d29fc1aaeaa5dd5c059d2e60)