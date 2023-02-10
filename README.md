# Backend Interview
Congratualzioni, se sei qui e' perche' hai passato il primo step di selezione, non vediamo l'ora di proseguire.

In questa fase, da svolgere offline, dovrai creare una REST Api con Spring Boot che abbia i seguenti endpoint:

- **GET** `/nodes`
- **POST** `/nodes`
- **PATCH** `/nodes/:id`

---

> **Note** 
> 
> E' possibile connettersi al database usando il docker-compose fornito. Se si sceglie di usare un'altro genere di database, va fornito un ambiente di test (e.g docker-compose riadattato)

## Assumptions 
- Il progetto deve contenere Unit Test. 
- Il progetto e' definito come completo solo e solamente se testato e privo di bug
- Il body delle richieste deve essere validato

## Struttura dei dati
Gli endpoint avranno il compito di gestire le relazioni tra dei nodi, e avranno la seguente struttura:

```jsonc
{
	"id": string,
	"value": number, // min = 0
	"parents": Array<string> 
}
```
> NOTA: I valori dei nodi sono relazionati tra loro

---


# Esempio 

# GET
- Ritorna la lista di nodi presenti nel database

```http
GET /nodes
```

```json
[
	{
		"id": "A",
		"value": 1,
		"parents": []
	}, {
		"id": "B",
		"value": 13,
		"parents": []
	}
]
```

---
# POST 
- Aggiunge uno o piu' nodi alla lista
- Ritorna la lista di nodi aggiornata

```http
POST /nodes 
```

### **Payload**

```jsonc
[
	{
		"value": 30,
		"parents": ["A", "B"] // campo opzionale
	}
]
```
> Creazione del Nodo **C**

### Response

```json
[
	{
		"id": "A",
		"value": 1,
		"parents": []
	}, {
		"id": "B",
		"value": 13,
		"parents": []
	}, {
		"id": "C",
		"value": 30,
		"parents": ["A", "B"]
	}
]
```

---
# PATCH 
- Aggiorna  il nodo indicato con un nuovo valore o parentela
- Ritorna la lista di nodi aggiornata.
- La modifica del valore di un nodo che ha all'attivo relazioni con altri nodi, comporta la modifica dei valori degli altri nodi in maniera proporzionale.

```http
PATCH /nodes/:id
```

### Payload

```json
{
	"value": 15
}
```

### Response

```json
[
	{
		"id": "A",
		"value": 0.5,
		"parents": []
	}, {
		"id": "B",
		"value": 6.5,
		"parents": []
	}, {
		"id": "C",
		"value": 15,
		"parents": ["A", "B"]
	}
]
```


# NOTE 
- La modifica deve essere propagata sia per i nodi precedenti che successivi
- Gli ID sono generati internamente e sono univoci
- Non e' possibile eliminare un nodo che e' parent di altri nodi

# Valutazione
- Architettura
- Qualita' del codice 
- Commenti / Documentazione
- Performance 
- Test

## Bonus Points
- Utilizzo di database a grafo (aggiornare docker-compose in caso di scelta differente da quella data)
- Approccio di programmazione reactive (Rx / Reactor)
- Generazione di un file OpenAPI

## Consegna
Creare una repository Github privata e aggiungere i seguenti collaboratori:
- [rawnly](https://github.com/rawnly)
- [filippocozzini](https://github.com/filippocozzini)

Inviare una email a _[`jobs+backend@aquacloud.it`](mailto:jobs+backend@aquacloud.it)_ con la conferma di avvenuta consegna.
