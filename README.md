# Azure_ml_lab
Laboratório do curso AI900 - Prof. Valeria

# Crie um espaço de trabalho do Azure Machine Learning

Para usar o Azure Machine Learning, você precisa provisionar um espaço de trabalho do Azure Machine Learning em sua assinatura do Azure. Então você poderá usar o Azure Machine Learning Studio para trabalhar com os recursos em seu espaço de trabalho.
Dica: Se você já tem um espaço de trabalho do Azure Machine Learning, pode usá-lo e pular para a próxima tarefa.
Sign into the Azure portal at https://portal.azure.com using your Microsoft credentials.
Selecione + Criar um recurso, pesquise por Aprendizado de Máquina e crie um novo recurso de Aprendizado de Máquina do Azure com as seguintes configurações:
Assinatura: Sua assinatura do Azure.
Grupo de recursos: Crie ou selecione um grupo de recursos.
Nome: Digite um nome exclusivo para o seu espaço de trabalho.
Região: Selecione a região geográfica mais próxima.
Conta de armazenamento: Observe a nova conta de armazenamento padrão que será criada para o seu espaço de trabalho.
Cofres de chaves: Observe o novo cofre de chaves padrão que será criado para o seu espaço de trabalho.
Insights do aplicativo: Observe o novo recurso padrão de insights do aplicativo que será criado para o seu espaço de trabalho.
Registro de contêiner: Nenhum (um será criado automaticamente na primeira vez que você implantar um modelo em um contêiner).
Selecione Revisar + criar e, em seguida, selecione Criar. Aguarde a criação do seu espaço de trabalho (pode levar alguns minutos) e, em seguida, vá para o recurso implantado.
Selecione Launch studio (ou abra uma nova guia do navegador e navegue até https://ml.azure.com e faça login no Azure Machine Learning studio usando sua conta Microsoft). Feche todas as mensagens que são exibidas.
No estúdio Azure Machine Learning, você deve ver seu espaço de trabalho recém-criado. Caso contrário, selecione Todos os espaços de trabalho no menu à esquerda e, em seguida, selecione o espaço de trabalho que você acabou de criar.
# Use o aprendizado de máquina automatizado para treinar um modelo

O aprendizado de máquina automatizado permite que você experimente vários algoritmos e parâmetros para treinar vários modelos e identificar o melhor para seus dados. Neste exercício, você usará um conjunto de dados de detalhes históricos de aluguel de bicicletas para treinar um modelo que prevê o número de aluguéis de bicicletas que devem ser esperados em um determinado dia, com base em características sazonais e meteorológicas.
Citação: Os dados usados neste exercício são derivados do Capital Bikeshare e são usados de acordo com o contrato de licença de dados publicado.
No Azure Machine Learning studio, visualize a página Automated ML (em Authoring).
Crie um novo trabalho de ML automatizado com as seguintes configurações, usando o Próximo conforme necessário para progredir pela interface do usuário:
Configurações básicas:
Nome do trabalho: mslearn-bike-automl
Novo nome do experimento: mslearn-bike-rental
Descrição: Aprendizado de máquina automatizado para previsão de aluguel de bicicletas
Tags: nenhuma
Tipo de tarefa e dados:
Selecione o tipo de tarefa: Regressão
Selecione o conjunto de dados: Crie um novo conjunto de dados com as seguintes configurações:
Tipo de dados:
Nome: aluguel de bicicletas
Descrição: Dados históricos de aluguel de bicicletas
Tipo: Tabular
Fonte de dados:
Selecione de arquivos da web
URL da Web:
URL da Web:https://aka.ms/bike-rentals
Ignorar validação de dados: não selecione
Configurações:
Formato de arquivo: Delimitado
Delimitador: Virgula
Codificação: UTF-8
Cabeçalhos de coluna: Apenas o primeiro arquivo tem cabeçalhos
Ignorar linhas: Nenhuma
O conjunto de dados contém dados de várias linhas: não selecione
Esquema:
Inclua todas as colunas que não sejam Path
Revise os tipos detectados automaticamente
Selecione Criar. Depois que o conjunto de dados for criado, selecione o conjunto de dados de aluguel de bicicletas para continuar enviando o trabalho de ML automatizado.
Configurações da tarefa:
Tipo de tarefa: Regressão
Conjunto de dados: aluguel de bicicletas
Coluna de destino: Aluguéis (inteiro)
Configurações adicionais de configuração:
Métrica primária: Erro ao quadrado médio de raiz normalizado
Explique o melhor modelo: Não selecionado
Use todos os modelos suportados: Não selecionado. Você restringirá o trabalho a tentar apenas alguns algoritmos específicos.
Modelos permitidos: Selecione apenas RandomForest e LightGBM — normalmente você gostaria de tentar o maior número possível, mas cada modelo adicionado aumenta o tempo necessário para executar o trabalho.
Limites: Expanda esta seção
Testes máximos: 3
Ensaios simultâneos máximos: 3
Nós máximos: 3
Limite de pontuação métrica: 0,085 (de modo que, se um modelo atingir uma pontuação métrica de erro quadrático médio de raiz normalizada de 0,085 ou menos, o trabalho termina.)
Tempo limite: 15
Tempo limite de iteração: 15
Ativar rescisão antecipada: Selecionado
Validação e teste:
Tipo de validação: Divisão de validação de trem
Porcentagem de dados de validação: 10
Conjunto de dados de teste: Nenhum
Computação:
Selecione o tipo de computação: Sem Servidor
Tipo de máquina virtual: CPU
Nível de máquina virtual: Dedicado
Tamanho da máquina virtual: Standard_DS3_V2*
Número de instâncias: 1
* Se a sua assinatura restringir os tamanhos de VM disponíveis para você, escolha qualquer tamanho disponível.
Envie o trabalho de treinamento. Começa automaticamente.
Espere o trabalho terminar. Pode demorar um pouco — agora pode ser um bom momento para uma pausa para o café!
# Reveja o melhor modelo

Quando o trabalho de aprendizado de máquina automatizado for concluído, você poderá revisar o melhor modelo que ele treinou.
Na guia Visão geral do trabalho de aprendizado de máquina automatizado, anote o melhor resumo do modelo.Captura de tela do melhor resumo do modelo do trabalho de aprendizado de máquina automatizado com uma caixa ao redor do nome do algoritmo.
Nota Você pode ver uma mensagem sob o status “Aviso: Pontuação de saída especificada pelo usuário alcançada...”. Esta é uma mensagem esperada. Por favor, continue para a próxima etapa.
Selecione o texto em Nome do algoritmo para o melhor modelo para visualizar seus detalhes.
Selecione a guia Métricas e selecione os resíduos e os gráficos predicted_true se eles ainda não estiverem selecionados.
Revise os gráficos que mostram o desempenho do modelo. O gráfico de resíduos mostra os resíduos (as diferenças entre valores previstos e reais) como um histograma. O gráfico predicted_true compara os valores previstos com os valores verdadeiros.
# Implante e teste o modelo

Na guia Modelo para o melhor modelo treinado pelo seu trabalho de aprendizado de máquina automatizado, selecione Implantar e use a opção de serviço da Web para implantar o modelo com as seguintes configurações:
Nome: predict-rentals
Descrição: Preveja aluguéis de bicicletas
Tipo de computação: Instância do Contêiner Azure
Ativar autenticação: Selecionado
Aguarde o início da implantação - isso pode levar alguns segundos. O status de Implantação para o ponto final predict-rentals será indicado na parte principal da página como Executando.
Aguarde que o status de Implantação mude para Bem-sucedido. Isso pode levar de 5 a 10 minutos.
# Teste o serviço implantado
Agora você pode testar seu serviço implantado.
No Azure Machine Learning studio, no menu à esquerda, selecione Endpoints e abra o endpoint predict-rentals em tempo real.
Na página do ponto final em tempo real predict-rentals, visualize a guia Teste.
No painel Dados de entrada para testar o ponto final, substitua o modelo JSON pelos seguintes dados de entrada:
