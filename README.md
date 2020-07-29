# GraphQL
Ayuda para Pipefy


### Rescate de informacion de tarjeta
´´´
{card(id:377184623)
  {
    title
    current_phase {
      id #Id de la phase
      name
      created_at
    }
    current_phase_age
    started_current_phase_at
    inbox_emails{
      from
    }
    assignees{
      id
      name
    }
    }
    }
}


´´´
### Mutation

### Para mover la tarjeta 375966557 a la phase 308965557
´´´
mutation{moveCardToPhase(
  input:{
    card_id:" 375966557",
    destination_phase_id:"308965557",
    clientMutationId:"lake"
  }) {
  clientMutationId
}
  }
´´´
### Para actualizar el campo de Asignacion
### Se utilizara UpdateCardInput
Id = numero de tarjeta y en assignee_ids se coloca el numero de persona.
´´´
mutation{updateCard(
  input:{
    id:" 376927452"
    assignee_ids:["301048281"]
    clientMutationId:"Cambio de asignacion"
  }) {
  clientMutationId
}
  }
´´´
