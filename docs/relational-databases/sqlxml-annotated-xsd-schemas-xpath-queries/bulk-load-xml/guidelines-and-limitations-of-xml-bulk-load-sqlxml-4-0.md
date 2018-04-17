---
title: Richtlinien und Einschränkungen von XML-Massenladen (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
ms.assetid: c5885d14-c7c1-47b3-a389-455e99a7ece1
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 24abfe07598e3bac0502189204fadf7ca0e9b349
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="guidelines-and-limitations-of-xml-bulk-load-sqlxml-40"></a>Richtlinien und Einschränkungen von XML-Massenladen (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Wenn Sie XML-Massenladen verwenden, sollten Sie mit den folgenden Richtlinien und Einschränkungen vertraut sein:  
  
-   Inlineschemas werden nicht unterstützt.  
  
     Wenn im XML-Quelldokument ein Inlineschema vorhanden ist, wird dieses Schema von XML-Massenladen ignoriert. Sie geben das Zuordnungsschema für XML-Massenladen außerhalb der XML-Daten an. Sie können nicht das Zuordnungsschema an einem Knoten angeben, indem die **Xmlns = "X: Schema"** Attribut.  
  
-   Es wird überprüft, ob ein XML-Dokument wohlgeformt ist, es wird jedoch nicht überprüft, ob es gültig ist.  
  
     XML-Massenladen überprüft, ob das XML-Dokument wohlgeformt ist, d. h. es wird sichergestellt, dass das XML-Dokument den Syntaxanforderungen der Empfehlung XML 1.0 des World Wide Web Consortium entspricht. Wenn das Dokument nicht wohlgeformt ist, wird die Verarbeitung durch XML-Massenladen abgebrochen und ein Fehler zurückgegeben. Die einzige Ausnahme hierbei stellen Dokumente dar, bei denen es sich um Fragmente handelt (wenn das Dokument beispielsweise kein einzelnes Stammelement aufweist). In diesem Fall wird das Dokument durch XML-Massenladen geladen.  
  
     XML-Massenladen überprüft das Dokument nicht im Hinblick auf XML-Daten oder DTD-Schemas, die in der XML-Datendatei definiert sind oder auf die in der XML-Datendatei verwiesen wird. XML-Massenladen überprüft die XML-Datendatei auch nicht im Hinblick auf das bereitgestellte Zuordnungsschema.  
  
-   Alle XML-Prologinformationen werden ignoriert.  
  
     XML-Massenladen ignoriert alle Informationen, die vor und nach der \<Root >-Elements im XML-Dokument. XML-Massenladen ignoriert beispielsweise sämtliche XML-Deklarationen, internen DTD-Definitionen, externen DTD-Verweise, Kommentare usw.  
  
-   Bei einem Zuordnungsschema, das eine Primärschlüssel-Fremdschlüssel-Beziehung zwischen zwei Tabellen (wie etwa zwischen den Tabellen Customer und CustOrder) definiert, muss die Tabelle mit dem Primärschlüssel im Schema zuerst beschrieben werden. Die Tabelle mit der Fremdschlüsselspalte muss später im Schema angezeigt werden. Der Grund dafür ist, dass die Reihenfolge, in der die Tabellen im Schema ermittelt werden, der Reihenfolge ab, das sie in der Datenbank laden. Beispielsweise wird das folgende XSD-Schema einen Fehler generiert, wenn es im XML-Massenladen verwendet wird, da die  **\<Reihenfolge >** Element wird beschrieben, bevor die  **\<Kunden >** Element. Die Spalte CustomerID in der Tabelle CustOrder ist eine Fremdschlüsselspalte, die auf die Primärschlüsselspalte CustomerID in der Tabelle Cust verweist.  
  
    ```  
    <?xml version="1.0" ?>  
    <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
            xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
            xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
        <ElementType name="Order" sql:relation="CustOrder" >  
          <AttributeType name="OrderID" />  
          <AttributeType name="CustomerID" />  
          <attribute type="OrderID" />  
          <attribute type="CustomerID" />  
        </ElementType>  
  
       <ElementType name="CustomerID" dt:type="int" />  
       <ElementType name="CompanyName" dt:type="string" />  
       <ElementType name="City" dt:type="string" />  
  
       <ElementType name="root" sql:is-constant="1">  
          <element type="Customers" />  
       </ElementType>  
       <ElementType name="Customers" sql:relation="Cust"   
                         sql:overflow-field="OverflowColumn"  >  
          <element type="CustomerID" sql:field="CustomerID" />  
          <element type="CompanyName" sql:field="CompanyName" />  
          <element type="City" sql:field="City" />  
          <element type="Order" >   
               <sql:relationship  
                   key-relation="Cust"  
                    key="CustomerID"  
                    foreign-key="CustomerID"  
                    foreign-relation="CustOrder" />  
          </element>  
       </ElementType>  
    </Schema>  
    ```  
  
-   Wenn das Schema keine überlaufspalten mithilfe der **Overflow-Feld** Anmerkung, XML-Massenladen ignoriert alle Daten, die in das XML-Dokument vorhanden ist, aber im Zuordnungsschema nicht beschrieben.  
  
     XML-Massenladen wendet das angegebene Zuordnungsschema an, sobald es im XML-Datenstrom auf bekannte Tags trifft. XML-Massenladen ignoriert Daten, die zwar im XML-Dokument vorhanden, im Schema jedoch nicht beschrieben sind. Nehmen wir beispielsweise an, Sie haben ein Zuordnungsschema, das beschreibt eine  **\<Kunden >** Element. Die XML-Datendatei verfügt über eine  **\<AllCustomers >** -Stammtag (das im Schema nicht beschrieben ist), die alle umschließt die  **\<Kunden >** Elemente:  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
      <Customer>...</Customer>  
       ...  
    </AllCustomers>  
    ```  
  
     In diesem Fall XML-Massenladen ignoriert die  **\<AllCustomers >** -Element und beginnt mit der Zuordnung an die  **\<Kunden >** Element. XML-Massenladen ignoriert die Elemente, die zwar im XML-Dokument vorhanden, im Schema jedoch nicht beschrieben sind.  
  
     Betrachten Sie eine andere XML-Quelldatendatei enthält, die  **\<Reihenfolge >** Elemente. Diese Elemente sind im Zuordnungsschema nicht beschrieben:  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
        <Order> ... </Order>  
        <Order> ... </Order>  
         ...  
      <Customer>...</Customer>  
        <Order> ... </Order>  
        <Order> ... </Order>  
         ...  
      ...  
    </AllCustomers>  
    ```  
  
     XML-Massenladen ignoriert diese  **\<Reihenfolge >** Elemente. Wenn Sie jedoch die **Overflow-Feld**-Anmerkung im Schema identifiziert eine Spalte als Überlaufspalte festlegen, XML-Massenladen speichert alle nicht verbrauchte Daten in dieser Spalte.  
  
-   CDATA-Abschnitte und Entitätsverweise werden vor dem Speichern in der Datenbank in das entsprechende Zeichenfolgenäquivalent übersetzt.  
  
     In diesem Beispiel umschließt ein CDATA-Abschnitt den Wert für die  **\<City >** Element. XML-Massenladen extrahiert den Zeichenfolgenwert ("NY"), bevor er fügt die  **\<City >** Element in der Datenbank.  
  
    ```  
    <City><![CDATA[NY]]> </City>  
    ```  
  
     XML-Massenladen behält Entitätsverweise nicht bei.  
  
-   Wenn in einem Zuordnungsschema der Standardwert eines Attributs angegeben ist, verwendet XML-Massenladen dieses Attribut, auch wenn das Attribut in den XML-Quelldaten nicht enthalten ist.  
  
     Das folgende Beispiel XDR-Schema weist einen Standardwert, der die **HireDate** Attribut:  
  
    ```  
    <?xml version="1.0" ?>  
    <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
            xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
            xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
       <ElementType name="root" sql:is-constant="1">  
          <element type="Customers" />  
       </ElementType>  
  
       <ElementType name="Customers" sql:relation="Cust3" >  
          <AttributeType name="CustomerID" dt:type="int"  />  
          <AttributeType name="HireDate"  default="2000-01-01" />  
          <AttributeType name="Salary"   />  
  
          <attribute type="CustomerID" sql:field="CustomerID" />  
          <attribute type="HireDate"   sql:field="HireDate"  />  
          <attribute type="Salary"     sql:field="Salary"    />  
       </ElementType>  
    </Schema>  
    ```  
  
     In dieser XML-Daten die **HireDate** Attribut fehlt in der zweiten  **\<Kunden >** Element. Wenn XML-Massenladen fügt den zweiten  **\<Kunden >** Element in der Datenbank, es wird der Standardwert verwendet, die im Schema angegeben wird.  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1" HireDate="1999-01-01" Salary="10000" />  
      <Customers CustomerID="2" Salary="10000" />  
    </ROOT>  
    ```  
  
-   Die **SQL: URL-codieren** Anmerkung wird nicht unterstützt:  
  
     Eine in der XML-Dateneingabe angegebene URL wird von Massenladen an diesem Speicherort nicht gelesen.  
  
     Die im Zuordnungsschema angegebenen Tabellen werden erstellt (die Datenbank muss vorhanden sein). Wenn mindestens eine der Tabellen in der Datenbank bereits vorhanden ist, bestimmt SGDropTables-Eigenschaft an, ob diese bereits vorhandenen Tabellen gelöscht und neu erstellt werden.  
  
-   Wenn Sie die Eigenschaft "schemagen" angeben (z. B. "schemagen" = "true"), werden die Tabellen, die im Zuordnungsschema identifiziert werden erstellt. "Schemagen" erstellt aber keinen Beschränkungen (z. B. die PRIMARY KEY/FOREIGN KEY-Einschränkungen) in diesen Tabellen mit einer Ausnahme: Wenn die XML-Knoten, die den Primärschlüssel in einer Beziehung bilden definiert sind, mit einem XML-Typ-ID (d. h. **Typ = "XSD: ID"** für XSD) SGUseID-Eigenschaft auf "true" für "schemagen" festgelegt ist, und werden nicht nur Primärschlüsseln aus erstellt. die ID eingegeben haben Knoten, aber Primär-/Fremdschlüssel-Beziehungen werden von mapping-Schema-Beziehungen erstellt.  
  
-   "Schemagen" verwendet keinen XSD-Schema-Facets und Erweiterungen zum Generieren des relationalen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Schema.  
  
-   Wenn Sie die Eigenschaft "schemagen" angeben (z. B. "schemagen" = "true") on Bulk Load, nur Tabellen (und nicht für Sichten von freigegebenen Namen), die angegeben werden, die aktualisiert werden.  
  
-   "Schemagen" bietet nur grundlegende Funktionalität für das Generieren des relationalen Schemas von XSD mit Anmerkungen. Der Benutzer muss die generierten Tabellen ggf. manuell ändern.  
  
-   In denen mehr als eine Beziehung zwischen Tabellen vorhanden ist, versucht "schemagen" eine Beziehung zu erstellen, die alle Beteiligten zwischen den beiden Tabellen Schlüssel enthält. Diese Einschränkung kann die Ursache eines [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Fehlers sein.  
  
-   Beim Massenladen von XML-Daten in eine Datenbank muss mindestens ein Attribut oder ein untergeordnetes Element im Zuordnungsschema vorhanden sein, das einer Datenbankspalte zugeordnet ist.  
  
-   Wenn Sie Datenwerte mithilfe von XML-Massenladen einfügen, müssen die Werte im Format (-)CCYY-MM-DD((+-)TZ) angegeben werden. Dies ist das XSD-Standardformat für das Datum.  
  
-   Einige Eigenschaftenflags sind mit anderen Eigenschaftenflags nicht kompatibel. Massenladen unterstützt beispielsweise keine **Ignoreduplicatekeys = True** zusammen mit **Keepidentity = False**. Wenn **Keepidentity = False**, Massenladen erwartet, dass den Server die Schlüsselwerte zu generieren. Tabellen müssen eine **Identität** Einschränkung für den Schlüssel. Der Server generiert keine doppelten Schlüssel, was bedeutet, besteht keine Notwendigkeit für **Ignoreduplicatekeys** festzulegende **"true"**. **IgnoreDuplicateKeys** sollte festgelegt werden, um **"true"** nur beim Hochladen der Primärschlüsselwerte aus den empfangenen Daten in eine Tabelle mit Zeilen und es besteht die Gefahr der Primärschlüsselwerte Konflikt.  
  
  
