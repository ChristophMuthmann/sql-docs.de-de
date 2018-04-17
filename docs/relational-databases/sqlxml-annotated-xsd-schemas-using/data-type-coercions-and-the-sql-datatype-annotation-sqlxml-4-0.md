---
title: 'Datentypumwandlungen und die SQL: DataType-Anmerkung (SQLXML 4.0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/17/2017
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
- mapping data types [SQLXML]
- type attribute
- sql:datatype
- data types [SQLXML], converting
- annotated XSD schemas, mapping data types
- xsd:type
- datatype annotation
- converting data types [SQLXML]
- data types [SQLXML], mapping data types
- XSD schemas [SQLXML], mapping data types
ms.assetid: db192105-e8aa-4392-b812-9d727918c005
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8a2dc2c3d91eea67e9e08a87d5aa7735a1b45b1f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="data-type-coercions-and-the-sqldatatype-annotation-sqlxml-40"></a>Datentypumwandlungen und die sql:datatype-Anmerkung (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In einem XSD-Schema der **xsd: Type** -Attribut gibt den XSD-Datentyp eines Elements oder Attributs an. Wenn Daten anhand eines XSD-Schemas aus der Datenbank extrahiert werden, wird der angegebene Datentyp zur Formatierung der Daten verwendet.  
  
 Zusätzlich zur XSD-Typ in einem Schema angeben, können Sie auch eine Microsoft angeben [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentyp mithilfe der **SQL: DataType** Anmerkung. Die **xsd: Type** und **SQL: DataType** Attribute steuern die Zuordnung zwischen XSD-Datentypen und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentypen.  
  
## <a name="xsdtype-attribute"></a>xsd:type-Attribut  
 Sie können die **xsd: Type** -Attribut zum Angeben des XML-Datentyp eines Attributs oder Elements, das einer Spalte zugeordnet. Die **xsd: Type** wirkt sich auf das Dokument, das zurückgegeben wird, von dem Server als auch die XPath-Abfrage, die ausgeführt wird. Wenn eine XPath-Abfrage ausgeführt wird, ein Zuordnungsschema, das enthält **xsd: Type**, verwendet XPath den angegebenen Datentyp beim Verarbeiten der Abfrage. Weitere Informationen zur Verwendung von XPath **xsd: Type**, finden Sie unter [Zuordnung von XSD-Datentypen zu XPath-Datentypen &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md).  
  
 In einem zurückgegebenen Dokument werden alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentypen in Zeichenfolgendarstellungen konvertiert. Einige Datentypen erfordern zusätzliche Konvertierungen. Die folgende Tabelle enthält die Konvertierungen, die für verschiedene **xsd: Type** Werte.  
  
|XSD-Datentyp|SQL Server-Konvertierung|  
|-------------------|---------------------------|  
|Boolean|CONVERT(bit, COLUMN)|  
|Datum|LEFT(CONVERT(nvarchar(4000), COLUMN, 126), 10)|  
|Decimal|CONVERT(money, COLUMN)|  
|id/idref/idrefs|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|nmtoken/nmtokens|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|Zeit|SUBSTRING(CONVERT(nvarchar(4000), COLUMN, 126), 1+CHARINDEX(N'T', CONVERT(nvarchar(4000), COLUMN, 126)), 24)|  
|Alle sonstigen|Keine zusätzliche Konvertierung|  
  
> [!NOTE]  
>  Einige der Werte von zurückgegebenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] möglicherweise nicht kompatibel mit den XML-Datentypen, die mit **xsd: Type**, entweder weil die Konvertierung nicht möglich ist (z. B. Konvertieren von "XYZ" in eine  **Decimal** -Datentyp) oder weil der Wert den Bereich dieses Datentyps überschreitet (z. B.-100000 in einen **UnsignedShort** XSD-Typ). Inkompatible Typkonvertierungen führen möglicherweise zu ungültigen XML-Dokumenten oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlern.  
  
## <a name="mapping-from-sql-server-data-types-to-xsd-data-types"></a>Zuordnen von SQL Server-Datentypen zu XSD-Datentypen  
 In der folgenden Tabelle wird eine offensichtliche Zuordnung zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentypen und XSD-Datentypen gezeigt. Wenn Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Typ kennen, können Sie dieser Tabelle den entsprechenden XSD-Typ für das XSD-Schema entnehmen.  
  
|SQL Server-Datentyp|XSD-Datentyp|  
|--------------------------|-------------------|  
|**bigint**|**long**|  
|**binary**|**base64Binary**|  
|**bit**|**boolean**|  
|**char**|**Zeichenfolge**|  
|**datetime**|**dateTime**|  
|**decimal**|**decimal**|  
|**float**|**double**|  
|**image**|**base64Binary**|  
|**int**|**int**|  
|**money**|**decimal**|  
|**nchar**|**Zeichenfolge**|  
|**ntext**|**Zeichenfolge**|  
|**nvarchar**|**Zeichenfolge**|  
|**numeric**|**decimal**|  
|**real**|**float**|  
|**smalldatetime**|**dateTime**|  
|**smallint**|**short**|  
|**smallmoney**|**decimal**|  
|**sql_variant**|**Zeichenfolge**|  
|**sysname**|**Zeichenfolge**|  
|**text**|**Zeichenfolge**|  
|**timestamp**|**dateTime**|  
|**tinyint**|**unsignedByte**|  
|**varbinary**|**base64Binary**|  
|**varchar**|**Zeichenfolge**|  
|**uniqueidentifier**|**Zeichenfolge**|  
  
## <a name="sqldatatype-annotation"></a>sql:datatype-Anmerkung  
 Die **SQL: DataType** Anmerkung dient zum Angeben der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentyp; diese Anmerkung muss angegeben werden, wenn:  
  
-   Sie sind Massenladen in eine **"DateTime"** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Spalte von einem XSD- **"DateTime"**, **Datum**, oder **Zeit** Typ. In diesem Fall müssen Sie bestimmen die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Spaltendatentyp mithilfe **SQL: datatype = "DateTime"**. Diese Regel gilt auch für Updategrams.  
  
-   Sie sind Massenladen in eine Spalte mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **"uniqueidentifier"** Typ und der XSD-Wert ist eine GUID mit Klammern ({und}). Geben Sie bei **SQL: datatype = "Uniqueidentifier"**, die geschweiften Klammern werden aus dem Wert entfernt, bevor er in der Spalte eingefügt wird. Wenn **SQL: DataType** nicht angegeben ist, wird der Wert wird gesendet, mit den geschweiften Klammern und die INSERT- oder Update ein Fehler auftritt.  
  
-   Der XML-Datentyp **base64Binary** Zuordnungen zu verschiedenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentypen (**binäre**, **Image**, oder **Varbinary**). Zuordnen von XML-Datentyps **base64Binary** bis zu einem bestimmten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentyp, verwenden Sie die **SQL: DataType** Anmerkung. Diese Anmerkung gibt den expliziten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentyp der Spalte an, der das Attribut zugeordnet ist. Dies ist nützlich, wenn Daten in der Datenbank gespeichert werden. Durch Angabe der **SQL: DataType** -Anmerkung können Sie erkennen das explizite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentyp.  
  
 Es wird im Allgemeinen empfohlen, die Angabe **SQL: DataType** im Schema.  
  
## <a name="examples"></a>Beispiele  
 Es müssen bestimmte Anforderungen erfüllt sein, damit aus den folgenden Beispielen funktionierende Beispiele erstellt werden können. Weitere Informationen finden Sie unter [Anforderungen für die Ausführung von SQLXML-Beispielen](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-xsdtype"></a>A. Angeben von "xsd:type"  
 In diesem Beispiel wird gezeigt, wie XSD-Code **Datum** Typ, der mithilfe des Parameters der **xsd: Type** -Attribut im Schema wirkt sich auf die resultierenden XML-Dokument. Das Schema stellt eine XML-Ansicht der Tabelle Sales.SalesOrderHeader in der AdventureWorks-Datenbank bereit.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader">  
     <xsd:complexType>  
       <xsd:attribute name="SalesOrderID" type="xsd:string" />   
       <xsd:attribute name="CustomerID"   type="xsd:string" />   
       <xsd:attribute name="OrderDate"    type="xsd:date" />   
       <xsd:attribute name="DueDate"  />   
       <xsd:attribute name="ShipDate"  type="xsd:time" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 In diesem XSD-Schema gibt es drei Attribute, die einen Datumswert von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurückgeben. Wenn das Schema:  
  
-   Gibt an, **xsd: Type = Datum** auf die **OrderDate** -Attribut der Date-Teil, der den Rückgabewert von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die **OrderDate** Attribut angezeigt wird.  
  
-   Gibt an, **xsd: Type = Zeit** auf die **ShipDate** -Attribut den Uhrzeitteil des Werts, der von zurückgegeben wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die **ShipDate** Attribut angezeigt wird.  
  
-   Gibt keinen **xsd: Type** auf die **DueDate** Attribut, den gleichen Wert, der zurückgegebene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird angezeigt.  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>So testen Sie eine Beispiel-XPath-Abfrage anhand des Schemas  
  
1.  Kopieren Sie den oben stehenden Schemacode, und fügen Sie ihn in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen xsdType.xml.  
  
2.  Kopieren Sie die folgende Vorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Namen xsdTypeT.xml im gleichen Verzeichnis wie sdType.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="xsdType.xml">  
        /Order  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungsschema (xsdType.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert ist. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\xsdType.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Im Folgenden wird ein Teil des Resultsets aufgeführt:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="43659"   
         CustomerID="676"   
         OrderDate="2001-07-01"   
         DueDate="2001-07-13T00:00:00"   
         ShipDate="00:00:00" />   
  <Order SalesOrderID="43660"   
         CustomerID="117"   
         OrderDate="2001-07-01"   
         DueDate="2001-07-13T00:00:00"   
         ShipDate="00:00:00" />   
 ...  
</ROOT>  
```  
  
 Dies ist das entsprechende XDR-Schema:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="Order" sql:relation="Sales.SalesOrderHeader">  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="CustomerID"  />  
    <AttributeType name="OrderDate" dt:type="date" />  
    <AttributeType name="DueDate" />  
    <AttributeType name="ShipDate" dt:type="time" />  
  
    <attribute type="SalesOrderID" sql:field="OrderID" />  
    <attribute type="CustomerID" sql:field="CustomerID" />  
    <attribute type="OrderDate" sql:field="OrderDate" />  
    <attribute type="DueDate" sql:field="DueDate" />  
    <attribute type="ShipDate" sql:field="ShipDate" />  
</ElementType>  
</Schema>  
```  
  
### <a name="b-specifying-sql-data-type-using-sqldatatype"></a>B. Angeben des SQL-Datentyps mit "sql:datatype"  
 Ein funktionierendes Beispiel finden Sie unter Beispiel G in [XML Bulk Load Beispiele &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md). In diesem Beispiel wird ein GUID-Wert, der "{" und "}" enthält, massengeladen. Gibt an, das Schema in diesem Beispiel **SQL: DataType** zum Identifizieren der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentyp als **"uniqueidentifier"**. In diesem Beispiel wird veranschaulicht, wann **SQL: DataType** im Schema angegeben werden.  
  
  
