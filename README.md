# O projeto

O projeto consiste em uma fonte de tensão ajustável, que deve ser ligada em uma entrada de 127V de corrente alternada a 60 Hz e deve fornecer entre 3V a 12V e 100 mA
de corrente contínua

**[Vídeo explicativo](https://drive.google.com/file/d/1LYwIoo3KqqAePAGEwZrHCSvGdLBT7RUE/view?usp=sharing)**

## Grupo
- Bacarin (10873351)
- Luis Eduardo de Brito Câmara (12690282)
- Pedro Falcão Rocha (12692408)

## A fonte

Uma fonte conforme a especificação precisa de algumas etapas e componentes para funcionar. São elas:

### - O transformador
  é o que transforma a tensão de 180V de entrada em uma tensão menor, para que passe pelos demais componentes. Para
  essa fonte, foi utilizado um transformador que fornece uma tensão de saída de 24 V, mais próxima dos 12V que queremos.
  Agora que temos valores menores para trabalhar, podemos nos preocupar em deixar a corrente contínua
 
### - A retificação
  é a primeira etapa para transformar AC em DC. A retificação faz com que a corrente alternada se torne uma corrente polarizada, removendo
  os "vales" da tensão de entrada e deixando apenas cristas.  
  
 ![image](https://user-images.githubusercontent.com/37711709/126834291-d438e1ff-30fb-4e94-9e6a-74ddc0e0cbf7.png)
  
  Senoide da fonte antes da retificação
  
  A retificação nessa fonte é feita por meio de uma ponte de diodos - que fazem com que a corrente flua em apenas um sentido (caso a sua tensão máxima não seja rompida)
  
  ![image](https://user-images.githubusercontent.com/37711709/126835671-2c83ff85-1724-4511-8bfe-9ac3e551dd7d.png)
  
  onda após a retificação
  
  É importante notar que cada diodo consome 0,7V da tensão, portanto nossa tensão anterior de 24V, nesse
  ponto, já caiu levemente para 22,6V (apenas dois diodos são usados por vez)
  
  Agora, o objetivo é deixar essa tensão com apenas cristas o mais estável possível
  
### - A filtragem
  é a etapa em que a tensão é filtrada para transformar a corrente em DC - corrente contínua - com menos oscilações.
  O principal responsável por essa etapa é o capacitor. Funciona da seguinte forma:
  O capacitor, em paralelo com o circuito que temos até agora, é carregado quando os diodos deixam a corrente passar, e, na falta
  de corrente, os momentos baixos do gráfico anterior, age como uma fonte para o resto do circuito.
  Para essa finalidade, quanto maior fosse a capacitância do capacitor, melhor seria, pois ele forneceria
  tensão suficiente para que o ripple, a variação de tensão, fosse mínima. Mas na prática, não se pode
  usar um capacitor tão grande, tanto pelo custo quanto pelo tamanho. Então o quão grande precisa ser o capacitor? O suficiente para que ele gere um ripple de no
  máximo 10% da tensão que ele recebe. Encontramos esse valor pela seguinte fórmula:
  
 ![image](https://user-images.githubusercontent.com/37711709/126879908-ea724e0a-bfeb-4d49-94d0-6d29a73d3e90.png)
 a qual nos diz que um capacitor de 370 µF é suficiente. Vamos então escolher um capacitor de valor comercial um pouco acima desse. Na loja em que estamos comprando, o mais
 próximo é o de 470 µF.
  
### - A regulação
  etapa em que a corrente recebe _tweaks_ para ficar conforme a especificação. Nessa etapa, é utilizado o diodo zener. Em diodos comuns, quando se atinge a tensão de ruptura, eles passam a deixar uma corrente extremamente grande passar por eles no sentido inverso. No diodo zener, quando se atinge uma tensão chamada tensão zener, ele passa a permitir a passagem de correntes de forma a manter constante a tensão entre seus terminais, agindo como um curto circuito. Isso tem como efeito, no circuito, "cortar" a tensão extra que tinhamos para o valor de sua tensão zener. Como queremos uma tensão de 12V, podemos usar o modelo comercial de Zener de 13V, logo acima disso. Precisamos também ligar um resistor em série com o zener, para que ele não queime.
  
  Partimos então da escolha de um diodo zener de tensão Vz = 13V, e que tem como potência máxima 1 W. Vamos escolher um resistor de forma que a potência máxima dissipada pelo zener seja de 0,5 W, para dar certa margem. Temos, então, que:
  
![image](https://user-images.githubusercontent.com/37711709/127086707-5b0e8467-49f0-4acb-ad1a-9b81313aaa67.png)

Essa é a resistência mínima que o resistor pode ter. Testando resistências acima disso, descobrimos que o circuito continua fornecendo uma tensão estável quando colocamos um resistor de até 2,7kΩ, então vamos escolher um desses. A vantagem é que, quanto maior esse resistor, menos corrente passa pelo diodo zener, e, como efeito, ele gasta menos potência e esquenta menos.



### - O circuito final no Falstad
![image](https://user-images.githubusercontent.com/37711709/127557114-cbe6ff6c-8df1-4325-93b1-9b88d5c618a5.png)



[link para o circuito no Falstad](https://tinyurl.com/ydmfa28s)

A montagem foi feita no simulador, o que forneceu os valores necessários de cada componente. Alguns outros componentes foram usados no circuito, e estão listados abaixo

  - Transistor bipolar: ligado da forma que está no circuito, ele controla e amplifica a corrente que chegará na carga
  - Potenciômetro: é usado para controlar a tensão no terminal de saída, variando de 3V a 12V
  - Resistor de 2.2KΩ: regula a voltagem do circuito

### - A montagem no software Eagle
![image](https://cdn.discordapp.com/attachments/369234563911778306/870393173405483018/unknown.png)
Esquemático

![image](https://cdn.discordapp.com/attachments/369234563911778306/870393606748385360/unknown.png)
PCB
  
 ### - Componentes e preços
 Abaixo vai uma tabela com os componentes usados, suas especificações, preços e links
 
 |Nome do Componente |Especificações|Preço R$ |
 |-------------------|--------------|------|
 |Transformador|trafo que transforma entradas de 110 ou 220 V em 24 V, com corrente de 1A|[38,77](https://www.baudaeletronica.com.br/transformador-trafo-1a-24v.html)|
 |Capacitor eletrolítico|470uF / 25V|[0,41](https://www.baudaeletronica.com.br/capacitor-eletrolitico-470uf-25v.html)|
 |Resistor 2.2k|2.2 kΩ, 2W de potência|[0,38](https://www.baudaeletronica.com.br/resistor-2k2-5-2w.html)|
 |Resistor 2.7k|2.7 Ω, 1/2W de potência|[0,14](https://www.baudaeletronica.com.br/resistor-2k7-1-2w.html)|
 |Potenciômetro|Potenciômetro linear de 5000Ω|[1,99](https://www.baudaeletronica.com.br/potenciometro-linear-de-5k-5000.html)|
 |Diodo Zener|1N4743, de 13V e 1 W|[0,19](https://www.baudaeletronica.com.br/diodo-zener-1n4743-13v-1w.html)|
 |Diodo retificador|1N5404, de 3A|4 x [0,34](https://www.baudaeletronica.com.br/diodo-1n5404.html)|
 |Transistor NPN BC337|tensão máxima de 45V e corrente máxima IC de 500mA|[0,20](https://www.baudaeletronica.com.br/transistor-npn-bc337.html)|
 ||total|R$ 43,44
 
