# fonte-de-tensao


## Componentes/Valores:
---
| Quantidades   | Componentes   | Preço |
| ------------- |:-------------:| -----:|
| 1      | Capacitor (1000uF x 25V)      | R$1,80  |
| 5      | LED 5mm vermelho              | R$2,50  |
| 1      | Chave - 3 terminais           | R$9,30  |
| 1      | Ponte retificadora (2A)       | R$3,90  |
| 1      | Potenciômetro 1W B5K B-16     | R$7,00  |
| 1      | Transistor BC639-16 (2A)      | R$0,80  |
| 2      | Diodo Zener 1N4743 (13V / 1W) | R$1,00  |
| 10     | Resistor 1K                   | R$0,70  |
| 10     | Resistor 4.7K                 | R$0,70  |
| 10     | Resistor 2.2K                 | R$0,70  |
| 10     | Jumper macho x macho          | R$7,00  |
|        | Total                         | R$35,40 |

## Descrição dos Componentes

### Transformador
* Este aparelho é responsável por reduzir a tensão total oriunda da tomada (neste caso, 127V) para uma tensão de trabalho mais baixa e segura.
* Neste circuito, a tensão secundária produzida é de aproximadamente 18.2V AC.
* Apesar de reduzir a tensão, a corrente continua sendo alternada (AC), assim como na entrada.

### Ponte de Diodos
* Um conjunto de quatro diodos, aqui encapsulados em um único componente.
* Cada diodo funciona como uma "válvula de retenção" ou uma "rua de mão única" para a eletricidade, forçando a corrente a fluir em apenas uma direção.
* A ponte de diodos converte a corrente alternada (AC) em corrente contínua (DC), garantindo que o fluxo de eletricidade tenha sempre o mesmo sentido.
* No entanto, a corrente resultante ainda não é constante, mas sim uma série de pulsos, com picos e vales de tensão.

### Capacitor
* Funciona como um "reservatório" de energia para suavizar os pulsos da corrente contínua.
* O capacitor se carrega durante os picos de tensão e descarrega durante os vales, preenchendo as "lacunas" e estabilizando a linha de tensão.
* A pequena variação de tensão que ainda resta após a filtragem é chamada de "ripple" (ondulação).

### LED
* Componente opcional que serve como um indicador visual, acendendo para demonstrar que o circuito está ligado e funcionando.

### Resistores
* Componentes que oferecem uma resistência à passagem da corrente elétrica.
* Sua principal função é limitar e controlar a corrente que flui para outros componentes, protegendo-os de sobrecargas e garantindo que operem sob as condições corretas de tensão e corrente.

### Diodo Zener
* Um tipo especial de diodo que, além de permitir o fluxo em um sentido, também permite o fluxo no sentido inverso se a tensão exceder seu valor nominal.
* Neste circuito, ele está travado em seu valor nominal de 13V. Sua função é criar um ponto de tensão de referência perfeitamente estável, garantindo que o circuito de controle sempre tenha uma base de 13V para trabalhar, independentemente de pequenas variações na fonte.

### Potenciômetro
* É um resistor variável que permite o ajuste manual da tensão de saída da fonte.
* Junto com o resistor R3, ele forma um divisor de tensão que "fatia" a referência estável de 13V do Zener.
* Ao girar o botão, o usuário seleciona uma "fatia" dessa tensão (entre ~4V e 13V) e a envia como um sinal de comando para o transistor.

### Transistor
* Funciona como uma válvula eletrônica de alta precisão, sendo o componente que efetivamente ajusta a tensão de saída da fonte.
* Ele recebe a tensão de comando do potenciômetro em seu pino **Base** e regula o fluxo principal de energia (que entra pelo **Coletor**) para que a tensão em sua saída (**Emissor**) seja sempre igual à tensão da Base, menos uma pequena queda fixa de ~0,7V.
* Sua grande vantagem é o **ganho de corrente**: ele permite que o sinal de controle fraco do potenciômetro gerencie a corrente forte necessária para alimentar a carga, agindo como um amplificador de força.
## Circuito no Falstad:
---

![falstad2.png](https://github.com/juan-tomba/fonte-ajustavel-arduino/blob/main/falstad3.png)

Link do circuito [aqui](https://tinyurl.com/272rv48x)

## Eagle:
---

### Esquemático:
![schematic.png](https://github.com/juan-tomba/fonte-ajustavel-arduino/blob/main/schematic3.png)


### Protoboard
![protoboard.png](https://github.com/juan-tomba/fonte-ajustavel-arduino/blob/main/protoboard3.png)


## Cálculos:
---
![calc1.jpg](https://github.com/juan-tomba/fonte-ajustavel-arduino/blob/main/20250701_091643.jpg)
![calc2.jpg](https://github.com/juan-tomba/fonte-ajustavel-arduino/blob/main/calc2.jpg)
![calc3.jpg](https://github.com/juan-tomba/fonte-ajustavel-arduino/blob/main/calc3.jpg)
![calc4.jpg](https://github.com/juan-tomba/fonte-ajustavel-arduino/blob/main/calc4.jpg)

## Vídeo no YouTube:
---
Link do vídeo: [link](https://www.youtube.com/watch?v=7NewHWRttzg)





# Projeto-Arduino:

## Introdução:
O circuito típico consiste em quatro botões coloridos e quatro LEDs correspondentes (vermelho, verde, azul e amarelo). Cada botão está ligado a uma entrada digital do Arduino, enquanto os LEDs são conectados às saídas digitais. Ao iniciar o jogo, o Arduino acende os LEDs em uma sequência aleatória. O jogador deve repetir essa sequência pressionando os botões na ordem correta. Se errar, o jogo reinicia.

## Componentes/Valores:
---
| Quantidades   | Componentes   | Preço |
| ------------- |:-------------:| -----:|
|  16           |  Jumper macho-macho   | R$11,20     |
|  4            |  Leds (variados)      | R$2,00      |
|  1            |  Arduíno Uno          | R$109,90    |
|  4            |  Botão push           | R$0,80      |
|  10           |  Resistor 150Ω        | R$0,70      |
|               |  Total                | R$124,60    |


## Circuito:

![circuito-esquema.png]


![circuito-foto.png]
## Software:
---
```c++
// Array para armazenar a sequência de cores (representadas por números de 0 a 3).
// O tamanho 32 define que o jogo pode ter no máximo 32 rodadas.
int sequencia[32] = {};

// Array que mapeia os 4 botões para os pinos digitais do Arduino.
// Botão 0 no pino 8, Botão 1 no pino 9, etc.
int botoes[4] = {8, 9, 10, 11};

// Array que mapeia os 4 LEDs para os pinos digitais do Arduino.
// LED 0 no pino 2, LED 1 no pino 3, etc.
int leds[4] = {2, 3, 4, 5};

// Variável para contar em qual rodada o jogo está. Inicia em 0.
int rodada = 0;

// Variável para acompanhar qual passo da sequência o jogador precisa pressionar.
int passo = 0;

// Guarda o último botão que o jogador pressionou (0, 1, 2 ou 3).
int botao_pressionado = 0;

// "Flag" (bandeira) booleana que indica se o jogo terminou por um erro do jogador.
bool gameover = false;

// --- FUNÇÃO SETUP ---
// É executada uma única vez quando o Arduino é ligado ou resetado.
void setup() {
  
  // Configura os pinos dos LEDs como SAÍDA (OUTPUT).
  pinMode(2, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(5, OUTPUT);

  // Configura os pinos dos botões como ENTRADA (INPUT) com resistor de PULL-UP.
  // INPUT_PULLUP ativa um resistor interno que mantém o pino em HIGH (nível alto).
  // Quando o botão é pressionado (conectando o pino ao GND), a leitura será LOW (nível baixo).
  // Isso evita a necessidade de resistores externos.
  pinMode(8, INPUT_PULLUP);
  pinMode(9, INPUT_PULLUP);
  pinMode(10, INPUT_PULLUP);
  pinMode(11, INPUT_PULLUP);

  // Inicia a comunicação serial para debug (opcional, mas muito útil).
  // Permite ver no Serial Monitor do PC o que está acontecendo, como os números sorteados.
  Serial.begin(9600);
}

// --- FUNÇÃO PARA PREPARAR A PRÓXIMA RODADA ---
void proximaRodada() {
  // Sorteia um número aleatório entre 0 e 3.
  int sorteio = random(4);

  // Armazena o número sorteado na sequência, na posição da rodada atual.
  sequencia[rodada] = sorteio;

  // Incrementa o contador de rodada para a próxima vez.
  rodada++;

  // Imprime o número sorteado no Serial Monitor para ajudar a depurar o código.
  Serial.print(sorteio);
}

// --- FUNÇÃO LOOP ---
// É o coração do programa, fica se repetindo infinitamente.
void loop() {
  // 1. Adiciona um novo passo aleatório à sequência para a rodada atual.
  proximaRodada();
  
  // 2. Mostra a sequência de luzes completa para o jogador.
  reproduzirSequencia();

  // 3. Espera o jogador tentar repetir a sequência.
  //    Esta função também irá definir a flag 'gameover' como 'true' se o jogador errar.
  aguardarJogador();

  // 4. Verifica se o jogo terminou na última rodada.
  if (gameover) {
    // Se sim, reseta todas as variáveis para o estado inicial.
    passo = 0;
    rodada = 0;
    
    //Limpa o array de sequência
    for (int i = 0; i < 32; i++){
      sequencia[i] = 0;
    } 
    gameover = false; // Prepara para um novo jogo.
  }
  
  // 5. Espera 1 segundo (1000 milissegundos) antes de iniciar a próxima rodada.
  delay(1000);
}

// --- FUNÇÃO PARA MOSTRAR A SEQUÊNCIA DE LEDS ---
void reproduzirSequencia() { 
  // Percorre a sequência até a rodada atual.
  for (int i = 0; i < rodada; i++) {
    // Acende o LED correspondente ao passo 'i' da sequência.
    digitalWrite(leds[sequencia[i]], HIGH);
    delay(500); // Mantém o LED aceso por meio segundo.
    digitalWrite(leds[sequencia[i]], LOW); //Apaga o LED.
    delay(100); // Pequena pausa antes de mostrar o próximo LED.
  }
}

// --- FUNÇÃO PARA AGUARDAR E VALIDAR A JOGADA ---
void aguardarJogador() {
  // Percorre cada passo que o jogador deve acertar nesta rodada.
  for (int i = 0; i < rodada; i++) { 
    bool jogou = false; // Flag para controlar se o jogador já pressionou um botão.

    // Este laço 'while' prende a execução aqui até que um botão seja pressionado.
    while (!jogou) {
      // Verifica cada um dos 4 botões.
      for (int j = 0; j <= 3; j++) {
        // Se a leitura do botão 'j' for LOW (pressionado)...
        if (digitalRead(botoes[j]) == LOW) {
          // ...guarda qual botão foi (0, 1, 2 ou 3).
          botao_pressionado = j;
          // Acende o LED correspondente para dar um feedback visual.
          digitalWrite(leds[j], HIGH);
          delay(300); // Mantém aceso por um instante (também ajuda a evitar 'debounce').
          digitalWrite(leds[j], LOW);
          // Avisa que o jogador já fez sua jogada para sair do laço 'while'.
          jogou = true;
        }
      }
    }

    // Após o jogador pressionar um botão, compara com o valor esperado na sequência.
    if (sequencia[passo] != botao_pressionado) {
      // SE ERROU:
      // Pisca todos os LEDs rapidamente para sinalizar 'Game Over'.
      for (int k = 0; k <= 3; k++) {
        digitalWrite(leds[k], HIGH);
        delay(100);
        digitalWrite(leds[k], LOW);
      }
      gameover = true; // Define a flag de game over.
      break;           // Interrompe o loop 'for', pois o jogo já acabou.
    }
    
    // SE ACERTOU:
    // Incrementa o contador de passos para verificar o próximo passo da sequência.
    passo += 1;
  }
  
  // Ao final da função (seja por acerto de todos os passos ou por game over),
  // reseta o 'passo' para 0, preparando para a próxima checagem de jogada.
  passo = 0; 
}
```


## Vídeo no YouTube:
---
[link](https://www.youtube.com/watch?v=Jz6tGamR_Pk)





# Integrantes do grupo:
---
#### Juan Pablo Tomba

#### João Pedro Neves

#### Enzo Trulenque Evangelista

#### Nicolas Jose Mota
