# Monitoramento de Célula de Carga com Raspberry Pi

### Requisitos

- Raspberry Pi
- Sensor de Célula de Carga HX711
- Python 3
- Bibliotecas Python:
  
  - `RPi.GPIO`
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
pip3 install RPi.GPIO hx711 matplotlib
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
import matplotlib.pyplot as plt
from hx711 import HX711

# Configurações do HX711 - Sensor
DT_PIN = 5  # GPIO5
SCK_PIN = 6  # GPIO6

hx = HX711(DT_PIN, SCK_PIN)
hx.set_reading_format("MSB", "MSB")
hx.set_reference_unit(1)  # Defina a unidade de referência de acordo com a calibração

# Inicializa a célula de carga
hx.reset()
hx.tare()

# Vetores para armazenar dados
times = []
forces = []

# Duração da coleta de dados (em segundos)
duration = 60
start_time = time.time()

print("Coletando dados...")

while time.time() - start_time < duration:
    try:
        # Obtém a leitura bruta da célula de carga
        val = hx.get_weight(5)
        current_time = time.time() - start_time

        # Armazena os dados
        times.append(current_time)
        forces.append(val)

        # Exibe a leitura
        print(f"Tempo: {current_time:.2f}s | Força: {val:.2f}g")

        # Diminui a frequência de amostragem para 10Hz
        time.sleep(0.1)
    except (KeyboardInterrupt, SystemExit):
        break

# Libera os pinos GPIO
hx.power_down()
hx.power_up()

# Plota os dados
plt.plot(times, forces, label="Força aplicada")
plt.xlabel("Tempo (s)")
plt.ylabel("Força (g)")
plt.title("Força aplicada ao longo do tempo")
plt.legend()
plt.show()
```

### Passo 4: Calibração
A calibração da célula de carga é um passo essencial para garantir a precisão das leituras. Ajuste a linha hx.set_reference_unit(1) para um valor que corresponda corretamente ao peso conhecido.

# Versão para Simulação

```bash
import time
import matplotlib.pyplot as plt
import numpy as np

# Função para simular a leitura do sensor de carga
def simulate_load_cell_reading(t):
    # Simula uma variação sinusoidal da carga com um pouco de ruído aleatório
    load = 10 * np.sin(0.1 * t) + np.random.normal(0, 1)
    return load

# Vetores para armazenar dados
times = []
forces = []

# Duração da coleta de dados (em segundos)
duration = 60
start_time = time.time()

print("Coletando dados simulados...")

while time.time() - start_time < duration:
    try:
        # Obtém a leitura simulada da célula de carga
        current_time = time.time() - start_time
        val = simulate_load_cell_reading(current_time)

        # Armazena os dados
        times.append(current_time)
        forces.append(val)

        # Exibe a leitura
        print(f"Tempo: {current_time:.2f}s | Força: {val:.2f}g")

        # Diminui a frequência de amostragem para 10Hz
        time.sleep(0.1)
    except (KeyboardInterrupt, SystemExit):
        break

# Plota os dados
plt.plot(times, forces, label="Força aplicada (simulada)")
plt.xlabel("Tempo (s)")
plt.ylabel("Força (g)")
plt.title("Força aplicada ao longo do tempo (simulação)")
plt.legend()
plt.show()
```
