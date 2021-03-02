---
theme : "beige"
transition: "slide"
highlightTheme: "monokai"
logoImg: "images/logo.png"
slideNumber: true
title: "CGr-2020-21 T1"
---

<!-- .slide: style="text-align: left;" -->
# Introdução

<aside class="notes">
Uma perspectiva geral sobre computação gráfica e a nossa abordagem.
</aside>

---

<!-- .slide: style="text-align: left;" -->
## Definição

Computação gráfica é a área da Informática que lida com a criação e manipulação de imagens.

Inclui:
- hardware
- software
- aplicações

<aside class="notes">
e vamos focar a atenção nas técnicas subjacentes e nos algoritmos de computação gráfica ( e não nas ferramentas para produzir conteúdos gráficos).
</aside>

---

<!-- .slide: style="text-align: left;" -->
## Aplicações de Computação gráfica

Atualmente todas as áreas usam computação gráfica de alguma forma.
- Ciência
- Arte
- Engenharia
- Indústria
- Medicina
- Entretenimento
- Educação

---

<!-- .slide: style="text-align: left;" -->
## Perspetiva histórica



--- 

<!-- .slide: style="text-align: left;" -->
### Sistemas Gráficos Interactivos

[SketchPAD (1963)](https://www.youtube.com/watch?v=57wj8diYpgY) 

[IBM2250 (1964)](https://en.wikipedia.org/wiki/IBM_2250)

[Xerox STAR (1981)](https://en.wikipedia.org/wiki/Xerox_Star)

[Apple Lisa (1983)](https://en.wikipedia.org/wiki/Apple_Lisa)

[PC com Windows 3.1 (1992)](https://en.wikipedia.org/wiki/Windows_3.1x)

[Silicon Graphics Indigo2 (1993)](https://en.wikipedia.org/wiki/SGI_Indigo%C2%B2_and_Challenge_M)


---

<!-- .slide: style="text-align: left;" -->
## Animações

[Short Films Collection Trailer, da Pixar (1984)](http://www.youtube.com/watch?v=C-L-WA-nQzI&feature=relmfu)

[Luxo Jr., da Pixar (1986)](https://youtu.be/6G3O60o5U7w)

[For the birds, da Pixar (2000)](https://youtu.be/nYTrIcn4rjg)

---

<!-- .slide: style="text-align: left;" -->
## Efeitos especiais

[Stargate Studios 2010 Virtual Backlot Demo](https://vimeo.com/9553622)

[Casino Royale miniature effects](https://www.youtube.com/watch?v=5LcfnyhW4g4)

[Harry Potter and the Half-Blood Prince - Death Eaters in London (HD)](https://www.youtube.com/watch?v=1jQmkJTCXcs], cena de pouco mais de 1 min, 1 ano de trabalho

---

<!-- .slide: style="text-align: left;" -->
## Como criar imagens sintéticas?


<!-- .slide: style="text-align: left;" -->
### *Pipeline*

Gera (ou mostra) uma imagem 2D de uma cena 3D

A cena 3D contém:
- uma câmera virtual: posição e orientação
- fonte(s) de luz - localização, tipo, cor
- objetos 3D: cada um tem posição, orientação e escala
    - textura ou material de cada objeto

### Visão geral
<!-- 
```{figure} /images/topicos.png
---
height: 100px
name: Tópicos
---
Grandes áreas de CGr.
``` -->

- Modelação (*modelling*)
- Representação (*rendering*)
    [Teste as sua sensibilidade](https://area.autodesk.com/fakeorfoto/)
- Animação (*animation*)
    [Flip book](https://youtu.be/0EF_mO9Iu4Y) :)


---
<!-- .slide: style="text-align: left;" -->
### Modelação (*modelling*)

Processamento de Vértices
- Converte representações dos objectos de um sistema de coordenadas para outro
Mundo >> Camâra >> Dispositivo

---
<!-- .slide: style="text-align: left;" -->
### Representação (*rendering*)

[Teste as sua sensibilidade](https://area.autodesk.com/fakeorfoto/)

---
<!-- .slide: style="text-align: left;" -->
### Modelação (*modelling*)


- Animação (*animation*)


---

<!-- .slide: style="text-align: left;" -->
### *Pipeline*

Gera (ou mostra) uma imagem 2D de uma cena 3D

A cena 3D contém:
- uma câmera virtual: posição e orientação
- fonte(s) de luz - localização, tipo, cor
- objetos 3D: cada um tem posição, orientação e escala
    - textura ou material de cada objeto

---



Processamento de Vértices
Converte representações dos objectos
de um sistema de coordenadas para outro
Mundo >> Camâra >> Dispositivo

Determina cores dos vértices

20

Projecção
Combina informação da câmara com a dos objectos
para produzir imagem 2D
Projecção perspectiva: raios de projecção convergentes
Projecção ortogonal: raios de projecção paralelos

21

Assemblagem de Primitivas
Vértices são associados às suas primitivas
antes de se realizar o recorte
Segmentos de recta, polígonos, curvas e superfícies

22

Recorte

Objectos fora do volume de visualização
são recortados da cena
23

Discretização
Se objecto fica na cena, devem ser associadas cores
aos pixéis correspondentes no frame buffer
Discretizador produz conjunto de fragmentos
para cada objecto

24

Discretização
Fragmentos são “pixéis potenciais” com
atributos cor e profundidade
Atributos dos vértices interpolados
para determinar atributos dos fragmentos
(localização, cor e profundidade)

25

Processamento de Fragmentos
Atributos dos fragmentos usados para determinar a
cor do pixel correspondente no frame buffer
Fragmentos podem ocultar outros
mais distantes da câmara

26

API Gráfica

27

API Gráfica
Componente chave de um sistema gráfico

Colecção de funções para realizar operações básicas
Desenhar Imagens Sintéticas
Representar Objectos 3D
Animar Cenas
...
28

Como criar imagens sintéticas?

Através da API especificam-se
Objectos, Materiais, Câmaras e Fontes de Luz

29

Especificar Objectos
APIs suportam
conjunto limitado de primitivas
Objectos definidos
pela sua localização no espaço ou
pelos seus vértices
30

Especificar um Triângulo
(à antiga)
Tipo de objecto
Localização dos vértices
glBegin(GL_POLYGON)
glVertex3f(0.0, 0.0, 0.0);
glVertex3f(0.0, 1.0, 0.0);
glVertex3f(0.0, 0.0, 1.0);
glEnd( );

31

Especificar um Triângulo
(usando GPU)
1.

Colocar informação geométrica num array
vec3 points[3];
points[0] = vec3(0.0, 0.0, 0.0);
points[1] = vec3(0.0, 1.0, 0.0);
points[2] = vec3(0.0, 0.0, 1.0);

2.

Enviar array para o GPU

3.

Ordenar ao GPU para renderizar um triângulo

32

Especificar Câmaras
Posição do centro de projecção
Orientação da câmara
Campo de visualização
Dimensão da janela

33

Especificar Fontes de Luz

34

Especificar Materiais
Reflexão Ambiente Difusa e Especular

35

Pipeline Gráfico
Primitivas
Câmara
Fontes de Luz

Frame

36

Frame
Animação:
representação sequencial de imagens estáticas
(tal como no cinematógrafo de Lumiére em 1890)

37

Animação

38

Animação em CG
Gerar sequência de frames
Desempenho dado por fps
Quanto mais, melhor… min. 25fps

39

Computação Gráfica Interactiva
Mais que gerar frames em tempo real…
dar ao utilizador o controlo
Resultado produzido depende do input do utilizador

?

Edward Angel, Cap. 2
40

E agora…

41

Enquadramento e Conceitos Fundamentais

Breve Introdução ao

three.js

42

43

44

45

46

three.js
Biblioteca JavaScript

API Gráfica

47

Editor
Notepad++

(apenas Windows)

Brackets

(apenas Mac)

Sublime Text Editor
(OS X, Windows, Linux)

WebStorm -- pago -(OS X, Windows, Linux)

... ou outro da vossa preferência
48

Debugging

49

Debugging (em Chrome)

50

Obter o three.js

descarregar versão completa da página oficial
http://threejs.org/
(não recomendado, a menos que estejam a pensar trabalhar offline)

51

Obter o three.js
descarregar apenas um ficheiro Javascript
three.js ou three.min.js

https://github.com/mrdoob/three.js/tree/master/build

52

Criar pastas e ficheiros
CG

exemplo

js

exemplo.html
53

Criar pastas e ficheiros

js

three.js

exemplo.js
54

exemplo.html

55

exemplo.js

56

exemplo.js

57

exemplo.js

58

exemplo.js

59

Ciclo Update/Display

60

exemplo.js

Update
Display

61

exemplo.html

62

Resultado final…

63


```{bibliography} ../referencias.bib
:style: plain
:filter: docname in docnames
```
