Os movers são definidos por RBAC, por regras de associação na regra de business.


tarefa               | funcao tipo IT     | flags
-------------------- | ------------------ | -------
agregacoes           | atualiza condicoes | atualizar funcoes atribuidas e detectadas desmarcado
refresh id           | dispara triggers   | atualizar atributos de identidade, provisionar atribuicoes, processar eventos
perform maint        | atualiza certs     | default
perform id req maint | conclui provision  | default

O critério é código do departamento X e situação ativo ou licença (não cobrir inativo ou bloqueado)


funcao tipo business   | funcao tipo IT | relacao | direitos 
---------------------- | -------------- | ------- | -------- 
p1                     | p1m1           | mandat  | A, F     
p1                     | p1p2p3         | mandat  | C        
p1                     | p1o1           | opcion  | B, F        
p2                     | p2m1           | mandat  | D, F     
p2                     | p1p2p3         | mandat  | C        
p2                     | p2o1           | opcion  | E, F        
p3                     | p3m1           | mandat  | G, F     
p3                     | p1p2p3         | mandat  | C        
p3                     | p3o1           | opcion  | I, F        
birthright             |                |         | H, J
(pre existente)        |                |         | K


situacao                                                                         | efeito
-------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------
ganhando acessos por regra de associacao                                         | x
trocando acessos por regra de associacao                                         | x
perdendo acessos por regra de associacao                                         | x
detectando funcoes por agregacao                                                 | x
requisitando funcoes manualmente                                                 | x
acionando processo de certificacao                                               | x
requisitando funcao de IT opcional                                               | x
direito requisitado manualmente faz parte de funcao atribuivel por associacao    | x
funcao de Biz associada ao depto corrente é explicitamente removida              | x
funcao de IT detectada e parte de funcao Biz atribuída é removida por RBAC       | x

