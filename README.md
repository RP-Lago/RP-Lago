```markdown
Código de Exemplo: Uso da API Generative AI do Google no Google Colab

Passo a passo para configurar e utilizar a API

Instalação da Biblioteca
Para começar, é necessário instalar a biblioteca `google-generativeai`:
```python
!pip install google-generativeai
```

### Importação de Módulos
Importe os módulos necessários:
```python
import google.generativeai as genai
from google.colab import userdata
```

### Recuperação da Chave de API
Recupere a chave de API armazenada no Secrets do Google Colab:
```python
secretkey = userdata.get('secretkey')
```

### Configuração da API
Configure a biblioteca com a chave de API recuperada:
```python
genai.configure(api_key=secretkey)
```

### Listagem de Modelos Disponíveis
Liste todos os modelos disponíveis e filtre aqueles que suportam o método de geração de conteúdo:
```python
for m in genai.list_models():
  if 'generateContent' in m.supported_generation_methods:
    print(m.name)
```

### Seleção do Modelo
Selecione o modelo "gemini-1.5-pro-latest":
```python
model = genai.GenerativeModel("gemini-1.5-pro-latest")
```

### Início de um Chat
Inicie uma sessão de chat com um histórico vazio:
```python
chat = model.start_chat(history=[])
```

### Loop de Conversação
Crie um loop que espera pelo input do usuário e envia a mensagem para o modelo, imprimindo a resposta até que o usuário digite "fim":
```python
conversa = input("Esperando texto:")

while conversa != "fim":
  response = chat.send_message(conversa)
  print(response.text)
  conversa = input("Esperando texto:")
```

## Explicação do Código

1. **Instalação da Biblioteca**: A linha `!pip install google-generativeai` instala a biblioteca necessária para usar a API Generative AI do Google.

2. **Importação de Módulos**: As linhas `import google.generativeai as genai` e `from google.colab import userdata` importam os módulos essenciais para o funcionamento do script.

3. **Recuperação da Chave de API**: `secretkey = userdata.get('secretkey')` obtém a chave de API armazenada nos dados do usuário do Google Colab.

4. **Configuração da API**: `genai.configure(api_key=secretkey)` configura a biblioteca `genai` com a chave de API obtida.

5. **Listagem e Filtragem de Modelos**: O loop `for m in genai.list_models():` itera sobre os modelos disponíveis e imprime os nomes dos modelos que suportam o método `generateContent`.

6. **Seleção do Modelo**: `model = genai.GenerativeModel("gemini-1.5-pro-latest")` seleciona o modelo especificado.

7. **Início de uma Sessão de Chat**: `chat = model.start_chat(history=[])` inicia uma nova sessão de chat com um histórico vazio.

8. **Loop de Conversação**: O loop `while conversa != "fim":` continua a coletar entradas do usuário, enviar essas entradas para o modelo e imprimir as respostas até que o usuário digite "fim".
```
