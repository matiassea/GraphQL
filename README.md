# GraphQL
Ayuda para Pipefy

https://graphql.org/learn/queries/



### Rescate de informacion de tarjeta general
```
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

```

### Mutation

### Para mover la tarjeta 375966557 a la phase 308965557
```
mutation{moveCardToPhase(
  input:{
    card_id:" 375966557",
    destination_phase_id:"308965557",
    clientMutationId:"lake"
  }) {
  clientMutationId
}
  }
```
### Para actualizar el campo de Asignacion
### Que solamente tiene la tarjeta cuando esta cerrada.

Id = numero de tarjeta y en assignee_ids se coloca el numero de persona.
```
mutation{updateCard(
  input:{
    id:" 376927452"
    assignee_ids:["301048281"]
    clientMutationId:"Cambio de asignacion"
  }) {
  clientMutationId
}
  }
```
### Para actualizar un campo de la tarjeta
### Se utilizara UpdateCardInput para modificar el Grupo de Colaboradores:, dado por el "label": del "fields", de "current_phase"
### En este caso asignacion

El field_id se toma desde el id de los fields de la current_phase. Aun asi queda como assignees

```
mutation{updateCardField(
  input:{
    card_id:" 377396362"
    field_id:"grupo_de_colaboradores"
    new_value:["301048281"]
    clientMutationId:"Cambio de asignacion"
  }) {
  clientMutationId
  
}
  }
```
### Para hacer la consulta de la card, rescatando el field a modificar.

```
  {card(id:377762484)
  {
    title
    url
    current_phase {
      id #Id de la phase
      name
      created_at
      description
      fields {
        id #nombre interno del campo para llamarlo y modificarlo
        index_name 
        internal_id
        description
        label #nombre en la tarjeta grafica
        phase {
          id #Id de la actual phase
        }
      }
    }
    fields {
			assignee_values {
			  id
			}
      indexName
      name
      report_value
      value
      phase_field {
        id
      }
    }
    assignees{
      id
      name
    }
    }
    }


```
















