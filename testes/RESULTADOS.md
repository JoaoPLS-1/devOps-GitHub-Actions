# Resultados dos experimentos

Repositorio: [JoaoPLS-1/devOps-GitHub-Actions](https://github.com/JoaoPLS-1/devOps-GitHub-Actions)

## Configuracao e baseline

GitHub Pages foi configurado com `build_type=workflow`. A primeira execucao do baseline falhou em `actions/configure-pages@v5` porque Pages ainda nao estava habilitado. A repeticao do run [36502799289](https://github.com/JoaoPLS-1/devOps-GitHub-Actions/actions/runs/36502799289) passou nos tres jobs.

O pipeline final do commit `a164944` tambem passou: [run 36504521549](https://github.com/JoaoPLS-1/devOps-GitHub-Actions/actions/runs/36504521549). O site publicado esta em https://joaopls-1.github.io/devOps-GitHub-Actions/.

## Experimentos

| Teste | Run da falha | Resultado | Restauracao verde |
| --- | --- | --- | --- |
| 1.2 Sem checkout | [36503462770](https://github.com/JoaoPLS-1/devOps-GitHub-Actions/actions/runs/36503462770) | `Smoke Test - index.html` falhou; `publicar-site` ignorado. | [48c8a59 / 36503512174](https://github.com/JoaoPLS-1/devOps-GitHub-Actions/actions/runs/36503512174) |
| 2.1 Dependencia `needs` | [36503568865](https://github.com/JoaoPLS-1/devOps-GitHub-Actions/actions/runs/36503568865) | Falha proposital em `validacao`; `publicar-site` ignorado. | [2f47620 / 36503639934](https://github.com/JoaoPLS-1/devOps-GitHub-Actions/actions/runs/36503639934) |
| 2.2 Smoke test | [36503774352](https://github.com/JoaoPLS-1/devOps-GitHub-Actions/actions/runs/36503774352) | `index.html` renomeado para `pagina.html`; smoke test falhou e deploy foi ignorado. | [dc8a951 / 36503856034](https://github.com/JoaoPLS-1/devOps-GitHub-Actions/actions/runs/36503856034) |
| 2.3 Artefato | [36503955233](https://github.com/JoaoPLS-1/devOps-GitHub-Actions/actions/runs/36503955233) | `tar: pasta-inexistente: Cannot open: No such file or directory` (exit 2). | [8f00391 / 36504021660](https://github.com/JoaoPLS-1/devOps-GitHub-Actions/actions/runs/36504021660) |
| 4.1 Isolamento | [36504166811](https://github.com/JoaoPLS-1/devOps-GitHub-Actions/actions/runs/36504166811) | `cowsay: command not found` (exit 127) no runner de publicacao; o job que instalou cowsay passou. | [61ec897 / 36504278914](https://github.com/JoaoPLS-1/devOps-GitHub-Actions/actions/runs/36504278914) |
| 4.3 Comando inexistente | [36504441596](https://github.com/JoaoPLS-1/devOps-GitHub-Actions/actions/runs/36504441596) | `comando_que_nao_existe: command not found` (exit 127); deploy ignorado. | [a164944 / 36504521549](https://github.com/JoaoPLS-1/devOps-GitHub-Actions/actions/runs/36504521549) |

Na primeira tentativa do teste 1.2, o step ficou incompleto e nao gerou jobs. O step inteiro foi comentado na tentativa seguinte, que produziu a falha esperada no smoke test.

## Runner

Saida de `lsb_release -a`, `free -h` e `nproc` no run [36503512174](https://github.com/JoaoPLS-1/devOps-GitHub-Actions/actions/runs/36503512174): Ubuntu 24.04.5 LTS, 15 GiB de memoria e 4 CPUs.

## Capturas

- Dashboard e workflow: [captura-dashboard.png](captura-dashboard.png)
- Sem checkout: [captura-checkout-falha.png](captura-checkout-falha.png)
- Falha de validacao e `needs`: [captura-needs-falha.png](captura-needs-falha.png)
- Smoke test falhando: [captura-smoke-falha.png](captura-smoke-falha.png)
- Smoke test passando: [captura-smoke-passa.png](captura-smoke-passa.png)
- Falha ao gerar artefato: [captura-artefato-falha.png](captura-artefato-falha.png)
- Artefato e publicacao: [captura-publicacao-ok.png](captura-publicacao-ok.png)
- Log do runner: [captura-runner.png](captura-runner.png)
- Isolamento de jobs: [captura-isolamento-falha.png](captura-isolamento-falha.png)
- Comando inexistente: [captura-comando-inexistente.png](captura-comando-inexistente.png)
- Pipeline corrigido: [captura-pipeline-final.png](captura-pipeline-final.png)