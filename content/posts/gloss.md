+++
title = "Glosas, LaTeX, html, Hugo"
date = "2020-08-20"
author = "Caio G"
authorTwitter = "silenus32" #do not include @
cover = "img/gloss2.png"
tags = ["linguística", "latex", "html", "Hugo"]
keywords = []
description = "Algumas questões sobre glosa e edição virtual de textos"
showFullContent = false
+++

Glosas são uma ferramenta comum na linguística para representar exemplos em uma língua que não necessariamente o público esteja familiarizado ou para incluir um nível morfossintático de análise na exibição.
Elas costumam vir em três linhas:

- texto na língua original com as palavras divididas em morfemas;
- a glosa propriamente dita, incluindo uma tradução da palavra correspondente e o valor de cada morfema, alinhada com a palavra correspondente à esquerda;
- tradução da frase para a língua do texto.

Uma linha no costuma ser incluída para indicar a língua do exemplo ou o nome de quem coletou o exemplo (isso é especialmente útil quando você está discutindo um fenômeno compartilhado entre línguas e que você não tem como dar um testemunho direto da língua, glosa e tradução).

Existem algumas práticas recomendadas, mas em geral as pessoas aderem às [normas de Leipzig](https://www.eva.mpg.de/lingua/resources/glossing-rules.php).
A ideia básica é: dividir com hifens os morfemas flexionais (que não geram palavras novas) tanto no texto original quanto na glosa e na glosa marcar informação morfológica compactada numa mesma entrada com pontos:

```
agni-m        iḷ-e                    (…) yajña-sya              dev-a-m
A.(M)-ACC.SG  celebrar(PRES)-MP.1SG   (…) sacrifício(M)-GEN.SG   deus-M-ACC.SG
Eu celebro Agni (= fogo) (…), o deus do sacrifício. (RV 1.1.1)
```

Por exemplo, _devam_ é o acusativo (ACC) masculino (M) singular (SG) do nome _deva-_ (m) / _-ī-_ (f) "deus" em sânscrito.
Como esse substantivo flexiona em gênero pelos morfemas _-a_ e _-ī_, é possível dividir _devam_ em _raiz_-_GÊNERO_-_CASO.NÚMERO_ = _dev-a-m_ = deus-M-ACC.SG.
As letras maiúsculas (ou versaletes) marcam morfemas e as traduções vem em caixa baixa, tirando nomes próprios que podem ser grafados com maiúscula + . (mas normalmente não com versaletes).
Já no caso de _yajñasya_, substantivo inerentemente neutro, a melhor opção é colocar o gênero entre parênteses ou ignorá-lo, a depender do que se pretende mostrar com a glosa, por isso _yajñasya_ pode ser dividido em _tema_(_GÊNERO_)-_CASO.NÚMERO_ = _yajña-sya_ = sacrifício(M)-GEN.SG.
Assim sucessivamente.

Existem _n_ critérios para escolher uma glosa ou outra e uma abreviação ou outra, mas via de regra as marcações relevantes vão ser comentadas no texto e autores mais gentis incluirão (quando editores mais gentis permitirem) uma lista de abreviações.

Por fim, as glosas de frases mais complicadas podem se tornar muito mais complicadas:

{{< figure "position"="center" "src"="/img/glossa.png" "caption"="Glosa de Tsez (Nakh-Daghestanian), em Polinsky e Comrie (1999) Agreement in Tsez.">}}

# Como tipografar isso?

Bom, se você é um linguista (ou editor, mas duvido que algum acabe aqui) e quer digitar um negócio desses, o mais difícil é conseguir algum tipo de consistência no alinhamento.
Só colocar espaços vai gerar muita dor de cabeça porque as fontes em geral são feitas para se ajustar às linhas e comprimir e separar sempre que possível, fazer ligaturas. Isso tudo faz que com os espaços e as letras variem de tamanho o que significa dor e desalinhamento.
Depende de qual plataforma você vai usar:

- LibreOffice, MS Office, Google Docs e afins: faz uma tabela, preenche, tira a cor das margens, deite no chão, chore. Deve ter algum tipo de plug-in, alguma magia, mas via de regra é horrível. Ou escolhe uma fonte monoespaçada, bate espaço até ficar mais ou menos onde parece alinhado e torce para o processador de textos não acordar com tudo bagunçado.
- LaTeX: `linguex`, `gb4e`, `expex`, todos funcionam perfeitamente bem.
- Web: muita gente faz truques com `<div>`s e regras complicadas de `css`, inclusive o site das normas de Leipzig, aparentemente, ou usa a tática da tabela ou fonte monoespaçada. Já existem alguns plugins pelo que vi e o `Leipzig.js` parece bom, ao menos eu conseguisse fazer funcionar nesse site (ME ENSINEM).

A elegância das soluções em LaTeX é incrível, linda, mas costuma dar faniquitos (como é normal no LaTeX) por absolutamente qualquer errinho.
Pra comentar dois:

## linguex

Pacote para exemplos linguísticos numerados, serve para um milhão de funções, relativamente simples de aprender a usar.
Dá muito faniquito, então tem que ser religioso com as regras e não aceita muito fazer balabarismo com as glosas.

```latex
% TEX program = xelatex
% TEX encoding = UTF-8

\documentclass[]{article}

\usepackage{fontspec} % só para o meu exemplo funcionar
\setmainfont{Noto Sans} % idem

\usepackage{linguex} % estrela do show

\begin{document}

\exg.agni-m iḷ-e (…) yajña-sya dev-a-m\\ % nunca se esquecer desses \\
A.(M)-ACC.SG celebrar(PRES)-MP.1SG (…) sacrifício(M)-GEN.SG deus-M-ACC.SG\\
Eu celebro Agni (= fogo) (…), o deus do sacrifício. (RV 1.1.1)

% sempre deixe uma linha a mais vazia, salva dor de cabeça

\end{document}
```

Caso você queira incluir um comentário no exemplo, você pode usar essa sintaxe:

```latex

\ex.Védico (R̥gveda 1.1.1)
\gll agni-m iḷ-e (…) yajña-sya dev-a-m\\ % nunca se esquecer desses \\
A.(M)-ACC.SG celebrar(PRES)-MP.1SG (…) sacrifício(M)-GEN.SG deus-M-ACC.SG\\
Eu celebro Agni (= fogo) (…), o deus do sacrifício.
```

A documentação é decente: [linguex](https://www.ctan.org/pkg/linguex)

## expex

Eu preciso tentar usar esse mais, ele parece permitir todo tipo de brincadeira com os detalhes, inclusive glosas de múltiplas linhas e em colunas.
Tem umas frescuras (barras invertidas no fim de cada linha).

```latex
% TEX program = xelatex
% TEX encoding = UTF-8

\documentclass[]{article}

\usepackage{fontspec} % só para o meu exemplo funcionar
\setmainfont{Noto Sans} % idem

\usepackage{expex} % estrela do show

\begin{document}

\ex
\begingl
\gla agni-m iḷ-e (…) yajña-sya dev-a-m// % todas as linhas levam isso
\glb A.(M)-ACC.SG celebrar(PRES)-MP.1SG (…) sacrifício(M)-GEN.SG deus-M-ACC.SG//
\glft Eu celebro Agni (= fogo) (…), o deus do sacrifício. (RV 1.1.1)//
\endgl
\xe
% sempre deixe uma linha a mais vazia, salva dor de cabeça

\end{document}
```

Eu vejo algumas situações em que eu escolheria escrever a glosa em colunas. Mesma glosa de cima escrita colunas (o resultado compilado é o mesmo):

```latex

\ex
\begingl[glstyle=nlevel]
agni-m [A.(M)-ACC.SG]
iḷ-e [celebrar(PRES)-MP.1SG]
(…) [(…)]
yajña-sya [sacrifício(M)-GEN.SG]
dev-a-m [deus-M-ACC.SG]
\glft Eu celebro Agni (= fogo) (…), o deus do sacrifício. (RV 1.1.1)
\endgl
\xe
```

# Resumo da ópera

Eu tinha que aprender a usar o `expex` e alguém me ensinar a usar o `Leipzig.js` no Hugo (fora do Hugo é simples, basta usar seguir a documentação do [site deles](https://bdchauvette.net/leipzig.js/)).

## Atualização

Eu descobri um jeito de incluir o `Leipzig.js` no Hugo!
O resultado aliás é bem agradável:

{{< leipzig "original"="agni-m iḷ-e (…) yajña-sya dev-a-m" "gloss"="Agni(M)-ACC.SG celebrar(PRS)-MP.1SG (…) sacrifício(M)-GEN.SG deus-M-ACC.SG" "trans"="Eu celebro Agni (= fogo) (…), o deus do sacrifício. (RV 1.1.1)" >}}

Basicamente, se você quiser incluir num site como o Hugo, você precisa modificar o arquivo com o `<head>` incluindo duas linhas:

```html
<!-- CSS -->
<link rel="stylesheet" href="//unpkg.com/leipzig/dist/leipzig.min.css" />

<!-- JavaScript -->
<script src="//unpkg.com/leipzig/dist/leipzig.min.js"></script>
```

Depois, adicionar a call pro script fazer a mágica dele. Recomendo incluir no finalzinho do `<body>`:

```html
<script>
  document.addEventListener("DOMContentLoaded", function () {
    Leipzig().gloss();
  });
</script>
```

O tema que eu estou usando não permite incluir divs direto no markdown, então criei um arquivo `layouts/shortcodes/leipzig.html` com o seguinte conteúdo:

```html
<div data-gloss>
  <p>{{ .Get "original" }}</p>
  <p>{{ .Get "gloss" }}</p>
  <p>‘{{ .Get "trans" }}’</p>
</div>
```

Assim eu consigo chamar a função `leipzig` com os argumentos `"original"`, `"gloss"` e `"trans"` para gerar tudo bonitinho. :)
