# Guia de contribuição da IA-Soberana

Este é o guia padrão da organização. Ele vale para todo repositório que não tenha um `CONTRIBUTING.md` próprio.

Os projetos usam um fluxo baseado em **issues**. Toda contribuição começa em uma issue e é entregue por um pull request que a referencia.

## 1. Issues

- Descreva o problema ou a proposta com contexto suficiente para reproduzir ou entender.
- Uma issue = uma entrega. Evite misturar assuntos não relacionados.
- Use os rótulos (labels) do repositório para classificar (`bug`, `enhancement`, `documentation`, etc.).

## 2. Branches

Nomeie a branch com o seu usuário do GitHub, o tipo e o número da issue:

```
nome_usuario/tipo/issue-descricao-curta
```

Exemplos:

```
notadson/feat/12-login-google
notadson/fix/34-calculo-frete
notadson/doc/56-guia-instalacao
```

Use o mesmo `nome_usuario` do seu login no GitHub em todas as branches.

## 3. Commits

Formato obrigatório:

```
tipo #issue: mensagem
```

| Campo | Regra |
| --- | --- |
| `tipo` | Um dos tipos da tabela abaixo |
| `#issue` | Número da issue relacionada (ex.: `#12`) |
| `mensagem` | Curta, no imperativo, em minúsculas, sem ponto final (até 72 caracteres) |

### Tipos

| Tipo | Uso |
| --- | --- |
| `feat` | Nova funcionalidade |
| `fix` | Correção de bug |
| `doc` | Documentação |
| `style` | Formatação, sem mudança de lógica |
| `refactor` | Refatoração sem mudança de comportamento |
| `perf` | Melhoria de performance |
| `test` | Testes |
| `build` | Build e dependências |
| `ci` | Configuração de CI/CD |
| `chore` | Tarefas gerais e manutenção |
| `revert` | Reversão de mudança anterior |

### Exemplos

```
feat #12: adiciona login com Google
fix #34: corrige cálculo de frete
doc #56: atualiza guia de instalação
refactor #78: extrai validação para serviço próprio
```

Commits de merge e reversões automáticas criadas pela interface do GitHub são ignorados pela validação.

## 4. Pull requests

O título do PR segue **o mesmo formato dos commits**:

```
tipo #issue: mensagem
```

Exemplo: `feat #12: adiciona login com Google`

O template em `.github/pull_request_template.md` é preenchido automaticamente. Referencie a issue nele com `Closes #12` para que ela seja fechada no merge.

Prefira **squash merge**: assim a mensagem final na branch principal é o título do PR, mantendo o histórico no padrão.

## 5. Validação automática

As regras são verificadas por três workflows mantidos em [`IA-Soberana/ia-soberana`](https://github.com/IA-Soberana/ia-soberana):

| Workflow | Valida |
| --- | --- |
| `pr-title.yml` | título do PR |
| `commit-messages.yml` | mensagens dos commits do PR |
| `branch-name.yml` | nome da branch |

Para ativar as validações em um repositório, crie `.github/workflows/padroes.yml`:

```yaml
name: Padrões de contribuição

on:
  pull_request:
    types: [opened, edited, reopened, synchronize]

permissions:
  contents: read

jobs:
  titulo:
    uses: IA-Soberana/ia-soberana/.github/workflows/pr-title.yml@main
  commits:
    uses: IA-Soberana/ia-soberana/.github/workflows/commit-messages.yml@main
  branch:
    uses: IA-Soberana/ia-soberana/.github/workflows/branch-name.yml@main
```

O próprio `ia-soberana` não precisa desse arquivo: os workflows rodam lá pelo gatilho `pull_request`.

## 6. Checklist antes de abrir o PR

- [ ] Issue aberta e referenciada
- [ ] Branch nomeada no padrão
- [ ] Commits no padrão
- [ ] Título do PR no padrão
- [ ] Template do PR preenchido
- [ ] Testes executados localmente
