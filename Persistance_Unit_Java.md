# Persistance Unit / Entity Manager

## Allgemein

Für unser vorgehen benötigen wir bestimmte Datentypen.

* EntityManager

  * > An `EntityManager` instance is associated with a persistence context. A persistence context is a set of entity instances in which for any persistent entity identity there is a unique entity instance. Within the persistence context, the entity instances and their lifecycle are managed. The `EntityManager` API is used to create and remove persistent entity instances, to find entities by their primary key, and to query over entities. [1]

* EntityManagerFactory

  * >The main role of an `EntityManagerFactory` instance is to support instantiation of [EntityManager](http://www.javaguides.net/2018/12/jpa-entitymanager-interface-with-example.html) instances. An `EntityManagerFactory` is constructed for a specific database, and by managing resources efficiently (e.g. a pool of sockets), it provides an efficient way to construct multiple [EntityManager](http://www.javaguides.net/2018/12/jpa-entitymanager-interface-with-example.html) instances for that database. [2]

* Logger

  * > This is the central class in the log4j package. Most logging operations, except configuration, are done through this class. [3]

```java
private static final Logger log = Logger.getLogger(Main.class);
private static EntityManagerFactory sessionFactory;
@PersistenceContext
private static EntityManager entitymanager;
```

## Mit der PersistanceUnit arbeiten

```java
try {
    // Erstellt eine Session mit dem namen 'westbahn'
    sessionFactory = Persistence.createEntityManagerFactory("westbahn");
    // Erstellt einen entitymanager mit welchen man weiter arbeiten kann
    entitymanager = sessionFactory.createEntityManager();
    // Ist eine 'selbst' erstellte Methode, welche die DB mit Werten befüllt
    fillDB(entitymanager);
    log.setLevel(Level.OFF);
    log.setLevel(Level.ALL);

} catch (ParseException e) {
    e.printStackTrace();
} catch (Exception e) {
    e.printStackTrace();
} finally {
    //Schließt alle offenen Sessions
    if (entitymanager.getTransaction().isActive())
        entitymanager.getTransaction().rollback();
    entitymanager.close();
    sessionFactory.close();
}    
```

## Logger ausschalten

Damit unsere Ausgabe mit keinen weiteren unwichtigen Meldungen versehen wird können wir die Level des Loggers ausschalten. Dies habe ich in der `main`-Methode.

```java
Logger.getLogger("org.hibernate").setLevel(Level.OFF);
Logger.getLogger("org.jboss.logging").setLevel(Level.OFF);
```

## CRUD

CRUD [4,5]

* **C**reate -- Eine Methode die uns ermöglicht Entitäten zu erstellen
  
    * Im EntityMangaer (Wird auch Storing genannt)
    
      * ```java
        //Zuerst muss man eine Transaktion staren 
        em.getTransaction().begin();
        //Für unser Beispiel werden diese Objekte gepseichert
        List<Benutzer> bList = new ArrayList<Benutzer>();
        		bList.add(new Benutzer("David", "Kupert","dkupert@student.tgm.ac.at","123","+4369910207761"));
        		bList.add(new Benutzer("Cayan", "Ayik","cayik@student.tgm.ac.at","123","+4369910207761"));
        		bList.add(new Benutzer("Klemens", "Meyer","kmeyer@student.tgm.ac.at","123","+4369910207761"));
        		bList.add(new Benutzer("Chris", "Haslinger","chaslinger@student.tgm.ac.at","123","+4369910207761"));
        
        //Mit persist kann man die Daten speichern
        
        for (Benutzer be : bList)
        			em.persist(be);
        
        //Nun muss man die Daten synchronisieren
        
        em.flush();
        
        //Transaktion beenden
        
        em.getTransaction().commit();
        ```
    
  
* **R**ead -- Eine Methode die uns ermöglicht Entitäten zu lesen

  * Im EntityMangaer (Wird auch Retrieving  genannt)

    * ```java
       Employee employee = em.getReference(Employee.class, 1);
      ```
      
* Hier ist es Wichtig zu schauen ob die gewählte Klasse eine Entität ist.
    
* Kann der EntitiyManager  kein Objekt finden übergibt er null
  
* **U**pdate -- Eine Methode die uns ermöglicht Entitäten zu verändern

  * Im EntityMangaer

    * ```java
      //Das gewünschte Objekt retrieven
      Employee employee = em.find(Employee.class, 1);
      //Transaktion starten 
      em.getTransaction().begin();
      //Mittels setter ein Attribut ändern
      employee.setNickname("Joe the Plumber");
      //Transaktion beenden
      em.getTransaction().commit();
      ```

* **D**elete -- Eine Methode die uns ermöglicht Entitäten zu löschen

  * Im EntityManager

    * ```java
      //Das gewünschte Objekt retrieven
      Employee employee = em.find(Employee.class, 1);
      //Transaktion starten
      em.getTransaction().begin();
      //Das Objekt mit der Remove Methode entfernen
      em.remove(employee);
      //Transaktion beenden
      em.getTransaction().commit();
      ```

## Daten anlegen

```java
//Zuerst muss man die Transaktion starten damit Dinge einspeichern kann
em.getTransaction().begin();
//Diese Liste beinhaltet alle Objekte, welche wir speichern möchten
List<Bahnhof> list = new ArrayList<Bahnhof>();
list.add(new Bahnhof("WienHbf", 0, 0, 0, true));
list.add(new Bahnhof("SalzburgHbf", 20, 60, 120, true));
list.add(new Bahnhof("Amstetten", 40, 124, 169, false));
list.add(new Bahnhof("Linz-Ost", 140, 320, 250, false));
list.add(new Bahnhof("Huetteldorf", 3, 5, 19, false));
list.add(new Bahnhof("Wels-Zentrum", 102, 400, 250, true));
//Geht jedes Element der Liste durch
for (Bahnhof b : list)
    //Gibt an das die Objekte der Liste persistiert werden
    em.persist(b);
//Synchronisieret den Persistenzkontext mit der zugrunde liegenden Datenbank
em.flush();
//commited die Transaktion
em.getTransaction().commit();
```

## Quellen

[1] : "JPA Hibernate persistence context" [online](https://www.baeldung.com/jpa-hibernate-persistence-context) |zuletzt besucht 28.04.2020

[2] : "jpa-entitymanagerfactory-interface" [online](jpa-entitymanagerfactory-interface) | zuletzt besucht 28.04.2020

[3] : "Class Logger" [online](https://logging.apache.org/log4j/1.2/apidocs/org/apache/log4j/Logger.html) | zuletzt besucht 28.04.2020

[4] : "What is CRUD" [online](https://www.codecademy.com/articles/what-is-crud) | zuletzt besucht 01.04.2020

[5] : "CRUD Operations with JPA" [online](https://www.objectdb.com/java/jpa/persistence/crud) | zuletzt besucht 28.04.2020