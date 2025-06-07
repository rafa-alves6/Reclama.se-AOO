# 1. 🎯 Caso de Uso: Pesquisar Denúncia
- [1. 🎯 Caso de Uso: Reclama.se](#1--caso-de-uso-reclama.se)
	- [1.1. Identificação](#11-identificação)
	- [1.2. Visão Geral](#12-visão-geral)
	- [1.3. Fluxo Principal de Eventos](#13-fluxo-principal-de-eventos)
	- [1.4. Fluxos Alternativos](#14-fluxos-alternativos)
		- [1.4.1. a. Credenciais Inválidas](#141-nenhum-resultado-encontrado)
	- [1.5. Fluxos de Exceção](#15-fluxos-de-exceção)
		- [1.5.2. a. Falha de Conexão com o Servidor](#151-b-falha-de-conexão-com-o-banco-de-dados)
	- [1.6. Pré-condições](#16-pré-condições)
	- [1.7. Pós-condições](#17-pós-condições)
	- [1.8. Regras de Negócio](#18-regras-de-negócio)
	- [1.9. Perfis de Usuário](#19-perfis-de-usuário)
- [2. Diagrama de Atividades](#2-diagrama-de-atividades)


## 1.1. Identificação
- **Nome**: Pesquisar Denúncia  
- **Ator Primário**: Cidadão; Moderador; Entidade (Órgão)
- **Descrição**:Permite pesquisas por denúncias registradas no sistema.
---


## 1.2. Visão Geral

```puml
@startuml

skinparam actorStyle awesome

actor "Usuário" as U
actor "Órgão Responsável" as O
actor "Sistema" as S

U --> (Cadastrar Usuário)
U --> (Autenticar Usuário)
U --> (Registrar Denúncia)
U --> (Assinar Denúncia)
U --> (Pesquisar Denúncia)
U --> (Editar/Excluir Publicação)

S --> (Notificar Atualizações)
S --> (Registrar Denúncia)
S --> (Gerar Relatório)
S --> (Editar/Excluir Publicação)

O --> (Responder Denúncia)

(Registrar Denúncia) .down.> (Gerar Relatório) : gera
(Registrar Denúncia) .down.> (Notificar Atualizações) : notifica

@enduml
```

## 1.3. Fluxo Principal de Eventos
1. O usuário ou moderador acessa a página de pesquisa de denúncias.
2. O sistema apresenta uma caixa de pesquisa e filtros de pesquisa, como:
	- Título da denúncia.
  - Status da denúncia.
  - Data da denúncia
  - Entidade (Órgão)
3. O usuário insere os critérios de pesquisa desejados.
4. O sistema retorna a consulta realizada. 
---

## 1.4. Fluxos Alternativos

### 1.4.1. a.Nenhum Resultado Encontrado
1. O sistema detecta que não há denúncias correspondentes aos critérios de pesquisa.
2. O sistema exibe a mensagem: `"Nenhum resultado encontrado."`

---

## 1.5. Fluxos de Exceção

### 1.5.1. a. Falha na Conexão com a Base de Dados
- Se ocorrer uma falha de conexão:
  - O sistema exibe a mensagem: `"Erro de conexão. Tente novamente mais tarde."`
    
---

## 1.6. Pré-condições
- O sistema deve estar online e acessível.
- O usuário deve estar autenticado.
- O usuário deve ter permissões adequadas para acessar a pesquisa de denúncias.

---

## 1.7. Pós-condições
- O usuário ou moderador visualiza os resultados da pesquisa.
- Caso existam denúncias correspondentes, o usuário pode visualizar os detalhes de cada uma.

---

## 1.8. Regras de Negócio
- A pesquisa deve ser realizada com base nos filtros disponíveis (título, status, data).
- O sistema deve garantir que apenas denúncias positivamente avaliadas e/ou acessíveis ao usuário sejam exibidas.
  
---

## 1.9. Perfis de Usuário
| Perfil             | Descrição                                                                                   | Acesso ao sistema             |
| ------------------ | ------------------------------------------------------------------------------------------- | ----------------------------- |
| **Órgão/Entidade** | Representante de órgão público ou privado responsável pela resolução das denúncias.         | Painel administrativo         |
| **Usuário comum**  | Cidadão comum, podendo registrar suas próprias denúncias, e dar feedback sobre as soluções. | Painel do usuário             |
| **Moderador**      | Usuário com permissões de moderação, incluindo editar ou excluir denúncias.                 | Painel do usuário/funcionário |

---

# 2. Diagrama de Atividades

```plantuml
@startuml

|#lightblue|Usuário|
|Sistema|
|#lightgreen|Entidade|

|Sistema|
start

|Usuário|
:Autenticar via gov.br; <<procedure>>
:Iniciar nova denúncia; <<procedure>>

split
  :Descrever o problema;
split again
  :Anexar arquivos;
  |Sistema|
  while (Arquivos compatíveis?) is (não)
    :Solicitação do reenvio dos arquivos;
    :Adição de novos arquivos; <<input>>
  endwhile (sim)
endsplit

:Confirmar e publicar denúncia;
|Usuário|
:Receber número de protocolo; <<input>>
|Sistema|
:Analisar conteúdo da denúncia; <<procedure>>

(A)
note right
  Início da verificação de conformidade com as diretrizes
end note
detach

(B)
note right
  Pós verificação de conformidade com as diretrizes
end note
:Gerar e enviar relatório; <<output>>

fork
  |Usuário|
  :Receber relatório; <<input>>
  :Enviar feedback;
  |Sistema|
  :Analisar feedback recebido; <<procedure>>
  (A)
  detach

fork again
  |Entidade|
  :Receber relatório gerado; <<input>>
  :Confirmar recebimento do feedback;
  detach
  |Sistema|
  (B)
end fork

|Entidade|
:Emitir resposta à denúncia; <<procedure>>

stop

|Sistema|
(A)
if (Conforme diretrizes?) then (sim)
  :Nenhuma ação necessária;
else (não)
  #red:<color:white>Editar ou excluir
  <color:white>conteúdo denunciado;
  :Notificar usuário sobre ação tomada;
  stop
endif


(B)
detach

@enduml
```
