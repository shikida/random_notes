# Acesso Temporário

Existe suporte nativo da ferramenta, para o cliente, foi adicionada uma versão custom.

* atributo estendido do tipo int no objeto Bundle
* atributo estendido do tipo boolean para indicar que o comportamento não é o default da ferramenta
* LCM Provisioning, novo step logo depois do Start pra calcular as datas do intervalo
* Approve and Provision Subprocess, novo step antes do Approve pra trocar as datas de inicio e fim do ApprovalSet
* Identity Request Provision, novo step entre Process Approval Decisions e DeProvisioning Forms Post Approval, adicionando datas no MasterPlan
* Role Modeler - Owner Approval - novo step entre Audit Success e Commit, adicionando mensagem com o intervalo de tempo na descrição da funçã
