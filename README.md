# DESAFIO-QA-BEEDOO-2026

## Introdução

Este documento apresenta os resultados dos testes realizados no microssistema web composto pelas telas `LISTAR CURSOS` e `CADASTRAR CURSO`, com o objetivo de identificar falhas funcionais, inconsistências de interface e oportunidades de melhoria.

Durante os testes também foram observados aspectos de usabilidade, validação de dados, persistência das informações e o comportamento do sistema em situações como acesso direto à rota ou recarregamento da página.

**Sistema testado:**  
https://creative-sherbet-a51eac.netlify.app/

---

## Visão geral da aplicação

A aplicação permite **cadastrar, visualizar e excluir cursos**.

O cadastro é realizado por meio de um formulário contendo as seguintes informações:

- Nome do curso  
- Descrição  
- Instrutor  
- URL da imagem de capa  
- Datas de início e fim  
- Número de vagas  
- Tipo de curso (Online ou Presencial)

Dependendo do tipo selecionado, o sistema apresenta um campo adicional:

- **Online:** link de inscrição  
- **Presencial:** endereço  

Após o cadastro, os cursos são exibidos na página de **listagem**, organizados em cards contendo parte das informações registradas. 
Cada card também possui a opção de **excluir o curso**.

---

## Fluxos do sistema

Durante a exploração da aplicação, foram identificados os seguintes fluxos principais:

- Navegação para a tela de listagem de cursos  
- Acesso à tela de cadastro de cursos  
- Cadastro de cursos online ou presenciais  
- Exibição dos cursos cadastrados na listagem  
- Exclusão de cursos na listagem  

---

## Pontos críticos para teste

Os principais pontos considerados críticos foram:

- Validação dos campos obrigatórios do formulário  
- Regras condicionais do tipo de curso (online ou presencial)  
- Validação das datas de início e fim  
- Validação do número de vagas  
- Persistência e exibição correta dos cursos cadastrados  
- Exclusão de cursos na listagem  
- Comportamento do sistema ao recarregar a página ou acessar rotas diretamente  

---

## Estratégia de testes

Os testes foram conduzidos utilizando **abordagem exploratória**, considerando cenários positivos e negativos.

Foram avaliados:

- Funcionamento do fluxo principal de cadastro de cursos  
- Exibição correta dos cursos na listagem  
- Validação dos campos do formulário  
- Regras condicionais relacionadas ao tipo de curso  
- Comportamentos inesperados da aplicação  

---

## Casos de teste

Os casos de teste foram elaborados com base nos fluxos identificados na aplicação, contemplando:

- Fluxo principal de cadastro de curso  
- Validação de campos obrigatórios  
- Cenários negativos  
- Regras de negócio  
- Comportamentos inesperados  
- Validações de interface e responsividade  

📄 **Planilha de Casos de Teste:** [Casos de Testes & Bugs](https://docs.google.com/spreadsheets/d/1FOh39QTZ9Sj4PHtwNINHAuFtWVm--hHP/edit?gid=1754773697#gid=1754773697)

---

## Execução dos testes

Os cenários definidos foram executados diretamente na aplicação.

Durante a execução foram registrados:

- Status de execução dos testes (**Passou / Falhou**)  
- Evidências da execução (prints ou gravações de tela)

As evidências foram armazenadas em uma pasta compartilhada no Google Drive e vinculadas na planilha de registro de bugs.

---

## Bugs identificados

Durante a execução dos testes foram identificados **13 bugs**, relacionados principalmente a:

- Ausência de validações de campos obrigatórios  
- Falta de validação de regras de negócio  
- Problemas de interface e responsividade  
- Falhas de comportamento da aplicação em cenários específicos  

Cada bug foi documentado contendo:

- **Título do bug**
- **Passos para reproduzir**
- **Resultado atual**
- **Resultado esperado**
- **Severidade / impacto**
- **Evidência da execução**

Os bugs identificados incluem, por exemplo:

- Cadastro de cursos em duplicidade  
- Cadastro com campos obrigatórios vazios  
- Aceitação de datas inconsistentes  
- Aceitação de número de vagas inválido  
- Aceitação de URLs de imagem inválidas  
- Problemas de layout na listagem de cursos  
- Falha de responsividade em dispositivos móveis  
- Erro **404 ao acessar diretamente a rota `/new-course`**

Todos os bugs estão registrados na planilha de testes junto com suas respectivas evidências.

---

## Considerações finais

A aplicação apresenta um fluxo simples e claro para cadastro e listagem de cursos. No entanto, foram identificadas oportunidades de melhoria, principalmente relacionadas à **validação de dados, consistência da interface e tratamento de cenários inesperados**.

A implementação dessas validações e ajustes pode contribuir para maior **robustez, confiabilidade e melhor experiência para o usuário**.

Durante a análise também foi observado que os elementos da interface possuem atributos `id`, o que é positivo para automação de testes. Entretanto, os identificadores aparentam ser gerados dinamicamente e não possuem significado semântico claro, por exemplo:

- `#f_0bca6e20-10a1-4ce6-a34f-d52ddb997942`
- `#f_004ce0c3-5b82-43e6-ba8a-570261b5d135`
- `#f_1e21b8fa-88ca-40b4-9c85-c7d85bbe37a3`

Além disso, alguns elementos precisam ser acessados por **seletores baseados na estrutura do DOM ou em classes genéricas**, como:

```javascript
cy.get('.q-select > .q-field__inner > .q-field__control > .q-field__control-container')
cy.get('.q-pa-md > .q-btn > .q-btn__content')
cy.get('.q-card__actions.justify-center > .q-btn > .q-btn__content > .block')

```

Esse tipo de seletor tende a ser mais frágil, pois pode quebrar facilmente caso haja mudanças na estrutura da interface.

Como melhoria, seria recomendável utilizar identificadores mais descritivos e estáveis, preferencialmente com atributos voltados para testes, como data-testid. 
Essa prática facilita a criação de testes automatizados mais claros, reduz o acoplamento com o layout da página e melhora a manutenção dos testes ao longo do tempo.
