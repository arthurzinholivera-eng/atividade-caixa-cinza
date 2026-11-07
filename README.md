# Introdução

Este repositório foi criado para armazenar os resultados da atividade prática de Testes de Caixa Cinza. O ambiente escolhido para o teste foi a API de autenticação do Supabase, e as requisições foram simuladas utilizando o software Postman Desktop.

Aluno: Arthur Oliveira
RA: 250786

# Objetivo da Atividade

O propósito desta atividade foi aplicar conceitos de testes funcionais em uma API real. O foco principal foi compreender a estrutura de uma requisição HTTP (endpoint, headers e body) e validar como o sistema se comporta diante de dados corretos e incorretos no processo de login.

# Configuração do Supabase

Para a realização dos testes, foi criado um projeto no Supabase. A autenticação por e-mail foi habilitada e a confirmação de e-mail foi desativada para facilitar o fluxo. Um usuário de teste foi cadastrado manualmente no painel. As credenciais de acesso (URL do projeto e chave pública) foram extraídas para configurar o Postman.

*Evidências:* 
![User](https://github.com/arthurzinholivera-eng/atividade-caixa-cinza/blob/main/Caixa-cinza-Arthur%20Oliveira/Prints/User%20Arthur.png?raw=true)

# Configuração do Postman

- **Workspace:** Foi configurado um Workspace exclusivo para a atividade de testes de API.
- **Environment:** Foi criado o ambiente `Env Supabase` contendo as variáveis: `url_api`, `chave_api`, `email_usuario` e `senha_usuario`. O uso dessas variáveis é uma boa prática, pois permite rodar os testes dinamicamente, sem a necessidade de digitar os dados de login manualmente a cada requisição.
- Os arquivos exportados da Collection e do Environment estão disponíveis na pasta `/postman` para consulta.

# Configuração das Requisições

A requisição foi montada utilizando o método HTTP POST no endpoint `/auth/v1/token?grant_type=password`. Os headers utilizados foram `apikey` (para autorizar a chamada) e `Content-Type: application/json`. O Body foi preenchido com um objeto JSON contendo as variáveis de e-mail e senha. O objetivo é receber um token de acesso válido.

*Evidências:*
![Configuração da Requisição](https://github.com/arthurzinholivera-eng/atividade-caixa-cinza/blob/main/Caixa-cinza-Arthur%20Oliveira/Prints/requisito%20-%20arthur.png?raw=true)

# Execução dos Testes

Foram executados os cinco cenários de teste obrigatórios. As validações foram feitas observando o código de status HTTP, as mensagens de erro em JSON e a presença do token no caso de sucesso.

*Tabela de Cenários:*

| Cenário | Entrada Utilizada | Resultado Esperado | Resultado Obtido | Status |
| :--- | :--- | :--- | :--- | :--- |
| Login com dados válidos | E-mail e senha corretos | Status 200 + token | Status 200 + token | OK |
| Tentativa com senha errada | E-mail correto, senha inválida | Erro de autenticação | 400 - invalid_credentials | OK |
| Tentativa com usuário falso | E-mail não cadastrado | Acesso negado | 400 - invalid_credentials | OK |
| Envio de campos em branco | E-mail e senha vazios | Erro de validação | 400 - missing email or phone | OK |
| Formato de e-mail inválido | E-mail sem @, senha curta | Mensagem de erro | 400 - invalid_credentials | OK |

*Evidências:*

**Login com dados válidos:**
![Teste Sucesso](https://github.com/arthurzinholivera-eng/atividade-caixa-cinza/blob/main/Caixa-cinza-Arthur%20Oliveira/Prints/login%20v%C3%A1lido%20-%20arthur.png?raw=true)

![Teste Sucesso](https://github.com/arthurzinholivera-eng/atividade-caixa-cinza/blob/main/Caixa-cinza-Arthur%20Oliveira/Prints/login%20v%C3%A1lido%202%20-%20arthur.png?raw=true)

**Tentativa com senha errada:**
![Teste Senha Errada](https://github.com/arthurzinholivera-eng/atividade-caixa-cinza/blob/main/Caixa-cinza-Arthur%20Oliveira/Prints/Senha%20incorreta%20-%20arthur.png?raw=true)

**Tentativa com usuário falso:**
![Teste Usuário Inexistente](https://github.com/arthurzinholivera-eng/atividade-caixa-cinza/blob/main/Caixa-cinza-Arthur%20Oliveira/Prints/usu%C3%A1rio%20n%C3%A3o%20existente%20-arthur.png?raw=true)

**Envio de campos em branco:**
![Teste Campos Vazios](https://github.com/arthurzinholivera-eng/atividade-caixa-cinza/blob/main/Caixa-cinza-Arthur%20Oliveira/Prints/dados%20vazios%20-%20arthur.png?raw=true)

**Formato de e-mail inválido:**
![Teste Formato Inválido](https://github.com/arthurzinholivera-eng/atividade-caixa-cinza/blob/main/Caixa-cinza-Arthur%20Oliveira/Prints/formato%20inv%C3%A1lido%20-%20arthur.png?raw=true)

# Registro dos Testes

Os resultados dos testes foram documentados numa tabela no Excel. Nela, constam os códigos de cada caso de teste (CT-01 a CT-05), os dados utilizados em cada tentativa, os retornos esperados e obtidos, e as notas do analista. Documentar é muito importante para que a equipe de desenvolvimento saiba como a API se comporta.

*Evidências:*
<img width="1387" height="147" alt="image" src="https://github.com/user-attachments/assets/97843c81-1cb3-4078-b750-8817a85bfc09" />

# Resultados Obtidos

Os cinco casos de teste planejados foram finalizados. A API do Supabase respondeu como o esperado: o JWT foi gerado no caso de sucesso, e os códigos HTTP 400 foram retornados para os casos de falha. Observou-se que a API utiliza uma mensagem genérica (`invalid_credentials`) para erros de senha e usuário falso, o que é uma boa prática de segurança. Para os campos em branco, a API retornou um erro específico de ausência de dados.

# Conclusão

A atividade foi finalizada com sucesso. A autenticação da API funcionou como esperado. A principal dificuldade foi entender como extrair as novas chaves de API do Supabase (as chaves Publishable). Não foram encontradas falhas de segurança nos cenários testados. Uma melhoria possível para o sistema seria a implementação de bloqueio temporário do usuário após múltiplas tentativas de login falhas (rate limit). Os testes de caixa cinza são essenciais para garantir que a autenticação e as regras de negócio estejam seguras.
