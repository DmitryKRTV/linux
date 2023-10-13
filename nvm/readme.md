## NVM

[Source](https://tecadmin.net/how-to-install-nvm-on-ubuntu-22-04/)

`sudo apt install curl`
`curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash` - скачать пакет, после требуется закрыть/открыть bash

`nvm install node`
`nvm ls` - уставленные версии
`nvm ls-remote` - доступные к установке версии
`nvm use node-version` - использовать версию
`nvm run default --version` - инфо о версии
`nvm exec 16.14.0 server.js` - использовать скрипт под определенной версией

