// Caso de Prueba 1: Creación del Replicaset

TorDepReplicaSet = new ReplSetTest ({name: "EventoDeportivo", nodes: 3});
TorDepReplicaSet.startSet();
TorDepReplicaSet.initiate();


// Caso de Prueba 2: Inserción de Datos en el Nodo Primario

conn=new Mongo("LAPTOP-GUF5QK8F:20000")
testDB=conn.getDB("TorneoDeportivo");

/**
 * Inserción de datos en el nodo primario
 */

conn=new Mongo("LAPTOP-GUF5QK8F:20000");


testDB = conn.getDB("TorneoDeportivo");

// Preguntamos si es el nodo primario utilizando la función isMaster()
testDB.isMaster();

// Inserción de registros en la colección 'Deportistas'
testDB.Deportistas.insert([
  {
 "Nombre": "Natalia Villa Lobos",
  "Identificación": "1.123.456",
  "Edad": 25,
  "Genereo": "Femenino",
  "Equipo": "Ataltico",
  "id_Deportista": 30
  },
  // ... (resto de los datos)
]);

// Inserción de registros en la colección 'Entrenadores'
testDB.Entrenadores.insert([
  {
  "Nombre": "Gustabo Martinez",
  "Identificación": "1.777.456",
  "Edad": 50,
  "Genereo": "Masculino",
  "Equipo": "Atlantico",
  "id_Entrenador": 100
  },
  // ... (resto de los datos)
]);

// Inserción de registros en la colección 'Arbitros_Oficiales'
testDB.Arbitros_Oficiales.insert([
  {
    "id": 300,
  "Nombre": "Misael Galindo",
  "Identificación": "28.456.987",
  "Genero": "Masculino",
  "Rol": "Primer Arbitro",
  "Edad": 56
  },
  // ... (resto de los datos)
]);

// Inserción de registros en la colección 'Encuentros_deportivo'
testDB.Encuentros_deportivo.insert([
  {
     "id_Partido": 520,
  "Fecha": "22/11/2023 15:15:00",
  "SetJugados": 4,
  "EquipoGanador": "Bolivar",
  "PuntosGanador": 97,
  "PuntosPerdedor": 87
  },
  // ... (resto de los datos)
]);

// Inserción de registros en la colección 'Equipos'
testDB.Equipos.insert([
  {
    "Nombre": "Atlantico",
  "Plantilla": 14,
  "Titulares": 6,
  "Departamento": "Atlantico",
  "id_Equipo": 1
  },
  // ... (resto de los datos)
]);

//Comprobamos que se han almacenado los registros en la colección
testDB.Deportistas.count();
testDB.Equipos.count();
testDB.Entrenadores.count();
testDB.EncuentrosDeportivo.count();
testDB.Arbitros_Oficiales.count();

// Caso de Prueba 3: Comprobación de la Réplica en Nodos Secundarios
// Conexión al nodo secundario del grupo de réplica
connSecondary = new Mongo("LAPTOP-GUF5QK8F:20001 ") ;
secondaryTestDB = connSecondary.getDB("TorneoDeportivo");

// Comprobación si el nodo secundario es maestro
secondaryTestDB.isMaster();
//Activación del Nodo secundario
connSecondary.setSecondaryOk();

//Comprobación de la Réplica en Nodos Secundarios
// Conexión al nodo secundario del grupo de réplica
connSecondary = new Mongo("LAPTOP-GUF5QK8F:20002 ") ;
secondaryTestDB = connSecondary.getDB("TorneoDeportivo");

// Comprobación si el nodo secundario es maestro
secondaryTestDB.isMaster();

//Activación del Nodo secundario
connSecondary.setSecondaryOk();

// Caso de Prueba 4: Prueba de Conmutación por Error
// Detener específicamente el nodo primario para simular una caída
connPrimary = new Mongo("localhost:20000")
primaryDB = connPrimary.getDB("TorneoDeportiva");

// Comprobamos si este nodo es el primario antes de detenerlo
primaryDB.isMaster();

// Simulacion de caida del Nodo primario
primaryDB.adminCommand({shutdown : 1});

//Comprobamos si el nodo secundario ha asumido el rol de nodo primario
connNewPrimary = new Mongo("localhost:20001");
newPrimaryDB = connNewPrimary.getDB("Biblioteca"); 
newPrimaryDB.isMaster();

//Detenemos la replicación y el funcionamiento de todos los nodos
TorDepReplicaSet.stopSet();








