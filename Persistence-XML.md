# Persistence.xml

### generelle Struktur

Persistence units werden in einer persistence.xml-Datei definiert, die sich im Verzeichnis META-INF im Klassenpfad befinden muss. Eine persistence.xml-Datei kann Definitionen für eine oder mehrere Persistence units enthalten. Die tragbare Methode zum Instanziieren einer EntityManagerFactory in JPA erfordert eine Persistence unitst. [1]

```xml
<persistence xmlns="http://xmlns.jcp.org/xml/ns/persistence" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence
             http://xmlns.jcp.org/xml/ns/persistence/persistence_2_1.xsd"
  version="2.1">

  <!-- Hier wird der name der UNIT bestimmt -->
  <persistence-unit name="westbahn">
    <description> Hibernate JPA Configuration Example</description>
    <provider>org.hibernate.jpa.HibernatePersistenceProvider</provider>

      <!-- TODO List all perstiting Classdefinitions -->
    <properties>
      <!--
      <property name="javax.persistence.jdbc.driver" value="com.mysql.cj.jdbc.Driver" />
      <property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost:3306/westbahn?serverTimezone=UTC" />
      <property name="javax.persistence.jdbc.user" value="westbahnUser" />
      <property name="javax.persistence.jdbc.password" value="westbahnPassword" />
      -->    
      <property name="javax.persistence.jdbc.driver" value="org.h2.Driver" />
      <property name="javax.persistence.jdbc.url"    value="jdbc:h2:file:./db/testing" />
      <property name="javax.persistence.jdbc.user" value="sa" />
      <property name="javax.persistence.jdbc.password" value="" />
      <property name="hibernate.dialect" value="org.hibernate.dialect.H2Dialect"/>
  
      <property name="hibernate.show_sql" value="false" />
      <property name="hibernate.hbm2ddl.auto" value="create-drop" />
    
    </properties>

  </persistence-unit>

</persistence>
```

Beschreibung der einzelnen Tags.

- The provider element indicates which JPA implementation should be used. ObjectDB is represented by the `com.objectdb.jpa.Provider` string. If not specified, the first JPA implementation that is found is used.
- The mapping-file elements specify XML mapping files that are added to the default `META-INF/orm.xml` mapping file. Every annotation that is described in this manual can be replaced by equivalent XML in the mapping files (as explained below).
- The `jar-file` elements specify JAR files that should be searched for managed persistable classes.
- The `class` elements specify names of managed persistable classes (see below).
- The `property` elements specify general properties. JPA 2 defines standard properties for specifying database url, username and password, as demonstrated above.

### weitere Klassen hinzufügen

```xml
<!-- wenn die Entiät in einer separaten XML-Datei beschrieben wurde -->
<mapping-file>/META-INF/Reservierungen.xml</mapping-file>
<!-- wenn die Entität mir Annotation definiert wurde -->
<class>model.Bahnhof</class>
<class>model.Benutzer</class>
<class>model.Einzelticket</class>
<class>model.Sonderangebot</class>
<class>model.Strecke</class>
<class>model.Zeitkarte</class>
<class>model.Zug</class>
```

## Quellen

[1] "JPA Persistence Unit" [online](https://www.objectdb.com/java/jpa/entity/persistence-unit#persistence.xml) | zuletzt besucht 28.04.2020

