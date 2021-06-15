# Joiner e Leaver
   
   * Fonte autoritativa informa que identidade mudou de status
   * IIQ dispara joiner com birthright (role) ou leaver a partir de refresh identity com processar eventos habilitado, dispara o identity trigger
   * Provisioning plan gerado no começo do workflow (a partir do leaver do LCM)
     * Atributos estendidos da aplicacao definem o comportamento para roles do IIQ (birthright), contas e entitlements de fontes autoritativas e nao autoritativas 
       * remover, 
       * preservar, 
       * bloquear) 
   * Notificações com sucesso ou falha
   
# Construção
   
   * adicione atributo estendido na config do hibernate - classes/sailpoint/object/ApplicationExtended.xml
     * property name... type string... length... access=sailpoint.persistence.ExtendedPropertyAccessor index=spt... 
   * atualize iiq extendedSchema - iiq extendedSchema (cria sql)
   * atualize BD - ../database/add_identityiq_extensions.mysql - ache o codigo gerado e atualize no bd
   * atualize i18n - classes/sailpoint/web/messages
   * reinicie
   * importe atributo - ObjectConfig - objectattribute name=... namedColumn=true displayName=att... editMode=Permanent
   * ative LCM - importe o init-lcm.xml
   * crie birthright - Pode ser um novo tipo de função (role), opcoes desmarcadas apenas sem deteccao automatica, sem perfil de direitos e sem atribuicao automatica com regra
   * crie templates de email
   * grupo de trabalho para receber email - degine um workgroup, define um email, direitos de diversos recursos (administrador de xxx, onde xxx é tudo)
   * processos de negocio
     * passo com catches=complete ele pega erros que ocorrerem no wf
     * parta de Lifecycle Event - Leaver
     * re-execução rodando um leaver e um joiner mais restritos (populações específicas)
   * definicao das populacoes
     * Inteligencia - análises avançadas - salve o resultado como população
   * eventos de ciclo de vida

# Parametros do workflow que sao usados 

   * nomeUsuario
   * identityRequestId
   * nomeTarefa - "Processo de Joiner/Leaver para funcionario/terceiro", etc
   * funcionalUsuario
   * dataInicio - IdentityRequest.getCreated()
   * dataFim - IdentityRequest.getVerified() ou getEndDate() (com falha, só chega até o verified)
   * mensagemFalha
   * comentarioSistema (detalhamento do que foi pedido a partir do TaskResult.getPlans() e getResult(), cada Plan tem um TargetIntegration e um NativeIdentity)

# Condições de disparo de joiner e leaver
   * Joiner: tipo de identidade, primeiro nome não nulo, último nome não nulo, status ativo, sem função birthright associada
   * Leaver: tipo de identidade, status inativo, com função de birthright associada

# Buildplan de Joiner
   * IdentityChangeEvent = wfcontext.getStepArguments().getEvent()
   * Identity = event.getNewObject()
   * Instancia um ProvisioningPlan
   * Instancia um AccountRequest(AccountRequest.Operation.Modify, "IIQ", null, identity.getName())
   * Instancia um AttributeRequest("assignedRoles", ProvisioningPlan.Operation.Set, assignments) onde assignments é um ArrayList de Strings contendo "ITAU Birthright"
   * monta o plan e manda



# Buildplan de Leaver
