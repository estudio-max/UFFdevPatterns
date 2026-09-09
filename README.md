# UFFdevPatterns

Skill de agente (Claude Code / Agent Skills) com o padrão de trabalho usado nos projetos: **entender e documentar antes de mexer, provar com teste e pipeline depois de mexer.**

Reúne duas disciplinas que só funcionam juntas:

1. **Documentação e planejamento incremental** — diagnóstico do estado real do projeto, `REQUIREMENTS.md`, `ARCHITECTURE.md`, `STEPS.md` sempre vivos, e implementação em fases com critérios de conclusão.
2. **Testes, segurança e CI/CD** — camadas de teste (unitário, integração, regressão, mutação, comportamento, segurança, fumaça, ponta a ponta), análise estática, quality gate e pipeline local e de CI.

## Conteúdo

| Arquivo | Papel |
|---|---|
| `SKILL.md` | Ordem de trabalho, gates inegociáveis e regras de preservação |
| `referencias/documentacao.md` | Checklists do diagnóstico, dos três documentos e das fases |
| `referencias/qualidade.md` | Camadas de teste, quality gate, pipeline e verificação final |

## Instalação

```bash
git clone https://github.com/estudio-max/UFFdevPatterns ~/.claude/skills/uffdevpatterns
```

Instalada em `~/.claude/skills/`, vale para todos os projetos da máquina. Para um projeto só, clone em `.claude/skills/uffdevpatterns` dentro do repositório.

No **Codex**, clone em `~/.codex/skills/uffdevpatterns` e aponte para ela no `~/.codex/AGENTS.md` (ou no `AGENTS.md` do projeto), já que lá as instruções chegam por esse arquivo:

```markdown
Siga a skill UFFdevPatterns: leia `~/.agents/skills/uffdevpatterns/SKILL.md` antes de mexer no projeto,
ao planejar fases, ao mexer em testes ou CI, e antes de declarar tarefa concluída.
```

O conteúdo é markdown puro — serve a qualquer agente que leia arquivo.

O nome da pasta e o campo `name` do frontmatter precisam ficar em minúsculas — é o formato que o carregador de skills aceita.

## Uso

A skill entra sozinha ao iniciar ou retomar um projeto, antes de funcionalidade nova ou mudança estrutural, ao planejar fases, ao escrever ou corrigir testes, ao configurar lint/tipagem/análise estática, ao montar pipeline e antes de declarar qualquer tarefa concluída. Também dá para chamar direto:

```
/uffdevpatterns
```

## Licença

MIT.
