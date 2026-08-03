# Fila única — Go Beesiness

Tela de leitura e edição do backlog da suíte.

> ⚠️ **Este repositório é GERADO.** A fonte da tela é `app/index.html` no repositório
> `go-beesiness-regras` (privado). **Editar aqui cria uma segunda cópia, e cópia diverge** —
> publique com `python scripts/publicar-tela.py`.

## O que esta página é

Um **cliente**. Ela não guarda dado nenhum: lê e escreve o `dados/tarefas.json` do repositório
privado **pela API do GitHub**, usando um token que você fornece e que **fica só no seu navegador**.

**Sem token, ela não mostra nada** — não há backlog embutido nesta página.

## O que ela não é

- **Não é um banco.** Se esta página sumir amanhã, o dado continua em git, versionado e legível num
  editor de texto. É a razão de ela existir assim: as sete tentativas anteriores de controle de
  tarefas nesta casa morreram por criar **mais um lugar** onde a informação passava a morar.
- **Não é pública no sentido do dado.** O repositório que ela lê é privado; quem não tem acesso a
  ele não vê item nenhum aqui.

## Sobre o token

A tela pede um token do GitHub com escopo `repo`. **Escopo `repo` é escrita em todos os
repositórios da organização** — mais permissão do que esta tela precisa. Reduzir isso está na fila
de trabalho.

▸ Se marcar *"lembrar neste navegador"*, o token fica no `localStorage` desta máquina.
