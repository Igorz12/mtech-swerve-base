# 📐 Estrutura Base - Swerve Drive (YAGSL Example)

Este repositório contém o código estrutural para a configuração e controle do sistema de movimentação Swerve Drive da **Equipe MTECH 9603**, baseado na biblioteca **YAGSL (Yet Another General Swerve Library)**.

⚠️ **IMPORTANTE (Compatibilidade):** Esta versão do código foi desenvolvida e testada utilizando o **WPILib 2026.2.1**. Certifique-se de que seu ambiente de desenvolvimento esteja atualizado na mesma versão para evitar conflitos.

---

## 🛠️ Hardware Suportado

Este template foi projetado especificamente para módulos **Swerve SDS MK4 e MK4i** utilizando a seguinte combinação de hardware:

* **Motores de Tração:** Falcon 500, NEO ou Kraken X60
* **Motores de Rotação:** Falcon 500 ou NEO
* **Giroscópio (IMU):** Pigeon 2.0
* **Sensores de Azimute (Ângulo):** CANcoder

> 🛑 **RECOMENDAÇÃO CRÍTICA:** Caso a sua Swerve utilize uma configuração **Full Kraken** (Kraken tanto na tração quanto na rotação), recomenda-se fortemente a utilização da estrutura oficial da **CTRE** para o controle nativo dos motores, em vez deste template.

---

## ⚙️ Configuração e Documentação

Antes de realizar o deploy do código, é fundamental entender a lógica de inversão dos motores e sensores para evitar danos ao robô.

* **Guia de Inversão dos Módulos e IMU:** Acesse a [Documentação de Inversão da YAGSL](https://docs.yagsl.com/configuring-yagsl/when-to-invert) para entender quando e como inverter os sinais no arquivo JSON.
* **Documentação Geral:** Para compreender a fundo a estrutura do código, criação de comandos e telemetria, consulte a [Documentação Oficial da YAGSL](https://docs.yagsl.com/).

---

## 📂 Onde estão as configurações? (Onde mexer?)

Para adaptar este código para o seu robô, você precisará alterar os arquivos de configuração JSON localizados na pasta do projeto:
`src/main/deploy/swerve/`

Dentro desta pasta, certifique-se de ajustar:
1. **`swervedrive.json`**: Configurações gerais físicas do robô (distância entre eixos, pesos, etc.).
2. **Pasta `modules/`**: Os 4 arquivos JSON correspondentes a cada módulo (Front Left, Front Right, Back Left, Back Right), onde você deve inserir os **CAN IDs** corretos e os **Absolute Offsets** dos seus CANcoders.

---

## 🚀 Primeiros Passos para Teste

1. Coloque o robô sobre cavaletes/blocos (com as rodas suspensas para segurança).
2. Faça o alinhamento físico das rodas apontando todas para frente.
3. Abra a telemetria do Swerve através do Shuffleboard/SmartDashboard para validar os ângulos absolutos.
4. Teste os eixos do Joystick devagar antes de colocar o robô no chão.

---

### 💡 Nota Técnica: Por que convertemos os valores do CANCoder?

Se você notar no código ou na telemetria que os valores do `Absolute Encoder` estão sendo multiplicados por **360**, isso acontece porque o CANCoder faz a leitura nativa em **rotações (de 0 a 1)**. 

Multiplicamos por 360 para converter essa unidade para **graus** ($360^\circ$ equivalem a 1 volta completa), que é o padrão que a YAGSL e a WPILib utilizam para calcular a direção correta de cada módulo.
