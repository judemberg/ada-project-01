# Arquitetura de Autenticação e Autorização para Gestão de Acessos

Empresa: Futuris Tech  
Equipe: Judemberg Donizete Nascimento  
Data: 03/08/2025

---

## 1. Introdução

​	Este projeto apresenta a proposta de implementação da arquitetura de autenticação e autorização da FuturisTech, todo o ecossistema foi construído de forma a garantir os pilares da segurança da informação de forma otimizada e eficiente para os clientes.

​	Os fluxos de autenticação são baseados em OAuth 2.0 e OpenID Connect, garantindo emissão e gerenciamento seguro de tokens JWT. Implementamos mecanismos de multifator (MFA) e single sign-on (SSO) para reforçar a identidade de usuário e reduzir vetores de ataque por credenciais comprometidas.

​	Modelos de controle de acesso baseados em RBAC, alinhados ao princípio do menor privilégio, para segmentar permissões de forma granular em aplicações web e APIs. As APIs com maior criticidade precisarão de ROLES configuradas no Keycloak e vinculadas ao Client ID de modo a garantir que um parceiro ou usuário não tenha acesso a recursos ou endpoints que não deveria. Além de trazer granularidade a gestão de acesso, tal mecanismo facilita no rastreio, auditoria e conformidade.

Adoção de SSL/TLS end-to-end, hashing forte de credenciais (bcrypt/Argon2) e revogação dinâmica de tokens para mitigar riscos de interceptação e replay.

​	Integração com sistemas de auditoria centralizada e SIEM, assegurando rastreabilidade completa dos eventos de segurança e compliance contínuo com LGPD, ISO 27001 e demais normativas aplicáveis.
Com essa solução, a FuturisTech fortalece sua postura de segurança, atende requisitos regulatórios e oferece aos usuários um fluxo de acesso fluido, escalável e resiliente.

### 1.1 Conectividade

​	Os parceiros externos deverão se conectar através de conexão privada via link dedicado ou FABRIC na EQUINIX, esta arquitetura busca maior segurança e confiabilidade provendo isolamento de tráfego, baixa latência e alta disponibilidade, maior controle de acesso por permitir regras específicas para cada parceiro e facilita o cumprimento de requisitos regulatórios como PCI e LGPD.

​	Esta modalidade de conexão evita exposição à internet e quase que praticamente pode eliminar os riscos com ataques de DDoS.

![Topologia de Conectividade](https://github.com/judemberg/ada-project-01/blob/main/Topologia%20conectividade.png)

---

## 2. Desenho da Arquitetura

### 2.1 Diagrama da Solução AWS

![Arquitetura da Solução em nuvem AWS](https://github.com/judemberg/ada-project-01/blob/main/diagrama_aws.png)



---

## 3. Tecnologias e Protocolos

| Componente               | Tecnologia/Protocolo      | Justificativa                       |
|--------------------------|---------------------------|-------------------------------------|
| Servidor de Autenticação | Auth0 / Keycloak / Azure AD | Suporte a OAuth 2.0, MFA      |
| API Gateway              | API Gateway AWS    | Rate limiting, logs, segurança      |
| Tokens                   | JSON Web Tokens - JWT     | Padrão de mercado, seguro           |
| Controle de Acesso       | RBAC               | Flexibilidade e granularidade       |
| Logs                     | CloudWatch    | Auditoria e monitoramento           |

---

## 4. Papéis e Permissões (RBAC/ABAC)

| Papel         | Permissões Principais         | Exemplos de Usuários       |
|---------------|-------------------------------|----------------------------|
| Administrador | Gerenciar usuários, acessar tudo | Equipe de TI              |
| Usuário       | Acessar recursos próprios     | Funcionários Padrão        |
| Visitante     | Acesso restrito               | Terceiros, parceiros       |



---

---

## 5. Gerenciamento de APIs

​	Antes de chegar até o consumo das API's, o cliente passará pelo API GATEWAY que contará com mecanismo de integração nativa com OAuth2, configuração de rate limit por cliente e endpoint.

​	O ecossistema contará com monitoramento de latência e erros, geração de logs e relatórios para auditoria com métricas de (quantidade de solicitações por segundo, quantidade de erros ou sucesso por status code, tokens emitidos e revogados, tentativas de falhas de login)

​	Os picos anômalos de autenticação e acesso às API's emitirão alerta automático e em tempo real.

---

## 📚 6. Documentação e Treinamento

​	A documentação ficará disponível na Wiki desenvolvido e apresentado em Sharepoint com toda topologia e arquitetura , manuais, especificações dos sistemas, normativos e Swaggers com histórico de versionamento das API's. 

​	Visando a colaboração e melhoria contínua, todas as Swaggers ficarão disponíveis em repositórios compartilhados do GitHub onde os clientes terão acesso e poderão fazer  melhorias no código por push. Temos uma equipe especializada de Devs Seniors que farão a análise dos códigos enviados.

​	Contamos com a plataforma em Moodle para treinamento e capacitação com vários vídeos e arquivos PDFs, na página inicial possui um link com um bot que responde as principais dúvidas e caso precise pode solicitar no chat para falar com um de nossos especialistas

## 7. Referências

- https://www.openapis.org/
- https://www.keycloak.org/
- https://docs.aws.amazon.com/pt_br/
- https://datatracker.ietf.org/doc/html/rfc7519 
- https://learn.microsoft.com/pt-br/azure/role-based-access-control/overview
- https://datatracker.ietf.org/doc/html/rfc6749
- https://docs.equinix.com/fabric/

- https://learn.microsoft.com/pt-br/sharepoint/


