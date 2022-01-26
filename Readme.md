![](https://github.com/rafaelgoncalvesmatos/RepoAssets/blob/master/Outros/repos/home_office_01_wide.jpeg)

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
$ pm2 stop all
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
$ pm2 stop 0
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
$ pm2 delete all 
[PM2] Applying action deleteProcessId on app [all](ids: [ 0 ])
[PM2] [main](0) ✓
┌────┬────────────────────┬──────────┬──────┬───────────┬──────────┬──────────┐
│ id │ name               │ mode     │ ↺    │ status    │ cpu      │ memory   │
└────┴────────────────────┴──────────┴──────┴───────────┴──────────┴──────────┘
[PM2][WARN] Current process list is not synchronized with saved list. App main differs. Type 'pm2 save' to synchronize.
```

Para remover uma app especifica colocar o ID:


```md
$ pm2 delete 1 
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

Descobrir informaçoes sobre o serviço:

```md
$ pm2 show  0
 Describing process with id 0 - name main 
┌───────────────────┬──────────────────────────────────────────┐
│ status            │ online                                   │
│ name              │ main                                     │
│ namespace         │ default                                  │
│ version           │ 0.0.1                                    │
│ restarts          │ 0                                        │
│ uptime            │ 102s                                     │
│ script path       │ /home/azureuser/scanelastic/main.js        │
│ script args       │ N/A                                      │
│ error log path    │ /home/azureuser/.pm2/logs/main-error.log │
│ out log path      │ /home/azureuser/.pm2/logs/main-out.log   │
│ pid path          │ /home/azureuser/.pm2/pids/main-0.pid     │
│ interpreter       │ node                                     │
│ interpreter args  │ N/A                                      │
│ script id         │ 0                                        │
│ exec cwd          │ /home/azureuser/scanelastic                │
│ exec mode         │ fork_mode                                │
│ node.js version   │ 14.18.1                                  │
│ node env          │ N/A                                      │
│ watch & reload    │ ✘                                        │
│ unstable restarts │ 0                                        │
│ created at        │ 2022-01-26T14:04:01.728Z                 │
└───────────────────┴──────────────────────────────────────────┘
 Actions available 
┌────────────────────────┐
│ km:heapdump            │
│ km:cpu:profiling:start │
│ km:cpu:profiling:stop  │
│ km:heap:sampling:start │
│ km:heap:sampling:stop  │
└────────────────────────┘
 Trigger via: pm2 trigger main <action_name>

 Code metrics value 
┌────────────────────────┬───────────────────────┐
│ Heap Size              │ 63.36 MiB             │
│ Heap Usage             │ 52.4 %                │
│ Used Heap Size         │ 33.20 MiB             │
│ Active requests        │ 0                     │
│ Active handles         │ 29                    │
│ Event Loop Latency     │ 0.30 ms               │
│ Event Loop Latency p95 │ 6.49 ms               │
│ HTTP Mean Latency      │ 20 ms                 │
│ HTTP P95 Latency       │ 51.599999999999994 ms │
│ HTTP                   │ 0.19 req/min          │
└────────────────────────┴───────────────────────┘
 Divergent env variables from local env
```

Visualizando os logs:

```md
$ pm2 logs
[TAILING] Tailing last 15 lines for [all] processes (change the value with --lines option)
/home/azureuser/.pm2/pm2.log last 15 lines:
PM2        | 2022-01-26T01:01:04: PM2 log: PM2 version          : 5.1.2
PM2        | 2022-01-26T01:01:04: PM2 log: Node.js version      : 14.18.1
PM2        | 2022-01-26T01:01:04: PM2 log: Current arch         : x64
PM2        | 2022-01-26T01:01:04: PM2 log: PM2 home             : /home/azureuser/.pm2
PM2        | 2022-01-26T01:01:04: PM2 log: PM2 PID file         : /home/azureuser/.pm2/pm2.pid
PM2        | 2022-01-26T01:01:04: PM2 log: RPC socket file      : /home/azureuser/.pm2/rpc.sock
PM2        | 2022-01-26T01:01:04: PM2 log: BUS socket file      : /home/azureuser/.pm2/pub.sock
PM2        | 2022-01-26T01:01:04: PM2 log: Application log path : /home/azureuser/.pm2/logs
PM2        | 2022-01-26T01:01:04: PM2 log: Worker Interval      : 30000
PM2        | 2022-01-26T01:01:04: PM2 log: Process dump file    : /home/azureuser/.pm2/dump.pm2
PM2        | 2022-01-26T01:01:04: PM2 log: Concurrent actions   : 2
PM2        | 2022-01-26T01:01:04: PM2 log: SIGTERM timeout      : 1600
PM2        | 2022-01-26T01:01:04: PM2 log: ===============================================================================
PM2        | 2022-01-26T11:04:01: PM2 log: App [main:0] starting in -fork mode-
PM2        | 2022-01-26T11:04:01: PM2 log: App [main:0] online

/home/azureuser/.pm2/logs/main-error.log last 15 lines:
0|main     | }
0|main     | [Error: ENOSPC: no space left on device, open '/home/azureuser/scanelastic/tmp/Geografia-%2BEspaco%2BGeografico.mp4'] {
0|main     |   errno: -28,
0|main     |   code: 'ENOSPC',
0|main     |   syscall: 'open',
0|main     |   path: '/home/azureuser/scanelastic/tmp/Geografia-%2BEspaco%2BGeografico.mp4'
0|main     | }
0|main     | [Error: ENOSPC: no space left on device, open '/home/azureuser/scanelastic/tmp/Generos%2Btextuais.mp4'] {
0|main     |   errno: -28,
0|main     |   code: 'ENOSPC',
0|main     |   syscall: 'open',
0|main     |   path: '/home/azureuser/scanelastic/tmp/Generos%2Btextuais.mp4'
0|main     | }
0|main     | [Error: ENOSPC: no space left on device, open '/home/azureuser/scanelastic/tmp/Geografia-%2BEspaco%2BGeografico.mp4'] {
0|main     |   errno: -28,
```

Abrir o pm2 monitor para monitorar:

```md
 $ pm2 monit
```

![](https://github.com/rafaelgoncalvesmatos/RepoAssets/blob/master/Outros/pm2/pm2_01.png)

## Cluster

Para subir sua app com varias instancias nodejs faz isso de forma fácil e prática, caso não tenha iniciado a app ainda poderá executar desta forma:

```md
$ pm2 start main.js -i 4 
[PM2] Starting /home/azureuser/scanelastic/main.js in cluster_mode (4 instances)
[PM2] Done.
┌────┬────────────────────┬──────────┬──────┬───────────┬──────────┬──────────┐
│ id │ name               │ mode     │ ↺    │ status    │ cpu      │ memory   │
├────┼────────────────────┼──────────┼──────┼───────────┼──────────┼──────────┤
│ 0  │ main               │ cluster  │ 0    │ online    │ 0%       │ 44.8mb   │
│ 1  │ main               │ cluster  │ 0    │ online    │ 0%       │ 42.0mb   │
│ 2  │ main               │ cluster  │ 0    │ online    │ 0%       │ 36.4mb   │
│ 3  │ main               │ cluster  │ 0    │ online    │ 0%       │ 30.0mb   │
└────┴────────────────────┴──────────┴──────┴───────────┴──────────┴──────────┘
[PM2][WARN] Current process list is not synchronized with saved list. Type 'pm2 save' to synchronize.
```

Neste comando irá subir 4 instancias da app, a distribuição das requests será feita pelo pm2 podendo ser visto diretamente nos logs:

```md
$ pm2 logs
```

Para escalar após a aplicação ter iniciada tem esta forma com parametro `-f` como aqui:


```md
$ pm2 start -f main.js -i 2
[PM2] Starting /home/azureuser/scanelastic/main.js in cluster_mode (2 instances)
[PM2] Done.
┌────┬────────────────────┬──────────┬──────┬───────────┬──────────┬──────────┐
│ id │ name               │ mode     │ ↺    │ status    │ cpu      │ memory   │
├────┼────────────────────┼──────────┼──────┼───────────┼──────────┼──────────┤
│ 0  │ main               │ cluster  │ 0    │ online    │ 0%       │ 108.6mb  │
│ 1  │ main               │ cluster  │ 0    │ online    │ 0%       │ 39.3mb   │
│ 2  │ main               │ cluster  │ 0    │ online    │ 0%       │ 30.2mb   │
└────┴────────────────────┴──────────┴──────┴───────────┴──────────┴──────────┘
```

Depois das alterações se ficar ideal e queira persistir está configurações nas próximas inicializações:

```md
$ pm2 save
[PM2] Saving current process list...
[PM2] Successfully saved in /home/azureuser/.pm2/dump.pm2
```