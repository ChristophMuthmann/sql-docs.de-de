---
title: Aktualisieren von Daten mit XML-Updategrams (SQLXML 4.0) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- IDREF type attribute [SQLXML]
- before attribute
- <sync> block
- <after> block
- id attribute
- <before> block
- updg:after attribute
- mapping-schema attribute
- IDREFS type attribute [SQLXML]
- updg:id attribute
- multiple record updates
- after attribute
- updategrams [SQLXML], updating data
- updg:before attribute
- record updates [SQLXML]
ms.assetid: 90ef8a33-5ae3-4984-8259-608d2f1d727f
caps.latest.revision: "28"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8c6ff13edf01370778da9361d5834e70ebfdb20a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="updating-data-using-xml-updategrams-sqlxml-40"></a>Aktualisieren von Daten mit XML-Updategrams (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Wenn Sie vorhandene Daten aktualisieren, müssen Sie angeben, sowohl die  **\<vor >** und  **\<nach >** blockiert. Die Elemente im angegebenen der  **\<vor >** und  **\<nach >** Blöcke beschreiben die gewünschte Änderung. Verwendet das Updategram die angegebene(n) Element(e), werden die  **\<vor >** Block, um die vorhandene Datensätze in der Datenbank zu identifizieren. Die entsprechenden Elemente in der  **\<nach >** -Block zeigen an, wie die Datensätze nach Ausführen des Updatevorgangs aussehen soll. Aus diesen Informationen erstellt das Updategram eine SQL-Anweisung, die entspricht der  **\<nach >** Block. Das Updategram verwendet dann diese Anweisung, um die Datenbank zu aktualisieren.  
  
 Dies ist das Updategramformat für einen Updatevorgang:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync [mapping-schema="SampleSchema.xml"]  >  
   <updg:before>  
      <ElementName [updg:id="value"] .../>  
      [<ElementName [updg:id="value"] .../> ... ]  
   </updg:before>  
   <updg:after>  
      <ElementName [updg:id="value"] ... />  
      [<ElementName [updg:id="value"] .../> ...]  
   </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 **\<Updg: vor dem >**  
 Die Elemente in der  **\<vor >** -Block identifizieren vorhandene Datensätze in den Datenbanktabellen.  
  
 **\<Updg: Nachdem >**  
 Die Elemente in der  **\<nach >** Block wird beschrieben, wie die Datensätze im angegebenen der  **\<vor >** Block sollte so aussehen, nachdem die Updates angewendet wurden.  
  
 Die **Zuordnungsschema** Attribut identifiziert das Zuordnungsschema vom Updategram verwendet werden. Wenn das Updategram ein Zuordnungsschema angibt, die Element- und Attributnamen Namen angegeben, der  **\<vor >** und  **\<nach >** -Blöcke müssen den Namen im Schema übereinstimmen. Das Zuordnungsschema ordnet diese Element- oder Attributnamen der Datenbanktabelle und den Spaltennamen zu.  
  
 Wenn ein Updategram kein Schema angibt, verwendet das Updategram die Standardzuordnung. Im Standardmodus zuordnen, die  **\<ElementName >** in der Updategram Karten der Datenbanktabelle und die untergeordneten Elemente oder Attribute den Datenbankspalten angegeben.  
  
 Ein Element in der  **\<vor >** Block muss mit nur einer Tabellenzeile in der Datenbank übereinstimmen. Wenn das Element entweder mehreren Tabellenzeilen entspricht oder keiner Tabellenzeile stimmt nicht überein, wird das Updategram einen Fehler zurück und bricht die gesamte  **\<Sync >** Block.  
  
 Ein Updategram kann mehrere enthalten  **\<Sync >** blockiert. Jede  **\<Sync >** Block wird als Transaktion behandelt. Jede  **\<Sync >** Block kann verfügen über mehrere  **\<vor >** und  **\<nach >** blockiert. Beispielsweise, wenn Sie zwei der vorhandenen Datensätze aktualisieren, geben Sie zwei  **\<vor >** und  **\<nach >** -Paare an, eine für jeden zu aktualisierenden Datensatz.  
  
## <a name="using-the-updgid-attribute"></a>Verwenden des updg:id-Attributs  
 Wenn mehrere Elemente angegeben werden, der  **\<vor >** und  **\<nach >** -Blöcke verwenden die **updg: ID** -Attribut markieren von Zeilen in der  **\<vor >** und  **\<nach >** blockiert. Die Verarbeitungslogik verwendet diese Informationen, um zu bestimmen, welcher Datensatz den  **\<vor >** -Block zu welchem Datensatz der  **\<nach >** Block.  
  
 Die **updg: ID** Attribut ist nicht notwendig (aber empfohlen), wenn eines der folgenden vorhanden ist:  
  
-   Die Elemente im angegebenen Zuordnungsschema verfügen über die **SQL: Key-Felder** Attribut definiert werden.  
  
-   Ein oder mehrere bestimmte Werte sind für das Schlüsselfeld oder die Schlüsselfelder im Updategram angegeben.  
  
 Wenn entweder der Fall ist, verwendet das Updategram die Schlüsselspalten, die im angegebenen der **SQL: Key-Felder** auf die Elemente in der  **\<vor >** und  **\< Nachdem >** blockiert.  
  
 Wenn das Zuordnungsschema keine Schlüsselspalten identifiziert (mit **SQL: Key-Felder**) oder wenn das Updategram einen schlüsselspaltenwert aktualisiert wird, müssen Sie angeben **updg: ID**.  
  
 Die Einträge, die im angegebenen der  **\<vor >** und  **\<nach >** Blöcke müssen nicht in derselben Reihenfolge befinden. Die **updg: ID** -Attribut erzwingt die Zuordnung zwischen den Elementen, die im angegebenen der  **\<vor >** und  **\<nach >** blockiert werden.  
  
 Wenn Sie angeben, dass ein Element in der  **\<vor >** Block und nur ein entsprechendes Element in der  **\<nach >** mit blockiert **updg: ID** ist nicht erforderlich. Es wird jedoch empfohlen, die Angabe **updg: ID** trotzdem um Mehrdeutigkeiten zu vermeiden.  
  
## <a name="examples"></a>Beispiele  
 Bevor Sie die Updategrambeispiele verwenden, beachten Sie Folgendes:  
  
-   Die meisten der Beispiele verwenden die Standardzuordnung (d. h. es ist kein Zuordnungsschema im Updategram angegeben). Weitere Beispiele für Updategrams, die Zuordnungsschemas verwenden, finden Sie unter [ein Mapping-Schema mit Anmerkungen angeben, in einem Updategram &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
-   Die meisten der Beispiele verwenden die AdventureWorks-Beispieldatenbank. Alle Updates werden für die Tabellen in dieser Datenbank übernommen. Sie können die AdventureWorks-Datenbank wiederherstellen.  
  
### <a name="a-updating-a-record"></a>A. Aktualisieren eines Datensatzes  
 Das folgende Updategram aktualisiert den Nachnamen des Mitarbeiters in der Person.Contact-Tabelle in der AdventureWorks-Datenbank zu "Fuller". Das Updategram gibt kein Zuordnungsschema an, deswegen verwendet das Updategram die Standardzuordnung.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" />  
</updg:before>  
<updg:after>  
   <Person.Contact LastName="Abel-Achong" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 Der Datensatz beschrieben, der  **\<vor >** Block stellt den aktuellen Datensatz in der Datenbank. Das Updategram verwendet alle im angegebenen Spaltenwerte der  **\<vor >** Block, um den Datensatz zu suchen. In diesem Updategram der  **\<vor >** Block stellt nur die ContactID-Spalte; aus diesem Grund verwendet das Updategram nur den Wert für den Datensatz zu suchen. Wenn Sie diesem Block den LastName-Wert hinzufügen würden, würde das Updategram sowohl den ContactID- als auch den LastName-Wert für die Suche verwenden.  
  
 In diesem Updategram der  **\<nach >** Block enthält nur den LastName-Spaltenwert, da dies der einzige Wert ist, die geändert wird.  
  
##### <a name="to-test-the-updategram"></a>So testen Sie das Updategram  
  
1.  Kopieren Sie die oben stehende Updategramvorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen UpdateLastName.xml.  
  
2.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um das Updategram auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="b-updating-multiple-records-by-using-the-updgid-attribute"></a>B. Aktualisieren von mehreren Datensätzen mit dem Attribut "updg:id"  
 In diesem Beispiel führt das Updategram zwei Updates auf die HumanResources.Shift-Tabelle in der AdventureWorks-Datenbank aus:  
  
-   Es ändert den Namen der ursprünglichen Tagschicht, die um 7.00 Uhr beginnt, von "Day" in "Early Morning".  
  
-   Es fügt eine neue Schicht namens "Late Morning" ein, die um 10.00 Uhr beginnt.  
  
 In das Updategram die **updg: ID** Attribut erstellt Zuordnungen zwischen Elementen in der  **\<vor >** und  **\<nach >** blockiert.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift updg:id="x" Name="Day" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift updg:id="y" Name="Late Morning"   
                            StartTime="1900-01-01 10:00:00.000"  
                            EndTime="1900-01-01 18:00:00.000"  
                            ModifiedDate="2004-06-01 00:00:00.000"/>  
      <HumanResources.Shift updg:id="x" Name="Early Morning" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Beachten Sie, dass wie die **updg: ID** Attribut-Paare für die erste Instanz von der \<HumanResources.Shift > Element in der  **\<vor >** Block mit der zweiten Instanz von der \< HumanResources.Shift >-Elements in der  **\<nach >** Block.  
  
##### <a name="to-test-the-updategram"></a>So testen Sie das Updategram  
  
1.  Kopieren Sie die oben stehende Updategramvorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen UpdateMultipleRecords.xml.  
  
2.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um das Updategram auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="c-specifying-multiple-before-and-after-blocks"></a>C. Angeben von mehreren \<vor > und \<nach > Blöcke  
 Um Mehrdeutigkeiten zu vermeiden, können Sie das Updategram in Beispiel B schreiben, durch die Verwendung mehrerer  **\<vor >** und  **\<nach >** -blockpaaren. Angeben von  **\<vor >** und  **\<nach >** -Paaren ist eine Möglichkeit, mehrere Updates mit einem Minimum von Verwechslungen angeben. Auch, wenn jeder von der  **\<vor >** und  **\<nach >** Blöcke geben Sie höchstens einem Element, Sie müssen keine verwenden die **updg: ID** Attribut .  
  
> [!NOTE]  
>  Um ein Paar bilden die  **\<nach >** Tag muss unmittelbar folgen dem entsprechenden  **\<vor >** Tag.  
  
 Im folgenden Updategram das erste  **\<vor >** und  **\<nach >** Paar aktualisiert den schichtnamen für die Tagschicht. Das zweite Paar fügt einen neuen Schichtdatensatz ein.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="1" Name="Day" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="Early Morning" />  
    </updg:after>  
    <updg:before>  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="Late Morning"   
                            StartTime="1900-01-01 10:00:00.000"  
                            EndTime="1900-01-01 18:00:00.000"  
                            ModifiedDate="2004-06-01 00:00:00.000"/>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>So testen Sie das Updategram  
  
1.  Kopieren Sie die oben stehende Updategramvorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen UpdateMultipleBeforeAfter.xml.  
  
2.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um das Updategram auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="d-specifying-multiple-sync-blocks"></a>D. Angeben von mehreren \<Sync > Blöcke  
 Sie können angeben, dass mehrere  **\<Sync >** -Blöcke in einem Updategram. Jede  **\<Sync >** Block, der angegeben wird, ist eine unabhängige Transaktion.  
  
 Im folgenden Updategram das erste  **\<Sync >** Block aktualisiert einen Datensatz in der Sales.Customer-Tabelle. Der Einfachheit halber gibt das Updategram nur die erforderlichen Spaltenwerte an, nämlich den Identitätswert (CustomerID) und den zu aktualisierenden Wert (SalesPersonID).  
  
 Die zweite  **\<Sync >** Block der Sales.SalesOrderHeader-Tabelle zwei Datensätze hinzugefügt. Für diese Tabelle ist SalesOrderID eine Spalte vom Typ IDENTITY. Daher das Updategram gibt keinen den Wert von SalesOrderID in jedem der \<Sales.SalesOrderHeader > Elemente.  
  
 Angeben von mehreren  **\<Sync >** -Blöcke ist nützlich da Wenn das zweite  **\<Sync >** Block (eine Transaktion) Sales.SalesOrderHeader-Tabelle Datensätze hinzufügen kann die erste  **\<Sync >** Block kann dennoch den Kundendatensatz in der Sales.Customer-Tabelle aktualisieren.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
      <Sales.Customer CustomerID="1" SalesPersonID="280" />  
    </updg:before>  
    <updg:after>  
      <Sales.Customer CustomerID="1" SalesPersonID="283" />  
    </updg:after>  
  </updg:sync>  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
   <Sales.SalesOrderHeader   
             CustomerID="1"  
             RevisionNumber="1"  
             OrderDate="2004-07-01 00:00:00.000"  
             DueDate="2004-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="01010101-2222-3333-4444-556677889900"  
             ModifiedDate="2004-07-08 00:00:00.000" />  
   <Sales.SalesOrderHeader  
             CustomerID="1"  
             RevisionNumber="1"  
             OrderDate="2004-07-01 00:00:00.000"  
             DueDate="2004-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="1000.0000"  
             TaxAmt="0.0000"  
             Freight="0.0000"  
             rowguid="10101010-2222-3333-4444-556677889900"  
             ModifiedDate="2004-07-09 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>So testen Sie das Updategram  
  
1.  Kopieren Sie die oben stehende Updategramvorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen UpdateMultipleSyncs.xml.  
  
2.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um das Updategram auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="e-using-a-mapping-schema"></a>E. Verwenden eines Zuordnungsschemas  
 In diesem Beispiel gibt das Updategram ein Zuordnungsschema mit der **Zuordnungsschema** Attribut. (Es gibt keine Standardzuordnung, d. h. das Zuordnungsschema bietet die erforderliche Zuordnung der Elemente und Attribute im Updategram zu den Datenbanktabellen und -spalten.)  
  
 Die im Updategram angegebenen Elemente und Attribute verweisen auf die Elemente und Attribute im Zuordnungsschema.  
  
 Die folgenden XSD-Zuordnungsschema umfasst  **\<Kunden >**,  **\<Reihenfolge >**, und  **\<OD >** Elemente, die zum Zuordnen der Tabellen Sales.Customer, Sales.SalesOrderHeader und Sales.SalesOrderDetail in der Datenbank.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustomerOrder"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  
    <sql:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                     sql:relationship="CustomerOrder" >  
           <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OD"   
                             sql:relation="Sales.SalesOrderDetail"  
                             sql:relationship="OrderOD" >  
                 <xsd:complexType>  
                  <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                  <xsd:attribute name="ProductID" type="xsd:integer" />  
                  <xsd:attribute name="UnitPrice" type="xsd:decimal" />  
                  <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  <xsd:attribute name="UnitPriceDiscount" type="xsd:decimal" />   
                 </xsd:complexType>  
                </xsd:element>  
              </xsd:sequence>  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="OrderDate" type="xsd:date" />  
           </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Dieses Zuordnungsschema (UpdategramMappingSchema.xml) wird im folgenden Updategram angegeben. Das Updategram fügt in der Sales.SalesOrderDetail-Tabelle ein Auftragselement für einen bestimmten Auftrag hinzu. Das Updategram schließt geschachtelte Elemente: ein  **\<OD >** Element geschachtelt ein  **\<Reihenfolge >** Element. Die Primärschlüssel-Fremdschlüssel-Beziehung zwischen diesen beiden Elementen wird im Zuordnungsschema angegeben.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="UpdategramMappingSchema.xml" >  
    <updg:before>  
       <Order SalesOrderID="43659" />  
    </updg:before>  
    <updg:after>  
      <Order SalesOrderID="43659" >  
          <OD ProductID="776" UnitPrice="2329.0000"  
              OrderQty="2" UnitPriceDiscount="0.0" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>So testen Sie das Updategram  
  
1.  Kopieren Sie das oben stehende Zuordnungsschema, und fügen Sie es in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen UpdategramMappingSchema.xml.  
  
2.  Kopieren Sie die oben stehende Updategramvorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen UpdateWithMappingSchema.xml im selben Ordner, indem Sie das Zuordnungsschema (UpdategramMappingSchema.xml) gespeichert haben.  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um das Updategram auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Weitere Beispiele für Updategrams, die Zuordnungsschemas verwenden, finden Sie unter [ein Mapping-Schema mit Anmerkungen angeben, in einem Updategram &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
### <a name="f-using-a-mapping-schema-with-idrefs-attributes"></a>F. Verwenden eines Zuordnungsschemas mit IDREFS-Attributen  
 Dieses Beispiel veranschaulicht, wie Updategrams die IDREFS-Attribute im Zuordnungsschema verwenden, um Datensätze in mehreren Tabellen zu aktualisieren. Nehmen Sie für dieses Beispiel an, dass die Datenbank aus den folgenden Tabellen besteht:  
  
-   Student(StudentID, LastName)  
  
-   Course(CourseID, CourseName)  
  
-   Enrollment(StudentID, CourseID)  
  
 Da ein Student sich in viele Kurse einschreiben kann und an einem Kurs zahlreiche Studenten teilnehmen können, wird die dritte Tabelle, die Enrollment-Tabelle, benötigt, um diese m:n-Beziehung darzustellen.  
  
 Das folgende XSD-Zuordnungsschema stellt eine XML-Sicht der Tabellen mithilfe der  **\<Student >**,  **\<Kurs >**, und  **\<Registrierung >** Elemente. Die **IDREFS** Attribute im Zuordnungsschema geben die Beziehung zwischen diesen Elementen. Die **StudentIDList** -Attribut auf die  **\<Kurs >** Element ist ein **IDREFS** Type-Attribut, das auf die StudentID-Spalte in der Enrollment-Tabelle verweist. Entsprechend der **EnrolledIn** -Attribut auf die  **\<Student >** Element ist ein **IDREFS** Type-Attribut, das auf die CourseID-Spalte in der Registrierung verweist Tabelle.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="StudentEnrollment"  
          parent="Student"  
          parent-key="StudentID"  
          child="Enrollment"  
          child-key="StudentID" />  
  
    <sql:relationship name="CourseEnrollment"  
          parent="Course"  
          parent-key="CourseID"  
          child="Enrollment"  
          child-key="CourseID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Course" sql:relation="Course"   
                             sql:key-fields="CourseID" >  
    <xsd:complexType>  
    <xsd:attribute name="CourseID"  type="xsd:string" />   
    <xsd:attribute name="CourseName"   type="xsd:string" />   
    <xsd:attribute name="StudentIDList" sql:relation="Enrollment"  
                 sql:field="StudentID"  
                 sql:relationship="CourseEnrollment"   
                                     type="xsd:IDREFS" />  
  
    </xsd:complexType>  
  </xsd:element>  
  <xsd:element name="Student" sql:relation="Student" >  
    <xsd:complexType>  
    <xsd:attribute name="StudentID"  type="xsd:string" />   
    <xsd:attribute name="LastName"   type="xsd:string" />   
    <xsd:attribute name="EnrolledIn" sql:relation="Enrollment"  
                 sql:field="CourseID"  
                 sql:relationship="StudentEnrollment"   
                                     type="xsd:IDREFS" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Jedes Mal, wenn Sie dieses Schema in einem Updategram angeben und einen Datensatz in die Course-Tabelle einfügen, fügt das Updategram einen neuen Kursdatensatz in die Course-Tabelle ein. Wenn Sie eine oder mehrere neue StudentIDs für das StudentIDList-Attribut angeben, fügt das Updategram ebenfalls einen Datensatz für jeden neuen Studenten in die Enrollment-Tabelle ein. Das Updategram stellt sicher, dass der Enrollment-Tabelle keine Duplikate hinzugefügt werden.  
  
##### <a name="to-test-the-updategram"></a>So testen Sie das Updategram  
  
1.  Erstellen Sie diese Tabellen in der Datenbank, die im virtuellen Stammverzeichnis angegeben wird:  
  
    ```  
    CREATE TABLE Student(StudentID varchar(10) primary key,   
                         LastName varchar(25))  
    CREATE TABLE Course(CourseID varchar(10) primary key,   
                        CourseName varchar(25))  
    CREATE TABLE Enrollment(StudentID varchar(10)   
                                      references Student(StudentID),  
                           CourseID varchar(10)   
                                      references Course(CourseID))  
    ```  
  
2.  Fügen Sie diese Beispieldaten hinzu:  
  
    ```  
    INSERT INTO Student VALUES ('S1','Davoli')  
    INSERT INTO Student VALUES ('S2','Fuller')  
  
    INSERT INTO Course VALUES  ('CS101', 'C Programming')  
    INSERT INTO Course VALUES  ('CS102', 'Understanding XML')  
  
    INSERT INTO Enrollment VALUES ('S1', 'CS101')  
    INSERT INTO Enrollment VALUES ('S1', 'CS102')  
    ```  
  
3.  Kopieren Sie das oben stehende Zuordnungsschema, und fügen Sie es in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen SampleSchema.xml.  
  
4.  Speichern Sie das Updategram (SampleUpdategram) im selben Ordner, indem Sie das Zuordnungsschema im vorherigen Schritt gespeichert haben. (Dieses Updategram löscht einen Studenten mit StudentID="1" aus dem Kurs CS102.)  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101 CS102" />  
        </updg:before>  
        <updg:after >  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
5.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um das Updategram auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
6.  Speichern Sie das Updategram wie in den vorherigen Schritten beschrieben und führen Sie es aus. Das Updategram fügt den Studenten mit StudentID="1" wieder dem Kurs CS102 hinzu, indem der Enrollment-Tabelle ein Datensatz hinzugefügt wird.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101" />  
        </updg:before>  
        <updg:after >  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101 CS102" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
7.  Speichern Sie das nächste Updategram wie in den vorherigen Schritten beschrieben und führen Sie es aus. Dieses Updategram fügt drei neue Studenten ein und schreibt Sie in den Kurs CS101 ein. Wieder fügt die IDREFS-Beziehung Datensätze in der Enrollment-Tabelle ein.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
           <Course updg:id="y" CourseID="CS101"   
                               CourseName="C Programming" />  
        </updg:before>  
        <updg:after >  
           <Student updg:id="x1" StudentID="S3" LastName="Leverling" />  
           <Student updg:id="x2" StudentID="S4" LastName="Pecock" />  
           <Student updg:id="x3" StudentID="S5" LastName="Buchanan" />  
           <Course updg:id="y" CourseID="CS101"  
                               CourseName="C Programming"  
                               StudentIDList="S3 S4 S5" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
 Dies ist das entsprechende XDR-Schema:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <ElementType name="Enrollment" sql:relation="Enrollment" sql:key-fields="StudentID CourseID">  
    <AttributeType name="StudentID" dt:type="id" />  
    <AttributeType name="CourseID" dt:type="id" />  
  
    <attribute type="StudentID" />  
    <attribute type="CourseID" />  
  </ElementType>  
  <ElementType name="Course" sql:relation="Course" sql:key-fields="CourseID">  
    <AttributeType name="CourseID" dt:type="id" />  
    <AttributeType name="CourseName" />  
  
    <attribute type="CourseID" />  
    <attribute type="CourseName" />  
  
    <AttributeType name="StudentIDList" dt:type="idrefs" />  
    <attribute type="StudentIDList" sql:relation="Enrollment" sql:field="StudentID" >  
        <sql:relationship  
                key-relation="Course"  
                key="CourseID"  
                foreign-relation="Enrollment"  
                foreign-key="CourseID" />  
    </attribute>  
  
  </ElementType>  
  <ElementType name="Student" sql:relation="Student">  
    <AttributeType name="StudentID" dt:type="id" />  
     <AttributeType name="LastName" />  
  
    <attribute type="StudentID" />  
    <attribute type="LastName" />  
  
    <AttributeType name="EnrolledIn" dt:type="idrefs" />  
    <attribute type="EnrolledIn" sql:relation="Enrollment" sql:field="CourseID" >  
        <sql:relationship  
                key-relation="Student"  
                key="StudentID"  
                foreign-relation="Enrollment"  
                foreign-key="StudentID" />  
    </attribute>  
  
    <element type="Enrollment" sql:relation="Enrollment" >  
        <sql:relationship key-relation="Student"  
                          key="StudentID"  
                          foreign-relation="Enrollment"  
                          foreign-key="StudentID" />  
    </element>  
  </ElementType>  
  
</Schema>  
```  
  
 Weitere Beispiele für Updategrams, die Zuordnungsschemas verwenden, finden Sie unter [ein Mapping-Schema mit Anmerkungen angeben, in einem Updategram &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheitsüberlegungen zu Updategrams &#40; SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
