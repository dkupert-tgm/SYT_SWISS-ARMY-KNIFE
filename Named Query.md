# Named Query

Für eine Query-Abfrage gibt es 2 Möglichkeit dies in Hibernate zu unternehmen. [1]

* native SQL
* Hibernate Query Language (HQL)

### Native SQL

#### Scalar Query

Die grundlegendste SQL-Abfrage besteht darin, eine Liste von Skalaren (Werten) aus einer oder mehreren Tabellen abzurufen. Im Folgenden finden Sie die Syntax für die Verwendung von nativem SQL für skalare Werte[1]

```java
String sql = "SELECT first_name, salary FROM EMPLOYEE";
SQLQuery query = session.createSQLQuery(sql);
query.setResultTransformer(Criteria.ALIAS_TO_ENTITY_MAP);
List results = query.list();
```

#### Entity Query

Bei den obigen Abfragen ging es ausschließlich um die Rückgabe von Skalarwerten, im Grunde genommen um die Rückgabe der "rohen" Werte aus der Ergebnismenge. Im Folgenden finden Sie die Syntax zum Abrufen von Entitätsobjekten als Ganzes aus einer nativen SQL-Abfrage über addEntity (). [1]

```java
String sql = "SELECT * FROM EMPLOYEE";
SQLQuery query = session.createSQLQuery(sql);
query.addEntity(Employee.class);
List results = query.list();
```

#### Named SQL Queries

Im Folgenden finden Sie die Syntax zum Abrufen von Entitätsobjekten aus einer nativen SQL-Abfrage über addEntity () und unter Verwendung einer benannten SQL-Abfrage. [1]

```java
String sql = "SELECT * FROM EMPLOYEE WHERE id = :employee_id";
SQLQuery query = session.createSQLQuery(sql);
query.addEntity(Employee.class);
query.setParameter("employee_id", 10);
List results = query.list();
```

### HQL

Hibernate Query Language (HQL) ist eine objektorientierte Query Language ähnlich wie SQL, aber anstatt Tabellen und Spalten zu bearbeiten, arbeitet HQL mit persistenten Objekten und ihren Eigenschaften. HQL-Abfragen werden von Hibernate in herkömmliche SQL-Abfragen übersetzt, die wiederum Aktionen für die Datenbank ausführen. 

Bei Schlüsselwörtern wie SELECT, FROM und WHERE usw. wird nicht zwischen Groß- und Kleinschreibung unterschieden, bei Eigenschaften wie Tabellen- und Spaltennamen wird in HQL zwischen Groß- und Kleinschreibung unterschieden. [2]

### Query Schreibweise

Anders als beim normalen SQL kann man beim HQL keinen Stern benutzen. Man arbeitet mit einem placeholder, der name ist egal. [3,4]

```sql
SELECT b FROM Benutzer b
```

Da wir mit Objekten arbeiten können wir auch auf die Attribute der Objekte zugreifen 

```sql
SELECT b.tickets.strecke.id FROM Benutzer b
```

#### Achtung

Bei einer OneToOne Beziehung kann man nicht direkt auf die Attribute des Objektes zugreifen 

Natürlich kann man auch Parameter bestimme, welche vom Programm ausgefüllt werden.

```sql
SELECT b from Benutzer b WHERE b.eMail = :mail
```

### Definition der Named Query (Java)

Vor dem Klassennamen muss man eine Name Query @Annotation erstellen. Wie oben erwähnt gibt es mehrere Möglichkeiten eine Query Abfrage zu gestalten in unseren Beispielen befassen wir und mit der HQL [3,4]

```java
@Entity
@NamedQueries ({@NamedQuery(name="Benutzer.getReservierungen",query="SELECT b from Benutzer b WHERE b.eMail = :mail"),
				@NamedQuery(name="Benutzer.getMonatskarten",query="SELECT b from Benutzer b WHERE b.tickets.typ = 'MONATSKARTE'")})
public class Benutzer {
```

### Definition der Named Query (XML)

```xml
</class>

<query name="Reservierung.findUserEmail">
    SELECT r FROM Reservierung r WHERE r.benutzer.eMail = :email
</query>

</hibernate-mapping>
```

### Abfragen in der Main

```java
//Die named Query mit dem namen 'Benutzer.getMonatskarten' wird ausgeführt
Query q = entitymanager.createNamedQuery("Benutzer.getMonatskarten");
//Die Ergebnisse der Abfrage werde in der Date gepseichert
List<?> l = q.getResultList();
for (Object b : l) {
    Benutzer ben = null;
    //Es wird überprüft ob die Ergebnisse der Abfrage unseren gewünschten Datentyp enstprechen
    if (b instanceof Benutzer) {
        //Es wird gecastet
        ben = (Benutzer) b;
        System.out.println("Benutzer: " + ben.getNachName());
    }
}
```

##### Mit Parametern in der Main arbeiten

```java
Query q = entitymanager.createNamedQuery("Reservierung.findUserEmail");
q.setParameter("email", "dkupert@student.tgm.ac.at");
List<?> l = q.getResultList();
for (Object b : l) {
    Reservierung ben = null;
    if (b instanceof Reservierung) {
        ben = (Reservierung) b;
        System.out.println("Reservierungen: "+ben.getDatum() +": "+ ben.getBenutzer().getNachName() + ":" + ben.getStrecke().getID());
    }
}
```

## Quellen

[1] : "Hibernate native SQL" : [online](https://www.tutorialspoint.com/hibernate/hibernate_native_sql.htm) | zuletzt besucht 28.04.2020

[2] : "Hibernate Query Language" [online](https://www.tutorialspoint.com/hibernate/hibernate_query_language.htm)  | zuletzt besucht 28.04.2020

[3] : "JPA Named Queries" : [online](https://www.objectdb.com/java/jpa/query/named) | zuletzt besucht 28.04.2020

[4] : "JPA Criteria API Queries" [online](https://www.objectdb.com/java/jpa/query/criteria) | zuletzt besucht 28.04.2020