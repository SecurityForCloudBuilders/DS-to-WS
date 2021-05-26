# DS-to-WS

## Alguns Pontos de Atenção ao Migrar o Deep Security On-Premise para o Cloud One Workload Security!

<br />
<hr />
<br />

## AVISO IMPORTANTE!

<b> Esse repositório não é oficial, criado, desenvolvido, afiliado, apoiado, mantido ou endossado pela organização Trend Micro.

A documentação oficial será sempre a sua melhor amiga: :smile: 

- https://cloudone.trendmicro.com/docs/workload-security/

Com esses pontos de atenção em mente, você pode ter uma estimativa de quanto tempo e esforço levará para migrar o seu ambiente! </b>

<br />
<hr />
<br />

<details>
  <summary>:smile: CRIAÇÃO DA NOVA CONSOLE DO CLOUD ONE: WORKLOAD SECURITY </summary>

<br />

Os clientes precisarão migrar as permissões de usuário e roles do seu Deep Security para o Workload Security, para continuar dando suporte, visibilidade e gerenciamento. 

1.	Cadastre-se para uma nova conta no Cloud One - Workload Security ao clicar em "Create an Account" no <a href="https://cloudone.trendmicro.com/"> Portal do Cloud One. </a>

As configurações de usuários e roles no Workload Security são quase idênticas à implementação no Deep Security.

2.	Permitir tráfego de saída para portas e URLs do Cloud One - Workload Security

Teste a conexão para o Cloud One - Workload Security

### Windows Powershell:

- test-netconnection relay.deepsecurity.trendmicro.com -Port 443 
- test-netconnection app.deepsecurity.trendmicro.com -Port 443 
- test-netconnection agents.deepsecurity.trendmicro.com -Port 443 
- test-netconnection dsmim.deepsecurity.trendmicro.com -Port 443


### Linux Shell:

- curl -v https://app.deepsecurity.trendmicro.com:443
- curl -v https://relay.deepsecurity.trendmicro.com:443
- curl -v https://agents.deepsecurity.trendmicro.com:443
- curl -v https://dsmim.deepsecurity.trendmicro.com:443 


</details>

<br />
<hr />


<details>
  <summary>:heart: MIGRAÇÃO DO(S) CONECTOR(ES) </summary>

## Migração dos Conectores

Identifique Cloud Connectors e VMware (AWS, Azure e/ou GCP) para serem migrados. Embora o inventário e a configuração possam ser recuperados programaticamente, 
credenciais não podem. No caso de grandes volumes de conectores a serem migrados, avalie e discuta as possibilidades de automação.


1.	Identifique os Connectors a ser migrados;
2.	Colete as Credenciais;
3.	Add Connectors para o Workload Security;


- <a href="https://cloudone.trendmicro.com/docs/workload-security/aws-add/"> Conectar o Workload Security com uma conta sua da AWS </a>
- <a href="https://cloudone.trendmicro.com/docs/workload-security/azure-application/"> Conectar o Workload Security com uma subscrição sua da Azure </a>
- <a href="https://cloudone.trendmicro.com/docs/workload-security/gcp-account-create/"> Conectar o Workload Security com uma conta sua do GCP </a>
- <a href="https://cloudone.trendmicro.com/docs/workload-security/vcenter-add/"> Conectar o Workload Security com o VCenter </a>


</details>

<br />
<hr />

<details>
  <summary>:vulcan_salute: MIGRAÇÃO DO(S) GRUPO(S) </summary>

## Migração dos Computer Groups 

Pode ser exigido a segmentação dos sistemas para gerenciar o inventário do host ou controle de acesso aos sistemas. A estrutura do grupo pode ser copiada como está ou reestruturada conforme considerado apropriado por você. Se a estrutura de grupo existente for recriada como está no Workload Security, e se desejável para aliviar a carga de uma hierarquia de um grande grupo, este processo pode ser automatizado via <a href="https://cloudone.trendmicro.com/docs/workload-security/api-reference/tag/Computer-Groups"> API. </a>
  

1.	Pesquise grupos existentes para migração.
2.	Criar uma estrutura de grupo(s) no Workload Security.
3.	Valide a estrutura de grupo(s).
4.  Registre grupos que serão usados ​​para hospedar sistemas Linux durante esta migração.

</details>

<br />
<hr />

<details>
  <summary>:ok_hand: CONFIGURAÇÃO DO PROXY </summary>

## Configuração do Proxy

A configuração das comunicações de proxy para atualizar os Agents, Appliances, e Relays, quando necessário, é definida em Configurações de sistemas do Deep Security Manager ou na console do Workload Security. Essas configurações devem ser migradas antes da migração da(s) política(s) para que as referências fiquem intactas.

1.	Exportar configurações de proxy já existentes do Deep Security Manager;
2.	Exclua todas as configurações de proxy existentes do Workload Security Console <b> (se aplicável); </b>
3.	<strong> *** A etapa anterior só deve ser concluída durante o esforço de migração inicial e não deve ser repetida nas tentativas de importação subsequentes; *** </strong>
4.	Importar configurações de proxy para a console do Workload Security;

</details>

<br />
<hr />

<details>
  <summary>:trophy: MIGRAÇÃO DA(S) POLITICA(S) </summary>

## Migração das Politicas

As Security Policies serão migradas do Deep Security para o Workload Security. A hierarquia e a estrutura organizacional das Security Policies podem ser complexas, por isso, estes pontos precisaram de detalhes adicionais após a revisão da estrutura da política atual para determinar o caminho mais adequado a seguir, e se esse texto faz sentido ou se adequa ao seu tipo de ambiente. Além das configurações de política, deve-se tomar cuidado e atenção com a migração de listas e objetos adicionais referenciados por, mas que não fazem parte do objeto da política.

 <strong> *** É altamente Recomendado realizar uma revisão da política, listas, exceções e objetos antes de mudar para a nova plataforma. *** </strong>

### Migração Manual

Esta seção irá detalhar algumas observações em itens de configuração a serem revisados ​​e migrados:

### Objects:

1.	Security Policy Module configurations

a.	Anti-Malware Module configurations
  i.	Anti-Malware configuration
  ii.	Anti-Malware scan schedule
  iii.	Anti-Malware proxy configurations
  iv.	Anti-Malware Directory Lists
  v.	Anti-Malware File Lists
  vi.	Anti-Malware File Extension Lists


- Anti-Malware Process Image File Lists

  1.	Web Reputation Module configurations
    a.	Web Reputation configuration
    b.	Web Reputation Allowed lists

- Web Reputation Blocked lists

  1.	Web Reputation proxy configurations
  1.	Application Control Module configuration
    a.	Global Rules
  2.	Integrity Monitoring Module configurations
    a.	Integrity Monitoring configuration
    b.	Integrity Monitoring Rules assigned
  3.	Log Inspection Module configurations
    a.	Log Inspection configuration
    b.	Log Inspection Rules assigned
  4.	Firewall Module configurations
    a.	Firewall Module configuration
    b.	Firewall rules assigned

- IP lists

  1.	Port lists
  2.	MAC lists
  3.	Stateful Configurations

- Interface Isolation Patterns
- Contexts

  1.	Intrusion Prevention configurations
    a.	Intrusion Prevention configuration
    b.	Intrusion Prevention rules assigned

- Application Type custom rules or customizations

  1.	Policy Interface Types customization
  2.	Policy Settings
  3.	Policy overrides
  4.	Syslog Configurations

</details>

<br />
<hr />

<details>
  <summary>:medal_sports: MIGRAÇÃO DO(S) USUÁRIO(S) E ROLES </summary>

## Migração de Usários e Roles  

Role Based Access Control em funções pode ser um mecanismo crítico para delegar o gerenciamento de sistemas e políticas específicas.

Não há mecanismo na console disponível para exportação ou importação de roles ou usuários.

As roles devem ser criadas antes dos usuários para que uma role possa ser atribuída durante a criação do usuário.

</details>

<br />
<hr />

<details>
  <summary>:eyeglasses: CONFIGURAÇÕES ADICIONAIS </summary>

## Configurações Adicionais

O Deep Security e o Workload Security têm várias configurações adicionais e opcionais que podem estar em uso. A recomendação é para revisar o uso dessas configurações e identificar aquelas que devem ser migradas.

- Integrity monitoring auto-tagging 
- Event Forwarding 
- Event Based Tasks 
- Scheduled tasks 
- User security requirements 

</details>

<br />
<hr />

<details>
  <summary>:dart: AVALIAÇÃO E CONFIGURAÇÃO DE REDE </summary>

## Avaliaçao e Configuraçao de Rede

Dado que o Workload Security é entregue como uma plataforma SaaS, será necessária conectividade da sua infraestrutura para os sistemas da Trend Micro.

Esta seção se concentrará especificamente na conectividade do agente e não abordará os requisitos do navegador para a console de gerenciamento. Detalhes adicionais sobre as configurações de proxy podem ser encontrados <a href="https://cloudone.trendmicro.com/docs/workload-security/proxy-set-up/"> aqui. </a>

### Lista de permissões de URL na saída (proxy ou outro Network Edge Device)

Todos os agentes exigirão, no mínimo, acesso aos seguintes URLs e portas 

- agents.deepsecurity.trendmicro.com:443 
- app.deepsecurity.trendmicro.com:443 
- relay.deepsecurity.trendmicro.com:443 


URLs adicionais podem ser necessários para recursos opcionais, incluindo Smart Scan, File Reputation e Web Reputation. A documentação completa de URLs e portas pode ser encontrada <a href="https://cloudone.trendmicro.com/docs/workload-security/communication-ports-urls-ip/"> aqui. </a>

</details>

<br />
<hr />

<details>
  <summary>:coffee: CONFIGURAÇÃO DE RELAY(S) </summary>

## Configuração de Relay(s)

Alguns clientes podem ter uma infraestrutura de <a href="https://cloudone.trendmicro.com/docs/workload-security/relay-overview/"> relay(s) </a> já existente que pode ser replicada para gerenciar o consumo de largura de banda em toda a infraestrutura.

E é possível replicar a infraestrutura de relay(s) existente e a topologia para distribuição de atualização do Workload Security e avaliação de uma retransmissão <i> "top of tree" </i> adicional para replicar a <i> update source </i> primária existente.

</details>

<br />
<hr />

<details>
  <summary>:checkered_flag: TESTE DO AGENTE </summary>

## Teste do Agente  

O teste deve ser focado na validação da migração:

### Escopo do Teste: 

1.	Escolha um agente na já existente infraestrutura do Deep Security Manager.
2.	Execute o script de migração [Apêndice 1 item A] 
3.	Valide o sucesso da reativação e da atribuição da Security Policy


### Validação da reativação do Agente 

1.  Verifique se o agente está disponível na aba Computers no Workload Security 
2.	Verifique se a saída do comando no [Apêndice 1 item B] corresponde a URL esperada

### Validação da atribuição da Security Policy  

1.	Verifique se o Workload Security mostra a política correta atribuída na console
2.	Verifique se a saída do comando no [Apêndice 1 item C] corresponde ao nome da Security Policy esperada


## Apêndice 1 

Este apêndice detalha referências adicionais, incluindo scripts e outras orientações de configuração, use conforme julgue necessário. 

### Item A 

Este script foi projetado para facilitar a automação para a migração do agente. Em um alto nível, ele irá:

1.	Desativar a instalação atual do agente
2.	Reativar o agente no Workload Security com nova configuração

Este é um Script de exemplo. Os scripts com mais detalhes serão criados pela console do Workload Security para cada grupo de computador / Security Policy / local de rede.

Some details, such as security policy id or name, if migrated 1:1 from the Deep Security implementation, may be scripted into the new activation commands to reduce the number of script variations required across the environment. 

Alguns detalhes, como <i> policyid </i> ou <i> policyname </i> da <i> groupid </i>, são opcionais e podem ser inseridos nos novos comandos de ativação para reduzir o número de variações de script necessárias em todo o ambiente.

<strong> Outras configurações, como Proxy e Relay devem ser só usadas se estão implementadas no ambiente. </strong>

<strong> O exemplo abaixo serve para ser executado em máquinas Linux: </strong>

/opt/ds_agent/dsa_control -r

sleep 30

PROXY_ADDR_PORT='1.2.3.4:3128' 

RELAY_PROXY_ADDR_PORT='1.2.3.4:3128' 

/opt/ds_agent/dsa_control -x dsm_proxy://$PROXY_ADDR_PORT/ 

/opt/ds_agent/dsa_control -y relay_proxy://$RELAY_PROXY_ADDR_PORT/ 

/opt/ds_agent/dsa_control -a dsm://agents.deepsecurity.trendmicro.com:443/ "tenantID:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" "token:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" "policyid:1" "policyname:mypolicy" "groupid:12345" 


<strong> O exemplo abaixo serve para ser executado em máquinas Windows: </strong>

& $Env:ProgramFiles"\Trend Micro\Deep Security Agent\dsa_control" -r

Start-Sleep -s 50

& $Env:ProgramFiles"\Trend Micro\Deep Security Agent\dsa_control" -a dsm://agents.deepsecurity.trendmicro.com:443/ "tenantID:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" "token:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" "policyid:1" "groupid:12345"


<strong> No caso acima, não estamos configurando Proxy e Relay no agente </strong>

<strong> Dependendo de como o seu ambiente está confirgurado, os comandos a seguir, podem necessitar serem executados como root </strong>

### Para recuperar o nome da Security Policy: 

/opt/ds_agent/sendCommand --get GetConfiguration | grep SecurityProfile | awk -F"name='" '{printf $2}' | awk -F"'" '{print $1}' 


### Item B 

Este comando produzirá a url da DSM no qual o agente está registrado atualmente. Use-o para validar se um agente foi reativado para o Workload Security corretamente. O dsmUrl esperado é https://agents.deepsecurity.trendmicro.com:443/ 

/opt/ds_agent/dsa_query --cmd GetAgentStatus | grep dsmUrl 

### Item C 

Este comando retornará o nome e o ID da política de segurança atribuída ao DSA.

/opt/ds_agent/sendCommand --get GetConfiguration | grep SecurityProfile 

### Item D 

Este é um exemplo do comando Curl que pode ser usado para listar Security Roles via API
 
curl -X GET $url/api/roles -H "api-secret-key: $secret" -H "api-version: v1" -k | json_pp 
- -k é usado porque o DSM está usando um self-signed certificate  
- json_pp é usado para exibir a saída no formato JSON


</details>

<br />
<hr />

<details>
  <summary>:100: AUTOMAÇÃO E MELHORES PRÁTICAS </summary>

## Best Practice: 

- Depois de importar as políticas, cheque a <a href="https://cloudone.trendmicro.com/docs/workload-security/communication-manager-agent/#Configur"> direção da comunicação </a> e se está definida como Agent-initiated;
- A comunicação bidirecional pode causar problemas de agentes offline se o Workload Security não for capaz de iniciar uma conexão com os hosts, especialmente quando usa um endereço de IP privado;

</details>