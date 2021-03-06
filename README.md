# Metodologia da Pesquisa Cientifica
Repositório destinado para aulas de Metodologia e pesquisa científica - Prof GIULIANO ARAUJO BERTOTI, 2º semestre de 2020

Aluno: Rodrigo Querino Ferreira da Costa - RA: 1460481821081

Tema: Sistema de validação de arquivos digitais SPED


# Qual o problema que pretendo resolver?

Tempo elevado na validação dos arquivos digitais da SPED fiscal, referente a empresa "Arcos Dourados"

# Por que este "problema" é de fato um problema?

A De Biasi foi contratada pela Arcos Dourados para realizar o calculo da restituição da Escrituração Fiscal da Contribuição para o PIS/Pasep e da Cofins - EFD-Contribuições dos exercícios de 2016 a 2020, são cerca de 60 arquivos para analise refente a cada mês do execício, no entanto, o maior dos problemas é o sistema de validação fiscal SPED, que demonstra ser ineficiente, assim tornado a vida dos colaboradores da De Biasi demasiado exaustivo. 

Durante a validação do arquivos digitais, o sistema SPED fiscal ira verificar se o arquivo estão em conformidade com os parâmetros da Escrituração Fiscal Digital, impostas pela Instituição Normativa RFB nº 1252, de março de 2012 e o Ato Declaratório Executivo Cofis nº 020 de 14 de março de 2012. 

No caso da Arcos Dourados, cada arquivo é referente a todas as notas ficais geradas por toda rede McDonald’s do Brasil em um único mês, levando cerca de 10 horas para cada arquivo ser validado, 600 horas de analise interruptas de todos os arquivos, caso esteja em conformidade com os parâmetros estabelecidos da EFD, caso contrario será relatado o erro somente no final da validação pelo sistema SPED, somente após as 10 horas de analise, e assim não poderá ser encaminhada para Receita Federal, isso não é conveniente, pois o prazo após receber todos os arquivos digitais será bem curto para tolerar erros de validações.   

# Qual a proposta para solucionar o problema?

Atualmente está em desenvolvimento na De Biasi um sistema de validação denominado SADI “Sistema de Auditoria Digital Integrado”, com o intuito de validar os arquivos antes de serem encaminhados ao SPED fiscal, dessa forma agilizando a análise e evitando o retrabalho pelo sistema SPED, que é o principal problema, dando ao analista fiscal mais autonomia ao verificar os parâmetros dos arquivos.
Primeiro precisamos identificar os parâmetros do arquivo digital para sua validação, podemos extrair algumas informações do guia prático EDF – Contribuições, que atualmente encontra-se na versão 1.33, que determina um padrão de validação por blocos, listamos alguns abaixo:

|BLOCO|DESCRIÇÃO|
|-----|----------|
| 0	| Abertura de identificação e referencias |
| A	| Documentos fiscais - Serviços (ISS) |
| C	| Documentos fiscais I – Mercadorias (ICMS/IPI) |
| D	| Documentos fiscais II – Serviços (ICMS) |
| F	| Demais Documentos e Operações |
| I	| Operações das Instituições Financeiras e Assemelhadas, Seguradoras, Entidades de Previdência Privada e Operadoras de Planos de Assistência a Saúde |
| M	| Apuração da Contribuição e Crédito de PIS/PASEP e da COFINS |
| P	| Apuração da Contribuição Previdenciária sobre Receita Bruta |
| 1	| Complemento da Escrituração – Controle de Saldo de Créditos e de Retenções, Operações Extemporâneas e Outras Informações |
| 9	| Controle e Encerramento do Arquivo Digital |

##### Organização dos blocos:
Todos os blocos deverão ser organizados e dispostos na sequência estabelecida, iniciando-se com o bloco 0 (zero) e seus registros, na sequência o bloco A e seus registros correspondentes, depois os blocos C, D, F, I, M, P e 1 e, no final, o bloco 9, que encerra o arquivo digital, obrigatório conter todos os blocos no arquivo com seus registros.

Algumas das características do arquivo: 
* Formato do arquivo em texto codificado em ASCII – ISSO 8859-1 (latin-1), não sendo aceitos campos compactados (packed decimal), zonados, binários, ponto flutuante (float point);
* O arquivo devera respeitar a hierarquia dos blocos;
*	Os registros deveram sempre ser iniciados na primeira coluna (posição 1), podendo ter tamanho variado; 
*	Não poderá haver linhas em branco

No sistema SADI haverá um script Python que fara a validação de cada bloco, verificando os arquivos individualmente, bloco a bloco, a procura de inconsistências no padrão estabelecido gerando um relatório da situação, apontando para cada falha no arquivo em tempo real.

###### Referências
[SPED Fiscal](http://sped.rfb.gov.br/)  
[Guia EFD-Contribuições](http://sped.rfb.gov.br/arquivo/download/4262)
