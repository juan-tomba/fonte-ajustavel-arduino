# fonte-de-tensao


# Componentes/Valores:
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




# Circuito no Falstad:
---

![falstad.png](https://github.com/juan-tomba/fonte-ajustavel-arduino/blob/main/falstad.png)

Link do circuito [aqui](https://www.falstad.com/circuit/circuitjs.html?ctz=CQAgjCAMB0l3BWEB2WZIICxgEwGZMA2QgDmRMJEwE4QlM86BTAWjDACgBnEHHTECUgg8CHIOGSQAMwCGAGy5MOAN179whYXwF4cUiFvBCopmAg4B3dbv28SJEXchX7jvcNHiPUDgRAAJgCWAPYBTAC2YUzypmDQDvBJyZB4rI4wkDgUvFRwvgF02RIghAiUJuLB0VHh8hyFZZQ+Yu524mAAcphwmA2l5U7CrSUd3b39Iz5No4FMcgCu8gAuHAAqecImU85UUNBgeHgUiSTlyFp4yEgs5oQ4yNTU7EdPOM+0bNBihKKiYMhILgENQEKxkPsntQOGB7ihSCULo4cIMqvNZEtlix5ExChApJlOAAneHIwZIoamTCAlzWHSjDSwySuLyUnqeZyuGYmQjIcQmWkDZp2UhtZnWXn84SikouADGpQcJRlPkksCB6mgr0g1EwQj4qSy+zgnGsJD0lKEHOZAHNFWL7SIxGZXNRigDKG7kZAMjDkAIvbwfSBA-xhBAEPBIaCUikIAAlJhcIJcZayAB2cuUJNDPRDxTwkAE2n0gsDhYDBc51nLdgotnFIcwAnp1AuNl8yxD7dbbo74ZAbBI0EIuvI1DIoLw1AwSBgvJIOFIcCuWWnE-A+XCixWrr7+kcbxDlBcOf3eaPqvA+j33jstcbR5MR+oJ9c5rvW0IDd8Nfd7cDMBm18fwAC8mHTJgiTYPAWHEcNoGQICvBIMAvXQOAcHBUwOkYThQMEb9LSIj1cnAyDoMOOD33yEx61ld8iOfPsBVdd1gPooDi0YgRSM44DT0IgQ6JIgTNzgFlnRMdkGIAD0EQYETIcQkL2Q4QHjTh5NHXiZxQGhwGoRheMYABhWQAAdZDlIJlhCIkOHkttvGOTd3hEbA1MYeMLKJIJMyCKz6ic-x9HECckH0ehBBAAAFEJlggmyABeIiYZYiRCRzBELXgwEcEhQXUCBeOEAARAAdLgAC0IIoqqYIANWy65aCORxkGuDySvAbycGyt1PGnEM8GaTBxBMjS8AGp51CQdBUWKSa1iJDNk1TezXApHwrUpQVtpFJVVS5JUTApVjrHOrZaOZeSsAhAhDH8AgBEm+L00Sqrwi+0IAiy+SHmlXRIAhXkvJAUyAAtZBUZQAaIXhPNeRHXt6kAADEQg+pgvpx1MIK4ABj-68ghf06D1FAIWW1b0y4aR7IiWQ-qJKrcGQBqAWakJeFB4s8lm5xoHg3IHhEDgeYtIjhB6QW1SyebcgtaagA)

# Projeto do Esquemático no Eagle:
---
![Imagem eagle]




# Cálculos:
---
* calculo1

* calculo2


# Vídeo no YouTube:
---
Link do vídeo: [link](########)





# Projeto-Arduino:

# Introdução:
O circuito típico consiste em quatro botões coloridos e quatro LEDs correspondentes (vermelho, verde, azul e amarelo). Cada botão está ligado a uma entrada digital do Arduino, enquanto os LEDs são conectados às saídas digitais. Ao iniciar o jogo, o Arduino acende os LEDs em uma sequência aleatória. O jogador deve repetir essa sequência pressionando os botões na ordem correta. Se errar, o jogo reinicia.


# Software:
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


# Vídeo no YouTube:
---
[link](link vídeo youtube)





# Integrantes do grupo:
---
#### Juan Pablo Tomba

#### João Pedro Neves

#### Enzo Trulenque Evangelista

#### Nicolas Jose Mota
