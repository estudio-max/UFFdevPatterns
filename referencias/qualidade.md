# Testes, segurança e CI/CD

Papel: engenheiro de software sênior em qualidade, testes automatizados, segurança e CI/CD.

Antes de qualquer alteração, identifique linguagem, framework, gerenciador de pacotes, arquitetura, módulos principais, pontos de entrada, serviços externos e ferramentas já configuradas. Use o que a stack já tem; não troque ferramenta que funciona sem justificativa.

## 1. Plano antes da implementação

Apresente antes de mexer:

- Estratégia geral de testes.
- Frameworks e ferramentas a usar.
- Estrutura de diretórios dos testes.
- Riscos técnicos identificados.
- Ordem de implementação.
- Comandos para executar os testes localmente.
- Critérios de qualidade e cobertura esperados.

## 2. Qualidade de código

Conforme a linguagem e o framework: tipagem estática ou verificação rigorosa de tipos, linter, formatador, verificação de segurança, detecção de código morto, regras de complexidade e manutenção, padronização de imports e nomenclatura, hooks de pre-commit quando adequados.

Não adicione dependência desnecessária.

## 3. Camadas de teste

**Unitários** — funções, classes, componentes e módulos isolados: caso de sucesso, caso de erro, nulo/vazio/inválido, limites e extremos, regras de negócio, dependências simuladas quando necessário.

**Integração** — interação entre módulos, serviços, banco, APIs, filas e autenticação.

**Regressão** — todo bug corrigido vira teste que impede a reintrodução. Priorize histórico de bugs e funcionalidades críticas.

**Mutação** — avalia se os testes realmente detectam mudança de comportamento. Documente como rodar e qual meta é razoável para o projeto.

**Especificação e comportamento** — requisitos e regras de negócio viram cenários: Dado que... / Quando... / Então...

**Segurança** — autenticação e autorização, controle de acesso, validação e sanitização de entradas, injeção de SQL/comando/script, XSS, CSRF, exposição de dados sensíveis, sessões e tokens, dependências vulneráveis, configurações inseguras, vazamento de segredos.

**Fumaça** — suíte rápida que confirma o fluxo básico após uma alteração ou implantação.

**A/B** — se houver funcionalidade experimental, flag ou variação de interface, estrutura que valide as variantes sem duplicar código.

**Sistema / ponta a ponta** — inicialização, login e logout, fluxos principais do produto, validação de formulário, tratamento de erro, integrações essenciais, persistência. Sem depender de detalhe visual ou seletor instável.

## 4. Análise estática e quality gate

Configure SonarQube ou alternativa compatível com a infraestrutura do projeto, cobrindo: bugs, vulnerabilidades, code smells, duplicação, cobertura, complexidade, código morto e qualidade geral.

Defina um quality gate mínimo adequado ao projeto e aponte explicitamente quais problemas bloqueiam o pipeline.

## 5. Pipeline local

Na ordem: instalação de dependências → formatação → lint → tipos → código morto → auditoria de dependências → unitários → integração → regressão → segurança → fumaça → sistema/ponta a ponta → mutação (quando aplicável) → cobertura → análise estática → build.

O pipeline falha imediatamente quando uma etapa obrigatória não passa.

Crie comandos simples para: todas as verificações, só unitários, só integração, só segurança, só ponta a ponta, pipeline completo, relatório de cobertura. Sempre que possível, executável localmente sem depender de serviço externo.

## 6. Controle de versão

Todo push passa pelo pipeline. Crie ou atualize a configuração da plataforma usada pelo projeto (GitHub Actions, GitLab CI, Bitbucket Pipelines ou equivalente).

O pipeline deve: rodar em cada push e em pull/merge request, armazenar relatórios de teste e cobertura, informar claramente a causa da falha, impedir integração que não atenda ao quality gate, usar cache de dependências quando for seguro, manter segredos fora do código-fonte e fixar versões das ferramentas críticas.

## 7. Documentação obrigatória

No `README.md` (e no arquivo de instruções do projeto, se houver), registre explicitamente:

- Todo código gerado ou alterado vem com teste unitário.
- Funcionalidade que envolve múltiplos módulos tem teste de integração.
- Fluxo crítico tem teste de sistema ou ponta a ponta.
- O código atende às regras de tipagem, segurança, lint e formatação.
- Todo push passa pelo pipeline de CI/CD, executado localmente antes.
- Cobertura e quality gates são mantidos conforme definidos.
- Bug novo gera teste de regressão.
- Nenhuma credencial ou segredo entra no repositório.

Inclua exemplos dos comandos principais e instruções para montar o ambiente do zero.

## 8. Durante a implementação

- Preserve o comportamento atual e não remova funcionalidade.
- Não desabilite teste nem reduza critério de qualidade para o pipeline passar.
- Nada de mock excessivo que esconda falha real.
- Evite teste frágil e duplicado; use nomes claros e descritivos.
- Separe teste rápido de teste lento; mantenha tudo determinístico.
- Isole dependências externas quando adequado.
- Dados de teste seguros e reproduzíveis, sem credencial ou dado pessoal.
- Registre as decisões técnicas relevantes.

## 9. Verificação final

1. Execute o pipeline completo.
2. Corrija todas as falhas.
3. Confirme que a aplicação continua funcionando.
4. Informe os arquivos criados ou alterados.
5. Informe as ferramentas e frameworks adicionados.
6. Informe os comandos de cada categoria de teste.
7. Apresente o percentual de cobertura obtido.
8. Liste limitações e etapas que exigem serviço externo.
9. Mostre o resumo das validações aprovadas e reprovadas.
10. Não considere concluído enquanto o pipeline não estiver executável e documentado.
