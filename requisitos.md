# 📃 Requisitos do Sistema


## 🧑‍💼 Regras de Negócio (RN)
- RDN01 - Cada usuário deve possuir um único cpf válido cadastrado
- RDN02 - Todos os usuários devem estar cadastrados e logados para realizar uma denúncia
- RDN03 - Cada denúncia deve conter os dados básicos da denúncia: título, data, descrição (caracterizando o problema reportado e o local do ocorrido), tipo e status, sendo registrada por um usuário (denunciante).
- RDN04 - O sistema deve manter os dados do denunciante totalmente ocultos, sem exibição para o público ou para os órgãos responsáveis, mesmo que a denúncia seja aceita.
- RDN05 - Após a denúncia, o usuário deve receber uma confirmação automática e um número de protocolo.
- RDN06 - Após a denúncia, o sistema deve geara um relatório
- RDN07 - O relatório deve conter os dados básicos da denúncia, os arquivos anexados, o tempo médio para resolução do problema, além de ser atualizado acerca do andamento da denúncia 
- RDN08 - Após a denúncia, o órgão responsável deve ser contactado, recebendo o relatório completo gerado pelo sitema.
- RDN09 - O sistema deve permitir que órgão realize uma resposta pública àquela denúncia
- RDN10 - Caso as publicações realizadas pelo usuário não estejam de acordo com as diretrizes, o serviço de moderção deve ter a permissão de editar ou excluir as publicações.
- RDN11 - O feedback realizado pelo usuário acerca dos serviços prestados pela organização responsável pela resolução do problema relatado na denúncia, só deve ser permitido após o tempo mínimo de 7 dias da publicação da denúncia.

## ✅ Requisitos Funcionais (RF)
- RF01 – O sistema deve permitir o cadastro de um novo usuário.
- RF02 – O sistema deve permitir que o usuário realize a autenticação.
- RF03 – O sistema deve permitir o registro de uma denúncia por parte do usuário.
- RF04 – O sistema deve permitir que o usuário assine/credite uma denúncia previamente registrada.
- RF05 – O sistema deve ser capaz de gerar relatórios relacionados ao problema denunciado.
- RF06 – O sistema deve permitir que o usuário cancele uma denúncia registrada por ele próprio.
- RF07 – O sistema deve permitir que o órgão responsável registre uma resposta à denúncia.
- RF08 – O sistema deve permitir a pesquisa de denúncias já registradas.
- RF09 – O sistema deve notificar o usuário sobre atualizações relacionadas à sua denúncia.
- RF10 – o sistema deve permitir que o usuário reaize um feedback acerca dos serviços prestados pelo órgão responsável após a denúncia. 

## :ballot_box_with_check: Requisitos Não Funcionais (RNF)
- RNF01 - O sistema deve possibililtar o cadastro do usuário por login com o Google e/ou Facebook
- RNF02 - O sistema deve permitir que o usuário realize sua autenticação com o gov.br
- RNF03 - O sistema deve ter baixa latência e permitir até 1000 denúncias simultâneas
- RNF04 - O sistema deve ter criptografia de ponta a ponta dos usuários
- RNF05 - A interface do sistema deve ser simples e acessível, funcionando de forma satisfatória em celulares e computadores
- RNF06 - A interface do sistema deve ser intuitiva
- RNF07 - O sistema deve ter baixa latência e permitir até 1000 denúncias simultâneas
- RNF08 - O sistema deve oferecer suporte a múltiplos idiomas
- RNF09 - As denúncias devem aceitar o anexo de arquivos com formatos variados (.pdf, .png, .jpg, .docx, .mp4 e etc)
- RNF10 - O sistema deve conter configuração de interface para se adequar a acessibilidade
- RNF11 - O sistema deve permitir filtros para as pesquisas, por data, tipo e órgão responsável
