# Painel da fila única — o que é esta página

`painel.html` é a **vista de leitura** do backlog da suíte: mapa de calor
projeto × situação, mapa de calor dono × situação, progresso por projeto,
envelhecimento, riscos de contrato e distribuições — tudo recalculado por um
filtro único no topo.

> ⚠️ **Este arquivo é GERADO.** A fonte é `app/painel.html` no repositório
> `go-beesiness-regras` (privado). **Editar aqui cria uma segunda cópia, e cópia
> diverge** — publique com `python scripts/publicar-painel.py`.

## Ele só lê

O painel **nunca escreve** no `dados/tarefas.json`. Não há um `PUT`, `POST`,
`PATCH` ou `DELETE` na página, e o script de publicação **recusa publicar** se
algum aparecer. Quem edita é a [tela](index.html).

## Ele não guarda dado nenhum

É um **cliente**. Lê o `dados/tarefas.json` do repositório **privado** pela API
do GitHub, com um token que você fornece e que fica **só no seu navegador**.

**Sem token, ele não mostra nada** — não há backlog embutido nesta página. O
script de publicação confere isso procurando o backlog real dentro do HTML,
título por título e id por id, e recusa publicar se achar.

## Ele não busca nada de fora

Zero CDN, zero fonte remota, zero imagem hospedada. Todo gráfico é SVG escrito na
própria página. O script de publicação também recusa se aparecer requisição para
fora do GitHub.

## Como ler os dois mapas de calor

- **Sombra = magnitude**, numa rampa de uma cor só, claro→escuro (invertida no
  tema escuro, onde o "quase zero" é que precisa encostar na superfície).
- O padrão é **% da linha**, não contagem: a pergunta do painel é *onde dar
  atenção*, e volume bruto faz o maior projeto apagar todos os outros. O chip
  `contagem` troca para a leitura absoluta.
- **O número dentro da célula é sempre a contagem** — a cor nunca é o único
  caminho para o valor, e todo gráfico tem uma tabela gêmea logo abaixo.
- Linha pequena satura fácil: 100% de 1 item fica tão escuro quanto 100% de 300.
  O número na célula e a coluna `total` dizem o peso.

## Por que dono × situação, e não projeto × prioridade

Foi medido, não escolhido por gosto: `prioridade` quase não varia — metade do
acervo é `alta` e nenhum projeto foge da faixa —, então o mapa sairia todo do
mesmo tom. `dono` separa muito, e é o corte que responde *quem segura o quê*.
A distribuição de prioridade continua na página, como barra: ela cabe numa
dimensão.

## Sobre o token

O mesmo da tela: token clássico do GitHub com escopo `repo`. Repositório privado
exige `repo` — não existe escopo "ler privado" separado no token clássico. O
painel usa **só o verbo `GET`**.

▸ Se marcar *"lembrar neste navegador"*, o token fica no `localStorage` desta
máquina.
