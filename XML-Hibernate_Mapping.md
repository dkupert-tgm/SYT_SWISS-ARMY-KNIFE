# XML Hibernate Mapping

## generelle Struktur

Der Grundaufbau der XML-Datei ist relativ simpel. [1]

```xml
<!-- Allgemeine struktur -->
<!-- Definiert die kodierung -->
<?xml version = "1.0" encoding = "utf-8"?>
<!-- definiert den DOCTYPE muss die Datei auf wohlgeformtheit zu überprüfen -->
<!DOCTYPE hibernate-mapping PUBLIC
        "-//Hibernate/Hibernate Mapping DTD//EN"
        "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd">
<!--Hier fängt das eigentliche Mapping an-->
<hibernate-mapping>
    <!-- Zuerst wird der Name der zugehörigen Klasse und auch der Tabellen name angegeben-->
    <class name = "model.Reservierung" table = "Reservierung">
        <!-- Hier kann (muss nicht) eine Beschreibung der Tabelle geschrieben werden-->
        <meta attribute = "class-description">
            DESC
        </meta>
    </class>
</hibernate-mapping>
```

## ID

Die ID wird im Klassen Tag definiert.

```xml
<!-- Wenn die Entität eine ID besitzt muss man diese mit folgeden Attribut definieren-->
<id name = "ID" type = "long" column = "id">
    <!-- Hier wird angegeben wie diese ID generiert werden soll -->
    <generator class="native"/>
</id>
```

## Property

Mit dem Property-Tag werden wie beim `@Column` Attribute bestimmt

```xml
<property name = "datum" column = "datum" type = "java.util.Date"/>
<property name = "praemienMeilenBonus" column = "praemienMeilenBonus" type = "int"/>
<property name = "preis" column = "preis" type = "int"/>
```

### ENUMS

Bei enums muss man des weiteren, die Typen bestimmen (Klasse).

```xml
<property name="status" column="status">
    <type name="model.StatusInfo">
        <param name="enumClass">model.StatusInfo</param>
    </type>
</property>
```

#### Foreign Key

```xml
<!-- Foreign keys -->
<!-- One to One -->
<one-to-one name="name" class="model.name"></one-to-one>
<!-- Many to One -->
<many-to-one name="name" class="model.name" column="name"/>
```

## Query

Wenn man eine Query in einer XML-Mapping bestimmen muss, sollte man nach dem `<class>`-Tag ein `<query>` mit einem bestimmten namen definieren.

```xml
<query name="Reservierung.findUserEmail">
    SELECT r FROM Reservierung r WHERE r.benutzer.eMail = :email
</query>
```

## Quellen

[1] : "JPA Persistence Unit Using ORM.xml Mapping Files" [online](https://webdev.jhuep.com/~jcs/ejava-javaee/coursedocs/605-784-site/docs/content/html/hibernate-migration-orm.html) | zuletzt besucht 28.04.2020