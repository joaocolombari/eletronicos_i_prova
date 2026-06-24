# Circuitos Eletrônicos I — Prova Final

Este repositório contém a resolução e a validação computacional dos exercícios propostos na lista de estudos para a **Prova Final** da disciplina de **Circuitos Eletrônicos I**.

---

## 🛠️ Ferramentas Utilizadas

* **`Python 3.10+`**: Ambiente de execução dos scripts e tratamento de dados.
* **`Ngspice`**: Motor open-source de simulação de circuitos elétricos em backend, responsável por resolver numericamente as matrizes de equações não lineares dos semicondutores.
* **`PySpice`**: Biblioteca de integração que faz a ponte entre o Python e o Ngspice, permitindo carregar netlists, configurar parâmetros de simulação e capturar formas de onda diretamente em estruturas de dados nativas.
* **`Matplotlib` & `NumPy`**: Ferramentas utilizadas para o processamento matemático dos vetores de simulação e plotagem gráfica de alta resolução.
* **`LTspice`**: Utilizado de forma auxiliar no fluxo de design para desenho visual dos esquemáticos e exportação direta das listas de conexões (*netlists*).

---

## 📐 Fluxo de Trabalho (Design Híbrido)

Para evitar a codificação manual exaustiva de nós e componentes linha por linha, o projeto adota um **fluxo de simulação híbrido**:

1. **Desenho Esquemático**: O circuito é montado visualmente no ambiente gráfico do **LTspice**.
2. **Exportação da Netlist**: O LTspice gera a lista estruturada de conexões em formato de texto com extensão `.net` ou `.asc` (*View -> SPICE Netlist*).
3. **Ajuste Fino**: O arquivo passa por breves modificações de sintaxe manuais ou automatizadas (como a adequação de parâmetros de modelos ou a injeção de resistências para caminhos de convergência DC).
4. **Leitura e Execução**: O módulo `SpiceParser` do **PySpice** lê o arquivo texto diretamente no Jupyter Notebook (`.ipynb`), executando análises transientes ou de variação contínua diretamente no Kernel do Python.

---

## 💻 Configuração do Ambiente e Dependências

### 1. Pré-requisito: Instalação do Motor SPICE
Para rodar as simulações locais através do ecossistema do PySpice, é obrigatório possuir o executável do **Ngspice** instalado no sistema operacional e configurado no PATH global.

* **macOS (via Homebrew):**
    ```bash
    brew install ngspice
    ```
* **Linux (Ubuntu/Debian):**
    ```bash
    sudo apt-get update
    sudo apt-get install ngspice
    ```
* **Windows:** É necessário baixar os binários do site oficial do SourceForge e apontar a variável de ambiente do sistema para a pasta `\bin` instalada.

### 2. Instalação das Bibliotecas do Python
O bloco inicial do notebook realiza a verificação e instalação silenciosa das dependências na instância ativa do seu Kernel:

```bash
pip install numpy matplotlib pyspice schemdraw
```