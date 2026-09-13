# Ícones do Eco para placas — BBC-Brasil

Galeria estática (GitHub Pages) com **1824 ícones** e um montador de placa.
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
| <kbd>BBC</kbd> | temos versão recortada no nosso mod. O comando sai com o nome `...BBC` e **só funciona com o mod instalado no servidor** |
| <kbd>?</kbd> | o nome **não corresponde a nenhuma classe do jogo** (quase todos `*Group`, agrupamentos do GoodPrice): pode não aparecer. Não está provado que falha — está provado que não é classe |

*A regra aqui é avisar, não esconder.*

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
python categorizar.py      # categorias, pelos componentes dos objetos
python nomes-reais.py      # nome que a tag aceita, contra as classes do servidor
python classificar-alfa.py # quais ícones saem com fundo
python extrair-icones.py   # monta o index.html
```

Os PNG foram extraídos das imagens que o mod **GoodPrice** embute, e os marcados <kbd>BBC</kbd> são
versões recortadas por nós. É material do jogo e de mods de terceiros, publicado aqui só para servir
de catálogo aos jogadores do servidor.
