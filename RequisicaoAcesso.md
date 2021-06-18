# Requisicao de Acessos

* Definir quicklinks
* Definir nos quicklinks quem pode pedir o que, filtrar, etc
* Expiração e escalada (globais - testado com debug/timemachine - regra de escalation global)
* Delegação
* Waived Approval
* LCM Provisioning
  * Approve and Provision Subprocess
  * Provisioning Approval Subprocess -> regra pra converter workgroup owner de roles em lista de aprovadores, regra de escalation 
  * Identity Request Notify
  * Identity Request Start Notify
  * Identity Request Finalize 
* configurar workflows em lifecycle manager -> business process
* múltiplas contas: configuracoes globais, identityiq, funções, opçoes de funcoes adicionais (multiplas contas e multiplas atribuicoes)
* regra target account privileged (AccountSelector)
* regra target account personal   (AccountSelector)


Regra de escalation

    if item.getAttribute("fallbackApprover")
      fallback = ...
    owner = item.getNotificationOwner(context)
    newOwner = owner.getManager()
    if (newOwner null)
      fallback
    else
      newOwner.getName
      
Regra de Approval Assignment      

    regra bem grande, nao vou reproduzir aqui
    
Regra de Inactive User WorkItem Escalation

    equivalente ao de escalation (90%)
