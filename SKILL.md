---
name: uffdevpatterns
description: Fundação de qualquer projeto de software - entender o estado real antes de mexer, manter REQUIREMENTS.md, ARCHITECTURE.md e STEPS.md vivos, implementar em fases incrementais e sustentar a camada de testes, segurança, quality gate e CI/CD. Use ao iniciar um projeto, ao retomar um projeto existente, antes de implementar funcionalidade nova ou mudança estrutural, ao planejar ou replanejar fases, ao escrever ou corrigir testes, ao configurar lint, tipagem ou análise estática, ao montar ou consertar pipeline local ou de CI, e antes de declarar qualquer tarefa concluída.
---

# UFFdevPatterns — documentação e qualidade

Duas obrigações que andam juntas em todo projeto: **entender e documentar antes de mexer**, **provar com teste e pipeline depois de mexer**. Uma sem a outra não vale: documentação sem prova é ficção, teste sem plano é retrabalho.

## Ordem de trabalho

1. **Diagnóstico** — leia o projeto real antes de escrever qualquer linha (`referencias/documentacao.md`, seção 1).
2. **Documentação** — crie ou atualize `REQUIREMENTS.md`, `ARCHITECTURE.md`, `STEPS.md`.
3. **Plano** — apresente o diagnóstico, as fases e o que será criado ou alterado. **Espere validação antes de mudanças de grande impacto.**
4. **Implementação** — uma fase por vez, incremental e reversível.
5. **Prova** — testes da fase + pipeline verde (`referencias/qualidade.md`).
6. **Registro** — atualize os três documentos com o que mudou de verdade.

Projeto já iniciado nunca recomeça do zero: diagnostique o progresso e reorganize as próximas etapas a partir do que existe.

## Gates inegociáveis

- Não começa funcionalidade nova sem entender o que já existe.
- Não avança de fase sem os critérios de conclusão da fase atual atendidos.
- Código escrito não é tarefa concluída — só validação executada conclui.
- Não desabilite teste, não afrouxe quality gate, não use mock que esconde falha real, para o pipeline passar.
- Nunca credencial, token ou dado pessoal em documentação, teste ou repositório.
- Informação ausente ou ambígua vira linha em `Dúvidas e decisões pendentes`, com alternativas — nunca uma regra inventada.

## Preservação

Preserve o que existe e funciona. Antes de apagar, substituir ou trocar tecnologia: verifique o uso, explique o problema atual, a solução, os benefícios, os riscos, o impacto nos arquivos e o esforço — e diga se é urgente ou pode esperar. Funcionalidade sem cobertura ganha teste **antes** de ser modificada.

## Os três documentos

| Arquivo | Responde |
|---|---|
| `REQUIREMENTS.md` | O que o produto faz, para quem, sob quais regras e critérios de aceitação |
| `ARCHITECTURE.md` | Como está construído hoje (e só depois, o desejado) |
| `STEPS.md` | Em que ponto estamos e qual é a próxima fase |

Cada item classificado por status — implementado, parcial, pendente, bloqueado, fora de escopo — e por prioridade. Estado real primeiro; ideal em seção separada.

## Quando abrir cada referência

- Diagnóstico, os três documentos, fases de implementação → `referencias/documentacao.md`
- Camadas de teste, segurança, análise estática, quality gate, pipeline local e de CI → `referencias/qualidade.md`

## Entrega

Ao terminar, informe: o que existe e o que falta, problemas, riscos e débitos técnicos, decisões técnicas tomadas, dúvidas pendentes, arquivos criados ou alterados, comandos para rodar cada categoria de teste, cobertura obtida, e o resumo do que passou e do que reprovou. Limitações que dependem de serviço externo entram explícitas na lista.
