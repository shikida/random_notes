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
ganhando acessos por regra de associacao                                         | Id pertence a 1, P1 é provisionado. Id fica elegível a p1o1 e ganha p1m1 e p1p2p3
trocando acessos por regra de associacao                                         | Id muda de 1 para 2. Id perde A e ganha D
perdendo acessos por regra de associacao                                         | Id muda de 2 para 4. Id perde os acessos
detectando funcoes por agregacao                                                 | Seja Id com acessos de A...K. IIQ identifica IT mas não Biz. Biz é sempre atribuída.
requisitando funcoes manualmente                                                 | Conforme cenário anterior, P1, P2 e P3, e seus opcionais PnO1. IIQ atribui as Biz
acionando processo de certificacao                                               | Id muda de 4 para 2. Certificação para P1, P2, P3 (manual) e K (detectado e não coberto)
revogando todos os acessos                                                       | (xxx) Id deve ter apenas birthright (H, J). Como está em 2, refresh identity provisiona P2 
requisitando funcao de IT opcional                                               | Id pertence a 1, elegível a p1o1. Requisite. Mude para 2. Id perde p1o1 pois não elegível
direito detectado na agregacao faz parte de funcao atribuivel por associacao     | Id possui A por agregação e está em 1. Id vai para 1, ganha P1. Vai para 2, perde P1 e A   
direito requisitado manualmente faz parte de funcao atribuivel por associacao    | Idem anterior, exceto que perde P1 mas mantém P1M1 (A) que vai para certificação
funcao de Biz associada ao depto corrente é explicitamente removida              | Id recebe P2 por RBAC. P2 aparece como opção para remoção. Não ganha P2 após refresh 
funcao de IT detectada e parte de funcao Biz atribuída é removida por RBAC       | Id requisita C. Id vai para 1 e ganha acessos. Id vai para 4, perde P1, P1P2P3 cert

(xxx) Se houver periodo de contestacao, time machine nao funciona. Neste caso, em modo debug, liste os objetos do tipo certificacao por data de criacao desc, edite automaticClosingDate=activated, salve, execute perform maint para encerrar a certificacao

