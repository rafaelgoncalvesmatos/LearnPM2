# PM2 Startup

PM2 é um comando instalado via npm que gerencia as apps que estão instaladas no ambiente local.

Ele tem vários recursos de monitoração, visualização de logs, cluster e entre outros.

# Instalação

Para instalação comando:

```md
$ npm install pm2@latest
```

Entre no local onde a app se encontra, neste caso exemplo:

```md
$ cd scanelastic

```

Iniciando a aplicação:

```md
$ pm2 start main.js
```

Pode ser visto o status das apps que estão na máquina:

```md
$ pm2 status
┌────┬────────────────────┬──────────┬──────┬───────────┬──────────┬──────────┐
│ id │ name               │ mode     │ ↺    │ status    │ cpu      │ memory   │
├────┼────────────────────┼──────────┼──────┼───────────┼──────────┼──────────┤
│ 0  │ main               │ cluster  │ 0    │ online    │ 0%       │ 191.6mb  │
└────┴────────────────────┴──────────┴──────┴───────────┴──────────┴──────────┘

```

# Manipulação

### Reload

```md
$ pm2 reload all
Use --update-env to update environment variables
[PM2] Applying action reloadProcessId on app [all](ids: [ 0 ])
[PM2] [main](0) ✓
```

### Parando

```md
~/alcantara$ pm2 stop all
[PM2] Applying action stopProcessId on app [all](ids: [ 0 ])
[PM2] [main](0) ✓
┌────┬────────────────────┬──────────┬──────┬───────────┬──────────┬──────────┐
│ id │ name               │ mode     │ ↺    │ status    │ cpu      │ memory   │
├────┼────────────────────┼──────────┼──────┼───────────┼──────────┼──────────┤
│ 0  │ main               │ fork     │ 1    │ stopped   │ 0%       │ 0b       │
└────┴────────────────────┴──────────┴──────┴───────────┴──────────┴──────────┘
```

Ou poderá parar uma app pelo id:

```md
~/alcantara$ pm2 stop 0
[PM2] Applying action stopProcessId on app [all](ids: [ 0 ])
[PM2] [main](0) ✓
┌────┬────────────────────┬──────────┬──────┬───────────┬──────────┬──────────┐
│ id │ name               │ mode     │ ↺    │ status    │ cpu      │ memory   │
├────┼────────────────────┼──────────┼──────┼───────────┼──────────┼──────────┤
│ 0  │ main               │ fork     │ 1    │ stopped   │ 0%       │ 0b       │
└────┴────────────────────┴──────────┴──────┴───────────┴──────────┴──────────┘
```

### Remoção

```md
~/alcantara$ pm2 delete all 
[PM2] Applying action deleteProcessId on app [all](ids: [ 0 ])
[PM2] [main](0) ✓
┌────┬────────────────────┬──────────┬──────┬───────────┬──────────┬──────────┐
│ id │ name               │ mode     │ ↺    │ status    │ cpu      │ memory   │
└────┴────────────────────┴──────────┴──────┴───────────┴──────────┴──────────┘
[PM2][WARN] Current process list is not synchronized with saved list. App main differs. Type 'pm2 save' to synchronize.
```

Para remover uma app especifica colocar o ID:


```md
~/alcantara$ pm2 delete 1 
[PM2] Applying action deleteProcessId on app [all](ids: [ 0 ])
[PM2] [main](0) ✓
┌────┬────────────────────┬──────────┬──────┬───────────┬──────────┬──────────┐
│ id │ name               │ mode     │ ↺    │ status    │ cpu      │ memory   │
└────┴────────────────────┴──────────┴──────┴───────────┴──────────┴──────────┘
[PM2][WARN] Current process list is not synchronized with saved list. App main differs. Type 'pm2 save' to synchronize.
```

Verifique a app se foi removido com o parametro status

```md
$ pm2 status 
┌────┬────────────────────┬──────────┬──────┬───────────┬──────────┬──────────┐
│ id │ name               │ mode     │ ↺    │ status    │ cpu      │ memory   │
└────┴────────────────────┴──────────┴──────┴───────────┴──────────┴──────────┘
[PM2][WARN] Current process list is not synchronized with saved list. App main differs. Type 'pm2 save' to synchron
```

Para que este estado seja persistido é necessário salvar as alterações:

```md
$ pm2 save
[PM2] Saving current process list...
[PM2] Successfully saved in /home/azureuser/.pm2/dump.pm2
```

## Startup

Para execucao da app toda a vez que o host for ligado

```md
$ pm2 startup
[PM2] Init System found: systemd
[PM2] To setup the Startup Script, copy/paste the following command:
sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u azureuser --hp /home/azureuser
```

Qualquer alteração posterior, adicionando uma nova app ou até mesmo escalando é preciso salvar:

```md
$ pm2 save
[PM2] Saving current process list...
[PM2] Successfully saved in /home/azureuser/.pm2/dump.pm2
```

## Monitoração

## Cluster