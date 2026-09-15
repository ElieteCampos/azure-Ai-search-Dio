# 🔎 Azure AI Search - Indexação e Enriquecimento de Dados com IA

## 📌 Sobre o projeto

Este projeto foi desenvolvido como parte do desafio prático da **Formação Microsoft Azure AI Fundamentals (AI-900)** da DIO.

O objetivo do laboratório foi explorar os recursos do **Azure AI Search**, realizando a ingestão de documentos armazenados no Azure Blob Storage, enriquecendo os dados com recursos de Inteligência Artificial e realizando consultas sobre o índice criado.

Durante o laboratório, foi possível compreender na prática o fluxo entre:

- Azure Blob Storage
- Data Source
- Skillset
- Indexer
- Index
- Search Explorer

---

## 🎯 Objetivos

Neste projeto foram praticados os seguintes conceitos:

- Criação de um serviço Azure AI Search;
- Criação de uma conta de armazenamento;
- Utilização do Azure Blob Storage;
- Upload de documentos para um container;
- Criação automática de uma fonte de dados;
- Enriquecimento de conteúdo utilizando IA;
- Extração de frases-chave;
- Extração de entidades;
- Divisão de documentos em partes;
- Extração de texto de imagens;
- Criação de índice e indexador;
- Realização de consultas no Search Explorer;
- Aplicação de filtros sobre dados enriquecidos.

---

## ☁️ Recursos utilizados no Azure

### Azure AI Search

Foi utilizado um serviço do **Azure AI Search** para indexar e consultar os documentos.

Serviço utilizado:

dioaisearch

##O índice criado pelo assistente foi:
search-1789504439174

##Azure Storage Account

Foi criada uma conta de armazenamento:
diosearchcurso

##Dentro dela foi criado o container:
coffeereviews

Foram adicionados 9 documentos no formato .docx, contendo avaliações de uma cafeteria.

---
## 🗂️ Arquitetura da solução

O fluxo utilizado no projeto pode ser representado da seguinte forma:
Documentos .docx
       │
       ▼
Azure Blob Storage
       │
       ▼
Data Source
       │
       ▼
Skillset
       │
       ├── Extração de frases-chave
       ├── Extração de entidades
       ├── Divisão de texto
       └── Extração de texto de imagens
       │
       ▼
Indexer
       │
       ▼
Index
       │
       ▼
Search Explorer

---

## ⚙️ Configuração da fonte de dados

No assistente de importação do Azure AI Search foi selecionado o cenário:
Keyword search

A fonte utilizada foi:
Azure Blob Storage

Container:
coffeereviews

O modo de análise dos documentos foi mantido como padrão.

---

## 🧠 Enriquecimento dos dados com IA

Na etapa de enriquecimento foram selecionadas as seguintes opções:

Extract phrases

Responsável por identificar frases e termos importantes existentes nos documentos.

Exemplos encontrados durante os testes:
Fourth Coffee
lavender honey latte
apple-chai latte
coffee tastings
seasonal baked goods

Extract entities

Responsável por identificar entidades presentes no conteúdo.

Entre os tipos encontrados estavam:
persons
locations
organizations

Por exemplo, o Azure conseguiu identificar localidades como:
Json
"locations": [
  "Chicago",
  "Illinois"
]

Também foram identificadas organizações como:
Json
"organizations": [
  "Fourth Coffee"
]

Split text

Essa opção permite dividir documentos maiores em partes menores.

No índice criado pelo assistente, essas partes aparecem através de campos como:
chunk
chunk_id
parent_id

Essa estratégia é útil para permitir buscas mais precisas dentro do conteúdo dos documentos.

Extract text from images

Também foi habilitada a extração de texto presente em imagens existentes nos documentos.

Isso permite que informações contidas visualmente nos arquivos possam participar do processo de indexação.

---
## 🔍 Testes no Search Explorer

Após a criação do índice, as consultas foram realizadas através do Search Explorer.

1. Consulta geral

Uma das primeiras consultas utilizadas foi:
search=*&$count=true

Onde:

search=* pesquisa todos os documentos;
$count=true retorna a quantidade de resultados encontrados.

---
## 📍 Busca por localização

Inicialmente foi testada uma pesquisa textual relacionada a Chicago.

Depois, foi utilizada uma consulta estruturada com filtro sobre o campo locations.
search=*&$filter=locations/any(l: l eq 'Chicago')&$count=true

Resultado

A consulta retornou:
json
"@odata.count": 3

Os documentos encontrados foram:
review-4.docx
review-5.docx
review-8.docx

Todos estavam relacionados à localização:
Chicago, Illinois

Um dos resultados apresentou:
json
"locations": [
  "Chicago",
  "Illinois"
]
Isso demonstrou que o enriquecimento por IA conseguiu identificar entidades geográficas e armazená-las no índice para posteriormente serem utilizadas em filtros.

---

## 🧩 Entendendo a consulta

A consulta utilizada foi:
search=*&$filter=locations/any(l: l eq 'Chicago')&$count=true

Ela pode ser entendida da seguinte forma:
search=*
│
└── considera todos os documentos

$filter=
│
└── aplica um filtro aos resultados

locations/any(...)
│
└── verifica os valores existentes dentro da coleção locations

l eq 'Chicago'
│
└── seleciona registros que possuem exatamente Chicago

$count=true
│
└── retorna a quantidade de documentos encontrados

O resultado final foi:

3 documentos encontrados

---
## 💡 Search x Filter

Durante o laboratório também foi possível perceber a diferença entre uma pesquisa textual e um filtro.

Uma busca textual procura termos considerados relevantes dentro dos campos pesquisáveis.

Já um filtro como:

$filter=locations/any(l: l eq 'Chicago')

utiliza o conteúdo estruturado existente no campo locations.

Isso permite realizar consultas muito mais específicas.

---
## 🤖 Semantic Ranker

Durante a criação do índice, o assistente atual do Azure habilitou o:

Semantic Ranker

Esse recurso utiliza processamento semântico para melhorar a relevância e a ordenação dos resultados.

Por isso, algumas respostas retornadas pelo Search Explorer também apresentaram informações como:

@search.score
@search.rerankerScore
@search.captions
@search.answers

---
## 🔄 Diferenças em relação ao laboratório original

A interface atual do Azure apresenta algumas diferenças em relação às versões exibidas nas aulas.

Entre elas:

O assistente atual apresenta primeiro opções como:
Keyword search
RAG
Multimodal RAG
As opções de enriquecimento aparecem de maneira diferente.

Neste projeto foram utilizados:

Extract phrases
Extract entities
Split text
Extract text from images

Além disso, o assistente utilizou um:

Free Foundry Tools resource

para executar os enriquecimentos configurados.

Apesar das diferenças visuais, o conceito principal do laboratório permanece o mesmo:

Fonte de dados
      ↓
Enriquecimento
      ↓
Indexação
      ↓
Pesquisa
📸 Evidências do laboratório

Os prints do laboratório podem ser armazenados em uma pasta:

/images

Exemplo de estrutura do repositório:

azure-ai-search-dio/
│
├── images/
│   ├── storage-container.png
│   ├── import-data.png
│   ├── ai-enrichment.png
│   ├── search-explorer.png
│   └── filtro-chicago.png
│
└── README.md

Um dos principais prints do projeto é a consulta:

search=*&$filter=locations/any(l: l eq 'Chicago')&$count=true

mostrando:

@odata.count: 3

e um dos resultados contendo:

"locations": [
  "Chicago",
  "Illinois"
]

---
## 📚 O que aprendi

Durante este laboratório consegui compreender melhor como o Azure AI Search transforma documentos não estruturados em informações pesquisáveis.

Antes do processo de indexação, os dados estavam armazenados apenas como documentos .docx.

Após o processamento, passaram a existir informações estruturadas como:

keyPhrases
persons
locations
organizations

Isso permite construir mecanismos de pesquisa muito mais inteligentes.

Também pude compreender melhor a função de cada componente:

Data Source

Define de onde os dados serão obtidos.

Neste laboratório:

Azure Blob Storage
Skillset

Define os processos de enriquecimento que serão aplicados aos documentos.

Indexer

Lê os documentos da fonte de dados, executa os enriquecimentos e envia os resultados para o índice.

Index

Estrutura onde os dados processados ficam disponíveis para pesquisa.

Search Explorer

Ferramenta utilizada para testar consultas diretamente sobre o índice.

---

## 🚀 Possibilidades de uso

A mesma arquitetura utilizada neste laboratório pode ser aplicada em diferentes cenários, como:

pesquisa em documentos empresariais;
pesquisa em contratos;
análise de avaliações de clientes;
bases de conhecimento;
catálogos de produtos;
sistemas internos de consulta;
mecanismos de busca corporativos;
soluções de RAG para Inteligência Artificial Generativa.
🛠️ Tecnologias utilizadas
Microsoft Azure
Azure AI Search
Azure Blob Storage
Azure AI Services / Foundry Tools
Search Explorer
Git
GitHub
📖 Referências
Microsoft Learn - Azure AI Search
Microsoft Learn - AI-900 Azure AI Fundamentals
Digital Innovation One (DIO)

---

## 🤝 Apoio durante o desenvolvimento

O ChatGPT foi utilizado como apoio ao processo de aprendizagem, especialmente para compreender as diferenças entre a interface apresentada, no curso e a interface atual do Azure.

A execução, configuração dos recursos, testes, análise dos resultados e construção do projeto foram realizados por mim.

--- 

## 👩‍💻 Autora

Projeto desenvolvido durante a formação Microsoft Azure AI Fundamentals (AI-900) da DIO.







