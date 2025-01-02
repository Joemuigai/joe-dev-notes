
# Node.js and npm Installation

## Uninstalling Node.js and npm

1. To uninstall Node.js and npm, run the following command in the terminal:

```bash
sudo apt-get remove --purge nodejs npm
```

2. To remove any remaining files, run the following command:

```bash
sudo apt-get autoremove
sudo apt-get autoclean
```

## Installing Node.js and npm

1. To install curl and nvm, run the following commands in the terminal:

```bash
sudo apt-get install curl
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

2. Load the nvm script:

```bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
```
3. Confirm that nvm is installed by running the following command:

```bash
nvm --version
```

4. Install the Latest Node.js and npm Versions:

```bash
nvm install --lts
```

5. Set the installed version as the default:

```bash
nvm use --lts
nvm alias default 'lts/*'
```

6. Confirm that Node.js and npm are installed by running the following commands:

```bash
node --version
npm --version
```

By following these steps, you'll have the latest versions of Node.js and npm installed

