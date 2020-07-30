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
#### El perfil de Jesus no esta autorizado para sacar tarjetas desde N1 a N2 via API, pero si puede reversar a N1 y esa misma volver a sacar.
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
### Para actualizar un campo en especifico de la tarjeta

#### Se utilizara UpdateCardInput para modificar el Grupo de Colaboradores:, dado por el "label": del "fields", de "current_phase"
#### En este caso asignacion

El field_id se toma desde el id de los fields de la current_phase.

#### Para la identificacion de los grupo de colaboradores. La tarjeta debe estar en N2 (quedan como Assignes)
```
{
"description": "",
"id": "grupo_de_colaboradores",
"index_name": "field_2_assignee_select",
"internal_id": "317897997",
"label": "Grupo de Colaboradores:",
"phase": {
"id": "308543346",
"name": "Nível 2"
}
```

#### Para el caso del grupo de colaboradores, solo en N2, se cambian con:
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
#### Para la identificacion de los ejecutivos de la mesa de servicios. La tarjeta debe estar en N1
```
{
"description": "",
"id": "ejecutivo_a_de_mesa_de_servicio",
"index_name": "field_1_assignee_select",
"internal_id": "317894376",
"label": "Ejecutivo(a) de Mesa de Servicio:",
"phase": {
"id": "308543343"
}
```


#### Para el caso de los ejecutivos de la mesa de servicios, solo en N1, se cambian con.
El field_id se toma desde el id de los fields de la current_phase.
```
mutation{updateCardField(
  input:{
    card_id:" 378069198"
    field_id:"ejecutivo_a_de_mesa_de_servicio"
    new_value:["301047252"]
    clientMutationId:"Cambio de asignacion"
  }) {
  clientMutationId
  
}
  }

```

### Para rescatar campos de la tarjeta, se esta optimizando la busqueda de los campos de la current phase.
```
{card(id:378069198)
  {
    title
    url
    current_phase {
      id #Id de la phase
      name
      created_at
      description
      fields {
        id
        index_name
        internal_id
        description
        label
        phase {
          id
        }
      }
    }
    assignees{
      id
      name
    }
    }
    }
```












