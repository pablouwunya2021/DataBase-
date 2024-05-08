# Base de Datos de Renta de Canchas Sintéticas de Fútbol

Esta es una base de datos diseñada para un programa de renta de canchas sintéticas de fútbol, implementada en Neo4j. Permite gestionar la información de las canchas, los clientes y las reservas realizadas por los clientes.

## Esquema de la Base de Datos

El esquema de la base de datos se compone de tres tipos de nodos principales:

- **Cliente**: Representa a los clientes que realizan reservas en las canchas.
- **Cancha**: Representa las canchas sintéticas de fútbol disponibles para la renta.
- **Reserva**: Representa las reservas realizadas por los clientes en las canchas.

## Creación de Nodos

Se pueden crear nodos de clientes y canchas utilizando las siguientes consultas Cypher:

```cypher
// Crear nodos para las canchas sintéticas
CREATE (:Cancha {nombre: "Cancha 1", tipo: "Sintética", ubicacion: "Ubicación 1", precio_por_hora: 50})
CREATE (:Cancha {nombre: "Cancha 2", tipo: "Sintética", ubicacion: "Ubicación 2", precio_por_hora: 60})
CREATE (:Cancha {nombre: "Cancha 3", tipo: "Sintética", ubicacion: "Ubicación 3", precio_por_hora: 55})

// Crear nodos para los clientes
CREATE (:Cliente {nombre: "Cliente 1", telefono: "123456789", email: "cliente1@example.com"})
CREATE (:Cliente {nombre: "Cliente 2", telefono: "987654321", email: "cliente2@example.com"})
CREATE (:Cliente {nombre: "Cliente 3", telefono: "456123789", email: "cliente3@example.com"})
```

## Relaciones

Las relaciones entre los nodos están definidas de la siguiente manera:

- **HA_RESERVADO**: Relación entre un cliente y una cancha que indica que el cliente ha reservado esa cancha.
- **HA_REALIZADO_RESERVA**: Relación entre un cliente y una cancha que indica que el cliente ha realizado una reserva en esa cancha en una fecha y hora específicas.

## Creación de Relaciones

Para crear relaciones entre los nodos, se pueden ejecutar las siguientes consultas Cypher:

```cypher
// Relacionar clientes con las canchas que han reservado
MATCH (c:Cancha)
WITH c
LIMIT 2
MATCH (cli:Cliente)
WITH c, cli
CREATE (cli)-[:HA_RESERVADO]->(c);

// Crear relaciones para las reservas
MATCH (cli:Cliente)-[:HA_RESERVADO]->(c:Cancha)
CREATE (cli)-[:HA_REALIZADO_RESERVA {fecha: date('2024-05-07'), hora_inicio: time('10:00'), hora_fin: time('12:00')}]->(c);
```

