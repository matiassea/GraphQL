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
        id #Para el rescate del field_id
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

### Status del phase, rescatando el nombre del phase, cantidad de tarjetas expiradas y cantidad de tarjetas por pipe

```
query{
phase (id:308543346){
  name
  cards_count
  lateCardsCount
  cards {
    edges {
      node {
        id
        title
      }
    }
  }
  expiredCardsCount
}
}

```

### Status de la tarjeta, consultando a los assignees.

```
{card(id:378069198)
  {
    title
    age
    url
    checklist_items_count
    checklist_items_checked_count
    cardAssignees {
      id
      assignedAt
      
    }
    current_phase{
      id #Id de la phase
      name
      created_at
      description
    }
    assignees{
      id
      name
      email
    }
	}
}
```

### Consulta de la organizacion

```
query{
organization (id:355438){
  name
  tables {
    edges {
      node {
        id
        name
      }
    }
  }
}
}

```


### Status del Pipe, con el nombre de la organizacion, cantidad de tarjeta, cantidad de tarjetas expiradas por fases.

```
query{
pipe (id:301279586 ){
  organization {
    id
    name
  }
  cards_count
  opened_cards_count
	description
  phases {
    id
    name
    expiredCardsCount
    cards_count
  }
}
}

```
### Status del Pipe, con el nombre de la organizacion, cantidad de tarjeta, cantidad de tarjetas expiradas por fases, asignados, age y URL
```
{cards(pipe_id:301279586
	first:2000) {
  edges {
    node {
      age
      id
      assignees {
        name
      }
#      current_phase {
#        name
#      }
#      subtitles {
#        filled_at
#        indexName
#        name
#        report_value
#        updated_at
#        value
#      }
      url
    }
  }
}

}
```

#### tiempo de estadia de la tarjeta, mide el age que es la edad total en segundos y desglosa por cada fase

```
{card(id:378069198)
  {
    title
    url
    age
    phases_history {
      created_at
      duration
      firstTimeIn
      lastTimeIn
      lastTimeOut
      phase {
        id
        name
      }
    }
  }
}
```
#### Para todas las cards de la unica Pipe, midel el tiempo de estadia (age) de la tarjeta y entrega el URL
```
{cards(pipe_id:301279586
	first:2) {
  edges {
    node {
      age
      id
#      current_phase {
#        name
#      }
#      subtitles {
#        filled_at
#        indexName
#        name
#        report_value
#        updated_at
#        value
#      }
      url
    }
  }
}

}
```

#### Para rastrear las Tablas imputadas a una institucion


```
query{
organization (id:355438){
  name
#  tables (name_search:"{SAMPLE} Departments") {
  tables {
  edges {
      node {
        id
        name
        public
        table_fields {
          id
          label
        }
        table_records {
          edges {
            node {
              id
              labels {
                id
                name
              }
              parent_relations {
                id
                name
              }
              table {
                id
                title_field {
                  id
                }
              }
              path
              url
            }
          }
        }
        table_records_count
      }
    }
  }
}
}

```
