# Campanha de certificacao

A certificacao de acesso certifica nao apenas os acessos que estão "sobrando" como os acessos detectados que não foram "oficialmente requisitados", de forma a nivelar que cada acesso foi efetivamente autorizado.

Na certificação, pode-se definir uma regra de exclusão para, por exemplo, ignorar birthright, e.g. 

    //ignora itens atribuidos por RBAC
    
    if (entity instanceof Identity)
      Identity target = entity
      assignments = target.getRoleAssigments()  
      RoleAssignment role = assignment.next
      if (!role.isManual()){
        Bundle b = role.getRoleObject();
        excludeItems.add(b);
      }
    }

    //ignora itens de birthright

    for(Item items){
      if (item instanceof Bundle){
        if ("Birthright".equals(b.getType())){
          excludeItems.add(b)
        }
      }
    }

    items.removeAll(excludeItems)
    itemsToExclude.addAll(excludeItems)
