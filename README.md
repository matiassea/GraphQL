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
#      description #campo en blanco
#      cards_count
    }
    current_phase_age
    started_current_phase_at
#    age
#    comments{
#      id
#      author {
#        id
#      }
#      author_name
#      text
#    }
#    emailMessagingAddress
    inbox_emails{
#      cc
      from
    }
#    labels{
#      name
#    }
#    comments_count
    assignees{
      id
      name
    }
#    creatorEmail
#    fields{
#      date_value
#      datetime_value
#      phase_field {
#        id
#      }
#      field{
#        description
#        id
#        help
#        internal_id
#        label        
#      }
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
