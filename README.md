# 💤 Sleep Detection System (Detecção de Sonolência com Visão Computacional)

Este projeto implementa um sistema de **detecção de sonolência em tempo real** utilizando visão computacional com **MediaPipe** e integração com hardware (Arduino) para emissão de alertas.

O objetivo é identificar quando os olhos permanecem fechados por um determinado período e acionar um **buzzer** como alerta — podendo ser aplicado em cenários como **segurança veicular**, monitoramento de operadores ou prevenção de fadiga.

---

## 🚀 Funcionalidades

* Detecção facial em tempo real via webcam
* Rastreamento de pontos dos olhos com MediaPipe Face Mesh
* Cálculo da distância entre pálpebras
* Identificação de olhos abertos/fechados
* Contagem do tempo com olhos fechados
* Acionamento de buzzer via Arduino
* Feedback visual na tela

---

## 🧠 Como funciona

O sistema utiliza o **Face Mesh do MediaPipe** para capturar landmarks faciais e seleciona pontos específicos dos olhos:

* Olho direito: landmarks 159 e 145
* Olho esquerdo: landmarks 386 e 374

A distância entre esses pontos é calculada usando a distância euclidiana.

* Se a distância for menor que um limiar → olhos fechados
* Caso contrário → olhos abertos

Se os olhos permanecerem fechados por **≥ 2 segundos**, o sistema considera estado de sonolência e:

* Exibe alerta na tela
* Envia sinal para o Arduino ativar o buzzer

---

## 🔌 Integração Hardware-Software

### Componentes

* Arduino
* Buzzer
* Cabo USB
* Computador com webcam

### Comunicação

A comunicação é feita via **Serial (pyserial)**:

* `"ON"` → ativa buzzer
* `"OFF"` → desativa buzzer

```python
arduino.write(b'ON\n')
arduino.write(b'OFF\n')
```

### Observação

A porta serial (`COM9`) deve ser ajustada conforme o seu sistema:

```python
arduino = serial.Serial('COM9', 9600)
```

No Linux/Mac, geralmente será algo como:

```bash
/dev/ttyUSB0
```

---

## 🛠️ Tecnologias utilizadas

* Python 3.10
* OpenCV
* MediaPipe
* PySerial
* Webcam

---

## 📦 Instalação

Clone o repositório:

```bash
git clone https://github.com/seu-usuario/seu-repo.git
cd seu-repo
```

Instale as dependências:

```bash
pip install -r requirements.txt
```

---

## ▶️ Execução

```bash
python SleepDetector.py
```

Pressione `q` para encerrar.

---

## ⚙️ Parâmetros importantes

Você pode ajustar a sensibilidade alterando:

```python
if distEs <= 10 and distDi <= 10:
```

E o tempo de detecção:

```python
if situacao == "F" and tempo >= 2:
```

---

## 🎯 Aplicações

* Segurança no trânsito (detecção de motorista sonolento)
* Monitoramento industrial
* Sistemas de vigilância inteligente
* Saúde ocupacional


