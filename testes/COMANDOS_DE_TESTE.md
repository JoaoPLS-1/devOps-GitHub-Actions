# Experimentos temporarios — execute um por vez

**Nao deixe os comandos de falha no deploy.yml final.** Para cada experimento: altere, commit, push, capture o log, restaure e execute novamente.

## 1.2 — Falha sem checkout
Comente temporariamente `uses: actions/checkout@v4` no job `validacao`. O `test -f index.html` devera falhar porque o repositorio nao foi baixado. Restaure o checkout.

## 2.1 — Dependencia needs
Adicione em `validacao.steps`:
```yaml
      - name: Falha proposital de validacao
        run: exit 1
```
O job `publicar-site` deve ser ignorado. Remova o step.

## 2.2 — Smoke test
Renomeie `index.html` para `pagina.html`, commit e push. O `test -f index.html` deve falhar. Restaure `index.html`.

## 2.3 — Artefato
Altere temporariamente `path: '.'` para `path: './pasta-inexistente'` no step de upload. Verifique o log e restaure `'.'`.

## 4.1 — Isolamento
Adicione ao job `publicar-site`, ANTES do deploy:
```yaml
      - name: Testar isolamento de jobs
        run: cowsay "Teste"
```
O programa instalado no outro job nao estara automaticamente neste runner. Remova o step. Observacao: se a imagem do runner ja incluir cowsay, use um executavel personalizado criado no primeiro job em um caminho exclusivo, sem transferir artefato.

## 4.3 — Comando inexistente
Adicione ao job `validacao`:
```yaml
      - name: Erro proposital
        run: comando_que_nao_existe
```
Capture o erro do shell, remova o step e execute novamente.

## Capturas exigidas
1. Dashboard com workflow personalizado e job renomeado.
2. Falha proposital de validacao e deploy ignorado.
3. Smoke test falhando e depois passando.
4. Artefato gerado e publicacao.
5. Log de lsb_release -a, free -h e nproc.
6. Erro do comando inexistente e pipeline corrigido.

## Git
```bash
git add .
git commit -m "Implementa workflow DevOps e site de demonstracao"
git push
```

## Configuracao do GitHub Pages
No repositorio, Settings > Pages > Build and deployment > Source: GitHub Actions. Acompanhe em Actions.
