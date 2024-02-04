# Azure_ml_lab
## Laboratório do curso AI900 - Prof. Valeria

[![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Azure Machine Learning](https://img.shields.io/badge/Azure%20Machine%20Learning-003366?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/en-us/services/machine-learning/)
[![JSON](https://img.shields.io/badge/JSON-4930a0?style=for-the-badge&logo=json&logoColor=white)](https://www.json.org/)


# Crie um espaço de trabalho do Azure Machine Learning

Na estrutura do Azure você precisa reservar um espaço de trabalho antes de iniciar um experimento, se você já tem um espaço de trabalho do Azure Machine Learning, pode usá-lo.

Acesse sua conta em https://portal.azure.com .

Selecione + Criar um recurso, pesquise por Aprendizado de Máquina e crie um novo recurso de Aprendizado de Máquina do Azure, em seguida, vá para o recurso implantado.

Selecione Launch studio no estúdio Azure Machine Learning, você deve ver seu espaço de trabalho recém-criado.

# Use o aprendizado de máquina automatizado para treinar um modelo

O aprendizado de máquina automatizado permite que você experimente vários algoritmos e parâmetros para treinar vários modelos e identificar o melhor para seus dados. Neste exercício, usamos um conjunto de dados de detalhes históricos de aluguel de bicicletas para treinar um modelo que prevê o número de aluguéis de bicicletas que devem ser esperados em um determinado dia, com base em características sazonais e meteorológicas. **(:https://aka.ms/bike-rentals)*


Em Authoring, crie um novo trabalho de ML automatizado com as configurações desejadas, usando o Próximo conforme necessário para progredir pela interface do usuário.

**Configurações Iniciais**
- **Nome do trabalho**: mslearn-bike-automl 
- **Novo nome do experimento**: mslearn-bike-rental 
- **Descrição:** Aprendizado de máquina automatizado para previsão de aluguel de bicicletas
- **Tags:** nenhuma

**Tipo de tarefa e dados:**
- Selecione o tipo de tarefa: Regressão
- Selecione o conjunto de dados: Crie um novo conjunto de dados com as seguintes configurações:

**Tipo de dados:**
- Nome: aluguel de bicicletas
- Descrição: Dados históricos de aluguel de bicicletas
- Tipo: Tabular

**Fonte de dados:**
- Selecione de arquivos da web
  - URL da Web: [https://aka.ms/bike-rentals](https://aka.ms/bike-rentals)
- Ignorar validação de dados: não selecione

**Configurações:**
- Formato de arquivo: Delimitado
- Delimitador: Vírgula
- Codificação: UTF-8
- Cabeçalhos de coluna: Apenas o primeiro arquivo tem cabeçalhos
- Ignorar linhas: Nenhuma
- O conjunto de dados contém dados de várias linhas: não selecione

**Esquema:**
- Inclua todas as colunas que não sejam Path

Revise os tipos detectados automaticamente e selecione Criar. Então selecione o conjunto de dados de aluguel de bicicletas para continuar enviando o trabalho de ML automatizado.
**Configurações da tarefa**
- Tipo de tarefa: Regressão
- Conjunto de dados: aluguel de bicicletas
- Coluna de destino: Aluguéis (inteiro)
- Configurações adicionais de configuração:
- Métrica primária: Erro ao quadrado médio de raiz normalizado
- Explique o melhor modelo: Não selecionado
- Use todos os modelos suportados: Não selecionado. Você restringirá o trabalho a tentar apenas alguns algoritmos específicos.
- Modelos permitidos: Selecione apenas RandomForest e LightGBM — normalmente você gostaria de tentar o maior número possível, mas cada modelo adicionado aumenta o tempo necessário para executar o trabalho.
- Limites: Expanda esta seção
- Testes máximos: 3
- Ensaios simultâneos máximos: 3
- Nós máximos: 3
- Limite de pontuação métrica: 0,085 (de modo que, se um modelo atingir uma pontuação métrica de erro quadrático médio de raiz normalizada de 0,085 ou menos, o trabalho termina.)
- Tempo limite: 15
- Tempo limite de iteração: 15
- Ativar rescisão antecipada: Selecionado
  
**Validação e teste:**

- Tipo de validação: Divisão de validação de trem
- Porcentagem de dados de validação: 10
- Conjunto de dados de teste: Nenhum

**Computação:**

- Selecione o tipo de computação: Sem Servidor
- Tipo de máquina virtual: CPU
- Nível de máquina virtual: Dedicado
- Tamanho da máquina virtual: Standard_DS3_V2*
- Número de instâncias: 1
  
**Se a sua assinatura restringir os tamanhos de VM disponíveis para você, escolha qualquer tamanho disponível.*
  
# Reveja o melhor modelo

Quando o trabalho de aprendizado de máquina automatizado for concluído, você poderá revisar o melhor modelo que ele treinou.
Na guia Visão geral do trabalho de aprendizado de máquina automatizado, anote o melhor resumo do modelo.Captura de tela do melhor resumo do modelo do trabalho de aprendizado de máquina automatizado com uma caixa ao redor do nome do algoritmo.

### Nota:
Você pode ver uma mensagem sob o status “Aviso: Pontuação de saída especificada pelo usuário alcançada...”. Esta é uma mensagem esperada. 

# Implante e teste o modelo

Na guia *Modelo*, para o melhor modelo treinado, selecione Implantar e use a opção de serviço da Web para implantar o modelo com as seguintes configurações:

- Nome: predict-rentals
- Descrição: Preveja aluguéis de bicicletas
- Tipo de computação: Instância do Contêiner Azure
- Ativar autenticação: Selecionado

Aguarde o início da implantação - isso pode levar alguns segundos. 
- O status de Implantação para o ponto final predict-rentals será indicado na parte principal da página como Executando.
- Aguarde que o status de Implantação mude para Bem-sucedido. Isso pode levar de 5 a 10 minutos.
  
# Teste o serviço implantado

Agora você pode testar seu serviço implantado.
No Azure Machine Learning studio, no menu à esquerda, selecione Endpoints e abra o endpoint predict-rentals em tempo real.
Na página do ponto final em tempo real predict-rentals, visualize a guia Teste.
No painel Dados de entrada para testar o ponto final, substitua o modelo JSON pelos dados adequados ao seu teste

### * Os dados usados neste exercício são derivados do Capital Bikeshare e são usados de acordo com o contrato de licença de dados publicado.
