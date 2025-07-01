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

![falstad.png](https://github.com/juan-tomba/fonte-ajustavel-arduino/blob/main/falstad.png)

Link do circuito [aqui](https://www.falstad.com/circuit/circuitjs.html?ctz=CQAgjCAMB0l3BWEB2WZIICxgEwGZMA2QgDmRMJEwE4QlM86BTAWjDACgBnEHHTECUgg8CHIOGSQAMwCGAGy5MOAN179whYXwF4cUiFvBCopmAg4B3dbv28SJEXchX7jvcNHiPUDgRAAJgCWAPYBTAC2YUzypmDQDvBJyZB4rI4wkDgUvFRwvgF02RIghAiUJuLB0VHh8hyFZZQ+Yu524mAAcphwmA2l5U7CrSUd3b39Iz5No4FMcgCu8gAuHAAqecImU85UUNBgeHgUiSTlyFp4yEgs5oQ4yNTU7EdPOM+0bNBihKKiYMhILgENQEKxkPsntQOGB7ihSCULo4cIMqvNZEtlix5ExChApJlOAAneHIwZIoamTCAlzWHSjDSwySuLyUnqeZyuGYmQjIcQmWkDZp2UhtZnWXn84SikouADGpQcJRlPkksCB6mgr0g1EwQj4qSy+zgnGsJD0lKEHOZAHNFWL7SIxGZXNRigDKG7kZAMjDkAIvbwfSBA-xhBAEPBIaCUikIAAlJhcIJcZayAB2cuUJNDPRDxTwkAE2n0gsDhYDBc51nLdgotnFIcwAnp1AuNl8yxD7dbbo74ZAbBI0EIuvI1DIoLw1AwSBgvJIOFIcCuWWnE-A+XCixWrr7+kcbxDlBcOf3eaPqvA+j33jstcbR5MR+oJ9c5rvW0IDd8Nfd7cDMBm18fwAC8mHTJgiTYPAWHEcNoGQICvBIMAvXQOAcHBUwOkYThQMEb9LSIj1cnAyDoMOOD33yEx61ld8iOfPsBVdd1gPooDi0YgRSM44DT0IgQ6JIgTNzgFlnRMdkGIAD0EQYETIcQkL2Q4QHjTh5NHXiZxQGhwGoRheMYABhWQAAdZDlIJlhCIkOHkttvGOTd3hEbA1MYeMLKJIJMyCKz6ic-x9HECckH0ehBBAAAFEJlggmyABeIiYZYiRCRzBELXgwEcEhQXUCBeOEAARAAdLgAC0IIoqqYIANWy65aCORxkGuDySvAbycGyt1PGnEM8GaTBxBMjS8AGp51CQdBUWKSa1iJDNk1TezXApHwrUpQVtpFJVVS5JUTApVjrHOrZaOZeSsAhAhDH8AgBEm+L00Sqrwi+0IAiy+SHmlXRIAhXkvJAUyAAtZBUZQAaIXhPNeRHXt6kAADEQg+pgvpx1MIK4ABj-68ghf06D1FAIWW1b0y4aR7IiWQ-qJKrcGQBqAWakJeFB4s8lm5xoHg3IHhEDgeYtIjhB6QW1SyebcgtaagA)

## Eagle:
---

### Esquemático:
![schematic.png](https://github.com/juan-tomba/fonte-ajustavel-arduino/blob/main/schematic.png)


### Protoboard
![protoboard.png](https://github.com/juan-tomba/fonte-ajustavel-arduino/blob/main/protoboard.png)


## Cálculos:
---
* calculo1

* calculo2


## Vídeo no YouTube:
---
Link do vídeo: [link](########)





# Projeto-Arduino:

## Introdução:
O circuito típico consiste em quatro botões coloridos e quatro LEDs correspondentes (vermelho, verde, azul e amarelo). Cada botão está ligado a uma entrada digital do Arduino, enquanto os LEDs são conectados às saídas digitais. Ao iniciar o jogo, o Arduino acende os LEDs em uma sequência aleatória. O jogador deve repetir essa sequência pressionando os botões na ordem correta. Se errar, o jogo reinicia.


## Software:
---
```c++
int sequencia[32] = {};
int botoes[4] = {8,9,10,11};
int leds[4] = {2,3,4,5};
int rodada = 0;
int passo = 0;
int botao_pressionado = 0;
bool gameover = false;
void setup() {
  
  pinMode(2,OUTPUT);
  pinMode(3,OUTPUT);
  pinMode(4,OUTPUT);
  pinMode(5,OUTPUT);

  pinMode(8,INPUT_PULLUP);
  pinMode(9,INPUT_PULLUP);
  pinMode(10,INPUT_PULLUP);
  pinMode(11,INPUT_PULLUP);

  Serial.begin(9600);
}
void proximaRodada()
{
  int sorteio = random(4);
  sequencia[rodada] = sorteio;
  rodada++;
  Serial.print(sorteio);
}
void loop() {


  proximaRodada();
  reproduzirSequencia();
  aguardarJogador();
  if(gameover)
  {
    passo = 0;
    rodada = 0;
    sequencia[32] = {};
    gameover = false;
  }
  delay(1000);
}
void reproduzirSequencia()
{ 
  for(int i = 0; i<rodada; i++)
  {
    digitalWrite(leds[sequencia[i]],HIGH);
    delay(500);
    digitalWrite(leds[sequencia[i]],LOW);
    delay(100);
  }

}
void aguardarJogador()
{
  for(int i = 0; i<rodada;i++)
  { 
    bool jogou = false;
    while(!jogou){
      for(int i = 0; i <=3; i++)
      {
        if(digitalRead(botoes[i]) == LOW)
        {
          botao_pressionado = i;
          digitalWrite(leds[i], HIGH);
          delay(300);
          digitalWrite(leds[i],LOW);
          jogou = true;
        }
      }
    }
    if(sequencia[passo] != botao_pressionado)
    {
      for(int i = 0;i<=3;i++)
      {
        digitalWrite(leds[i],HIGH);
        delay(100);
        digitalWrite(leds[i],LOW);

      }
      gameover = true;
      break;
    }
    
    passo+=1;
  }
 
  
  passo = 0; 
}

```


## Vídeo no YouTube:
---
[link](link vídeo youtube)





# Integrantes do grupo:
---
#### Juan Pablo Tomba

#### João Pedro Neves

#### Enzo Trulenque Evangelista

#### Nicolas Jose Mota
