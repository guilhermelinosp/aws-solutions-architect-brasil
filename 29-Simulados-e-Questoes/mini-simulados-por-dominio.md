# Mini-Simulados por Domínio — SAA-C03

> Use estes blocos quando um simulado completo mostrar lacuna em um domínio específico. Cada mini-simulado tem 20 questões e deve ser feito em até 40 minutos.

---

## Mini-Simulado 1 — Segurança

**1.** Uma aplicação em EC2 precisa acessar objetos em S3 sem credenciais fixas. Qual opção é mais segura?  
A) Access key no código  
B) IAM Role associada ao instance profile  
C) Usuário IAM compartilhado  
D) Arquivo credentials no servidor  
**Resposta: B.** Role entrega credenciais temporárias. A, C e D mantêm credenciais long-lived e aumentam risco de vazamento.

**2.** Um bucket S3 privado deve ser servido por CloudFront sem acesso direto ao bucket. O que usar?  
A) Bucket público com CORS  
B) Origin Access Control  
C) NAT Gateway  
D) Security Group no S3  
**Resposta: B.** OAC permite acesso do CloudFront ao S3 privado. A expõe o bucket; C não resolve origem; D não existe para S3.

**3.** A empresa quer impedir qualquer conta-membro de usar regiões não aprovadas. O que aplicar?  
A) SCP com condição de região  
B) IAM policy em cada usuário  
C) AWS Config apenas  
D) Security Hub  
**Resposta: A.** SCP define limite máximo em Organizations. B é frágil em escala; C/D detectam ou consolidam, mas não bloqueiam por si só.

**4.** Qual serviço identifica dados sensíveis, como PII, em buckets S3?  
A) GuardDuty  
B) Macie  
C) Inspector  
D) Shield  
**Resposta: B.** Macie descobre dados sensíveis no S3. GuardDuty detecta ameaças, Inspector vulnerabilidades, Shield DDoS.

**5.** Uma API pública sofre tentativas de SQL injection. Qual serviço é mais adequado?  
A) AWS WAF com regras gerenciadas  
B) NACL  
C) KMS  
D) CloudTrail  
**Resposta: A.** WAF atua em camada 7. NACL é rede, KMS criptografa, CloudTrail audita.

**6.** Uma empresa precisa rotação automática de senha do RDS. Qual serviço usar?  
A) Parameter Store Standard sem automação  
B) Secrets Manager com Lambda de rotação  
C) KMS key rotation  
D) S3 Object Lock  
**Resposta: B.** Secrets Manager tem integração de rotação. KMS rotaciona chave, não senha; A não faz rotação nativa; D é retenção WORM.

**7.** (Selecione duas) Para reduzir exposição de uma instância EC2 administrativa, quais opções ajudam?  
A) SSM Session Manager  
B) Remover inbound SSH público  
C) Colocar access key no userdata  
D) Abrir porta 22 para 0.0.0.0/0  
**Resposta: A e B.** Session Manager evita bastion/SSH público e remover inbound reduz superfície. C/D pioram segurança.

**8.** EKS pods precisam acessar DynamoDB com permissões específicas. Qual padrão usar?  
A) IRSA  
B) Access key no ConfigMap  
C) Role única no nó com admin  
D) Bucket policy  
**Resposta: A.** IRSA associa IAM Role a service account. B/C ampliam risco; D é irrelevante.

**9.** Para auditar chamadas de API de gerenciamento na conta AWS, use:  
A) CloudTrail management events  
B) VPC Flow Logs apenas  
C) CloudWatch metrics apenas  
D) AWS Backup  
**Resposta: A.** CloudTrail registra chamadas de API. Flow Logs mostram tráfego de rede, não API.

**10.** Um volume EBS existente não criptografado precisa virar criptografado. Qual fluxo é adequado?  
A) Habilitar criptografia diretamente no volume em uso  
B) Snapshot, copiar snapshot criptografado e restaurar volume  
C) Aplicar Security Group  
D) Usar Macie  
**Resposta: B.** EBS existente exige cópia criptografada via snapshot. As outras opções não criptografam o volume.

**11.** Um bucket deve negar acesso via HTTP não criptografado. Qual condição usar em bucket policy?  
A) Deny quando `aws:SecureTransport` for `false`  
B) Allow para `Principal:*`  
C) Deny por `s3:prefix` vazio  
D) ACL pública  
**Resposta: A.** Essa condição força HTTPS. B/D expõem; C não trata transporte.

**12.** Qual serviço detecta comportamento suspeito como chamadas anômalas e mineração de criptomoeda?  
A) GuardDuty  
B) Macie  
C) Athena  
D) Cost Explorer  
**Resposta: A.** GuardDuty detecta ameaças por logs e sinais. Macie é dados sensíveis; Athena consulta; Cost Explorer custo.

**13.** Para proteger uma aplicação contra DDoS L3/L4 sem configuração adicional, a AWS oferece:  
A) Shield Standard  
B) Inspector  
C) Systems Manager  
D) Glue  
**Resposta: A.** Shield Standard é automático. Shield Advanced adiciona recursos pagos e suporte especializado.

**14.** Uma chave KMS deve ser administrada pelo cliente, com política própria e rotação configurável. Qual tipo usar?  
A) AWS owned key  
B) Customer managed key  
C) Chave SSH EC2  
D) ACM public certificate  
**Resposta: B.** Customer managed key permite controle de policy e rotação. AWS owned é gerenciada pela AWS e invisível ao cliente.

**15.** (Selecione duas) Para acesso cross-account a um bucket S3, quais controles são comuns?  
A) Bucket policy concedendo acesso à conta externa  
B) IAM role/trust policy para AssumeRole  
C) Colocar bucket público  
D) Criar EIP no bucket  
**Resposta: A e B.** Bucket policy e AssumeRole são padrões cross-account. C expõe dados; D não se aplica.

**16.** Uma empresa precisa avaliar conformidade contínua de recursos, como buckets públicos e volumes não criptografados. Qual serviço usar?  
A) AWS Config  
B) Route 53  
C) DAX  
D) Snowball  
**Resposta: A.** Config avalia compliance de configuração. Os demais não fazem avaliação contínua.

**17.** Para autenticação de usuários finais em aplicação web/mobile com login social, qual serviço é candidato natural?  
A) Amazon Cognito  
B) IAM Users  
C) AWS Organizations  
D) STS apenas  
**Resposta: A.** Cognito gerencia identidade de usuários finais. IAM é para identidades AWS/workloads.

**18.** O que limita permissões máximas que um usuário ou role pode receber, sem conceder permissões sozinho?  
A) Permission boundary  
B) Inline policy com Allow  
C) Access Analyzer  
D) WAF rule  
**Resposta: A.** Boundary é teto de permissão. Não concede por si só.

**19.** Qual ferramenta ajuda a identificar recursos compartilhados publicamente ou cross-account de forma não pretendida?  
A) IAM Access Analyzer  
B) CloudFront  
C) Kinesis  
D) EFS Lifecycle  
**Resposta: A.** Access Analyzer avalia políticas de recursos e acessos externos.

**20.** Para armazenar parâmetros não sensíveis e alguns segredos simples com hierarquia, use:  
A) SSM Parameter Store  
B) CloudTrail  
C) Route 53 Resolver  
D) ECR  
**Resposta: A.** Parameter Store atende parâmetros e segredos simples. Secrets Manager é melhor quando rotação de segredo é requisito.

### Pontuação e diagnóstico — Segurança

| Acertos | Diagnóstico | Prioridade de revisão |
|---:|---|---|
| 0-11 | Lacuna crítica em controles básicos | IAM, S3 privado, KMS, WAF, CloudTrail |
| 12-15 | Base razoável, mas com confusões de serviço | GuardDuty/Macie/Inspector/Config e cross-account |
| 16-18 | Bom domínio | Revisar pegadinhas de SCP, OAC, IRSA e boundaries |
| 19-20 | Pronto no domínio | Manter revisão espaçada no caderno de erros |

---

## Mini-Simulado 2 — Resiliência

**1.** Banco relacional precisa failover automático entre AZs.  
A) RDS Multi-AZ  
B) Read Replica apenas  
C) S3 Standard  
D) EC2 Spot  
**Resposta: A.** Multi-AZ oferece standby e failover. Read Replica escala leitura, não substitui HA síncrona.

**2.** Aplicação web deve tolerar falha de instância EC2.  
A) Instância única  
B) ALB + Auto Scaling Group multi-AZ  
C) EIP manual  
D) Snapshot semanal apenas  
**Resposta: B.** ELB e ASG multi-AZ removem ponto único. Backup não é HA.

**3.** (Selecione duas) Para reduzir acoplamento entre produtor e consumidor assíncrono:  
A) SQS  
B) EventBridge  
C) SSH direto entre serviços  
D) Banco compartilhado como fila  
**Resposta: A e B.** SQS/EventBridge desacoplam. C/D aumentam acoplamento e fragilidade.

**4.** Objetos S3 críticos devem ser replicados para outra região automaticamente.  
A) CRR com versioning  
B) Transfer Acceleration  
C) Multipart Upload  
D) Lifecycle para IA  
**Resposta: A.** CRR replica entre regiões e requer versioning.

**5.** DR com menor custo e RTO/RPO mais altos costuma ser:  
A) Backup and Restore  
B) Active-active  
C) Warm standby  
D) Multi-site full capacity  
**Resposta: A.** Backup/restore custa menos, mas recupera mais devagar.

**6.** RTO baixo com ambiente reduzido sempre ligado em outra região caracteriza:  
A) Warm standby  
B) Backup and Restore  
C) Arquivamento Glacier  
D) Single-AZ  
**Resposta: A.** Warm standby mantém capacidade mínima pronta.

**7.** Para failover DNS entre regiões, use:  
A) Route 53 failover routing + health checks  
B) IAM Identity Center  
C) EBS snapshot  
D) NAT Gateway  
**Resposta: A.** Route 53 monitora saúde e altera resolução DNS.

**8.** SQS consumer falha durante processamento. O que evita perda imediata da mensagem?  
A) Visibility timeout  
B) CORS  
C) KMS rotation  
D) ALB stickiness  
**Resposta: A.** A mensagem fica invisível temporariamente e reaparece se não for deletada.

**9.** Mensagens com falhas repetidas devem ir para:  
A) Dead-letter queue  
B) Bucket público  
C) Security Group  
D) Placement group  
**Resposta: A.** DLQ isola mensagens problemáticas para análise.

**10.** Uma aplicação precisa proteger dados contra exclusão acidental no S3.  
A) Versioning e, se aplicável, Object Lock  
B) NAT Gateway  
C) WAF  
D) DAX  
**Resposta: A.** Versioning ajuda recuperação; Object Lock atende retenção forte.

**11.** (Selecione duas) Para HA de aplicação stateless em EC2:  
A) Múltiplas AZs  
B) Auto Scaling Group  
C) Sessão fixa obrigatória em disco local  
D) Banco Single-AZ sem backup  
**Resposta: A e B.** Multi-AZ e ASG são base. C/D criam estado e ponto único.

**12.** Para replicação global com RPO baixo em banco Aurora, considere:  
A) Aurora Global Database  
B) EBS gp3  
C) S3 One Zone-IA  
D) CloudTrail Lake  
**Resposta: A.** Aurora Global Database replica para região secundária com baixa latência.

**13.** Uma fila precisa preservar ordem estrita por grupo de pedidos.  
A) SQS FIFO  
B) SQS Standard  
C) SNS Standard apenas  
D) Kinesis Firehose  
**Resposta: A.** FIFO preserva ordem por message group e deduplica.

**14.** Para orquestrar etapas com retry, fallback e compensação, use:  
A) Step Functions  
B) EIP  
C) NACL  
D) ACM  
**Resposta: A.** Step Functions modela workflow resiliente com retries/catches.

**15.** RDS Read Replica cross-region ajuda principalmente em:  
A) DR e leitura regional, com replicação assíncrona  
B) Failover síncrono automático de escrita  
C) Criptografia em trânsito  
D) Cache HTTP  
**Resposta: A.** Replica assíncrona pode apoiar DR/leitura, mas não é Multi-AZ síncrono.

**16.** Um ALB só deve enviar tráfego para instâncias saudáveis.  
A) Health checks do target group  
B) Bucket policy  
C) IAM Access Analyzer  
D) S3 Select  
**Resposta: A.** Health checks removem targets não saudáveis do balanceamento.

**17.** Para backup centralizado e políticas por conta/região, use:  
A) AWS Backup  
B) Macie  
C) DMS CDC  
D) Global Accelerator  
**Resposta: A.** AWS Backup centraliza políticas e vaults.

**18.** Para reduzir impacto de falha de AZ em subnets, distribua recursos em:  
A) Pelo menos duas AZs  
B) Uma AZ com instância maior  
C) Uma subnet pública apenas  
D) Um volume EBS maior  
**Resposta: A.** Resiliência regional exige distribuição entre AZs.

**19.** Se uma EC2 precisa manter instance ID e IP privado após falha de hardware, use:  
A) EC2 Auto Recovery  
B) ASG substituindo instância  
C) Spot Fleet  
D) CloudFront  
**Resposta: A.** Auto Recovery recupera em novo hardware mantendo identidade quando compatível.

**20.** Para fanout de um evento a vários consumidores, use:  
A) SNS com múltiplas assinaturas  
B) SQS única com vários consumers competindo  
C) EBS Multi-Attach para todos  
D) NAT Gateway  
**Resposta: A.** SNS distribui para múltiplos destinos; SQS única divide mensagens entre consumidores.

### Pontuação e diagnóstico — Resiliência

| Acertos | Diagnóstico | Prioridade de revisão |
|---:|---|---|
| 0-11 | Falta base de HA/DR | Multi-AZ, ASG/ELB, SQS/DLQ, Route 53, backups |
| 12-15 | Entende padrões, mas confunde HA com DR | RTO/RPO, Multi-AZ vs réplica, pilot light/warm standby |
| 16-18 | Bom domínio | Revisar edge cases de filas, failover regional e Object Lock |
| 19-20 | Pronto no domínio | Manter simulados mistos |

---

## Mini-Simulado 3 — Performance

**1.** Conteúdo estático global com baixa latência.  
A) CloudFront  
B) RDS Multi-AZ  
C) SQS FIFO  
D) AWS Backup  
**Resposta: A.** CloudFront entrega em edge locations e reduz latência.

**2.** Aplicação TCP global precisa IPs anycast e menor latência.  
A) Global Accelerator  
B) Athena  
C) Macie  
D) EFS IA  
**Resposta: A.** Global Accelerator otimiza tráfego TCP/UDP via rede global AWS.

**3.** Leituras repetidas em banco relacional estão sobrecarregando o banco.  
A) ElastiCache  
B) S3 Glacier  
C) SCP  
D) EIP  
**Resposta: A.** Cache em memória reduz leituras repetidas no banco.

**4.** DynamoDB precisa leitura em microssegundos para itens frequentemente acessados.  
A) DAX  
B) RDS Proxy  
C) FSx for Windows  
D) NAT Gateway  
**Resposta: A.** DAX é cache gerenciado para DynamoDB.

**5.** (Selecione duas) Para melhorar Athena em dados no S3:  
A) Converter para Parquet  
B) Particionar por data/chaves consultadas  
C) Usar CSV gigante sem compressão  
D) Aumentar NAT Gateway  
**Resposta: A e B.** Parquet e particionamento reduzem dados escaneados. C/D pioram ou não impactam.

**6.** Banco em EC2 precisa IOPS muito alta e latência baixa.  
A) EBS io2 Block Express  
B) S3 Standard  
C) EFS IA  
D) Glacier Deep Archive  
**Resposta: A.** io2 Block Express é indicado para workloads críticos de I/O de bloco.

**7.** HPC com filesystem compartilhado de alta performance e integração S3.  
A) FSx for Lustre  
B) SQS  
C) Route 53 Resolver  
D) Parameter Store  
**Resposta: A.** FSx for Lustre atende HPC e pode integrar com S3.

**8.** Lambda Java tem cold start crítico.  
A) SnapStart ou Provisioned Concurrency conforme cenário  
B) Colocar em subnet pública  
C) Criar NAT Gateway  
D) Usar S3 Lifecycle  
**Resposta: A.** SnapStart reduz cold start Java; Provisioned Concurrency pré-aquece ambientes.

**9.** Upload de arquivo grande para S3 deve ser eficiente e resiliente.  
A) Multipart Upload  
B) Single PUT obrigatório  
C) CloudTrail  
D) Shield  
**Resposta: A.** Multipart paraleliza e permite retomar partes.

**10.** (Selecione duas) Para escalar leitura em Aurora:  
A) Aurora Replicas  
B) Reader endpoint  
C) Multi-AZ standby lido diretamente  
D) EBS snapshot a cada leitura  
**Resposta: A e B.** Réplicas e reader endpoint distribuem leitura. Standby Multi-AZ tradicional não serve leitura.

**11.** API precisa limitar taxa por cliente para proteger backend.  
A) API Gateway usage plans/throttling  
B) EBS encryption  
C) S3 CRR  
D) AWS Backup Vault  
**Resposta: A.** API Gateway controla throttling e quotas.

**12.** Comunicação de baixa latência entre EC2 na mesma AZ para HPC.  
A) Cluster placement group  
B) Spread placement group  
C) S3 IA  
D) Route 53 geolocation  
**Resposta: A.** Cluster placement group aproxima instâncias para baixa latência.

**13.** Workload ARM compatível busca melhor preço/performance.  
A) Graviton  
B) T2.nano sempre  
C) Dedicated Host obrigatório  
D) Classic Load Balancer  
**Resposta: A.** Graviton costuma oferecer bom preço/performance para cargas compatíveis.

**14.** Consultas analíticas recorrentes e pesadas com muitos usuários concorrentes.  
A) Redshift com ajustes de workload/concurrency scaling  
B) S3 Select para tudo  
C) DynamoDB TTL  
D) IAM Access Analyzer  
**Resposta: A.** Redshift é DW gerenciado para analytics recorrente. S3 Select é pontual por objeto.

**15.** Container precisa service discovery gerenciado entre serviços ECS.  
A) AWS Cloud Map ou ECS Service Connect  
B) EBS snapshot  
C) S3 Object Lock  
D) ACM PCA apenas  
**Resposta: A.** Ambos ajudam descoberta/comunicação entre serviços.

**16.** RDS tem muitas conexões Lambda abrindo e fechando.  
A) RDS Proxy  
B) DAX  
C) CloudFront OAC  
D) Transit Gateway  
**Resposta: A.** RDS Proxy gerencia pool de conexões e melhora resiliência/performance.

**17.** EFS precisa lidar com milhares de clientes e maior throughput agregado.  
A) Modo Max I/O ou throughput adequado ao caso  
B) EBS gp2 único  
C) S3 Glacier  
D) NACL outbound deny  
**Resposta: A.** EFS permite modos/perfis conforme latência e escala.

**18.** Para reduzir latência de DNS global com health checks, use:  
A) Route 53 latency-based routing  
B) CloudTrail data events  
C) SSM Patch Manager  
D) ECR scan  
**Resposta: A.** Latency routing responde com endpoint de menor latência saudável.

**19.** App web em ALB precisa rotear por path `/api` e `/static`.  
A) ALB listener rules  
B) NLB UDP  
C) SQS DLQ  
D) KMS alias  
**Resposta: A.** ALB camada 7 roteia por path/host.

**20.** Redis gerenciado para cache com failover.  
A) ElastiCache for Redis/Valkey com Multi-AZ  
B) DMS  
C) Macie  
D) AWS Artifact  
**Resposta: A.** ElastiCache gerencia cache em memória e pode ter replicação/failover.

### Pontuação e diagnóstico — Performance

| Acertos | Diagnóstico | Prioridade de revisão |
|---:|---|---|
| 0-11 | Lacuna em seleção de serviço por gargalo | Cache, CDN, storage I/O, banco e compute |
| 12-15 | Boa base, mas falta diferenciar otimizações | Athena/Parquet, DAX, RDS Proxy, placement groups |
| 16-18 | Bom domínio | Revisar serviços de borda e performance de banco |
| 19-20 | Pronto no domínio | Manter revisão com cenários mistos |

---

## Mini-Simulado 4 — Custo

**1.** Workload batch tolerante a interrupção.  
A) Spot Instances  
B) Dedicated Hosts  
C) On-Demand sempre ligado  
D) Multi-region active-active  
**Resposta: A.** Spot reduz custo quando interrupção é aceitável.

**2.** Compute estável 24/7 por um ano.  
A) Savings Plans ou Reserved Instances  
B) Spot apenas  
C) Lambda obrigatoriamente  
D) NAT Gateway extra  
**Resposta: A.** Compromisso reduz custo para uso previsível.

**3.** S3 com padrão de acesso imprevisível.  
A) Intelligent-Tiering  
B) One Zone-IA para tudo  
C) Glacier Deep Archive para dados quentes  
D) Bucket público  
**Resposta: A.** Intelligent-Tiering move objetos conforme acesso.

**4.** Subnets privadas acessam S3 com alto volume e NAT caro.  
A) Gateway VPC Endpoint para S3  
B) Mais NAT Gateways  
C) Internet Gateway direto na subnet privada  
D) CloudTrail Lake  
**Resposta: A.** Endpoint evita tráfego via NAT e costuma reduzir custo.

**5.** (Selecione duas) Para reduzir custo de EC2 superdimensionada:  
A) Compute Optimizer  
B) Rightsizing  
C) Aumentar todas para maior família  
D) Remover métricas  
**Resposta: A e B.** Compute Optimizer recomenda; rightsizing aplica ajuste. C/D pioram governança/custo.

**6.** Ambiente dev/test deve ficar desligado fora do expediente.  
A) EventBridge Scheduler + Lambda/SSM Automation  
B) Reserved Instance 3 anos para tudo  
C) Multi-AZ obrigatório  
D) CloudFront  
**Resposta: A.** Agendamento reduz horas ociosas.

**7.** Analytics ad-hoc sobre dados no S3, sem cluster permanente.  
A) Athena  
B) Redshift provisionado sempre ligado  
C) EC2 com scripts manuais  
D) RDS Multi-AZ  
**Resposta: A.** Athena paga por consulta e evita cluster ocioso.

**8.** Arquivo raramente acessado e tolera horas de recuperação.  
A) S3 Glacier Flexible Retrieval ou Deep Archive conforme requisito  
B) S3 Standard sempre  
C) EFS Standard  
D) EBS io2  
**Resposta: A.** Glacier reduz custo para arquivamento com latência de recuperação.

**9.** (Selecione duas) Para custos de Lambda, impactam diretamente:  
A) Duração  
B) Memória configurada  
C) Nome da função  
D) Cor da tag  
**Resposta: A e B.** Cobrança considera requests, duração e memória. C/D não impactam computação.

**10.** Transferência de dados para internet a partir de conteúdo estático S3 pode ser otimizada com:  
A) CloudFront  
B) Mais EBS  
C) SCP  
D) RDS Proxy  
**Resposta: A.** CloudFront cacheia em edge e pode reduzir custo/latência de entrega.

**11.** EBS volumes não usados continuam gerando custo. Como identificar?  
A) Cost Explorer/Trusted Advisor/Compute Optimizer conforme conta e plano  
B) Macie  
C) WAF  
D) Cognito  
**Resposta: A.** Ferramentas de custo e otimização ajudam localizar recursos ociosos.

**12.** Banco relacional dev sem requisito de HA pode economizar usando:  
A) Single-AZ  
B) Multi-AZ obrigatório  
C) Aurora Global Database  
D) Active-active  
**Resposta: A.** Em dev/test, Single-AZ pode ser aceitável. Produção crítica costuma exigir HA.

**13.** Para containers com carga variável e sem gerenciar servidores:  
A) ECS Fargate com autoscaling  
B) EC2 superdimensionado fixo  
C) Dedicated Host  
D) S3 Object Lock  
**Resposta: A.** Fargate reduz operação e escala conforme demanda.

**14.** EFS com arquivos pouco acessados pode usar:  
A) EFS lifecycle para IA  
B) EBS io2 sempre  
C) DynamoDB DAX  
D) Global Accelerator  
**Resposta: A.** Lifecycle move arquivos frios para classe mais barata.

**15.** Para orçamento e alerta de gasto mensal, use:  
A) AWS Budgets  
B) GuardDuty  
C) Inspector  
D) Route 53  
**Resposta: A.** Budgets monitora custo/uso e alerta.

**16.** Workload de contêiner tolerante a interrupção em ECS pode reduzir custo com:  
A) Fargate Spot quando compatível  
B) Multi-AZ RDS  
C) WAF Bot Control  
D) ACM  
**Resposta: A.** Fargate Spot reduz custo para tarefas tolerantes a interrupção.

**17.** S3 One Zone-IA é adequado quando:  
A) Dados são recriáveis e acessados raramente  
B) Dados críticos exigem resiliência multi-AZ  
C) Arquivo precisa latência de milissegundos e alta resiliência regional  
D) Bucket precisa replicação global obrigatória  
**Resposta: A.** One Zone-IA custa menos, mas fica em uma AZ; não use para dados irrecuperáveis.

**18.** Para estimar custos antes de implantar arquitetura, use:  
A) AWS Pricing Calculator  
B) IAM Access Analyzer  
C) CloudTrail  
D) VPC Flow Logs  
**Resposta: A.** Pricing Calculator estima custos planejados.

**19.** (Selecione duas) Em arquitetura serverless custo-efetiva, evite:  
A) Recursos ociosos sempre ligados sem necessidade  
B) Overprovisioning manual fixo  
C) Escala sob demanda  
D) Pagar por invocação quando carga é esporádica  
**Resposta: A e B.** Ociosidade e superdimensionamento elevam custo. C/D costumam ajudar em carga variável.

**20.** Reduzir custo de DynamoDB em carga imprevisível e baixa administração pode apontar para:  
A) On-demand mode  
B) Provisionar RCU/WCU muito altas fixas  
C) EC2 com banco manual  
D) NAT Gateway  
**Resposta: A.** On-demand evita capacity planning para tráfego variável, embora provisionado possa ser melhor em carga previsível.

### Pontuação e diagnóstico — Custo

| Acertos | Diagnóstico | Prioridade de revisão |
|---:|---|---|
| 0-11 | Lacuna em modelos de cobrança | EC2 compra, S3 classes, NAT/endpoints, serverless |
| 12-15 | Entende custo, mas erra contexto | Spot vs Savings Plans, dev/test vs prod, Athena vs Redshift |
| 16-18 | Bom domínio | Revisar transferências, storage frio e recursos ociosos |
| 19-20 | Pronto no domínio | Manter leitura de armadilhas de custo |

---
_Credito autoral: Thiago Cardoso - [LinkedIn](https://www.linkedin.com/in/analyticsthiagocardoso)_
