---
title: Angeben eines Zuordnungsschemas in einem Updategram (SQLXML 4.0) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
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
- annotated XSD schemas, updategrams
- data types [SQLXML], mapping schema in updategrams
- updategrams [SQLXML], annotated mapping schemas
- annotated XDR schemas, updategrams
- inverse attribute
- parent-child relationships [SQLXML]
- mapping-schema attribute
- mapping schema [SQLXML], updategrams
- sql:inverse
ms.assetid: 2e266ed9-4cfb-434a-af55-d0839f64bb9a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b7114229a879e05222d67cbb0147ced02628bfe9
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-40"></a>Angeben eines Zuordnungsschemas mit Anmerkungen in einem Updategram (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
In diesem Thema wird erläutert, wie das in einem Updategram angegebene Zuordnungsschema (XSD oder XDR) zur Verarbeitung von Updates verwendet wird. In einem Updategram, können Sie angeben, der Name des Zuordnungsschemas verwenden Sie bei der Zuordnung der Elemente und Attribute im Updategram zu Tabellen und Spalten in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Wenn in einem Updategram ein Zuordnungsschema angegeben ist, müssen die im Updategram festgelegten Element- und Attributnamen den Elementen und Attributen im Zuordnungsschema zugeordnet werden.  
  
 Um ein Zuordnungsschema anzugeben, verwenden Sie die **Zuordnungsschema** Attribut von der  **\<Sync >** Element. Die folgenden Beispiele zeigen zwei Updategrams: ein Updategram, das ein einfaches Zuordnungsschema verwendet, und ein Updategram, das ein komplexeres Schema verwendet.  
  
> [!NOTE]  
>  Diese Dokumentation setzt voraus, dass Sie mit Vorlagen und der Unterstützung von Zuordnungsschemas in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vertraut sind. Weitere Informationen finden Sie unter [Einführung in XSD-Schemas mit Anmerkungen versehen &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md). Ältere Anwendungen, die XDR verwenden, finden Sie unter [XDR-Schemas mit Anmerkungen versehen &#40; veraltet in SQLXML 4.0 &#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="dealing-with-data-types"></a>Umgehen mit Datentypen  
 Wenn im Schema angegeben die **Image**, **binäre**, oder **Varbinary** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp (mit **SQL: DataType**) verwendet und keine Geben Sie einen XML-Datentyp, der XML-Datentyp ist, geht das Updategram **binary Base64**. Wenn Ihre Daten **bin.base** geben, müssen Sie den Typ explizit angeben (**dt:type=bin.base** oder **Type = "xsd: hexBinary"**).  
  
 Wenn das Schema gibt die **"DateTime"**, **Datum**, oder **Zeit** XSD-Datentyp, müssen Sie auch angeben der entsprechenden [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp mit  **SQL: datatype = "DateTime"**.  
  
 Beim Verarbeiten von Parametern des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **Money** geben, müssen Sie explizit angeben **SQL: datatype = "Money"** auf dem entsprechenden Knoten im Zuordnungsschema.  
  
## <a name="examples"></a>Beispiele  
 Um funktionierende Beispiele, die über folgende Beispiele zu erstellen, müssen Sie in angegebenen Anforderungen erfüllen [Anforderungen für die Ausführung von SQLXML-Beispielen](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-creating-an-updategram-with-a-simple-mapping-schema"></a>A. Erstellen eines Updategrams mit einem einfachen Zuordnungsschema  
 Das folgende XSD-Schema (SampleSchema.xml) ist ein Zuordnungsschema, das ordnet die  **\<Kunden >** -Element der Sales.Customer-Tabelle:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
        <xsd:attribute name="CustID"    
                       sql:field="CustomerID"   
                       type="xsd:string" />  
        <xsd:attribute name="RegionID"    
                       sql:field="TerritoryID"    
                       type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Das folgende Updategram fügt einen Datensatz in die Sales.Customer-Tabelle ein und ordnet diese Daten anhand des vorherigen Zuordnungsschemas der Tabelle ordnungsgemäß zu. Beachten Sie, dass das Updategram den gleichen Elementnamen verwendet  **\<Kunden >**, wie im Schema definiert. Dies ist obligatorisch, da das Updategram ein bestimmtes Schema angibt.  
  
##### <a name="to-test-the-updategram"></a>So testen Sie das Updategram  
  
1.  Kopieren Sie den oben stehenden Schemacode, und fügen Sie ihn in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen SampleUpdateSchema.xml.  
  
2.  Kopieren Sie die unten stehende Updategramvorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Namen SampleUpdategram.xml im gleichen Verzeichnis, in dem Sie SampleUpdateSchema.xml gespeichert haben.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleUpdateSchema.xml">  
        <updg:before>  
          <Customer CustID="1" RegionID="1"  />  
        </updg:before>  
        <updg:after>  
          <Customer CustID="1" RegionID="2" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungschema (SampleUpdateSchema.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Dies ist das entsprechende XDR-Schema:  
  
```  
<?xml version="1.0" ?>  
   <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
         xmlns:dt="urn:schemas-microsoft-com:datatypes"   
         xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
     <ElementType name="Customer" sql:relation="Sales.Customer" >  
       <AttributeType name="CustID" />  
       <AttributeType name="RegionID" />  
  
       <attribute type="CustID" sql:field="CustomerID" />  
       <attribute type="RegionID" sql:field="TerritoryID" />  
     </ElementType>  
   </Schema>   
```  
  
### <a name="b-inserting-a-record-by-using-the-parent-child-relationship-specified-in-the-mapping-schema"></a>B. Einfügen eines Datensatzes durch Verwenden der im Zuordnungsschema angegebenen Über-/Unterordnungsbeziehung  
 Schemaelemente können in Beziehung gesetzt werden. Die  **\<SQL: Relationship >** Element gibt die über-/ unterordnungsbeziehung zwischen den Schemaelementen an. Mit diesen Informationen werden die entsprechenden Tabellen aktualisiert, die Primärschlüssel-Fremdschlüssel-Beziehungen aufweisen.  
  
 Das folgende Zuordnungsschema (SampleSchema.xml) besteht aus zwei Elementen  **\<Reihenfolge >** und  **\<OD >**:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="OD"   
                     sql:relation="Sales.SalesOrderDetail"  
                     sql:relationship="OrderOD" >  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID"   type="xsd:integer" />  
              <xsd:attribute name="ProductID" type="xsd:integer" />  
             <xsd:attribute name="UnitPrice"  type="xsd:decimal" />  
             <xsd:attribute name="OrderQty"   type="xsd:integer" />  
             <xsd:attribute name="UnitPriceDiscount"   type="xsd:decimal" />  
  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
        <xsd:attribute name="SalesOrderID"  type="xsd:integer" />  
        <xsd:attribute name="OrderDate"  type="xsd:date" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Das folgende Updategram verwendet dieses XSD-Schema zum Hinzufügen einer neuen bestelldetaildatensatz (ein  **\<OD >** Element in der  **\<nach >** Block) für Auftrag 43860. Die **Zuordnungsschema** Attribut wird verwendet, um das Zuordnungsschema im Updategram angegeben.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="SampleUpdateSchema.xml" >  
    <updg:before>  
       <Order SalesOrderID="43860" />  
    </updg:before>  
    <updg:after>  
      <Order SalesOrderID="43860" >  
           <OD ProductID="753" UnitPrice="$10.00"  
               Quantity="5" Discount="0.0" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>So testen Sie das Updategram  
  
1.  Kopieren Sie den oben stehenden Schemacode, und fügen Sie ihn in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen SampleUpdateSchema.xml.  
  
2.  Kopieren Sie die oben stehende Updategramvorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Namen SampleUpdategram.xml im gleichen Verzeichnis, in dem Sie SampleUpdateSchema.xml gespeichert haben.  
  
     Der für das Zuordnungschema (SampleUpdateSchema.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Dies ist das entsprechende XDR-Schema:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="OD" sql:relation="Sales.SalesOrderDetail" >  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="ProductID" />  
    <AttributeType name="UnitPrice"  dt:type="fixed.14.4" />  
    <AttributeType name="OrderQty" />  
    <AttributeType name="UnitPriceDiscount" />  
  
    <attribute type="SalesOrderID" />  
    <attribute type="ProductID" />  
    <attribute type="UnitPrice" />  
    <attribute type="OrderQty" />  
    <attribute type="UnitPriceDiscount" />  
</ElementType>  
  
<ElementType name="Order" sql:relation="Sales.SalesOrderHeader" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="OrderDate" />  
  
    <attribute type="CustomerID" />  
    <attribute type="SalesOrderID" />  
    <attribute type="OrderDate" />  
    <element type="OD" >  
             <sql:relationship   
                   key-relation="Sales.SalesOrderHeader"  
                   key="SalesOrderID"  
                   foreign-key="SalesOrderID"  
                   foreign-relation="Sales.SalesOrderDetail" />  
    </element>  
</ElementType>  
</Schema>  
```  
  
### <a name="c-inserting-a-record-by-using-the-parent-child-relationship-and-inverse-annotation-specified-in-the-xsd-schema"></a>C. Einfügen eines Datensatzes durch Verwenden der im XSD-Schema angegebenen Über-/Unterordnungsbeziehung und der inverse-Anmerkung  
 In diesem Beispiel wird veranschaulicht, wie die updategramlogik die über-/ unterordnungsbeziehung, angegeben in der XSD zur Verarbeitung von Updates verwendet und wie die **Inverse** Anmerkung verwendet wird. Weitere Informationen zu den **Inverse** Anmerkung, finden Sie unter [des SQL: Inverse-Attribut angeben, auf die SQL: Relationship &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md).  
  
 In diesem Beispiel wird davon ausgegangen, dass in den folgenden Tabellen sind die **Tempdb** Datenbank:  
  
-   `Cust (CustomerID, CompanyName)`, wobei `CustomerID` der Primärschlüssel ist  
  
-   `Ord (OrderID, CustomerID)`, wobei `CustomerID` ein Fremdschlüssel ist, der auf den `CustomerID` Primärschlüssel in der `Cust`-Tabelle verweist.  
  
 Das Updategram verwendet das folgende XSD-Schema, um Datensätze in die Cust und Ord-Tabellen einzufügen:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
       <sql:relationship name="OrdCust" inverse="true"  
                  parent="Ord"  
                  parent-key="CustomerID"  
                  child-key="CustomerID"  
                  child="Cust"/>  
  </xsd:appinfo>  
</xsd:annotation>  
  
<xsd:element name="Order" sql:relation="Ord">  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element ref="Customer" sql:relationship="OrdCust"/>  
    </xsd:sequence>  
    <xsd:attribute name="OrderID"   type="xsd:int"/>  
    <xsd:attribute name="CustomerID" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:element>  
  
<xsd:element name="Customer" sql:relation="Cust">  
  <xsd:complexType>  
     <xsd:attribute name="CustomerID"  type="xsd:string"/>  
    <xsd:attribute name="CompanyName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:element>  
  
</xsd:schema>  
```  
  
 Die XSD-Schema in diesem Beispiel sind  **\<Kunden >** und  **\<Reihenfolge >** Elemente und gibt eine über-/ unterordnungsbeziehung zwischen den beiden Elementen. Es identifiziert  **\<Reihenfolge >** als übergeordnetes Element und  **\<Kunden >** als untergeordnetes Element.  
  
 Die Verarbeitungslogik des Updategrams bestimmt mit den Informationen über die Über-/Unterordnungsbeziehung die Reihenfolge, in der die Datensätze in die Tabellen eingefügt werden. In diesem Beispiel wird die updategramlogik zuerst versucht, einen Datensatz in die Ord-Tabelle einzufügen (da  **\<Reihenfolge >** ist das übergeordnete Element) und dann versucht, einen Datensatz in die Cust-Tabelle einzufügen (da  **\<Customer >** das untergeordnete Element). Aufgrund der Primärschlüssel-Fremdschlüssel-Informationen, die im Datenbanktabellenschema enthalten sind, verursacht dieser Einfügevorgang jedoch eine Fremdschlüsselverletzung in der Datenbank und der Vorgang schlägt fehl.  
  
 Um die über-/ unterordnungsbeziehung während des Updatevorgangs umzukehren die updategramlogik anzuweisen, die **Inverse** -Anmerkung wird auf die  **\<Beziehung >** Element. Als Folge werden die Datensätze zuerst in die Cust-Tabelle und anschließend in die Ord-Tabelle eingefügt, und der Vorgang wird erfolgreich ausgeführt.  
  
 Das folgende Updategram fügt mit dem angegebenen XSD-Schema einen Auftrag (OrderID=2) in die Ord-Tabelle ein und einen Kunden (CustomerID='AAAAA') in die Cust-Tabelle.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="SampleUpdateSchema.xml" >  
    <updg:before/>  
    <updg:after>  
      <Order OrderID="2" CustomerID="AAAAA" >  
        <Customer CustomerID="AAAAA" CompanyName="AAAAA Company" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>So testen Sie das Updategram  
  
1.  Erstellen Sie diese Tabellen in der **Tempdb** Datenbank:  
  
    ```  
    USE tempdb  
    CREATE TABLE Cust(CustomerID varchar(5) primary key,   
                      CompanyName varchar(20))  
    GO  
    CREATE TABLE Ord (OrderID int primary key,   
                      CustomerID varchar(5) references Cust(CustomerID))  
    GO  
    ```  
  
2.  Kopieren Sie den oben stehenden Schemacode, und fügen Sie ihn in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen SampleUpdateSchema.xml.  
  
3.  Kopieren Sie die oben stehende Updategramvorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Namen SampleUpdategram.xml im gleichen Verzeichnis, in dem Sie SampleUpdateSchema.xml gespeichert haben.  
  
     Der für das Zuordnungschema (SampleUpdateSchema.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
4.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheitsüberlegungen zu Updategrams &#40; SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
