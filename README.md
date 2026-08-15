# Códigos da tese de doutorado — HATS

Este repositório reúne os códigos utilizados nos testes computacionais e nas análises apresentadas na tese de doutorado:

**A demodulação do sinal do sensor opto-acústico do Telescópio HATS**

Autora: **Gedeane Gomes da Silva Kenshima**  
Programa de Pós-Graduação em Engenharia Elétrica e Computação  
Universidade Presbiteriana Mackenzie  
São Paulo, 2026.

O trabalho investiga técnicas de processamento digital de sinais aplicadas ao telescópio **High Altitude Terahertz Solar (HATS)**, com foco na recuperação da amplitude do sinal proveniente de uma célula de Golay, cuja radiação é modulada mecanicamente por um *fork chopper* em aproximadamente 20 Hz.

Os códigos deste repositório foram utilizados para simulações, calibração experimental, análise de funções de janelamento, processamento por FFT e estimativa da frequência efetiva de modulação do sistema.

---

## Conteúdo do repositório

### `Simulacao_gaussiana.ipynb`

Simulação de um sinal com envelope gaussiano modulado em aproximadamente 20 Hz.

O notebook é utilizado para avaliar o comportamento de diferentes funções de janelamento na recuperação da amplitude do sinal, considerando diferentes condições de ruído e vazamento espectral.

As funções de janela analisadas incluem:

- Retangular;
- Hamming;
- Hann;
- Bartlett;
- Blackman;
- Flat-top.

Os resultados são comparados utilizando métricas como RMSE e erro na recuperação da amplitude.

---

### `Simulacao_flare.ipynb`

Simulação de um sinal assimétrico representativo de uma explosão solar (*flare*).

O sinal possui tempos distintos de subida e decaimento, permitindo analisar o desempenho das funções de janela em sinais transitórios que apresentam comportamento diferente de um envelope gaussiano simétrico.

O objetivo é avaliar a reconstrução do envelope do sinal após o processamento por FFT.

---

### `CurvadeCalibracao.ipynb`

Código utilizado no processamento dos sinais obtidos nos ensaios de bancada com:

- calibrador de corpo negro Dwyer Omega BB-4A;
- célula de Golay Tydex GC-1P;
- *fork chopper*;
- osciloscópio digital.

O notebook realiza o processamento dos sinais adquiridos para diferentes temperaturas da fonte de corpo negro e permite obter a relação entre:

**temperatura da fonte → amplitude do sinal elétrico**

Essa relação é utilizada para gerar a curva de calibração tensão-temperatura do sistema de aquisição.

---

### `CurvadeCalibracao_02.ipynb`

Versão complementar da análise de calibração.

Inclui a comparação entre diferentes métodos de recuperação da amplitude do sinal, incluindo:

- ajuste de função senoidal;
- FFT;
- aplicação de diferentes funções de janelamento.

Os resultados permitem comparar os coeficientes da regressão linear e os valores de RMSE obtidos para cada método.

---

### `JanelamentoeFFT_dadosHATS.ipynb`

Processamento dos dados observacionais reais obtidos pelo telescópio HATS.

O notebook realiza:

1. leitura dos dados adquiridos pelo telescópio;
2. divisão do sinal em segmentos;
3. aplicação das funções de janelamento;
4. cálculo da FFT;
5. extração da componente associada à modulação do *fork chopper*;
6. reconstrução da série temporal da amplitude.

Esse procedimento permite comparar o desempenho das diferentes funções de janela nos dados observacionais.

---

### `Estimativa_de_frequencia_fork_chopper.ipynb`

Análise desenvolvida para determinar experimentalmente a frequência efetiva de funcionamento do *fork chopper*.

Foram analisados:

- dados experimentais de bancada;
- dados observacionais reais do HATS.

A frequência foi estimada utilizando métodos baseados em:

- FFT com interpolação do pico espectral;
- evolução temporal da fase do sinal analítico obtido pela Transformada de Hilbert.

Nos experimentos de bancada, a frequência medida permaneceu próxima ao valor nominal de 20 Hz.

Nos dados observacionais do HATS, foi observada uma frequência efetiva de aproximadamente:

**20,334 Hz**

Esse deslocamento em relação ao valor nominal torna-se relevante quando o processamento é realizado em segmentos de 1 s, cuja resolução espectral é de 1 Hz, produzindo um desalinhamento de aproximadamente 33% da largura de um bin da FFT.

Esse resultado ajuda a explicar a influência do fenômeno de *scalloping loss* na recuperação da amplitude dos dados reais.

---

## Ambiente de execução

Os códigos foram desenvolvidos em **Python** e podem ser executados em:

- Google Colab;
- Jupyter Notebook;
- JupyterLab;
- ambientes Python locais compatíveis.

As principais bibliotecas utilizadas são:

```text
numpy
scipy
pandas
matplotlib
