🧠 Contexto e Objetivos

Este projeto tem como objetivo principal explorar o uso da ferramenta NotebookLM como apoio ao aprendizado técnico, demonstrando na prática como a Inteligência Artificial pode acelerar a aquisição, organização e consolidação de conhecimento.
Para isso, foi construído um caderno temático com foco em estratégias de backup e recuperação de dados em bancos de dados Oracle, utilizando a ferramenta Oracle Recovery Manager (RMAN) como base técnica para estudo.
A proposta consiste em utilizar o NotebookLM para centralizar fontes, gerar insights, estruturar resumos e apoiar a compreensão de conceitos importantes como tipos de backup, RTO e RPO, além de boas práticas para garantir a integridade e disponibilidade dos dados em ambientes corporativos.
Além disso, o projeto busca evidenciar a aplicação de engenharia de prompts e análise crítica das respostas geradas pela IA, destacando tanto os ganhos de produtividade quanto os desafios encontrados durante o processo.



📚 Curadoria de Fontes

YouTube – https://www.youtube.com/watch?v=XEv5oWK1IuA
YouTube – https://www.youtube.com/watch?v=xQLVCyRP6mg
YouTube – https://www.youtube.com/watch?v=7RUNO1d13EQ
CCM Tecnologia – https://blog.ccmtecnologia.com.br/post/como-calcular-rto-e-rpo-e-validar-seu-backup
Oracle Corporation – https://docs.oracle.com/en/database/oracle/oracle-database/21/rcmrf/database-backup-and-recovery-reference.pdf



🤖 Engenharia de Prompts

🔹 Prompts Estratégicos Utilizados
“Explique como funciona o Oracle Recovery Manager (RMAN) com exemplos práticos”
“Quais são os tipos de backup no Oracle e quando utilizar cada um?”
“Explique a diferença entre backup incremental level 0 e level 1 no RMAN”
“Como realizar um processo completo de backup e recovery utilizando RMAN?”
“Explique RTO e RPO com exemplos aplicados a ambientes Oracle”
“Quais são as melhores práticas de backup em bancos Oracle corporativos?”

🔹 Variações de Prompts
“Explique como se eu fosse iniciante em Oracle”
“Explique de forma técnica como um DBA experiente”
“Simule um cenário real de falha e recuperação com RMAN passo a passo”
“Liste comandos reais utilizados em backup e recovery no Oracle”



❤️‍🩹 Cicatrizes (Troubleshooting e Aprendizados)
- As respostas iniciais foram muito genéricas e pouco aplicáveis ao ambiente real
- Foi necessário solicitar exemplos com comandos RMAN para obter maior clareza
- A IA não trouxe cenários reais de falha até que fosse solicitado explicitamente



MINIGUIA DE ESTUDO

Resumo estruturado do assunto:

Abaixo estão resumos estruturados dos principais tópicos abordados nas fontes, organizados para facilitar a compreensão técnica e estratégica sobre backup e recuperação, com ênfase no Oracle e nas regulamentações vigentes.
1. Fundamentos de Backup no Oracle
Existem duas abordagens principais para proteger os dados, com finalidades distintas:
- Backup Físico: É a cópia dos arquivos reais do banco de dados (datafiles, control files e archived redo logs)
É a base fundamental de qualquer estratégia de recuperação de desastres
A ferramenta recomendada é o RMAN (Recovery Manager)
- Backup Lógico: Envolve a exportação de objetos (como tabelas e procedimentos) usando utilitários como o Data Pump (expdp/impdp)
É considerado um método suplementar, útil para migrações ou transporte de dados, mas insuficiente se usado sozinho
- Modos de Operação:
Hot (Online): Realizado com o banco aberto, exigindo que ele esteja em modo ARCHIVELOG
Cold (Offline): Exige o desligamento do banco para garantir consistência em modo NOARCHIVELOG

2. Comandos e Arquitetura do RMAN
O RMAN é um cliente que gerencia as operações e armazena metadados no arquivo de controle do banco de dados (repositório) ou em um catálogo de recuperação externo
Principais Comandos:
- BACKUP: Cria cópias de segurança de arquivos ou conjuntos de backup
- RESTORE: Recupera os arquivos físicos de um backup para o disco
- RECOVER: Aplica logs de refação e backups incrementais para sincronizar os dados até o ponto desejado
- LIST / REPORT: Exibem informações sobre backups existentes e analisam quais arquivos precisam de proteção
Estratégia Incremental:
- Nível 0: Backup base que contém todos os blocos de dados (equivalente a um backup full, mas utilizável em estratégias incrementais)
- Nível 1: Copia apenas os blocos alterados desde o último backup. Pode ser Diferencial (desde o último nível 0 ou 1) ou Cumulativo (desde o último nível 0)

3. Métricas Estratégicas de Continuidade (RPO e RTO)
Esses indicadores definem a eficácia do plano de continuidade de negócios:
- RPO (Recovery Point Objective): Define a quantidade máxima de dados que se aceita perder. Na prática, determina a frequência dos backups (ex: RPO de 4h exige backups incrementais a cada 4h)
- RTO (Recovery Time Objective): Define o tempo máximo de indisponibilidade permitido para restaurar o sistema após uma falha
- MTPD (Maximum Tolerable Period of Disruption): Tempo máximo que uma interrupção pode durar antes que os danos se tornem inaceitáveis para a organização

4. Conformidade Regulatória (Provimento 213/2026 - CNJ)
Para serventias de Registro Civil no Brasil, o Provimento 213/2026 estabelece requisitos rigorosos de segurança proporcionais à arrecadação (Classes 1, 2 e 3)
- Segurança Técnica: Uso obrigatório de criptografia AES-256 para backups externos, autenticação multifator (MFA) para acessos críticos e proteção contra ransomware (mecanismos WORM ou isolamento lógico)
- Requisitos por Classe (Exemplos):
Classe 1 (Essencial): RPO/RTO de 24 horas
Classe 3 (Ampliada): RPO de 4 horas e RTO de 8 horas
- Documentação: Necessidade de manter um Dossiê Técnico atualizado com inventário de ativos, política de segurança e registros de testes de restauração

5. Fluxo de Recuperação (Recovery)
O processo padrão para restaurar um banco de dados após uma falha total segue esta ordem técnica
1-STARTUP NOMOUNT: Inicia a instância sem montar arquivos
2-RESTORE CONTROLFILE: Restaura o arquivo de controle a partir de um backup
3-ALTER DATABASE MOUNT: Permite que o RMAN reconheça a estrutura do banco
4-RESTORE DATABASE: Copia os arquivos de dados do backup para o local de origem
5-RECOVER DATABASE: Aplica as mudanças contidas nos logs e backups incrementais
6-ALTER DATABASE OPEN RESETLOGS: Abre o banco de dados reiniciando a sequência de logs (obrigatório após restauração de control file)


Um glossário com os principais conceitos aprendidos:

1. Conceitos de Banco de Dados (Oracle)
AES-256: Padrão de criptografia simétrica que utiliza chaves de 256 bits. É o nível mínimo de robustez exigido para dados em repouso e backups externos de serventias
Archived Redo Log Files: Arquivos físicos que contêm cópias de logs de refação preenchidos. Eles são essenciais para recuperar transações ocorridas entre o último backup físico e o momento da falha
Backup Físico: Cópia dos arquivos reais que compõem o banco (datafiles, control files e logs). É a fundação fundamental de qualquer estratégia de recuperação de desastres
Backup Lógico: Extração de dados (como tabelas e usuários) usando utilitários como o Data Pump (expdp). É considerado suplementar e não substitui o backup físico
Control File: Arquivo binário que mantém o registro da estrutura física do banco de dados e metadados sobre backups realizados pelo RMAN
Fast Recovery Area (FRA): Local em disco gerenciado pelo Oracle para armazenar arquivos relacionados à recuperação (backups, logs e flashback) de forma automática
Flashback Database: Tecnologia que permite "rebobinar" o banco de dados para um estado anterior sem a necessidade de restaurar backups físicos
Incremental Backup: Tipo de backup físico que salva apenas os blocos de dados alterados desde o último backup. Divide-se em Nível 0 (base completa) e Nível 1 (diferencial ou cumulativo)
Recovery Catalog: Repositório externo (outro banco de dados) que armazena metadados de backup de um ou mais bancos de dados, oferecendo redundância caso o arquivo de controle original seja perdido
RMAN (Recovery Manager): A ferramenta padrão da Oracle para gerenciar todas as operações de backup, restauração e recuperação física

2. Estratégia e Resiliência (RTO/RPO)
BIA (Business Impact Analysis): Processo de análise para identificar funções críticas de negócio e o efeito que uma interrupção pode causar na organização
MTPD (Maximum Tolerable Period of Disruption): O tempo máximo que um serviço pode ficar interrompido antes que os danos se tornem inaceitáveis
PCN (Plano de Continuidade de Negócio): Estratégia estruturada que define como a organização deve responder e manter operações essenciais durante e após um desastre
RPO (Recovery Point Objective): Quantidade máxima de dados que uma empresa aceita perder em tempo (ex: aceitar perder 4 horas de digitação). Determina a frequência dos backups
RTO (Recovery Time Objective): Tempo máximo permitido para que um sistema volte a operar após uma falha (ex: o sistema deve voltar em no máximo 8 horas)

3. Conformidade e Segurança (Provimento 213/2026)
Dossiê Técnico: Conjunto organizado de documentos e evidências que comprovam a implementação das medidas de segurança exigidas pelo Provimento 213
IdRC: Sistema de autenticação segura disponibilizado pelo ON-RCPN para garantir acesso individualizado e multifator
MFA (Autenticação Multifator): Mecanismo que exige dois ou mais fatores de verificação para acesso (ex: senha + código no celular). Obrigatório para acessos administrativos
Provimento 213/2026 (CNJ): Norma que estabelece requisitos mínimos de segurança da informação e gestão tecnológica para serventias extrajudiciais no Brasil
WORM (Write Once, Read Many): Mecanismo de armazenamento imutável que impede a modificação ou exclusão de dados por um tempo definido, protegendo backups contra ransomware

4. Processos de Recuperação
Recover: Processo de aplicar logs de refação e backups incrementais aos arquivos restaurados para levá-los até o ponto desejado no tempo
Restore: Ato físico de recuperar os arquivos de dados (datafiles) de uma mídia de backup para o servidor
SLA (Service Level Agreement): Acordos de nível de serviço que definem expectativas de tempo de resposta e disponibilidade


Prompts Reutilizáveis para Revisão

“Resuma os principais conceitos de backup e recovery no Oracle em tópicos curtos”
“Explique o funcionamento do Oracle Recovery Manager (RMAN) de forma objetiva”
“Explique rapidamente a diferença entre RTO e RPO”
“Simule um cenário de falha de banco Oracle e descreva o passo a passo do recovery usando RMAN”
“Crie um checklist de backup e recovery para um ambiente de produção”
“Crie 5 perguntas de múltipla escolha sobre RMAN com gabarito”
“Explique os erros mais comuns em estratégias de backup Oracle”
