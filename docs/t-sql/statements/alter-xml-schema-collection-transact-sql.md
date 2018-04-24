---
title: ALTER XML SCHEMA COLLECTION (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_XML_SCHEMA_COLLECTION_TSQL
- ALTER XML SCHEMA COLLECTION
dev_langs:
- TSQL
helpviewer_keywords:
- schema collections [SQL Server], altering
- xml_schema_namespace function
- adding schema components
- ALTER XML SCHEMA COLLECTION statement
- XML schemas [SQL Server], adding
- XML schema collections [SQL Server], modifying
- schema collections [SQL Server], adding components
- XML schema collections [SQL Server], adding components
- importing schemas
- XML schema collections [SQL Server], altering
- schema collections [SQL Server], modifying
- multiple schema namespaces
ms.assetid: e311c425-742a-4b0d-b847-8b974bf66d53
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc97d52c0d3d67443f6ed83f24db1104b7be47ee
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alter-xml-schema-collection-transact-sql"></a>ALTER XML SCHEMA COLLECTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt einer vorhandenen XML-Schemaauflistung neue Schemakomponenten hinzu.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER XML SCHEMA COLLECTION [ relational_schema. ]sql_identifier ADD 'Schema Component'  
```  
  
## <a name="arguments"></a>Argumente  
 *relational_schema*  
 Identifiziert den Namen des relationalen Schemas. Wenn kein Name angegeben ist, wird das relationale Standardschema verwendet.  
  
 *sql_identifier*  
 Der SQL-Bezeichner für die XML-Schemaauflistung.  
  
 **'** *Schema Component* **'**  
 Die einzufügende Schemakomponente.  
  
## <a name="remarks"></a>Remarks  
 Verwenden Sie ALTER XML SCHEMA COLLECTION zum Einfügen neuer XML-Schemas, deren Namespaces noch nicht in der XML-Schemaauflistung vorhanden sind, oder zum Hinzufügen neuer Komponenten zu vorhandenen Namespaces in der Auflistung.  
  
 Im folgenden Beispiel wird dem vorhandenen Namespace `http://MySchema/test_xml_schema` in der Collection `MyColl` ein neues \<Element> hinzugefügt.  
  
```  
-- First create an XML schema collection.  
CREATE XML SCHEMA COLLECTION MyColl AS '  
   <schema   
    xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="http://MySchema/test_xml_schema">  
      <element name="root" type="string"/>   
  </schema>'  
-- Modify the collection.   
ALTER XML SCHEMA COLLECTION MyColl ADD '  
  <schema xmlns="http://www.w3.org/2001/XMLSchema"   
         targetNamespace="http://MySchema/test_xml_schema">   
     <element name="anotherElement" type="byte"/>   
 </schema>';  
```  
  
 `ALTER XML SCHEMA` fügt das Element `<anotherElement>` dem zuvor definierten `http://MySchema/test_xml_schema`-Namespace hinzu.  
  
 Falls einige der Komponenten, die Sie in den Auflistungsverweiskomponenten hinzufügen möchten, bereits in derselben Auflistung vorhanden sind, müssen Sie `<import namespace="referenced_component_namespace" />` verwenden. Es ist jedoch nicht zulässig, den aktuellen Schemanamespace in `<xsd:import>` zu verwenden. Deshalb werden Komponenten aus demselben Zielnamespace wie der aktuelle Schemanamespace automatisch importiert.  
  
 Informationen zum Entfernen von Collections finden Sie unter [DROP XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md).  
  
 Wenn die Schemaauflistung bereits ein Platzhalterzeichen für die Lax-Überprüfung oder ein Element vom Typ **xs:anyType** enthält, wird beim Hinzufügen eines neuen globalen Elements oder Typs bzw. einer Attributdeklaration zu der Schemaauflistung eine erneute Überprüfung aller gespeicherten Daten ausgeführt, die durch die Schemaauflistung beschränkt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Ändern von XML SCHEMA COLLECTION ist die ALTER-Berechtigung für die Auflistung erforderlich.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-xml-schema-collection-in-the-database"></a>A. Erstellen einer XML-Schemaauflistung in der Datenbank  
 Im folgenden Beispiel wird die XML-Schemaauflistung `ManuInstructionsSchemaCollection` erstellt. Diese Auflistung hat nur einen Schemanamespace.  
  
```  
-- Create a sample database in which to load the XML schema collection.  
CREATE DATABASE SampleDB;  
GO  
USE SampleDB;  
GO  
CREATE XML SCHEMA COLLECTION ManuInstructionsSchemaCollection AS  
N'<?xml version="1.0" encoding="UTF-16"?>  
<xsd:schema targetNamespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"   
   xmlns          ="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"   
   elementFormDefault="qualified"   
   attributeFormDefault="unqualified"  
   xmlns:xsd="http://www.w3.org/2001/XMLSchema" >  
  
    <xsd:complexType name="StepType" mixed="true" >  
        <xsd:choice  minOccurs="0" maxOccurs="unbounded" >   
            <xsd:element name="tool" type="xsd:string" />  
            <xsd:element name="material" type="xsd:string" />  
            <xsd:element name="blueprint" type="xsd:string" />  
            <xsd:element name="specs" type="xsd:string" />  
            <xsd:element name="diag" type="xsd:string" />  
        </xsd:choice>   
    </xsd:complexType>  
  
    <xsd:element  name="root">  
        <xsd:complexType mixed="true">  
            <xsd:sequence>  
                <xsd:element name="Location" minOccurs="1" maxOccurs="unbounded">  
                    <xsd:complexType mixed="true">  
                        <xsd:sequence>  
                            <xsd:element name="step" type="StepType" minOccurs="1" maxOccurs="unbounded" />  
                        </xsd:sequence>  
                        <xsd:attribute name="LocationID" type="xsd:integer" use="required"/>  
                        <xsd:attribute name="SetupHours" type="xsd:decimal" use="optional"/>  
                        <xsd:attribute name="MachineHours" type="xsd:decimal" use="optional"/>  
                        <xsd:attribute name="LaborHours" type="xsd:decimal" use="optional"/>  
                        <xsd:attribute name="LotSize" type="xsd:decimal" use="optional"/>  
                    </xsd:complexType>  
                </xsd:element>  
            </xsd:sequence>  
        </xsd:complexType>  
    </xsd:element>  
</xsd:schema>' ;  
GO  
-- Verify - list of collections in the database.  
SELECT *  
FROM sys.xml_schema_collections;  
-- Verify - list of namespaces in the database.  
SELECT name  
FROM sys.xml_schema_namespaces;  
  
-- Use it. Create a typed xml variable. Note the collection name   
-- that is specified.  
DECLARE @x xml (ManuInstructionsSchemaCollection);  
GO  
--Or create a typed xml column.  
CREATE TABLE T (  
        i int primary key,   
        x xml (ManuInstructionsSchemaCollection));  
GO  
-- Clean up.  
DROP TABLE T;  
GO  
DROP XML SCHEMA COLLECTION ManuInstructionsSchemaCollection;  
Go  
USE master;  
GO  
DROP DATABASE SampleDB;  
```  
  
 Alternativ können Sie die Schemaauflistung einer Variablen zuweisen und die Variable in der `CREATE XML SCHEMA COLLECTION`-Anweisung wie folgt angeben:  
  
```  
DECLARE @MySchemaCollection nvarchar(max);  
SET @MySchemaCollection  = N' copy the schema collection here';  
CREATE XML SCHEMA COLLECTION AS @MySchemaCollection;   
```  
  
 Die Variable im Beispiel ist vom Datentyp `nvarchar(max)`. Möglich ist auch der Datentyp **xml**. In diesem Fall wird die Variable implizit in eine Zeichenfolge konvertiert.  
  
 Weitere Informationen finden Sie unter [Anzeigen einer gespeicherten XML-Schemaauflistung](../../relational-databases/xml/view-a-stored-xml-schema-collection.md).  
  
 Schemaauflistungen können in einer Spalte vom Datentyp **xml** gespeichert werden. Führen Sie in diesem Fall die folgenden Schritte aus, um eine XML-Schemaauflistung zu erstellen:  
  
1.  Rufen Sie die Schemaauflistung mithilfe einer SELECT-Anweisung aus der Spalte ab, und weisen Sie sie einer Variablen vom Datentyp **xml** oder **varchar** zu.  
  
2.  Geben Sie den Variablennamen in der CREATE XML SCHEMA COLLECTION-Anweisung an.  
  
 Die CREATE XML SCHEMA COLLECTION-Anweisung speichert nur die Schemakomponenten, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpretieren kann. Nicht alles im XML-Schema wird in der Datenbank gespeichert. Wenn Sie den ursprünglichen Zustand der XML-Schemaauflistung wiederherstellen möchten, sollten Sie daher Ihre XML-Schemas in einer Datenbankspalte oder in einem anderen Ordner auf dem Computer speichern.  
  
### <a name="b-specifying-multiple-schema-namespaces-in-a-schema-collection"></a>B. Angeben mehrerer Schemanamespaces in einer Schemaauflistung  
 Sie können mehrere XML-Schemas angeben, wenn Sie eine XML-Schemaauflistung erstellen. Zum Beispiel:  
  
```  
CREATE XML SCHEMA COLLECTION N'  
<xsd:schema>....</xsd:schema>  
<xsd:schema>...</xsd:schema>';  
```  
  
 Im folgenden Beispiel wird die XML-Schemaauflistung `ProductDescriptionSchemaCollection` erstellt, die zwei XML-Schemanamespaces enthält.  
  
```  
CREATE XML SCHEMA COLLECTION ProductDescriptionSchemaCollection AS   
'<xsd:schema targetNamespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"  
    xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
    elementFormDefault="qualified"   
    xmlns:xsd="http://www.w3.org/2001/XMLSchema" >  
    <xsd:element name="Warranty"  >  
        <xsd:complexType>  
            <xsd:sequence>  
                <xsd:element name="WarrantyPeriod" type="xsd:string"  />  
                <xsd:element name="Description" type="xsd:string"  />  
            </xsd:sequence>  
        </xsd:complexType>  
    </xsd:element>  
</xsd:schema>  
 <xs:schema targetNamespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
    xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
    elementFormDefault="qualified"   
    xmlns:mstns="http://tempuri.org/XMLSchema.xsd"   
    xmlns:xs="http://www.w3.org/2001/XMLSchema"  
    xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain" >  
    <xs:import   
namespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain" />  
    <xs:element name="ProductDescription" type="ProductDescription" />  
        <xs:complexType name="ProductDescription">  
            <xs:sequence>  
                <xs:element name="Summary" type="Summary" minOccurs="0" />  
            </xs:sequence>  
            <xs:attribute name="ProductModelID" type="xs:string" />  
            <xs:attribute name="ProductModelName" type="xs:string" />  
        </xs:complexType>  
        <xs:complexType name="Summary" mixed="true" >  
            <xs:sequence>  
                <xs:any processContents="skip" namespace="http://www.w3.org/1999/xhtml" minOccurs="0" maxOccurs="unbounded" />  
            </xs:sequence>  
        </xs:complexType>  
</xs:schema>'  
;  
GO   
-- Clean up  
DROP XML SCHEMA COLLECTION ProductDescriptionSchemaCollection;  
GO  
```  
  
### <a name="c-importing-a-schema-that-does-not-specify-a-target-namespace"></a>C. Importieren eines Schemas ohne Zielnamespaceangabe  
 Falls ein Schema, das kein **targetNamespace**-Attribut enthält, in eine Collection importiert wird, werden dessen Komponenten wie im folgenden Beispiel dem Zielnamespace mit einer leeren Zeichenfolge zugeordnet. Wenn nicht mindestens ein importiertes Schema in der Auflistung zugeordnet wird, werden mehrere Schemakomponenten (möglicherweise nicht verknüpfte Komponenten) dem standardmäßigen Namespace mit einer leeren Zeichenfolge zugeordnet.  
  
```  
-- Create a collection that contains a schema with no target namespace.  
CREATE XML SCHEMA COLLECTION MySampleCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  xmlns:ns="http://ns">  
<element name="e" type="dateTime"/>  
</schema>';  
GO  
-- query will return the names of all the collections that   
--contain a schema with no target namespace  
SELECT sys.xml_schema_collections.name   
FROM   sys.xml_schema_collections   
JOIN   sys.xml_schema_namespaces   
ON     sys.xml_schema_collections.xml_collection_id =   
       sys.xml_schema_namespaces.xml_collection_id   
WHERE  sys.xml_schema_namespaces.name='';  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)   
 [DROP XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Anforderungen und Einschränkungen für XML-Schemaauflistungen auf dem Server](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
