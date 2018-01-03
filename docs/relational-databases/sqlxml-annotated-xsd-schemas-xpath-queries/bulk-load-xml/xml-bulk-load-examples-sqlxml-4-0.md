---
title: XML Bulk Load-Beispiele (SQLXML 4.0) | Microsoft Docs
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
- overflow-field annotation
- ConnectionCommand property
- XMLFragment property
- relationship chains [SQLXML]
- multiple table bulk loading
- examples [SQLXML], XML Bulk Load
- overflow data [SQLXML]
- sql:datatype
- transaction mode [SQLXML]
- CheckConstraints property
- sql:overflow-field
- XML Bulk Load [SQLXML], examples
- TempFilePath property
- datatype annotation
- Transaction property
- KeepIdentity property
- Execute method
- streaming XML data
- xml data type [SQL Server], SQLXML
- bulk load [SQLXML], examples
ms.assetid: 970e4553-b41d-4a12-ad50-0ee65d1f305d
caps.latest.revision: "41"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3a218d6f89ee2c190361441a6922770e770ec11a
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="xml-bulk-load-examples-sqlxml-40"></a>Beispiele für XML-Massenladen (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Die folgenden Beispiele veranschaulichen die XML-Massenladen in Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Alle Beispiele enthalten ein XSD-Schema und das entsprechende XDR-Schema.  
  
## <a name="bulk-loader-script-validateandbulkloadvbs"></a>Skript für das Massenladen (ValidateAndBulkload.vbs)  
 Das folgende Skript geschrieben, der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript), lädt ein XML-Dokument in das XML-DOM; überprüft es anhand eines Schemas und, wenn das Dokument gültig ist, wird führt diesen einem XML-Massenladevorgang auf des Load der XML-Daten in einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabelle. Dieses Skript kann mit allen Beispielen in diesem Kapitel ausgeführt werden, die einen entsprechenden Verweis enthalten.  
  
> [!NOTE]  
>  Der XML-Massenladevorgang gibt keine Warnung aus, wenn kein Inhalt von der Datendatei hochgeladen wird. Es wird daher empfohlen, die XML-Datendatei vor dem Ausführen eines Massenladevorgangs zu überprüfen.  
  
```vbs  
Dim FileValid  
  
set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=MyServer;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
  
'Validate the data file prior to bulkload  
Dim sOutput   
sOutput = ValidateFile("SampleXMLData.xml", "", "SampleSchema.xml")  
WScript.Echo sOutput  
  
If FileValid Then  
   ' Check constraints and initiate transaction (if needed)  
   ' objBL.CheckConstraints = True  
   ' objBL.Transaction=True  
  'Execute XML bulkload using file.  
  objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
  set objBL=Nothing  
End If  
  
Function ValidateFile(strXmlFile,strUrn,strXsdFile)  
  
   ' Create a schema cache and add SampleSchema.xml to it.  
   Dim xs, fso, sAppPath  
   Set fso = CreateObject("Scripting.FileSystemObject")   
   Set xs = CreateObject("MSXML2.XMLSchemaCache.6.0")  
   sAppPath = fso.GetFolder(".")   
   xs.Add strUrn, sAppPath & "\" & strXsdFile  
  
   ' Create an XML DOMDocument object.  
   Dim xd   
   Set xd = CreateObject("MSXML2.DOMDocument.6.0")  
  
   ' Assign the schema cache to the DOM document.  
   ' schemas collection.  
   Set xd.schemas = xs  
  
   ' Load XML document as DOM document.  
   xd.async = False  
   xd.Load sAppPath & "\" & strXmlFile  
  
   ' Return validation results in message to the user.  
   If xd.parseError.errorCode <> 0 Then  
        ValidateFile = "Validation failed on " & _  
             strXmlFile & vbCrLf & _  
             "=======" & vbCrLf & _  
             "Reason: " & xd.parseError.reason & _  
             vbCrLf & "Source: " & _  
             xd.parseError.srcText & _  
             vbCrLf & "Line: " & _  
             xd.parseError.Line & vbCrLf  
             FileValid = False  
    Else  
        ValidateFile = "Validation succeeded for " & _  
             strXmlFile & vbCrLf & _  
             "========" & _  
             vbCrLf & "Contents to be bulkloaded" & vbCrLf  
             FileValid = True  
    End If  
End Function  
```  
  
## <a name="a-bulk-loading-xml-in-a-table"></a>A. Massenladen von XML-Daten in eine Tabelle  
 In diesem Beispiel wird eine Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , die in die "ConnectionString"-Eigenschaft (MyServer) angegeben wird. Im Beispiel wird auch die ErrorLogFile-Eigenschaft. Daher wird die Fehlerausgabe in der angegebenen Datei (C:\error.log) gespeichert. Sie können den Speicherort auch jederzeit ändern. Beachten Sie außerdem, dass die Execute-Methode als Parameter sowohl die Zuordnungsschemadatei (SampleSchema.xml) als auch die XML-Datendatei (SampleXMLData.xml) verfügt. Wenn das Massenladen ausführt, werden die Cust-Tabelle, die Sie in erstellt haben **Tempdb** Datenbank neue Datensätze basierend auf den Inhalt der XML-Datendatei enthält.  
  
#### <a name="to-test-a-sample-bulk-load"></a>So testen Sie ein Beispiel für einen Massenladevorgang  
  
1.  Erstellen Sie die folgende Tabelle:  
  
    ```sql  
    CREATE TABLE Cust(CustomerID  int PRIMARY KEY,  
                      CompanyName varchar(20),  
                      City        varchar(20));  
    GO  
    ```  
  
2.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als SampleSchema.xml. Fügen Sie dieser Datei das folgende XSD-Schema hinzu:  
  
    ```xml  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
       <xsd:element name="ROOT" sql:is-constant="1" >  
         <xsd:complexType>  
           <xsd:sequence>  
             <xsd:element name="Customers" sql:relation="Cust" maxOccurs="unbounded">  
               <xsd:complexType>  
                 <xsd:sequence>  
                   <xsd:element name="CustomerID"  type="xsd:integer" />  
                   <xsd:element name="CompanyName" type="xsd:string" />  
                   <xsd:element name="City"        type="xsd:string" />  
                 </xsd:sequence>  
               </xsd:complexType>  
             </xsd:element>  
           </xsd:sequence>  
          </xsd:complexType>  
         </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als SampleXMLData.xml. Fügen Sie dieser Datei das folgende XML-Dokument hinzu:  
  
    ```xml  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Sean Chai</CompanyName>  
        <City>New York</City>  
      </Customers>  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Tom Johnston</CompanyName>  
         <City>Los Angeles</City>  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Institute of Art</CompanyName>  
        <City>Chicago</City>  
      </Customers>  
    </ROOT>  
    ```  
  
4.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als ValidateAndBulkload.vbs. Fügen Sie zu dieser Datei den VBScript-Code hinzu, der am Anfang dieses Themas bereitgestellt wird. Ändern Sie die Verbindungszeichenfolge, um den entsprechenden Servernamen bereitzustellen. Geben Sie den entsprechenden Pfad für die Dateien, die als Parameter für die Execute-Methode angegeben werden.  
  
5.  Führen Sie den VBScript-Code aus. XML-Massenladen lädt den XML-Code in die Cust-Tabelle.  
  
 Dies ist das entsprechende XDR-Schema:  
  
```xml  
  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers"  sql:relation="Cust" >  
      <element type="CustomerID"  sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City"        sql:field="City" />  
  
   </ElementType>  
</Schema>  
```  
  
## <a name="b-bulk-loading-xml-data-in-multiple-tables"></a>B. Massenladen von XML-Daten in mehrere Tabellen  
 In diesem Beispiel wird das XML-Dokument besteht aus den  **\<Kunden >** und  **\<Reihenfolge >** Elemente.  
  
```xml  
<ROOT>  
  <Customers>  
    <CustomerID>1111</CustomerID>  
    <CompanyName>Sean Chai</CompanyName>  
    <City>NY</City>  
    <Order OrderID="1" />  
    <Order OrderID="2" />  
  </Customers>  
  <Customers>  
    <CustomerID>1112</CustomerID>  
    <CompanyName>Tom Johnston</CompanyName>  
     <City>LA</City>    
    <Order OrderID="3" />  
  </Customers>  
  <Customers>  
    <CustomerID>1113</CustomerID>  
    <CompanyName>Institute of Art</CompanyName>  
    <Order OrderID="4" />  
  </Customers>  
</ROOT>  
```  
  
 Dieses Beispiel wird ein Massenimport lädt das XML-Daten in zwei Tabellen **Cust** und **CustOrder**:  
  
-   Cust (CustomerID, CompanyName, Ort)  
  
-   CustOrder ("OrderID", "CustomerID")  
  
 Das folgende XSD-Schema definiert die XML-Ansicht für diese Tabellen. Das Schema gibt die über-/ unterordnungsbeziehung zwischen den  **\<Kunden >** und  **\<Reihenfolge >** Elemente.  
  
```xml  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="ROOT" sql:is-constant="1" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Customers" sql:relation="Cust" >  
          <xsd:complexType>  
            <xsd:sequence>  
              <xsd:element name="CustomerID"  type="xsd:integer" />  
              <xsd:element name="CompanyName" type="xsd:string" />  
              <xsd:element name="City"        type="xsd:string" />  
              <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
                <xsd:complexType>  
                  <xsd:attribute name="OrderID" type="xsd:integer" />  
                </xsd:complexType>  
              </xsd:element>  
             </xsd:sequence>  
          </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Die Primärschlüssel-Fremdschlüssel-Beziehung zwischen der oben angegebene XML-Massenladen verwendet die  **\<Cust >** und  **\<CustOrder >** Elemente für den Massenimport Laden der Daten in beiden Tabellen .  
  
#### <a name="to-test-a-sample-bulk-load"></a>So testen Sie ein Beispiel für einen Massenladevorgang  
  
1.  Erstellen Sie zwei Tabellen in **Tempdb** Datenbank:  
  
    ```sql  
    USE tempdb;  
    CREATE TABLE Cust(  
           CustomerID  int PRIMARY KEY,  
           CompanyName varchar(20),  
           City        varchar(20));  
    CREATE TABLE CustOrder(        OrderID     int PRIMARY KEY,   
            CustomerID int FOREIGN KEY REFERENCES Cust(CustomerID));  
    ```  
  
2.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als SampleSchema.xml. Fügen Sie der Datei das XSD-Schema hinzu, das in diesem Beispiel bereitgestellt wird.  
  
3.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als SampleData.xml. Fügen Sie der Datei das XML-Dokument hinzu, das weiter oben in diesem Beispiel bereitgestellt wird.  
  
4.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als ValidateAndBulkload.vbs. Fügen Sie zu dieser Datei den VBScript-Code hinzu, der am Anfang dieses Themas bereitgestellt wird. Ändern Sie die Verbindungszeichenfolge, um den entsprechenden Server- und Datenbanknamen bereitzustellen. Geben Sie den entsprechenden Pfad für die Dateien, die als Parameter für die Execute-Methode angegeben werden.  
  
5.  Führen Sie den oben angegebenen VBScript-Code aus. XML-Massenladen lädt das XML-Dokument in die Tabellen Cust und CustOrder.  
  
 Dies ist das entsprechende XDR-Schema:  
  
```xml  
  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust" >  
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
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
## <a name="c-using-chain-relationships-in-the-schema-to-bulk-load-xml"></a>C. Verwenden von Kettenbeziehungen im Schema für das XML-Massenladen  
 Dieses Beispiel zeigt, wie die im Zuordnungsschema festgelegte M:N-Beziehung des XML-Massenladevorgangs zum Laden von Daten in eine Tabelle verwendet wird, die eine M:N-Beziehung darstellt.  
  
 Das folgende XSD-Schema ist ein Beispiel dafür:  
  
```xml  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrderOD"  
          parent="Ord"  
          parent-key="OrderID"  
          child="OrderDetail"  
          child-key="OrderID" />  
  
    <sql:relationship name="ODProduct"  
          parent="OrderDetail"  
          parent-key="ProductID"  
          child="Product"  
          child-key="ProductID"   
          inverse="true"/>  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="ROOT" sql:is-constant="1" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Ord"   
                     sql:key-fields="OrderID" >  
          <xsd:complexType>  
            <xsd:sequence>  
             <xsd:element name="Product"  
                          sql:relation="Product"   
                          sql:key-fields="ProductID"  
                          sql:relationship="OrderOD ODProduct">  
               <xsd:complexType>  
                 <xsd:attribute name="ProductID" type="xsd:int" />  
                 <xsd:attribute name="ProductName" type="xsd:string" />  
               </xsd:complexType>  
             </xsd:element>  
           </xsd:sequence>  
           <xsd:attribute name="OrderID"   type="xsd:integer" />   
           <xsd:attribute name="CustomerID"   type="xsd:string" />  
         </xsd:complexType>  
       </xsd:element>  
      </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Das Schema gibt ein  **\<Reihenfolge >** Element mit einer  **\<Product >** untergeordnetes Element. Die  **\<Reihenfolge >** Element ordnet Ord-Tabelle und die  **\<Product >** Element wird der Product-Tabelle in der Datenbank zugeordnet. Auf angegebene der  **\<Product >** Element identifiziert eine m: n-Beziehung, die durch die OrderDetail-Tabelle dargestellt. (Eine Bestellung kann viele Produkte beinhalten, und ein Produkt kann in vielen Bestellungen enthalten sein.)  
  
 Wenn Sie mit diesem Schema einen Massenladevorgang für ein XML-Dokument durchführen, werden den Tabellen Ord, Product und OrderDetail Datensätze hinzugefügt.  
  
#### <a name="to-test-a-working-sample"></a>So testen Sie ein funktionstüchtiges Beispiel  
  
1.  Erstellen Sie drei Tabellen:  
  
    ```sql  
    CREATE TABLE Ord (  
             OrderID     int  PRIMARY KEY,  
             CustomerID  varchar(5));  
    GO  
    CREATE TABLE Product (  
             ProductID   int PRIMARY KEY,  
             ProductName varchar(20));  
    GO  
    CREATE TABLE OrderDetail (  
           OrderID     int FOREIGN KEY REFERENCES Ord(OrderID),  
           ProductID   int FOREIGN KEY REFERENCES Product(ProductID),  
                       CONSTRAINT OD_key PRIMARY KEY (OrderID, ProductID));  
    GO  
    ```  
  
2.  Speichern Sie das oben in diesem Beispiel bereitgestellte Schema unter dem Dateinamen SampleSchema.xml.  
  
3.  Speichern Sie die folgenden XML-Daten unter dem Dateinamen SampleXMLData.xml:  
  
    ```xml  
    <ROOT>    
      <Order OrderID="1" CustomerID="ALFKI">  
        <Product ProductID="1" ProductName="Chai" />  
        <Product ProductID="2" ProductName="Chang" />  
      </Order>  
      <Order OrderID="2" CustomerID="ANATR">  
        <Product ProductID="3" ProductName="Aniseed Syrup" />  
        <Product ProductID="4" ProductName="Gumbo Mix" />  
      </Order>  
    </ROOT>  
    ```  
  
4.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als ValidateAndBulkload.vbs. Fügen Sie zu dieser Datei den VBScript-Code hinzu, der am Anfang dieses Themas bereitgestellt wird. Ändern Sie die Verbindungszeichenfolge, um den entsprechenden Server- und Datenbanknamen bereitzustellen. Entfernen Sie die Kommentierung der folgenden Zeilen aus dem Quellcode für dieses Beispiel.  
  
    ```vbs  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    ```  
  
5.  Führen Sie den VBScript-Code aus. XML-Massenladen lädt das XML-Dokument in die Tabellen Ord und Product.  
  
## <a name="d-bulk-loading-in-identity-type-columns"></a>D. Massenladen in Identitätsspalten  
 Dieses Beispiel zeigt den Umgang mit Identitätsspalten beim Massenladen. In dem Beispiel werden Daten in einem Massenvorgang in drei Tabellen (Ord, Product und OrderDetail) geladen.  
  
 Tabellen:  
  
-   OrderID in der Ord-Tabelle ist eine Identitätsspalte.  
  
-   ProductID ist eine Identitätsspalte.  
  
-   Die Spalten OrderID und ProductID in der OrderDetail-Tabelle sind Fremdschlüsselspalten, die sich auf Primärschlüsselspalten in den Tabellen Ord und Product beziehen.  
  
 Hier sehen Sie die Tabellenschemas für dieses Beispiel:  
  
```  
Ord (OrderID, CustomerID)  
Product (ProductID, ProductName)  
OrderDetail (OrderID, ProductID)  
```  
  
 In diesem Beispiel der XML-Massenladen wird der KeepIdentity-Eigenschaft des Objektmodells BulkLoad auf "false" festgelegt. Daher erstellt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Identitätswerte für die Spalten ProductID und OrderID in den Tabellen Product und Ord (alle in den Dokumenten für das Massenladen angegebenen Werte werden ignoriert).  
  
 In diesem Fall gibt der XML-Massenladevorgang die Primärschlüssel- bzw. Fremdschlüsselbeziehung zwischen Tabellen an. Der Massenladevorgang fügt zunächst Datensätze in die Tabelle mit den Primärschlüsseln ein und gibt dann die von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] generierten Identitätswerte an die Tabellen mit den Fremdschlüsselspalten weiter. Im folgenden Beispiel fügt der XML-Massenladevorgang Daten in dieser Reihenfolge in Tabellen ein:  
  
1.  Product  
  
2.  Ord  
  
3.  OrderDetail  
  
    > [!NOTE]  
    >  Die Verarbeitungslogik erfordert, dass der XML-Massenladevorgang die Identitätswerte für das spätere Einfügen in die OrderDetails-Tabelle aufzeichnet, um sie in die Tabellen Products und Orders einzufügen. Zu diesem Zweck erstellt der XML-Massenladevorgang Zwischentabellen, fügt die Daten in diese Tabellen ein und entfernt sie später.  
  
#### <a name="to-test-a-working-sample"></a>So testen Sie ein funktionstüchtiges Beispiel  
  
1.  Erstellen Sie die folgenden Tabellen:  
  
    ```  
    CREATE TABLE Ord (  
             OrderID     int identity(1,1)  PRIMARY KEY,  
             CustomerID  varchar(5));  
    GO  
    CREATE TABLE Product (  
             ProductID   int identity(1,1) PRIMARY KEY,  
             ProductName varchar(20));  
    GO  
    CREATE TABLE OrderDetail (  
           OrderID     int FOREIGN KEY REFERENCES Ord(OrderID),  
           ProductID   int FOREIGN KEY REFERENCES Product(ProductID),  
                       CONSTRAINT OD_key PRIMARY KEY (OrderID, ProductID));  
    GO  
    ```  
  
2.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als SampleSchema.xml. Fügen Sie dieses XSD-Schema der Datei hinzu.  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
     <xsd:annotation>  
       <xsd:appinfo>  
        <sql:relationship name="OrderOD"  
              parent="Ord"  
              parent-key="OrderID"  
              child="OrderDetail"  
              child-key="OrderID" />  
        <sql:relationship name="ODProduct"  
              parent="OrderDetail"  
              parent-key="ProductID"  
              child="Product"  
              child-key="ProductID"   
              inverse="true"/>  
       </xsd:appinfo>  
     </xsd:annotation>  
  
      <xsd:element name="Order" sql:relation="Ord"   
                                sql:key-fields="OrderID" >  
       <xsd:complexType>  
         <xsd:sequence>  
            <xsd:element name="Product" sql:relation="Product"   
                         sql:key-fields="ProductID"  
                         sql:relationship="OrderOD ODProduct">  
              <xsd:complexType>  
                 <xsd:attribute name="ProductID" type="xsd:int" />  
                 <xsd:attribute name="ProductName" type="xsd:string" />  
              </xsd:complexType>  
            </xsd:element>  
         </xsd:sequence>  
            <xsd:attribute name="OrderID"   type="xsd:integer" />   
            <xsd:attribute name="CustomerID"   type="xsd:string" />  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als SampleXMLData.xml. Fügen Sie das folgende XML-Dokument hinzu:  
  
    ```  
    <ROOT>    
      <Order OrderID="11" CustomerID="ALFKI">  
        <Product ProductID="11" ProductName="Chai" />  
        <Product ProductID="22" ProductName="Chang" />  
      </Order>  
      <Order OrderID="22" CustomerID="ANATR">  
         <Product ProductID="33" ProductName="Aniseed Syrup" />  
        <Product ProductID="44" ProductName="Gumbo Mix" />  
      </Order>  
    </ROOT>  
    ```  
  
4.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als ValidateAndBulkload.vbs. Fügen Sie dieser Datei den folgenden VBScript-Code hinzu: Ändern Sie die Verbindungszeichenfolge, um den entsprechenden Server- und Datenbanknamen bereitzustellen. Geben Sie den entsprechenden Pfad für die Dateien, die als Parameter für die **Execute** Methode.  
  
    ```  
    Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "C:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction = False  
    objBL.KeepIdentity = False  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    Set objBL = Nothing  
    MsgBox "Done."  
    ```  
  
5.  Führen Sie den VBScript-Code aus. Der XML-Massenladevorgang lädt die Daten in die entsprechenden Tabellen.  
  
## <a name="e-generating-table-schemas-before-bulk-loading"></a>E. Erstellen von Tabellenschemas vor dem Massenladen  
 Der XML-Massenladevorgang kann die Tabellen optional erstellen, wenn sie vor dem Massenladen nicht vorhanden sind. Festlegen der Eigenschaft "schemagen" SQLXMLBulkLoad-Objekt auf "true" wird dies. Sie können optional auch anfordern, dass XML-Massenladen an vorhandenen Tabellen löschen und Neuerstellen von SGDropTables-Eigenschaft auf "true" festlegen. Das folgende VBScript-Beispiel zeigt die Verwendung dieser Eigenschaften.  
  
 In diesem Beispiel werden außerdem zwei zusätzliche Eigenschaften auf TRUE festgelegt:  
  
-   CheckConstraints. Durch Festlegen dieser Eigenschaft auf TRUE wird sichergestellt, dass das Einfügen von Daten in die Tabellen keine Einschränkungen verletzt, die für die Tabellen festgelegt wurden (in diesem Fall die Einschränkungen PRIMARY KEY bzw. FOREIGN KEY für die Tabellen Cust und CustOrder). Liegt eine Einschränkungsverletzung vor, schlägt das Massenladen fehl.  
  
-   XMLFragment. Diese Eigenschaft muss auf TRUE festgelegt werden, da das XML-Beispieldokument (Datenquelle) kein einzelnes Element der obersten Ebene enthält (und daher ein Fragment ist).  
  
 Dies ist der VBScript-Code:  
  
```  
Dim objBL   
Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
  
objBL.CheckConstraints=true  
objBL.XMLFragment = True  
objBL.SchemaGen = True  
objBL.SGDropTables = True  
  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
Set objBL = Nothing  
```  
  
#### <a name="to-test-a-working-sample"></a>So testen Sie ein funktionstüchtiges Beispiel  
  
1.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als SampleSchema.xml. Fügen Sie der Datei das XSD-Schema aus dem oben aufgeführten Beispiel "Verwenden von Kettenbeziehungen im Schema für das XML-Massenladen" hinzu.  
  
2.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als SampleXMLData.xml. Fügen Sie der Datei das XML-Dokument aus dem oben aufgeführten Beispiel "Verwenden von Kettenbeziehungen im Schema für das XML-Massenladen" hinzu. Entfernen Sie die \<ROOT >-Element aus dem Dokument (um ein Fragment zu vereinfachen).  
  
3.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als ValidateAndBulkload.vbs. Fügen Sie dieser Datei den VBScript-Code in diesem Beispiel hinzu. Ändern Sie die Verbindungszeichenfolge, um den entsprechenden Server- und Datenbanknamen bereitzustellen. Geben Sie den entsprechenden Pfad für die Dateien, die als Parameter für die Execute-Methode angegeben werden.  
  
4.  Führen Sie den VBScript-Code aus. Der XML-Massenladevorgang erstellt die erforderlichen Tabellen basierend auf dem bereitgestellten Zuordnungsschema und lädt die Daten in einem Massenvorgang.  
  
## <a name="f-bulk-loading-from-a-stream"></a>F. Massenladen von einem Datenstrom  
 Die Execute-Methode des XML-Massenladen-Objektmodells verwendet zwei Parameter. Der erste Parameter ist die Zuordnungsschemadatei. Der zweite Parameter gibt die XML-Daten an, die in die Datenbank geladen werden sollen. Es gibt zwei Möglichkeiten, um die XML-Daten an die Execute-Methode des XML-Massenladen übergeben:  
  
-   Angeben des Dateinamen als Parameter  
  
-   Übergeben eines Datenstroms, der die XML-Daten enthält  
  
 Dieses Beispiel zeigt, wie ein Datenstrom in einem Massenvorgang geladen wird.  
  
 VBScript führt zunächst eine SELECT-Anweisung aus, um Kundeninformationen aus der Customers-Tabelle in der Northwind-Datenbank abzurufen. Da die FOR XML-Klausel (mit der ELEMENTS-Option) in der SELECT-Anweisung angegeben wurde, gibt die Abfrage ein elementzentriertes XML-Dokument in folgendem Format zurück:  
  
```  
<Customer>  
  <CustomerID>..</CustomerID>  
  <CompanyName>..</CompanyName>  
  <City>..</City>  
</Customer>  
...  
```  
  
 Das Skript übergibt dann den XML-Code als Datenstrom an die Execute-Methode als zweiten Parameter. Der Großteil der Execute-Methode lädt die Daten in die Cust-Tabelle.  
  
 Da dieses Skript die SchemaGen-Eigenschaft auf "true" und SGDropTables-Eigenschaft auf "true" festgelegt, erstellt XML-Massenladevorgang die Cust-Tabelle in der angegebenen Datenbank. (Wenn die Tabelle bereits vorhanden ist, löscht sie zuerst die Tabelle und erstellt sie dann erneut.)  
  
 Dies ist das VB-Script-Beispiel:  
  
```  
Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
Set objCmd = CreateObject("ADODB.Command")  
Set objConn = CreateObject("ADODB.Connection")  
Set objStrmOut = CreateObject ("ADODB.Stream")  
  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile     = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.SchemaGen        = True  
objBL.SGDropTables     = True  
objBL.XMLFragment      = True  
' Open a connection to the instance of SQL Server to get the source data.  
  
objConn.Open "provider=SQLOLEDB;server=(local);database=tempdb;integrated security=SSPI"  
Set objCmd.ActiveConnection = objConn  
objCmd.CommandText = "SELECT CustomerID, CompanyName, City FROM Customers FOR XML AUTO, ELEMENTS"  
  
' Open the return stream and execute the command.  
Const adCRLF = -1  
Const adExecuteStream = 1024  
objStrmOut.Open  
objStrmOut.LineSeparator = adCRLF  
objCmd.Properties("Output Stream").Value = objStrmOut  
objCmd.Execute , , adExecuteStream  
objStrmOut.Position = 0  
  
' Execute bulk load. Read source XML data from the stream.  
objBL.Execute "SampleSchema.xml", objStrmOut  
  
Set objBL = Nothing  
```  
  
 Das folgende XSD-Zuordnungsschema stellt die notwendigen Informationen bereit, um die Tabelle zu erstellen:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:element name="ROOT" sql:is-constant="true" >  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element ref="Customers"/>  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="Customers" sql:relation="Cust" >  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element name="CustomerID"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(5)"/>  
      <xsd:element name="CompanyName"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(40)"/>  
      <xsd:element name="City"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(40)"/>  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
</xsd:schema>  
```  
  
 Dies ist die entsprechende XDR-Schema:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
    </ElementType>  
</Schema>  
```  
  
### <a name="opening-a-stream-on-an-existing-file"></a>Öffnen eines Datenstroms in einer vorhandenen Datei  
 Sie können auch einen Datenstrom in eine vorhandene XML-Datendatei öffnen und übergeben Sie den Datenstrom als Parameter an die Execute-Methode (anstatt den Dateinamen als Parameter übergeben).  
  
 In diesem Visual Basic-Beispiel wird ein Datenstrom als Parameter übergeben:  
  
```  
Private Sub Form_Load()  
Dim objBL As New SQLXMLBulkLoad  
Dim objStrm As New ADODB.Stream  
Dim objFileSystem As New Scripting.FileSystemObject  
Dim objFile As Scripting.TextStream  
  
MsgBox "Begin BulkLoad..."  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.SchemaGen = True  
objBL.SGDropTables = True  
' Here again a stream is specified that contains the source data   
' (instead of the file name). But this is just an illustration.  
' Usually this is useful if you have an XML data   
' stream that is created by some other means that you want to bulk   
' load. This example starts with an XML text file, so it may not be the   
' best to use a stream (you can specify the file name directly).  
' Here you could have specified the file name itself.   
Set objFile = objFileSystem.OpenTextFile("c:\SampleData.xml")  
objStrm.Open  
objStrm.WriteText objFile.ReadAll  
objStrm.Position = 0  
objBL.Execute "c:\SampleSchema.xml", objStrm  
  
Set objBL = Nothing  
MsgBox "Done."  
End Sub  
```  
  
 Zum Testen der Anwendung verwenden Sie das folgende XML-Dokument in einer Datei (SampleData.xml) sowie das in diesem Beispiel angegebene XSD-Schema:  
  
 Dies sind die XML-Quelldaten (SampleData.xml):  
  
```  
<ROOT>  
  <Customers>  
    <CustomerID>1111</CustomerID>  
    <CompanyName>Hanari Carnes</CompanyName>  
    <City>NY</City>  
    <Order OrderID="1" />  
    <Order OrderID="2" />  
  </Customers>  
  
  <Customers>  
    <CustomerID>1112</CustomerID>  
    <CompanyName>Toms Spezialitten</CompanyName>  
     <City>LA</City>  
    <Order OrderID="3" />  
  </Customers>  
  <Customers>  
    <CustomerID>1113</CustomerID>  
    <CompanyName>Victuailles en stock</CompanyName>  
    <Order CustomerID= "4444" OrderID="4" />  
</Customers>  
</ROOT>  
```  
  
 Dies ist das entsprechende XDR-Schema:  
  
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
  
   <ElementType name="Customers" sql:relation="Cust"  >  
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
  
## <a name="g-bulk-loading-in-overflow-columns"></a>G. Massenladen in Überlaufspalten  
 Wenn das Zuordnungsschema eine Überlaufspalte mithilfe gibt der **Overflow-Feld** Anmerkung, XML-Massenladen alle nicht verbrauchte Daten aus dem Quelldokument in diese Spalte kopiert.  
  
 Betrachten Sie dieses XSD-Schema aus:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  <xsd:element name="Customers" sql:relation="Cust"  
                                sql:overflow-field="OverflowColumn" >  
   <xsd:complexType>  
     <xsd:sequence>  
       <xsd:element name="CustomerID"  type="xsd:integer" />  
       <xsd:element name="CompanyName" type="xsd:string" />  
       <xsd:element name="City"        type="xsd:string" />  
       <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
         <xsd:complexType>  
          <xsd:attribute name="OrderID" type="xsd:integer" />  
          <xsd:attribute name="CustomerID" type="xsd:integer" />  
         </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Das Schema identifiziert eine Überlaufspalte (OverflowColumn) für die Cust-Tabelle. Folglich alle XML-Daten für jede verbrauchten  **\<Kunden >** Element, das dieser Spalte hinzugefügt wird.  
  
> [!NOTE]  
>  Alle abstrakten Elemente (Elemente, für die **abstrakte = "true"** angegeben ist) und alle nicht zulässigen Attribute (Attribute, für die **verboten = "true"** angegeben wird) werden von XML-Massenladevorgang als Überlauf angesehen Laden und sind Overflow-Spalte hinzugefügt, wenn angegeben. (Andernfalls werden sie ignoriert.)  
  
#### <a name="to-test-a-working-sample"></a>So testen Sie ein funktionstüchtiges Beispiel  
  
1.  Erstellen Sie zwei Tabellen in **Tempdb** Datenbank:  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust (  
                  CustomerID     int         PRIMARY KEY,  
                  CompanyName    varchar(20) NOT NULL,  
                  City           varchar(20) DEFAULT 'Seattle',  
                  OverflowColumn nvarchar(200));  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID    int PRIMARY KEY,  
                  CustomerID int FOREIGN KEY   
                                 REFERENCES Cust(CustomerID));  
    GO  
    ```  
  
2.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als SampleSchema.xml. Fügen Sie der Datei das XSD-Schema hinzu, das in diesem Beispiel bereitgestellt wird.  
  
3.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als SampleXMLData.xml. Fügen Sie der Datei das folgende XML-Dokument hinzu:  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City><![CDATA[NY]]> </City>  
        <Junk>garbage in overflow</Junk>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
      </Customers>  
  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <![CDATA[LA]]>   
        <!-- <xyz><address>111 Maple, Seattle</address></xyz>   -->  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als ValidateAndBulkload.vbs. Fügen Sie dieser Datei den folgenden VBScript-Code (Microsoft Visual Basic Scripting Edition) hinzu. Ändern Sie die Verbindungszeichenfolge, um den entsprechenden Server- und Datenbanknamen bereitzustellen. Geben Sie den entsprechenden Pfad für die Dateien, die als Parameter für die Execute-Methode angegeben werden.  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  Führen Sie den VBScript-Code aus.  
  
 Dies ist das entsprechende XDR-Schema:  
  
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
  
## <a name="h-specifying-the-file-path-for-temp-files-in-transaction-mode"></a>H. Angeben des Dateipfads für temporäre Dateien im Transaktionsmodus  
 Wenn Sie Massenladevorgangs im Transaktionsmodus aktiviert sind (d. h., wenn die Transaktionseigenschaft auf "true" festgelegt ist), Sie müssen festlegen die TempFilePath-Eigenschaft, wenn eine der folgenden Bedingungen zutrifft:  
  
-   Sie führen einen Massenladevorgang zu einem Remoteserver aus.  
  
-   Sie möchten zum Speichern der Dateien, die im Transaktionsmodus erstellt werden, ein alternatives lokales Laufwerk oder einen alternativen Ordner verwenden (einen anderen als von der TEMP-Umgebungsvariable festgelegten Pfad).  
  
 Der folgende VBScript-Code lädt beispielsweise im Transaktionsmodus Daten in einem Massenvorgang von der Datei SampleXMLData.xml in die Datenbanktabellen. Die TempFilePath-Eigenschaft wird angegeben, um den Pfad für die temporären Dateien festzulegen, die im Transaktionsmodus generiert werden.  
  
```  
set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.Transaction=True  
objBL.TempFilePath="\\Server\MyDir"  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
set objBL=Nothing  
```  
  
> [!NOTE]  
>  Der Pfad für die temporäre Datei muss ein freigegebener Speicherort sein, auf den das Dienstkonto der Zielinstanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] und das Konto, das die Massenladeanwendung ausführt, zugreifen können. Es sei denn, Sie Massenimport von Daten auf einem lokalen Server sind, muss der Pfad für die temporäre Datei einen UNC-Pfad (z. B. \\\servername\sharename).  
  
#### <a name="to-test-a-working-sample"></a>So testen Sie ein funktionstüchtiges Beispiel  
  
1.  Erstellen Sie diese Tabelle im **Tempdb** Datenbank:  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust (     CustomerID uniqueidentifier,   
          LastName  varchar(20));  
    GO  
    ```  
  
2.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als SampleSchema.xml. Fügen Sie das folgende XSD-Schema in die Datei ein:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:attribute name="CustomerID"  type="xsd:string" />  
         <xsd:attribute name="LastName" type="xsd:string" />  
       </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als SampleXMLData.xml. Fügen Sie der Datei das folgende XML-Dokument hinzu:  
  
    ```  
    <ROOT>  
    <Customers CustomerID="6F9619FF-8B86-D011-B42D-00C04FC964FF"   
               LastName="Smith" />  
    </ROOT>  
    ```  
  
4.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als ValidateAndBulkload.vbs. Fügen Sie dieser Datei den folgenden VBScript-Code hinzu: Ändern Sie die Verbindungszeichenfolge, um den entsprechenden Server- und Datenbanknamen bereitzustellen. Geben Sie den entsprechenden Pfad für die Dateien, die als Parameter für die Execute-Methode angegeben werden. Geben Sie auch den entsprechenden Pfad für die TempFilePath-Eigenschaft.  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    objBL.TempFilePath="\\server\folder"  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  Führen Sie den VBScript-Code aus.  
  
     Das Schema muss das entsprechende angeben **SQL: DataType** für die **CustomerID** -Attribut festlegen, wenn der Wert für **CustomerID** wird angegeben, wie eine GUID mit Klammern ({} und}), z. B.:  
  
    ```  
    <ROOT>  
    <Customers CustomerID="{6F9619FF-8B86-D011-B42D-00C04FC964FF}"   
               LastName="Smith" />  
    </ROOT>  
    ```  
  
     Dies ist das aktualisierte Schema:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:attribute name="CustomerID"  type="xsd:string"   
                        sql:datatype="uniqueidentifier" />  
         <xsd:attribute name="LastName" type="xsd:string" />  
       </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
     Wenn **SQL: DataType** angegeben ist, der Spaltentyp als **"uniqueidentifier"**, des Massenladevorgangs entfernt die geschweiften Klammern ({und}) aus der **CustomerID** Wert vor dem Einfügen in der Spalte.  
  
 Dies ist das entsprechende XDR-Schema:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
<ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
</ElementType>  
<ElementType name="Customers" sql:relation="Cust" >  
  <AttributeType name="CustomerID"  sql:datatype="uniqueidentifier" />  
  <AttributeType name="LastName"   />  
  
  <attribute type="CustomerID" />  
  <attribute type="LastName"   />  
</ElementType>  
</Schema>  
```  
  
## <a name="i-using-an-existing-database-connection-with-the-connectioncommand-property"></a>I. Verwenden einer vorhandenen Datenbankverbindung mit der "ConnectionCommand"-Eigenschaft  
 Sie können eine vorhandene ADO-Verbindung für das XML-Massenladen verwenden. Dies ist dann hilfreich, wenn der XML-Massenladevorgang nur einer von mehreren Vorgängen ist, der für eine Datenquelle ausgeführt wird.  
  
 Der "connectioncommand"-Eigenschaft können Sie eine vorhandene ADO-Verbindung mit einer ADO-Befehlsobjekt verwenden. Dies wird im folgenden Visual Basic-Beispiel veranschaulicht:  
  
```  
Private Sub Form_Load()  
Dim objBL As New SQLXMLBulkLoad4  
Dim objCmd As New ADODB.Command  
Dim objConn As New ADODB.Connection  
  
'Open a connection to an instance of SQL Server.  
objConn.Open "provider=SQLOLEDB;data source=(local);database=tempdb;integrated security=SSPI"  
'Ask the Command object to use the connection just established.  
Set objCmd.ActiveConnection = objConn  
  
'Tell Bulk Load to use the active command object that is using the Connection obj.  
objBL.ConnectionCommand = objCmd  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
'The Transaction property must be set to True if you use ConnectionCommand.  
objBL.Transaction = True  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
Set objBL = Nothing  
End Sub  
```  
  
#### <a name="to-test-a-working-sample"></a>So testen Sie ein funktionstüchtiges Beispiel  
  
1.  Erstellen Sie zwei Tabellen in **Tempdb** Datenbank:  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust(  
                   CustomerID   varchar(5) PRIMARY KEY,  
                   CompanyName  varchar(30),  
                   City         varchar(20));  
    GO  
    CREATE TABLE CustOrder(  
                   CustomerID  varchar(5) references Cust (CustomerID),  
                   OrderID     varchar(5) PRIMARY KEY);  
    GO  
    ```  
  
2.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als SampleSchema.xml. Fügen Sie das folgende XSD-Schema in die Datei ein:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
    <xsd:annotation>  
      <xsd:appinfo>  
        <sql:relationship name="CustCustOrder"  
              parent="Cust"  
              parent-key="CustomerID"  
              child="CustOrder"  
              child-key="CustomerID" />  
      </xsd:appinfo>  
    </xsd:annotation>  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:sequence>  
           <xsd:element name="CustomerID"  type="xsd:integer" />  
           <xsd:element name="CompanyName" type="xsd:string" />  
           <xsd:element name="City"        type="xsd:string" />  
           <xsd:element name="Order"   
                              sql:relation="CustOrder"  
                              sql:relationship="CustCustOrder" >  
             <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:integer" />  
             </xsd:complexType>  
           </xsd:element>  
         </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als SampleXMLData.xml. Fügen Sie der Datei das folgende XML-Dokument hinzu:  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
      </Customers>  
  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <City>LA</City>  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  Erstellen Sie eine Visual Basic (Standard-EXE)-Anwendung und den vorangehenden Code. Fügen Sie dem Projekt die folgenden Verweise hinzu:  
  
    ```  
    Microsoft XML BulkLoad for SQL Server 4.0 Type Library  
    Microsoft ActiveX Data objects 2.6 Library  
    ```  
  
5.  Führen Sie die Anwendung.  
  
 Dies ist das entsprechende XDR-Schema:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
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
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
## <a name="j-bulk-loading-in-xml-data-type-columns"></a>J. Massenladen in XML-Datentypspalten  
 Wenn das Zuordnungsschema eine [Xml-Datentyp](../../../t-sql/xml/xml-transact-sql.md) Spalte, indem die **SQL: datatype = "Xml"** Anmerkung, XML-Massenladen kann untergeordnete XML-Elemente für das zugeordnete Feld aus dem Quelldokument in diese kopieren die Spalte.  
  
 Beachten Sie das folgende XSD-Schema, das eine Sicht der Production.ProductModel-Tabelle in der AdventureWorks-Beispieldatenbank zuordnet. In dieser Tabelle wird das CatalogDescription-Feld der **Xml** Datentyp zugeordnet ist, eine  **\<"DESC" >** Element mit dem **SQL: field** und **Sql: Datentyp = "Xml"** Anmerkungen.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
           xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
           xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">   
  <xsd:element name="ProductModel"  sql:relation="Production.ProductModel" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Name" type="xs:string"></xsd:element>  
        <xsd:element name="Desc" sql:field="CatalogDescription" sql:datatype="xml">  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element name="ProductDescription">  
              <xsd:complexType>  
                <xsd:sequence>  
                  <xsd:element name="Summary" type="xs:anyType"/>  
                </xsd:sequence>  
              </xsd:complexType>  
            </xsd:element>  
          </xsd:sequence>  
        </xsd:complexType>  
        </xsd:element>   
     </xsd:sequence>  
     <xsd:attribute name="ProductModelID" sql:field="ProductModelID" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
#### <a name="to-test-a-working-sample"></a>So testen Sie ein funktionstüchtiges Beispiel  
  
1.  Prüfen Sie, ob die AdventureWorks-Beispieldatenbank installiert ist.  
  
2.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als SampleSchema.xml. Kopieren Sie das oben stehende XSD-Schema, fügen Sie es in die Datei ein, und speichern Sie diese.  
  
3.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als SampleXMLData.xml. Kopieren Sie das folgende XML-Dokument, fügen Sie es in die Datei ein und speichern diese in dem selben Ordner, den Sie im vorherigen Schritt verwendet haben.  
  
    ```  
    <ProductModel ProductModelID="2005">  
        <Name>Mountain-100 (2005 model)</Name>  
        <Desc><?xml-stylesheet href="ProductDescription.xsl" type="text/xsl"?>  
            <p1:ProductDescription xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
                  xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
                  xmlns:wf="http://www.adventure-works.com/schemas/OtherFeatures"   
                  xmlns:html="http://www.w3.org/1999/xhtml"   
                  xmlns="">  
                <p1:Summary>  
                    <html:p>Our top-of-the-line competition mountain bike.   
          Performance-enhancing options include the innovative HL Frame,   
          super-smooth front suspension, and traction for all terrain.  
                            </html:p>  
                </p1:Summary>  
                <p1:Manufacturer>  
                    <p1:Name>AdventureWorks</p1:Name>  
                    <p1:Copyright>2002-2005</p1:Copyright>  
                    <p1:ProductURL>HTTP://www.Adventure-works.com</p1:ProductURL>  
                </p1:Manufacturer>  
                <p1:Features>These are the product highlights.   
                     <wm:Warranty>  
                        <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
                        <wm:Description>parts and labor</wm:Description>  
                    </wm:Warranty><wm:Maintenance>  
                        <wm:NoOfYears>10 years</wm:NoOfYears>  
                        <wm:Description>maintenance contract available through your dealer or any AdventureWorks retail store.</wm:Description>  
                    </wm:Maintenance><wf:wheel>High performance wheels.</wf:wheel><wf:saddle>  
                        <html:i>Anatomic design</html:i> and made from durable leather for a full-day of riding in comfort.</wf:saddle><wf:pedal>  
                        <html:b>Top-of-the-line</html:b> clipless pedals with adjustable tension.</wf:pedal><wf:BikeFrame>Each frame is hand-crafted in our Bothell facility to the optimum diameter   
          and wall-thickness required of a premium mountain frame.   
          The heat-treated welded aluminum frame has a larger diameter tube that absorbs the bumps.</wf:BikeFrame><wf:crankset> Triple crankset; alumunim crank arm; flawless shifting. </wf:crankset></p1:Features>  
                <!-- add one or more of these elements... one for each specific product in this product model -->  
                <p1:Picture>  
                    <p1:Angle>front</p1:Angle>  
                    <p1:Size>small</p1:Size>  
                    <p1:ProductPhotoID>118</p1:ProductPhotoID>  
                </p1:Picture>  
                <!-- add any tags in <specifications> -->  
                <p1:Specifications> These are the product specifications.  
                       <Material>Almuminum Alloy</Material><Color>Available in most colors</Color><ProductLine>Mountain bike</ProductLine><Style>Unisex</Style><RiderExperience>Advanced to Professional riders</RiderExperience></p1:Specifications>  
            </p1:ProductDescription>  
        </Desc>  
    </ProductModel>  
    ```  
  
4.  Erstellen Sie eine Datei in Ihrem bevorzugten Text- oder XML-Editor, und speichern Sie sie als BulkloadXml.vbs. Kopieren Sie den folgenden VBScript-Code, und fügen Sie ihn in die Datei ein. Speichern Sie die Datei in dem gleichen Ordner wie die vorherigen XML-Daten- und Schemadateien.  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=MyServer;database=AdventureWorks;integrated security=SSPI"  
  
    Dim fso, sAppPath  
    Set fso = CreateObject("Scripting.FileSystemObject")   
    sAppPath = fso.GetFolder(".")   
  
    objBL.ErrorLogFile = sAppPath & "\error.log"  
  
    'Execute XML bulkload using file.  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  Führen Sie das Skript BulkloadXml.vbs aus.  
  
  
