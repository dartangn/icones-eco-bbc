# Ícones do Eco para placas — BBC-Brasil

Galeria estática (GitHub Pages) com **1908 ícones** e um montador de placa.

| | de onde vem | |
|---|---|---|
| **1581** | atlas de ícones do **cliente** | itens do jogo base |
| **219** | bundle de cada **mod** instalado | levam a etiqueta <kbd>mod</kbd> |
| **108** | ninguém entrega | marcados com <kbd>!</kbd>: **copiar a tag dá engrenagem** |
Clique num ícone para escolhê-lo; o comando sai pronto para colar no texto da placa (tecla **E**).

Também servida dentro do painel do servidor, em `/placas/`.

---

## O que a galeria faz

| | |
|---|---|
| **Por categoria** | 34 categorias, montadas pelo que o objeto **faz** no jogo, não por tag |
| **Montador** | texto, alinhamento, tamanho, cor por palavra, negrito/itálico/sublinhado, ícones antes/depois/embaixo |
| **Prévia** | desenha uma placa de madeira com halo, para julgar **a cor sobre a madeira** |
| **Busca** | por nome, em qualquer categoria |

## As três etiquetas, e o que cada uma avisa

| Etiqueta | Significa |
|---|---|
| <kbd>FUNDO</kbd> | a arte não tem recorte: **sai com um quadrado na placa mesmo com `type="nobg"`**, e não há tag que conserte. São 290 — 64 do jogo base (lixo, sucata, filtros) e o resto de mods |
| <kbd>mod</kbd> | o ícone vem do bundle de um **mod**, e o tooltip diz de qual. Se aquele mod sair do servidor, **a placa que usa este ícone passa a mostrar engrenagem** |
| <kbd>!</kbd> | **ninguém entrega este ícone** — nem o cliente, nem mod instalado. Copiar a tag mostra **engrenagem** na placa. São 108, e 94 terminam em `Group`: são agrupamentos internos do GoodPrice, não itens |

*A regra aqui é avisar, não esconder.* O ícone marcado com <kbd>!</kbd> aparece **apagado**, e no
montador a linha dele fica vermelha com o aviso *"sai engrenagem"* — onde a pessoa está montando,
não numa legenda no fim da página.

**O critério do <kbd>!</kbd> mudou em 21/09/2026**, e essa é a correção que importa. Antes ele
perguntava *"este nome é classe do jogo?"*, e isso deixava passar os 94 `*Group` — justamente os
que quebraram uma placa em campo. Agora pergunta **"o cliente entrega este ícone?"**, cruzando cada
nome contra o atlas do cliente e os bundles dos mods instalados.

## Como as categorias são montadas

Não por *tag*. As tags do Eco descrevem **efeito**, não identidade: das 106 com `Mountable`,
94 são cadeiras e bancos (montável porque você senta) e nenhuma é veículo.

A categoria vem do que o objeto **faz**, lido dos `[RequireComponent]` que o próprio jogo pendura
nele — `VehicleComponent` → Veículos, `CraftingComponent` → Mesas de fabricação,
`HousingComponent` → Móveis. A ordem importa: mesa de fabricação também dá moradia, então a função
específica vem primeiro. Quem não é objeto (minério, comida, semente, roupa) cai pelas tags, que ali
descrevem bem.

## Sobre o nome que sai no comando

O nome do arquivo nem sempre é o nome que a tag aceita. Para profissão, o arquivo se chama
`TailoringSkillItem` e a classe do jogo é `TailoringSkill` — **o `Item` no fim não existe**.
A galeria confere cada nome contra as 10.804 classes declaradas no servidor e corrige os 34 casos.

## Tags da placa, todas do próprio jogo

```
<align="center">…</align>     <color=#RRGGBB>…</color>     <size=NN%>…</size>
<icon name="X" type="nobg"></icon>
<icon name="X" type="" iconcolor='RRGGBBAA'></icon>
```

Medido em campo em 12/09/2026: **`iconcolor` é `RRGGBBAA`** (tem canal alfa), e existe também
`overlayimg='X' overlaycolor='RRGGBBAA'`. Aspas **simples** nesses dois, duplas em `name` e `type`.

Três coisas que o comando **não** controla, todas testadas em placa de verdade:

1. **o halo** em volta de cada letra — vem do material do texto no cliente, não há tag;
2. **não há realce atrás da letra** — `<mark>` foi colado numa placa e a placa ignorou;
3. **maiúsculas** — a placa grande escreve tudo em caixa alta, e `<lowercase>` não vence.

## Como a galeria é gerada

```
python categorizar.py          # categorias, pelos componentes dos objetos
python nomes-reais.py          # nome que a tag aceita, contra as classes do servidor
python classificar-alfa.py     # quais ícones saem com fundo
python extrair-icones-de-mod.py  # extrai a arte de dentro do bundle de cada mod
python gerar-procedencia.py    # cada nome vale? cruza contra o atlas do cliente e os mods
python categorizar-novos.py    # categoria dos que vieram dos bundles
python extrair-icones.py       # monta o index.html
```

Os dois do meio existem porque a galeria era montada **só** dos PNG que o GoodPrice embute — e o
GoodPrice não é a fonte que o cliente usa para desenhar ícone. Ela oferecia 108 nomes que não
funcionam e escondia 84 que funcionam.

Os PNG foram extraídos das imagens que o mod **GoodPrice** embute, e os marcados <kbd>BBC</kbd> são
versões recortadas por nós. É material do jogo e de mods de terceiros, publicado aqui só para servir
de catálogo aos jogadores do servidor.
