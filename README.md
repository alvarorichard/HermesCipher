## Modelo de Treinamento
 Usar uma Árvore de Decisão simples, treinada para distinguir entre tipos de arquivos comuns e arquivos de sistema críticos.

 ## Tipo de Dados para Treinamento
 Utiliza um conjunto de dados de arquivos benignos e maliciosos, incluindo metadados como tamanho do arquivo, tipo e data de criação.

 ## Linguagem de Programação

 Utilizou Python e a biblioteca Scikit-learn para o aprendizado de máquina.

 ## Técnicas para Evitar Detecção:

 * Ofuscação de Código
 * Simulação de Atividade de Usuário: O malware tentava simular cliques e movimentos de mouse para parecer uma atividade de usuário legítima
 * Execução Condicional: O malware só ativava suas funções maliciosas se certas condições fossem cumpridas, como uma verificação de localização ou a presença de certos arquivos, tornando mais difícil para os analistas de malware desencadear seu comportamento malicioso em um ambiente controlado.

## Modelo de Análise de Ambiente

treinou um modelo de aprendizado de máquina para analisar o ambiente do sistema infectado. Usando técnicas de aprendizado não supervisionado, o modelo podia identificar padrões de atividade típicos de sistemas de segurança e analistas de malware. Ele coletou dados como:

    Utilização da CPU e memória
    Atividade de rede
    Processos em execução
    Perfis de comportamento de usuário

Com esses dados, o modelo podia identificar se o malware estava em um ambiente "hostil" (ou seja, um ambiente de teste usado por analistas de segurança) e se adaptar de acordo.

## Estratégia Adaptativa

Se o ambiente era considerado "hostil," o HermesCipher tomaria medidas evasivas:

* Dormência: O malware entraria em um estado "dormente," onde evitaria qualquer atividade maliciosa até que o ambiente fosse considerado "seguro" novamente.

* Modificação de Comportamento: O malware adaptaria seu comportamento para imitar o de um software legítimo, baseando-se nos dados coletados pelo modelo de aprendizado de máquina sobre o que constitui um "comportamento normal" no sistema.

* Autodeleção Condicional: Em casos extremos, o malware poderia se autodeletar para evitar a captura e análise.
  
#### Quando o malware identificava um padrão normal, ele ajustava suas próprias operações para se alinhar com esse padrão. Por exemplo:

*  Se o usuário frequentemente jogava jogos online,  HermesCipher evitaria usar muita CPU ou largura de banda durante esses períodos.
* Se o sistema frequentemente ficava ocioso, o malware aproveitaria esse tempo para realizar atividades mais intensivas, como comunicação com o servidor C2 ou espalhar-se para outros sistemas.

## Técnica de Polimorfismo

* Alteração de Nome de Arquivo: A cada nova infecção, HermesCipher mudava o nome de seu arquivo executável para algo que se assemelhava a programas legítimos, como svchost.exe ou explorer.exe
  

## Exemplo de Codigo de Treinamento 

```python
from sklearn.tree import DecisionTreeClassifier
import pandas as pd

# Carregar os dados de treinamento (metadados de arquivos, tipo, etc.)
# Cada linha representa um arquivo, com a última coluna indicando se é malicioso (1) ou benigno (0)
data = pd.read_csv("file_metadata.csv")

X = data.iloc[:, :-1]  # Características
y = data.iloc[:, -1]  # Rótulos

# Treinar o modelo de Árvore de Decisão
clf = DecisionTreeClassifier()
clf.fit(X, y)

# Salvar o modelo treinado para uso futuro
import joblib
joblib.dump(clf, 'hermes_cipher_model.pkl')
```

## Exemplo de Codigo com poliformismo 
```python
import random
import os
import joblib

# Carregar o modelo de aprendizado de máquina treinado
clf = joblib.load('hermes_cipher_model.pkl')

# Função para criptografar arquivos
def encrypt_file(file_path):
    # [código para criptografar o arquivo]
    pass

# Função para keylogging
def keylogger():
    # [código para registrar as teclas digitadas]
    pass

# Função para espionar via webcam
def spy_cam():
    # [código para capturar vídeo e áudio]
    pass

# Função polimórfica para alterar o código do malware
def polymorphic_code():
    new_code = "[gerar novo código]"
    # [código para auto-modificar e substituir partes do código com 'new_code']
    pass

# Função principal para distribuir o worm
def distribute_worm():
    for root, dirs, files in os.walk("."):
        for name in files:
            file_path = os.path.join(root, name)
            # [Características extraídas do arquivo, como tamanho, data de modificação, etc.]
            features = extract_features(file_path)
            
            # Usar o modelo para prever se o arquivo é valioso
            is_valuable = clf.predict([features])[0]
            
            if is_valuable:
                encrypt_file(file_path)
    
    keylogger()
    spy_cam()

    # tornar o código polimórfico para evitar detecção
    polymorphic_code()
``````

## Formato do Conjunto de Dados

O conjunto de dados é um arquivo CSV com as seguintes colunas:

* tamanho_do_arquivo: Tamanho do arquivo em kilobytes.
* extensao: Extensão do arquivo (e.g., .txt, .pdf, .jpg).
* data_de_criacao: Data de criação do arquivo (formato AAAA-MM-DD).
* numero_de_acessos: Quantas vezes o arquivo foi aberto ou modificado.
* sistema_de_arquivos: Sistema de arquivos onde o arquivo está armazenado (e.g., NTFS, exFAT, HFS+).
* is_valioso: Rótulo indicando se o arquivo é valioso (1) ou não (0).
  
## Exemplo de Linhas no Arquivo CSV
tamanho_do_arquivo,extensao,data_de_criacao,numero_de_acessos,sistema_de_arquivos,is_valioso
1548,.txt,2021-06-15,3,NTFS,0
8923,.pdf,2021-04-01,50,NTFS,1
2387,.jpg,2021-08-19,7,exFAT,0
4820,.docx,2021-05-21,32,NTFS,1
128,.ini,2021-09-02,1,NTFS,0
