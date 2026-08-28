# CLAUDE.md — {{Nome do Projeto}}

Este arquivo tem três camadas com regras de herança diferentes. Ao criar um projeto novo a partir deste template, cada camada é tratada de um jeito:

- **[UNIVERSAL]** — herda sempre, sem perguntar.
- **[CONDICIONAL]** — pergunta objetivamente (sim/não) antes de manter ou remover cada bloco.
- **[PROJETO]** — nunca herda conteúdo daqui; abre sempre vazio pra preencher na hora.

---

## [UNIVERSAL]

- Sudo sempre pergunta e explica antes de rodar.
- Comandos não-triviais são explicados antes de executar.
- `git push` sempre pede confirmação explícita.
- PARE E REPORTE antes de qualquer ação corretiva (mover, deletar, sobrescrever).
- Entrega de arquivo por substituição completa, não edição cirúrgica.
- `.env`/`.env.local` nunca são lidos, impressos ou citados.
- Comentários curtos e didáticos; nomes intuitivos.
- `docs/etapas/` é enriquecido continuamente; uma etapa só fecha com commit + push confirmados, doc da etapa atualizado, `CONVENCOES.md` atualizado, e `README.md` atualizado se a arquitetura mudou.
- Handoff inclui sempre: estado git completo, dependências críticas em aberto, decisões e aprendizados acumulados, próximos passos.
- README e Handoff sempre referenciam que o repositório é parte da organização DMMofServices (selo de pertencimento — sem link, a org não tem perfil público ainda).
- Etapa pendente registrada no Handoff vira Issue no GitHub — corpo no formato Cenário/Contexto/Escopo/Plano/Dependências/Referências/Resultado (mesmo template de `.github/ISSUE_TEMPLATE/etapa.md`), com o máximo de referências concretas (arquivos, docs, seções do Handoff, estado atual datado) pra quem abrir a Issue depois saber de onde começar sem reconstruir contexto. Label de área, Milestone só quando há prazo real (item bloqueado por critério, não por data, não leva Milestone). Ao concluir: preencher `Resultado` na própria Issue antes de fechar; atualizar Handoff (sai da lista de pendências, entra o que foi feito); `CONVENCOES.md` só se surgiu lição nova; `CLAUDE.md` só se mudou regra de trabalho de fato — nunca por reflexo.

## [CONDICIONAL]

Cada bloco abaixo só entra no `CLAUDE.md` final do projeto se confirmado sim na criação do repo. Pergunta-se um bloco por vez, não em lote.

### Supabase

- Grants explícitos após todo `CREATE TABLE`.
- Idempotência em webhooks via claim atômico.
- Client `service_role` isolado, server-only, para tabelas com PII.

### Cloudflare Workers

- Exigir `cache-status: MISS/EXPIRED` antes de reportar sucesso pós-deploy.
- `Cache-Control` diferenciado entre admin/API e público.

### Webhooks entre sistemas externos (ex.: Database Webhook do Supabase)

- Secret compartilhado entre dois sistemas externos exige teste ponta a ponta depois de QUALQUER rotação — "cadastrado nos dois lados" não é o mesmo que "confirmado que os dois lados batem" (lição real, `desconforto-diario` `CONVENCOES.md` #75 — uma semana de falha silenciosa de newsletter por secret dessincronizado pós-rotação).
- Se o provedor for Supabase: `select * from net._http_response order by created desc` é a fonte de evidência mais direta pra qualquer bug de Database Webhook — mais rápida que inferir por log do lado receptor.

## [PROJETO]

Nunca herda conteúdo — abre vazio em todo projeto novo.

### Objetivo

### Stack real

### Dependências externas

### Ambiente de produção
