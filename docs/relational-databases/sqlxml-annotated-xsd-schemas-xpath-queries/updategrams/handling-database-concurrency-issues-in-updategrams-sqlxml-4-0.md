---
title: "Behandeln von Parallelitätsproblemen in Updategrams (SQLXML 4.0) Datenbank | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- <before> block
- low concurrency protection
- database concurrency [SQLXML]
- timestamp column [SQLXML]
- updategrams [SQLXML], database concurrency
- high concurrency protection [SQLXML]
- optimistic concurrency control
- concurrency [SQLXML]
- intermediate concurrency protection [SQLXML]
ms.assetid: d4b908d1-b25b-4ad9-8478-9cd882e8c44e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e19d8397d59b4c85d60593c63faa5bc6f0f2ea4
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="handling-database-concurrency-issues-in-updategrams-sqlxml-40"></a>Behandlungsdatenbankparallelität gibt in Updategrams (SQLXML 4.0) heraus
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Wie andere Datenbankupdatemechanismen müssen Updategrams gleichzeitige Updates von Daten in einer Mehrbenutzerumgebung verarbeiten können. Updategrams verwenden die Steuerung durch vollständige Parallelität, bei der ausgewählte Felddaten als Momentaufnahmen verglichen werden, um sicherzustellen, dass die zu aktualisierenden Daten seit ihrem letzten Abruf aus der Datenbank nicht von einer anderen Benutzeranwendung geändert wurden. Updategrams schließen diese momentaufnahmewerte in den  **\<vor >** -Block der Updategrams. Vor dem Aktualisieren der Datenbank, überprüft das Updategram die Werte, die im angegebenen der  **\<vor >** Block für den aktuellen Werten in der Datenbank, um sicherzustellen, dass das Update gültig ist.  
  
 Die Steuerung durch vollständige Parallelität bietet drei Ebenen des Schutzes in einem Updategram: Niedrig (kein), mittel und hoch. Sie können entscheiden, welche Ebene des Schutzes Sie benötigen, indem Sie das Updategram entsprechend festlegen.  
  
## <a name="lowest-level-of-protection"></a>Niedrigste Ebene des Schutzes  
 Diese Ebene ist ein blindes Update, bei dem das Update ohne Verweis auf andere Updates verarbeitet wird, die seit dem letzten Lesen der Datenbank vorgenommen wurden. In einem solchen Fall geben Sie nur die Primärschlüsselspalte(n) in der  **\<vor >** -Block an, um den Datensatz zu identifizieren, und geben Sie die aktualisierte Informationen in den  **\<nach >** Block.  
  
 Die neue Telefonnummer des Kontakts im folgenden Updategram ist beispielsweise korrekt, unabhängig davon, welche Telefonnummer davor verwendet wurde. Beachten Sie, dass der  **\<vor >** -Block gibt nur die Primärschlüsselspalte (ContactID).  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" />  
</updg:before>  
<updg:after>  
   <Person.Contact ContactID="1" Phone="111-111-1111" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="intermediate-level-of-protection"></a>Mittlere Ebene des Schutzes  
 Bei dieser Ebene des Schutzes vergleicht das Updategram die aktuellen Werte der Daten, die mit den Werten in den Datenbankspalten aktualisiert werden, um sicherzustellen, dass die Werte seit dem Lesen des Datensatzes durch Ihre Transaktion durch keine andere Transaktion geändert wurden.  
  
 Sie können dieses Maß an Schutz abrufen, indem Sie angeben, die Primärschlüsselspalte(n) und die Spalte(n), die Sie aktualisieren die  **\<vor >** Block.  
  
 Bei diesem Updategam wird beispielsweise der Wert in der Spalte Phone der Tabelle Person.Contact für den Kontakt mit der ContactID 1 geändert. Die  **\<vor >** -Block gibt die **Phone** Attribut, um sicherzustellen, dass der Wert dieses Attributs den Wert in der entsprechenden Spalte in der Datenbank entspricht, bevor der aktualisierte Wert angewendet .  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" Phone="398-555-0132" />  
</updg:before>  
<updg:after>  
   <Person.Contact ContactID="1" Phone="111-111-1111" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="high-level-of-protection"></a>Höchste Ebene des Schutzes  
 Eine hohe Ebene des Schutzes stellt sicher, dass der Datensatz seit dem letzten Lesen dieses Datensatzes durch Ihre Anwendung gleich geblieben ist (d. h. seitdem Ihre Anwendung den Datensatz gelesen hat, wurde er von keiner anderen Transaktion geändert).  
  
 Es gibt zwei Methoden, diese hohe Ebene des Schutzes gegen gleichzeitige Updates zu erreichen:  
  
-   Geben Sie zusätzliche Spalten in der Tabelle in der  **\<vor >** Block.  
  
     Wenn Sie angeben, dass zusätzliche Spalten in der  **\<vor >** Block, das Updategram vergleicht die Werte, die für diese Spalten mit den Werten angegeben werden, die in der Datenbank wurden vor dem Anwenden des Updates. Wenn eine der Datensatzspalten seit dem letzten Lesen des Datensatzes durch Ihre Transaktion geändert wurde, wird das Update vom Updategram nicht durchgeführt.  
  
     Z. B. das folgende Updategram aktualisiert den schichtnamen, sondern zusätzliche Spalten (StartTime, EndTime) in der  **\<vor >** Block, wodurch ein höheres Maß an Schutz vor gleichzeitigen anfordern aktualisiert.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="1"   
                 Name="Day"   
                 StartTime="1900-01-01 07:00:00.000"   
                 EndTime="1900-01-01 15:00:00.000" />  
    </updg:before>  
    <updg:after>  
       <HumanResources.Shift Name="Morning" />  
    </updg:after>  
    </updg:sync>  
    </ROOT>  
    ```  
  
     In diesem Beispiel gibt das höchste Maß an Schutz durch Angabe alle Spaltenwerte für den Datensatz in die  **\<vor >** Block.  
  
-   Geben Sie die Timestamp-Spalte (falls vorhanden) in der  **\<vor >** Block.  
  
     Statt alle Datensatzspalten im anzugeben der  **\<vor**>-Block können nur Geben Sie die Timestamp-Spalte (falls die Tabelle vorhanden) zusammen mit den Primärschlüsselspalte(n) im die  **\<vor >** Block. Die Datenbank aktualisiert nach jedem Update des Datensatzes die timestamp-Spalte auf einen eindeutigen Wert. In diesem Fall vergleicht das Updategram den Wert des Timestamps mit dem zugehörigen Wert in der Datenbank. Der in der Datenbank gespeicherte Timestampwert ist ein Binärwert. Aus diesem Grund muss die Timestamp-Spalte angegeben werden, im Schema als **dt:type="bin.hex"**, **dt:type="bin.base64"**, oder **SQL: datatype = "Timestamp"**. (Geben Sie entweder die **Xml** -Datentyp oder die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp.)  
  
#### <a name="to-test-the-updategram"></a>So testen Sie das Updategram  
  
1.  Erstellen Sie diese Tabelle in der **Tempdb** Datenbank:  
  
    ```  
    USE tempdb  
    CREATE TABLE Customer (  
                 CustomerID  varchar(5),  
                 ContactName varchar(20),  
                 LastUpdated timestamp)  
    ```  
  
2.  Fügen Sie diesen Beispieldatensatz hinzu:  
  
    ```  
    INSERT INTO Customer (CustomerID, ContactName) VALUES   
                         ('C1', 'Andrew Fuller')  
    ```  
  
3.  Kopieren Sie das folgende XSD-Schema, und fügen Sie es in den Editor ein. Speichern Sie es unter dem Namen ConcurrencySampleSchema.xml:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="Customer" sql:relation="Customer" >  
       <xsd:complexType>  
            <xsd:attribute name="CustomerID"    
                           sql:field="CustomerID"   
                           type="xsd:string" />   
  
            <xsd:attribute name="ContactName"    
                           sql:field="ContactName"   
                           type="xsd:string" />  
  
            <xsd:attribute name="LastUpdated"   
                           sql:field="LastUpdated"   
                           type="xsd:hexBinary"   
                 sql:datatype="timestamp" />  
  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
4.  Kopieren Sie den folgenden Updategramcode in Editor, und speichern Sie ihn unter dem Namen ConcurrencySampleTemplate.xml im selben Verzeichnis, in dem Sie das im vorherigen Schritt erstellte Schema gespeichert haben. (Beachten Sie, dass der unten aufgeführte Timestampwert für LastUpdated sich von dem in Ihrer Customer-Tabelle unterscheidet. Kopieren Sie daher den tatsächlichen Wert für LastUpdated aus der Tabelle, und fügen Sie ihn in das Updategram ein.)  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync mapping-schema="SampleSchema.xml" >  
    <updg:before>  
       <Customer CustomerID="C1"   
                 LastUpdated = "0x00000000000007D1" />  
    </updg:before>  
    <updg:after>  
       <Customer ContactName="Robert King" />  
    </updg:after>  
    </updg:sync>  
    </ROOT>  
    ```  
  
5.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Dies ist das entsprechende XDR-Schema:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<ElementType name="Customer" sql:relation="Customer" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="ContactName" />  
    <AttributeType name="LastUpdated"  dt:type="bin.hex"   
                                       sql:datatype="timestamp" />  
    <attribute type="CustomerID" />  
    <attribute type="ContactName" />  
    <attribute type="LastUpdated" />  
</ElementType>  
</Schema>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheitsüberlegungen zu Updategrams &#40; SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
