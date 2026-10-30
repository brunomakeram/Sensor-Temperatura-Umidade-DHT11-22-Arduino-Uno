# Glossário

Este glossário reúne os principais termos e conceitos usados no projeto de medição de temperatura e umidade com Arduino Uno e sensor DHT, sem alterar a lógica do código original.

# 1. Visão geral do projeto

## 1.1 `DHT11` / `DHT22`
São sensores de temperatura e umidade da família DHT. O código foi validado com os dois modelos, trocando apenas o tipo definido no início do projeto.
Aparece em: `#define TIPO_DHT DHT11` e na explicação da `README.md`.
Exemplo: `#define TIPO_DHT DHT22` para a simulação Wokwi.
Referência: https://learn.adafruit.com/dht

## 1.2 `DHT sensor library`
É a biblioteca usada para ler dados de temperatura e umidade do sensor DHT.
Aparece em: `#include <DHT.h>` no código.
Exemplo: `DHT dht(PINO_DHT, TIPO_DHT);`.
Referência: https://github.com/adafruit/DHT-sensor-library

## 1.3 `temperatura`
É a leitura da temperatura ambiente em graus Celsius.
Aparece em: `float temperatura = dht.readTemperature();`.
Exemplo: `Serial.print(temperatura);`.

## 1.4 `umidade`
É a leitura da umidade relativa do ar em porcentagem.
Aparece em: `float umidade = dht.readHumidity();`.
Exemplo: `Serial.print(umidade);`.

# 2. Pinos e hardware

## 2.1 `TIPO_DHT`
Define qual sensor da família DHT está sendo usado no projeto.
Aparece em: `#define TIPO_DHT DHT11`.
Exemplo: `#define TIPO_DHT DHT22`.

## 2.2 `PINO_DHT`
É o pino digital em que o sensor DHT está conectado.
Aparece em: `#define PINO_DHT 8`.
Exemplo: `DHT dht(PINO_DHT, TIPO_DHT);`.

## 2.3 `PINO_LED_VERMELHO`
É o pino do LED vermelho que indica a faixa de temperatura alta.
Aparece em: `#define PINO_LED_VERMELHO 2`.
Exemplo: `digitalWrite(PINO_LED_VERMELHO, ledAceso == "vermelho");`.

## 2.4 `PINO_LED_AMARELO`
É o pino do LED amarelo, usado na faixa intermediária de temperatura.
Aparece em: `#define PINO_LED_AMARELO 4`.
Exemplo: `digitalWrite(PINO_LED_AMARELO, ledAceso == "amarelo");`.

## 2.5 `PINO_LED_VERDE`
É o pino do LED verde, usado na faixa de temperatura baixa.
Aparece em: `#define PINO_LED_VERDE 7`.
Exemplo: `digitalWrite(PINO_LED_VERDE, ledAceso == "verde");`.

## 2.6 `TEMPERATURA_LIMITE_BAIXO`
É o valor que define quando a temperatura cai na faixa verde.
Aparece em: `const float TEMPERATURA_LIMITE_BAIXO = 30.0;`.
Exemplo: `if (temperatura < TEMPERATURA_LIMITE_BAIXO)`.

## 2.7 `TEMPERATURA_LIMITE_ALTO`
É o valor que define quando a temperatura se enquadra na faixa vermelha.
Aparece em: `const float TEMPERATURA_LIMITE_ALTO = 34.0;`.
Exemplo: `else if (temperatura <= TEMPERATURA_LIMITE_ALTO)`.

# 3. Objetos e funções do sensor

## 3.1 `DHT dht`
É o objeto que representa o sensor DHT no código e permite chamar `readTemperature()` e `readHumidity()`.
Aparece em: `DHT dht(PINO_DHT, TIPO_DHT);`.
Exemplo: `float temperatura = dht.readTemperature();`.

## 3.2 `dht.begin()`
Inicializa o sensor DHT e o prepara para leitura.
Aparece em: `dht.begin();` no `setup()`.
Exemplo: `dht.begin();`.

## 3.3 `dht.readTemperature()`
Lê a temperatura em graus Celsius diretamente do sensor.
Aparece em: `float temperatura = dht.readTemperature();`.
Exemplo: `float temperatura = dht.readTemperature();`.

## 3.4 `dht.readHumidity()`
Lê a umidade relativa do ar em porcentagem.
Aparece em: `float umidade = dht.readHumidity();`.
Exemplo: `float umidade = dht.readHumidity();`.

## 3.5 `isnan()`
Verifica se a leitura retornou `NaN`, ou seja, se houve falha de comunicação ou leitura inválida.
Aparece em: `if (isnan(temperatura) || isnan(umidade))`.
Exemplo: `if (isnan(temperatura) || isnan(umidade)) { ... }`.
Referência: https://www.cplusplus.com/reference/cmath/isnan/

# 4. Lógica de indicação visual

## 4.1 `ledAceso`
É a string que guarda qual LED deve ser aceso conforme a faixa de temperatura.
Aparece em: `String ledAceso;`.
Exemplo: `ledAceso = "amarelo";`.

## 4.2 `faixa verde`
É a condição em que a temperatura está abaixo do limite inferior.
Aparece em: `if (temperatura < TEMPERATURA_LIMITE_BAIXO) { ledAceso = "verde"; }`.

## 4.3 `faixa amarela`
É a condição em que a temperatura está dentro da faixa intermediária.
Aparece em: `else if (temperatura <= TEMPERATURA_LIMITE_ALTO) { ledAceso = "amarelo"; }`.

## 4.4 `faixa vermelha`
É a condição em que a temperatura está acima do limite superior.
Aparece em: `else { ledAceso = "vermelho"; }`.

# 5. Funções principais do Arduino

## 5.1 `Serial.begin()`
Inicializa a comunicação serial para exibir os valores no Monitor Serial.
Aparece em: `Serial.begin(9600);`.
Exemplo: `Serial.println("Erro ao ler o sensor DHT");`.
Referência: https://www.arduino.cc/reference/en/language/functions/communication/serial/begin/

## 5.2 `digitalWrite()`
Acende ou apaga um LED de acordo com a faixa de temperatura detectada.
Aparece em: `digitalWrite(PINO_LED_VERDE, ledAceso == "verde");`.
Exemplo: `digitalWrite(PINO_LED_VERMELHO, ledAceso == "vermelho");`.

## 5.3 `delay()`
Cria o intervalo de 2 segundos entre duas leituras da temperatura e umidade.
Aparece em: `delay(2000);`.
Exemplo: `delay(2000);`.

# 6. Ciclos e execução

## 6.1 `setup()`
Configura os pinos dos LEDs como saída e inicializa o sensor DHT.
Aparece em: `void setup() { ... }`.

## 6.2 `loop()`
Executa periodicamente a leitura do sensor, decide a faixa de temperatura e aciona o LED correspondente.
Aparece em: `void loop() { ... }`.

## 6.3 `Monitor Serial`
É a saída do Arduino usada para mostrar a temperatura, a umidade e o LED ativo.
Aparece em: `Serial.print("Temperatura: ");` e `Serial.println(ledAceso);`.
Referência: https://www.arduino.cc/reference/en/language/functions/communication/serial/
