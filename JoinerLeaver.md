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
   * importe atributo - ObjectConfig
   * ative LCM
   * crie birthright
   * crie templates de email
   * grupo de trabalho para receber email
   * processos de negocio
   * definicao das populacoes
   * eventos de ciclo de vida
   * 
