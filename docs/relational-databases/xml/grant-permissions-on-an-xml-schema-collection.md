---
title: "Erteilen von Berechtigungen für eine XML-Schemaauflistung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- granting permissions [SQL Server], XML schema collections
- ALTER permission
ms.assetid: ffbb829c-3b8f-4e5d-97d9-ab4059aab0db
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 686fe65b9749fbafd2052d7a531f11aae44c6b65
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="grant-permissions-on-an-xml-schema-collection"></a>Erteilen von Berechtigungen für eine XML-Schemaauflistung
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
Sie können Berechtigungen zum Erstellen von XML-Schemaauflistungen sowie Berechtigungen für ein XML-Schemaauflistungsobjekt erteilen.  
  
## <a name="granting-permission-to-create-an-xml-schema-collection"></a>Berechtigung zum Erstellen einer XML-Schemaauflistung  
 Zum Erstellen einer XML-Schemaauflistung sind die folgenden Berechtigungen erforderlich:  
  
-   Der Prinzipal benötigt die CREATE XML SCHEMA COLLECTION-Berechtigung auf Datenbankebene.  
  
-   Da die XML-Schemaauflistungen relationale Schemas als Bereiche besitzen, muss der Prinzipal außerdem die ALTER-Berechtigung für das relationale Schema besitzen.  
  
 Mithilfe der folgenden Berechtigungen kann ein Prinzipal eine XML-Schemaauflistung in einem relationalen Schema in einer Datenbank auf einem Server erstellen:  
  
-   CONTROL-Berechtigung auf dem Server  
  
-   ALTER ANY DATABASE-Berechtigung auf dem Server  
  
-   ALTER-Berechtigung für die Datenbank  
  
-   CONTROL-Berechtigung in der Datenbank  
  
-   ALTER ANY SCHEMA-Berechtigung und CREATE XML SCHEMA COLLECTION-Berechtigung in der Datenbank  
  
-   ALTER- oder CONTROL-Berechtigung für das relationale Schema und CREATE XML SCHEMA COLLECTION-Berechtigung in der Datenbank  
  
 Die letztgenannten Berechtigungen werden im folgenden Beispiel verwendet.  
  
 Der Besitzer des relationalen Schemas wird zum Besitzer der XML-Schemaauflistung, die in diesem Schema erstellt wird. Dieser Besitzer besitzt die vollständige Kontrolle über die XML-Schemaauflistung. Aus diesem Grund kann dieser Besitzer die XML-Schemaauflistung ändern, eine xml-Spalte typisieren oder die XML-Schemaauflistung löschen.  
  
## <a name="granting-permissions-on-an-xml-schema-collection-object"></a>Erteilen von Berechtigungen für ein XML-Schemaauflistungsobjekt  
 Die folgenden Berechtigungen sind für die XML-Schemaauflistung zulässig:  
  
-   Die ALTER-Berechtigung ist erforderlich, wenn der Inhalt einer vorhandenen XML-Schemaauflistung mithilfe der ALTER XML SCHEMA COLLECTION-Anweisung geändert wird.  
  
-   Mit der CONTROL-Berechtigung kann ein Benutzer beliebige Vorgänge mit der XML-Schemaauflistung ausführen.  
  
-   Die TAKE OWNERSHIP-Berechtigung ist zum Übertragen des Besitzes der XML-Schemaauflistung von einem Prinzipal an einen anderen erforderlich.  
  
-   Mit der REFERENCES-Berechtigung wird der Prinzipal dazu autorisiert, mithilfe der XML-Schemaauflistung Spalten des **xml** -Typs in Tabellen und Sichten sowie Parametern zu typisieren oder einzuschränken. Die REFERENCES-Berechtigung ist auch erforderlich, wenn eine XML-Schemaauflistung auf eine andere verweist.  
  
-   Die VIEW DEFINITION-Berechtigung ermöglicht dem Prinzipal das Abfragen des Inhalts einer XML-Schemaauflistung mithilfe von XML_SCHEMA_NAMESPACE oder Katalogsichten, wenn dieser Prinzipal auch eine der ALTER-, REFERENCES- oder CONTROL-Berechtigungen für die Auflistung besitzt.  
  
-   Die EXECUTE-Berechtigung ist zum Überprüfen von Werten erforderlich, die vom Prinzipal für die XML-Schemaauflistung eingefügt oder aktualisiert werden, durch die Spalten, Variablen und Parameter vom Typ **xml** typisiert oder einschränkt werden. Sie benötigen diese Berechtigung auch, wenn Sie das in diesen Spalten und Variablen gespeicherte XML abfragen.  
  
## <a name="examples"></a>Beispiele  
 Die Szenarien in den folgenden Beispielen veranschaulichen, wie XML-Schemaberechtigungen funktionieren. Jedes dieser Beispiele erstellt die erforderliche Testdatenbank, die relationalen Schemas und Anmeldungen. Diesen Anmeldenamen werden die erforderlichen Berechtigungen für XML-Schemaauflistungen erteilt. Jedes der Beispiele führt am Ende den erforderlichen Cleanup aus.  
  
### <a name="a-granting-permissions-to-create-an-xml-schema-collection"></a>A. Erteilen der Berechtigungen zum Erstellen einer XML-Schemaauflistung  
 Im folgenden Beispiel wird gezeigt, wie Berechtigungen erteilt werden, damit ein Prinzipal eine XML-Schemaauflistung erstellen kann. Dieses Beispiel erstellt eine Beispieldatenbank und den Testbenutzer `TestLogin1`. `TestLogin1` wird anschließend die `ALTER` -Berechtigung für das relationale Schema und die `CREATE XML SCHEMA COLLECTION` -Berechtigung für die Datenbank erteilt. Mit diesen Berechtigungen kann `TestLogin1` erfolgreich eine XML-Beispielschemaauflistung erstellen.  
  
```  
SETUSER  
GO  
USE master  
GO  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
CREATE USER TestLogin1  
GO  
-- User must have ALTER permission on the relational schema in the database.  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
GO  
-- User also must have permission to create XML schema collections in the database.  
GRANT CREATE XML SCHEMA COLLECTION   
TO TestLogin1  
GO  
-- Execute CREATE XML SCHEMA COLLECTION.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="AdditionalContactInfo" >  
  <xsd:complexType mixed="true" >  
    <xsd:sequence>  
      <xsd:any processContents="strict"    
               namespace="http://schemas.adventure-works.com/Contact/Record   
                          http://schemas.adventure-works.com/AdditionalContactTypes"  
               minOccurs="0" maxOccurs="unbounded" />  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="root" type="xsd:byte"/>  
</xsd:schema>'  
GO  
-- Final cleanup  
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
GO  
```  
  
### <a name="b-granting-permission-to-use-an-existing-xml-schema-collection"></a>B. Erteilen der Berechtigungen zum Verwenden einer vorhandenen XML-Schemaauflistung  
 Das folgende Beispiel veranschaulicht das Berechtigungsmodell für die XML-Schemaauflistung. Es veranschaulicht die verschiedenen Berechtigungen, die zum Erstellen und Verwenden der XML-Schemaauflistung erforderlich sind.  
  
 Das Beispiel erstellt eine Testdatenbank und den Anmeldenamen `TestLogin1`. `TestLogin1` erstellt eine XML-Schemaauflistung in der Datenbank. Der Anmeldename erstellt anschließend eine Tabelle und verwendet die XML-Schemaauflistung zum Erstellen einer typisierten xml-Spalte. Der Benutzer fügt anschließend Daten ein und fragt diese ab. Für diese verschiedenen Schritte sind die jeweiligen Schemaberechtigungen wie im Code gezeigt erforderlich.  
  
```  
SETUSER  
GO  
USE master  
GO  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
CREATE USER TestLogin1  
GO  
-- Grant permission to the user.  
SETUSER  
GO  
-- User must have ALTER permission on the relational schema in the database.  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
GO  
-- User also must have permission to create XML schema collections in the database.  
GRANT CREATE XML SCHEMA COLLECTION   
TO TestLogin1  
GO  
-- Now user can execute the previous CREATE XML SCHEMA COLLECTION statement.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
  
<xsd:element name="AdditionalContactInfo" >  
  <xsd:complexType mixed="true" >  
    <xsd:sequence>  
      <xsd:any processContents="strict"    
               namespace="http://schemas.adventure-works.com/Contact/Record   
                          http://schemas.adventure-works.com/AdditionalContactTypes"  
               minOccurs="0" maxOccurs="unbounded" />  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
  
-- Create a table by using the collection to type an XML column.   
--TestLogin1 must have permission to create a table.  
SETUSER  
GO  
GRANT CREATE TABLE TO TestLogin1  
GO  
-- The user also must have REFERENCES permission to use the XML schema collection  
-- to create a typed XML column (REFERENCES permission on schema   
-- collection is not needed).  
GRANT REFERENCES ON XML SCHEMA COLLECTION::myTestSchemaCollection   
TO TestLogin1  
GO  
-- Now user can create a table and use the XML schema collection to create   
-- a typed XML column.  
SETUSER 'TestLogin1'  
GO  
CREATE TABLE MyTestTable (xmlCol xml (dbo.myTestSchemaCollection))  
GO  
-- To insert data in the table, the user needs EXECUTE permission on the XML schema collection.  
-- GRANT EXECUTE permission to TestLogin2 on the xml schema collection.  
SETUSER  
GO  
GRANT EXECUTE ON XML SCHEMA COLLECTION::myTestSchemaCollection   
TO TestLogin1  
GO  
-- TestLogin1 does not own the dbo schema. This user must have INSERT permission.  
GRANT INSERT TO TestLogin1  
GO  
-- Now the user can insert data into the table.  
SETUSER 'TestLogin1'  
GO  
INSERT INTO MyTestTable VALUES('  
<telephone xmlns="http://schemas.adventure-works.com/Additional/ContactInfo">111-1111</telephone>  
')  
GO  
-- To query the table, TestLogin1 must have permissions: SELECT on the table and EXECUTE on the XML schema collection.  
SETUSER  
GO  
GRANT SELECT TO TestLogin1  
GO  
-- TestLogin1 already has EXECUTE permission on the schema (granted before inserting a record in the table).  
SELECT xmlCol.query('declare default element namespace "http://schemas.adventure-works.com/Additional/ContactInfo" /telephone[1]')  
FROM MyTestTable  
GO  
-- To show that the user must have EXECUTE permission to query, revoke the  
-- previously granted permission and return the query.  
SETUSER  
GO  
REVOKE EXECUTE ON XML SCHEMA COLLECTION::myTestSchemaCollection to TestLogin1  
Go  
-- Now TestLogin1 cannot execute the query.  
SETUSER 'TestLogin1'  
GO  
SELECT xmlCol.query('declare default element namespace "http://schemas.adventure-works.com/Additional/ContactInfo" /telephone[1]')  
FROM MyTestTable  
GO  
-- Final cleanup   
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
GO  
```  
  
### <a name="c-granting-alter-permission-on-an-xml-schema-collection"></a>C. Erteilen der ALTER-Berechtigung für eine XML-Schemaauflistung  
 Ein Benutzer benötigt die ALTER-Berechtigung, um eine vorhandene XML-Schemaauflistung in der Datenbank ändern zu können. Im folgenden Beispiel wird veranschaulicht, wie die `ALTER` -Berechtigung erteilt wird.  
  
```  
SETUSER  
GO  
USE master  
GO  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
CREATE USER TestLogin1  
GO  
-- Grant permission to the user.  
SETUSER  
GO  
-- User must have ALTER permission on the relational schema in the database.  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
GO  
-- User also must have permission to create XML schema collections in the database.  
GRANT CREATE XML SCHEMA COLLECTION   
TO TestLogin1  
GO  
-- Now user can execute the previous CREATE XML SCHEMA COLLECTION statement.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
  
<xsd:element name="AdditionalContactInfo" >  
  <xsd:complexType mixed="true" >  
    <xsd:sequence>  
      <xsd:any processContents="strict"    
               namespace="http://schemas.adventure-works.com/Contact/Record   
                          http://schemas.adventure-works.com/AdditionalContactTypes"  
               minOccurs="0" maxOccurs="unbounded" />  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
-- Grant ALTER permission to TestLogin1.  
setuser  
GO  
GRANT ALTER ON XML SCHEMA COLLECTION::myTestSchemaCollection TO TestLogin1  
GO  
-- TestLogin1 should be able to add components to the collection.  
SETUSER 'TestLogin1'  
GO  
ALTER XML SCHEMA COLLECTION myTestSchemaCollection ADD '  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns="http://schemas.adventure-works.com/Additional/ContactInfo"   
elementFormDefault="qualified">  
 <xsd:element name="pager" type="xsd:string"/>  
</xsd:schema>  
'  
Go  
-- Final cleanup   
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
GO  
```  
  
### <a name="d-granting-take-ownership-permission-on-an-xml-schema-collection"></a>D. Erteilen der TAKE OWNERSHIP-Berechtigung für eine XML-Schemaauflistung  
 Im folgenden Beispiel wird veranschaulicht, wie der Besitz des XML-Schemas von einem Benutzer an einen anderen übertragen werden kann. Damit das Beispiel interessanter wird, arbeiten die Benutzer in diesem Beispiel in verschiedenen relationalen Standardschemas.  
  
 In diesem Beispiel werden die folgenden Aufgaben ausgeführt:  
  
-   Erstellen einer Datenbank mit zwei relationalen Schemas, `dbo` und `myOtherDBSchema`.  
  
-   Erstellen von zwei Benutzern, `TestLogin1` und `TestLogin2`. `TestLogin2` wird Besitzer des relationalen `myOtherDBSchema` -Schemas.  
  
-   `TestLogin1` erstellt eine XML-Schemaauflistung im relationalen `dbo` -Schema.  
  
-   `TestLogin1` erteilt anschließend `TAKE OWNERSHIP` die `TestLogin2`-Berechtigung für die XML-Schemaauflistung.  
  
-   `TestLogin2` wird zum Besitzer der XML-Schemaauflistung im `myOtherDBSchema`, ohne dass das relationale Schema der XML-Schemaauflistung geändert wird.  
  
```  
CREATE LOGIN TestLogin1 with password='SQLSvrPwd1'  
GO  
CREATE LOGIN TestLogin2 with password='SQLSvrPwd2'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
-- Create another relational schema in the database.  
CREATE SCHEMA myOtherDBSchema  
GO  
-- Create users in the database. Note TestLogin2's default schema is  
-- myOtherDBSchema.  
CREATE USER TestLogin1  
GO  
CREATE USER TestLogin2 WITH DEFAULT_SCHEMA=myOtherDBSchema  
GO  
-- TestLogin2 will own myOtherDBSchema relational schema.  
ALTER AUTHORIZATION ON SCHEMA::myOtherDBSchema TO TestLogin2  
GO  
  
-- For TestLogin1 to create XML schema collection, the following  
-- permission is required.  
GRANT CREATE XML SCHEMA COLLECTION   
TO TestLogin1  
GO  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
GO  
-- Now TestLogin1 can create an XML schema collection.  
setuser 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
  
<xsd:element name="AdditionalContactInfo" >  
 <xsd:complexType mixed="true" >  
    <xsd:sequence>  
      <xsd:any processContents="strict"   
               namespace="http://schemas.adventure-works.com/Contact/Record   
                          http://schemas.adventure-works.com/AdditionalContactTypes"  
               minOccurs="0" maxOccurs="unbounded" />  
    </xsd:sequence>  
 </xsd:complexType>  
</xsd:element>  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
  
-- Grant TAKE OWNERSHIP to TestLogin2.  
SETUSER  
GO  
GRANT TAKE OWNERSHIP ON XML SCHEMA COLLECTION::dbo.myTestSchemaCollection   
TO TestLogin2  
GO  
-- Verify the owner. Note the UserName and Principal_id is null.   
SELECT user_name(sys.xml_schema_collections.principal_id) as UserName,   
       sys.schemas.name as RelSchemaName,*   
FROM   sys.xml_schema_collections   
      JOIN sys.schemas   
      ON sys.schemas.schema_id=sys.xml_schema_collections.schema_id  
GO  
-- TestLogin2 can take ownership now.  
setuser 'TestLogin2'  
GO  
ALTER AUTHORIZATION ON XML SCHEMA COLLECTION::dbo.myTestSchemaCollection   
TO TestLogin2  
GO  
-- Note that although TestLogin2 is the owner,the XML schema collection   
-- is still in dbo.  
SELECT user_name(sys.xml_schema_collections.principal_id) as UserName,   
      sys.schemas.name as RelSchemaName,*   
FROM sys.xml_schema_collections JOIN sys.schemas   
     ON sys.schemas.schema_id=sys.xml_schema_collections.schema_id  
GO  
  
-- TestLogin2 moves the collection from dbo to myOtherDBSchema relational schema.  
-- TestLogin2 already has all necessary permissions.  
-- 1) TestLogin2 owns the destination relational schema so he can alter it.  
-- 2) TestLogin2 owns the XML schema collection (therefore, has CONTROL permission).  
ALTER SCHEMA myOtherDBSchema  
TRANSFER XML SCHEMA COLLECTION::dbo.myTestSchemaCollection  
GO  
  
SELECT user_name(sys.xml_schema_collections.principal_id) as UserName,   
       sys.schemas.name as RelSchemaName,*   
FROM   sys.xml_schema_collections JOIN sys.schemas   
       ON sys.schemas.schema_id=sys.xml_schema_collections.schema_id  
GO  
-- Final cleanup   
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
DROP LOGIN TestLogin2  
go   
```  
  
### <a name="e-granting-view-definition-permission-on-an-xml-schema-collection"></a>E. Erteilen der VIEW DEFINITION-Berechtigung für eine XML-Schemaauflistung  
 Im folgenden Beispiel wird gezeigt, wie VIEW DEFINITION-Berechtigungen für eine XML-Schemaauflistung erteilt werden.  
  
```  
SETUSER  
GO  
USE master  
GO  
IF EXISTS( SELECT * FROM sysdatabases WHERE name='permissionsDB' )  
   DROP DATABASE permissionsDB  
GO  
IF EXISTS( SELECT * FROM sys.sql_logins WHERE name='schemaUser' )  
   DROP LOGIN schemaUser  
GO  
CREATE DATABASE permissionsDB  
GO  
CREATE LOGIN schemaUser WITH PASSWORD='Pass#123',DEFAULT_DATABASE=permissionsDB  
GO  
GRANT CONNECT SQL TO schemaUser  
GO  
USE permissionsDB  
GO  
CREATE USER schemaUser WITH DEFAULT_SCHEMA=dbo  
GO  
CREATE XML SCHEMA COLLECTION MySC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns"  
xmlns:ns="http://ns">  
  
   <simpleType name="ListOfIntegers">  
      <list itemType="integer"/>  
   </simpleType>  
  
   <element name="root" type="ns:ListOfIntegers"/>  
  
   <element name="gRoot" type="gMonth"/>  
  
</schema>  
'  
GO  
-- schemaUser cannot see the contents of the collection.  
SETUSER 'schemaUser'  
GO  
SELECT XML_SCHEMA_NAMESPACE(N'dbo',N'MySC')  
GO  
  
-- Grant schemaUser VIEW DEFINITION and REFERENCES permissions  
-- on the XML schema collection.  
SETUSER  
GO  
GRANT VIEW DEFINITION ON XML SCHEMA COLLECTION::dbo.MySC TO schemaUser  
GO  
GRANT REFERENCES ON XML SCHEMA COLLECTION::dbo.MySC TO schemaUser  
GO  
-- Now schemaUser can see the content of the collection.  
SETUSER 'schemaUser'  
GO  
SELECT XML_SCHEMA_NAMESPACE(N'dbo',N'MySC')  
GO  
-- Revoke schemaUser VIEW DEFINITION permissions  
-- on the XML schema collection.  
SETUSER  
GO  
REVOKE VIEW DEFINITION ON XML SCHEMA COLLECTION::dbo.MySC FROM schemaUser  
GO  
-- Now schemaUser cannot see the contents of   
-- the collection.  
setuser 'schemaUser'  
GO  
SELECT XML_SCHEMA_NAMESPACE(N'dbo',N'MySC')  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [XML-Daten &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)   
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML-Schemaauflistungen &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [Anforderungen und Einschränkungen für XML-Schemaauflistungen auf dem Server](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
