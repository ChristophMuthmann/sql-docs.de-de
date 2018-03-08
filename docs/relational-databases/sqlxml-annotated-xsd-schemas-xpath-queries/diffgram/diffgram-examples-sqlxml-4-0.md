---
title: DiffGram-Beispiele (SQLXML 4.0) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
- DiffGrams [SQLXML], examples
- examples [SQLXML], DiffGram
- diffgr:parentID
- parentID annotation
ms.assetid: fc148583-dfd3-4efb-a413-f47b150b0975
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6bba1fe2e0a141d9bbac3ae67ece5d7e32d0b197
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="diffgram-examples-sqlxml-40"></a>DiffGram-Beispiele (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Die Beispiele in diesem Thema umfassen DiffGrams, mit denen Einfüge-, Update- und Löschvorgänge in der Datenbank vorgenommen werden. Bevor Sie die Beispiele verwenden, beachten Sie Folgendes:  
  
-   In den Beispielen werden zwei Tabellen verwendet (Cust und Ord), die erstellt werden müssen, wenn Sie die DiffGram-Beispiele testen möchten:  
  
    ```  
    Cust(CustomerID, CompanyName, ContactName)  
    Ord(OrderID, CustomerID)  
    ```  
  
-   Die meisten der Beispiele in diesem Thema verwenden das folgende XSD-Schema:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
    <xsd:annotation>  
      <xsd:documentation>  
        Diffgram Customers/Orders Schema.  
      </xsd:documentation>  
      <xsd:appinfo>  
           <sql:relationship name="CustomersOrders"   
                      parent="Cust"  
                      parent-key="CustomerID"  
                      child-key="CustomerID"  
                      child="Ord"/>  
      </xsd:appinfo>  
    </xsd:annotation>  
  
    <xsd:element name="Customer" sql:relation="Cust">  
      <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="CompanyName"    type="xsd:string"/>  
          <xsd:element name="ContactName"    type="xsd:string"/>  
           <xsd:element name="Order" sql:relation="Ord" sql:relationship="CustomersOrders">  
            <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:int" sql:field="OrderID"/>  
              <xsd:attribute name="CustomerID" type="xsd:string"/>  
            </xsd:complexType>  
          </xsd:element>  
        </xsd:sequence>  
        <xsd:attribute name="CustomerID" type="xsd:string" sql:field="CustomerID"/>  
      </xsd:complexType>  
    </xsd:element>  
  
    </xsd:schema>     
    ```  
  
     Speichern Sie dieses Schema als DiffGramSchema.xml im gleichen Ordner, in dem Sie auch die anderen in diesem Beispiel verwendeten Dateien gespeichert haben.  
  
## <a name="a-deleting-a-record-by-using-a-diffgram"></a>A. Löschen eines Datensatzes mit einem DiffGram  
 Mit dem DiffGram in diesem Beispiel werden ein Kundendatensatz (mit der CustomerID ALFKI) aus der Cust-Tabelle und der entsprechende Auftragsdatensatz (mit der OrderID 1) aus der Ord-Tabelle gelöscht.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance/>  
  
    <diffgr:before>  
        <Order diffgr:id="Order1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI"   
               OrderID="1"/>  
        <Customer diffgr:id="Customer1"   
                  msdata:rowOrder="0"   
                  CustomerID="ALFKI">  
           <CompanyName>Alfreds Futterkiste</CompanyName>  
           <ContactName>Maria Anders</ContactName>  
        </Customer>  
    </diffgr:before>  
    <msdata:errors/>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 In der  **\<vor >** blockieren, es ist ein  **\<Reihenfolge >** Element (**diffgr: ID = "Order1"**) und ein  **\< Kunde >** Element (**diffgr: ID = "Customer1"**). Diese Elemente stellen vorhandene Datensätze in der Datenbank dar. Die  **\<DataInstance >** -Element verfügt nicht über die entsprechenden Datensätze (mit dem gleichen **diffgr: ID**). Dies gibt einen Löschvorgang an.  
  
#### <a name="to-test-the-diffgram"></a>So testen Sie das DiffGram-Objekt  
  
1.  Erstellen Sie diese Tabellen in der **Tempdb** Datenbank.  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  Fügen Sie diese Beispieldaten hinzu:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Kopieren Sie das oben stehende DiffGram, und fügen Sie es in eine Textdatei ein. Speichern Sie die Datei als MyDiffGram.xml in demselben Ordner, den Sie im vorherigen Schritt verwendet haben.  
  
4.  Kopieren Sie das zuvor in diesem Thema bereitgestellte DiffGramSchema, und fügen Sie es in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen DiffGramSchema.xml.  
  
5.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um das DiffGram auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="b-inserting-a-record-by-using-a-diffgram"></a>B. Einfügen eines Datensatzes mit einem DiffGram  
 In diesem Beispiel fügt das DiffGram einen Datensatz in die Tabellen Cust und Ord ein.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"   
      sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
          xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
          xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
       <Customer diffgr:id="Customer1" msdata:rowOrder="0"    
                 diffgr:hasChanges="inserted" CustomerID="ALFKI">  
        <CompanyName>C3Company</CompanyName>  
        <ContactName>C3Contact</ContactName>  
        <Order diffgr:id="Order1"   
               msdata:rowOrder="0"  
               diffgr:hasChanges="inserted"   
               CustomerID="ALFKI" OrderID="1"/>  
      </Customer>  
    </DataInstance>  
  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 In diesem DiffGram der  **\<vor >** -Block nicht angegeben (keine vorhandenen Datenbank-Datensätze erkannt). Es gibt zwei Datensatzinstanzen (identifiziert durch die  **\<Kunden >** und  **\<Reihenfolge >** Elemente in der  **\<DataInstance >** Block), zuordnen zu Cust und Ord-Tabellen bzw. Beide Elemente geben die **diffgr: HasChanges** Attribut (**HasChanges = "inserted"**). Dies gibt einen Einfügevorgang an. In diesem DiffGram, bei der Angabe **HasChanges = "modified"**, Sie an, dass einen Datensatz, der nicht vorhanden ist, was zu einem Fehler führt, ändern möchten.  
  
#### <a name="to-test-the-diffgram"></a>So testen Sie das DiffGram-Objekt  
  
1.  Erstellen Sie diese Tabellen in der **Tempdb** Datenbank.  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  Fügen Sie diese Beispieldaten hinzu:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Kopieren Sie das oben stehende DiffGram, und fügen Sie es in eine Textdatei ein. Speichern Sie die Datei als MyDiffGram.xml in demselben Ordner, den Sie im vorherigen Schritt verwendet haben.  
  
4.  Kopieren Sie das zuvor in diesem Thema bereitgestellte DiffGramSchema, und fügen Sie es in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen DiffGramSchema.xml.  
  
5.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um das DiffGram auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="c-updating-an-existing-record-by-using-a-diffgram"></a>C. Aktualisieren eines vorhandenen Datensatzes mit einem DiffGram  
 In diesem Beispiel aktualisiert das DiffGram Kundeninformationen (CompanyName und ContactName) für den Kunden ALFKI.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer1"   
                msdata:rowOrder="0" diffgr:hasChanges="modified"   
                CustomerID="ALFKI">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Antonio Moreno</ContactName>  
      </Customer>  
    </DataInstance>  
  
    <diffgr:before>  
     <Customer diffgr:id="Customer1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
    </diffgr:before>  
  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 Die  **\<vor >** -Block enthält ein  **\<Kunden >** Element (**diffgr: ID = "Customer1"**). Die  **\<DataInstance >** -Block enthält das entsprechende  **\<Kunden >** -Element mit derselben **Id**. Die  **\<Kunden >** Element in der  **\<NewDataSet >** überdies **diffgr: HasChanges = "modified"**. Hiermit wird eine Update-Vorgang und der Kundendatensatz in der **Cust** -Tabelle wird entsprechend aktualisiert. Beachten Sie, dass bei der **diffgr: HasChanges** -Attribut nicht angegeben ist, das DiffGram-Verarbeitungslogik ignoriert diese-Element, und keine Updates ausgeführt werden.  
  
#### <a name="to-test-the-diffgram"></a>So testen Sie das DiffGram-Objekt  
  
1.  Erstellen Sie diese Tabellen in der **Tempdb** Datenbank.  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  Fügen Sie diese Beispieldaten hinzu:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Kopieren Sie das oben stehende DiffGram, und fügen Sie es in eine Textdatei ein. Speichern Sie die Datei als MyDiffGram.xml in demselben Ordner, den Sie im vorherigen Schritt verwendet haben.  
  
4.  Kopieren Sie das zuvor in diesem Thema bereitgestellte DiffGramSchema, und fügen Sie es in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen DiffGramSchema.xml.  
  
5.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um das DiffGram auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="d-inserting-updating-and-deleting-records-by-using-a-diffgram"></a>D. Einfügen, Aktualisieren und Löschen von Datensätzen mit einem DiffGram  
 In diesem Beispiel wird ein relativ komplexes DiffGram verwendet, um Einfüge-, Update- und Löschvorgänge durchzuführen.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer2" msdata:rowOrder="1"   
                diffgr:hasChanges="modified"   
                CustomerID="ANATR">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Elizabeth Lincoln</ContactName>  
          <Order diffgr:id="Order2" msdata:rowOrder="1"   
               msdata:hiddenCustomerID="ANATR"   
               CustomerID="ANATR" OrderID="2"/>  
      </Customer>  
  
      <Customer diffgr:id="Customer3" msdata:rowOrder="2"   
                CustomerID="ANTON">  
         <CompanyName>Chop-suey Chinese</CompanyName>  
         <ContactName>Yang Wang</ContactName>  
         <Order diffgr:id="Order3" msdata:rowOrder="2"   
               msdata:hiddenCustomerID="ANTON"   
               CustomerID="ANTON" OrderID="3"/>  
      </Customer>  
      <Customer diffgr:id="Customer4" msdata:rowOrder="3"   
                diffgr:hasChanges="inserted"   
                CustomerID="AROUT">  
         <CompanyName>Around the Horn</CompanyName>  
         <ContactName>Thomas Hardy</ContactName>  
         <Order diffgr:id="Order4" msdata:rowOrder="3"   
                diffgr:hasChanges="inserted"   
                msdata:hiddenCustomerID="AROUT"   
               CustomerID="AROUT" OrderID="4"/>  
      </Customer>  
    </DataInstance>  
    <diffgr:before>  
      <Order diffgr:id="Order1" msdata:rowOrder="0"   
             msdata:hiddenCustomerID="ALFKI"   
             CustomerID="ALFKI" OrderID="1"/>  
      <Customer diffgr:id="Customer1" msdata:rowOrder="0"   
                CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
      <Customer diffgr:id="Customer2" msdata:rowOrder="1"   
                CustomerID="ANATR">  
        <CompanyName>Ana Trujillo Emparedados y helados</CompanyName>  
        <ContactName>Ana Trujillo</ContactName>  
      </Customer>  
    </diffgr:before>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 Die DiffGram-Logik verarbeitet dieses DiffGram folgendermaßen:  
  
-   In Übereinstimmung mit der DiffGram-Verarbeitungslogik werden alle Elemente der obersten Ebene in der  **\<vor >** blockieren Sie den entsprechenden Tabellen zugeordnet, wie im Zuordnungsschema beschrieben.  
  
-   Die  **\<vor >** -Block umfasst ein  **\<Reihenfolge >** Element (**Dffgr:id = "Order1"**) und ein  **\<Kunden >** Element (**diffgr: ID = "Customer1"**) für das es kein entsprechendes Element in der  **\<DataInstance >** -Block (mit der gleichen ID). Dies gibt einen Löschvorgang an, und die Datensätze werden aus den Cust- und Ord-Tabellen gelöscht.  
  
-   Die  **\<vor >** -Block umfasst ein  **\<Kunden >** Element (**diffgr: ID = "Customer2"**) für das es eine entsprechende  **\<Kunden >** Element in der  **\<DataInstance >** -Block (mit der gleichen ID). Das Element in der  **\<DataInstance >** -Block gibt **diffgr: HasChanges = "modified"**. Dies ist ein Updatevorgang, bei dem für den Kunden ANATR, CompanyName und ContactName-Informationen in der Cust-Tabelle mit Werten, die im angegebenen aktualisiert, die  **\<DataInstance >** Block.  
  
-   Die  **\<DataInstance >** -Block umfasst ein  **\<Kunden >** Element (**diffgr: ID = "Customer3"**) und ein  **\<Reihenfolge >** Element (**diffgr: ID = "Order3"**). Keines dieser Elemente geben die **diffgr: HasChanges** Attribut. Daher ignoriert die DiffGram-Verarbeitungslogik diese Elemente.  
  
-   Die  **\<DataInstance >** -Block umfasst ein  **\<Kunden >** Element (**diffgr: ID = "Customer4"**) und ein  **\<Reihenfolge >** Element (**diffgr: ID = "Order4"**) für das es keine entsprechenden Elemente in der \<vor > Block. Diese Elemente in der  **\<DataInstance >** -Block geben **diffgr: HasChanges = "inserted"**. Daher wird ein neuer Datensatz der Cust-Tabelle und der Ord-Tabelle hinzugefügt.  
  
#### <a name="to-test-the-diffgram"></a>So testen Sie das DiffGram-Objekt  
  
1.  Erstellen Sie die folgenden Tabellen in der **Tempdb** Datenbank.  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  Fügen Sie diese Beispieldaten hinzu:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Kopieren Sie das oben stehende DiffGram, und fügen Sie es in eine Textdatei ein. Speichern Sie die Datei als MyDiffGram.xml in demselben Ordner, den Sie im vorherigen Schritt verwendet haben.  
  
4.  Kopieren Sie das zuvor in diesem Thema bereitgestellte DiffGramSchema, und fügen Sie es in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen DiffGramSchema.xml.  
  
5.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um das DiffGram auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="e-applying-updates-by-using-a-diffgram-with-the-diffgrparentid-annotation"></a>E. Übernehmen von Updates mit einem DiffGram mit der "diffgr:parentID"-Anmerkung  
 In diesem Beispiel wird veranschaulicht, wie die **ParentID** Anmerkung, die im angegebenen der  **\<vor >** Block des DiffGram-Objekts übernehmen der Updates verwendet wird.  
  
```  
<NewDataSet />  
<diffgr:before>  
   <Order diffgr:id="Order1" msdata:rowOrder="0" OrderID="2" />  
   <Order diffgr:id="Order3" msdata:rowOrder="2" OrderID="4" />  
  
   <OrderDetail diffgr:id="OrderDetail1"   
                diffgr:parentId="Order1"   
                msdata:rowOrder="0"   
                ProductID="13"   
                OrderID="2" />  
   <OrderDetail diffgr:id="OrderDetail3"   
                diffgr:parentId="Order3"  
                ProductID="77"  
                OrderID="4"/>  
</diffgr:before>  
</diffgr:diffgram>  
```  
  
 Dieses DiffGram gibt einen Löschvorgang an, da es nur eine  **\<vor >** Block. Im DiffGram-Objekt das **ParentID** -Anmerkung verwendet, um eine über-/ unterordnungsbeziehung zwischen den Bestellungen und Bestellungsdetails angeben. Wenn SQLXML die Datensätze löscht, werden auch die Datensätze aus der untergeordneten Tabelle, die durch diese Beziehung gekennzeichnet wird, gelöscht. Anschließend werden die Datensätze aus der entsprechenden übergeordneten Tabelle gelöscht.  
  
  
