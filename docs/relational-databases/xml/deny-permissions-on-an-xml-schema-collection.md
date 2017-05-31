---
title: "Verweigern von Berechtigungen für eine XML-Schemaauflistung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- denying permissions [SQL Server], XML server collections
ms.assetid: e2b300b0-e734-4c43-a4da-c78e6e5d4fba
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 803150cde12790eefbeea8c8f4ef0ad32dc350fe
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="deny-permissions-on-an-xml-schema-collection"></a>Verweigern von Berechtigungen für eine XML-Schemaauflistung
  Die Berechtigung zum Erstellen einer neuen XML-Schemaauflistung bzw. zum Verwenden einer vorhandenen Schemaauflistung kann verweigert werden.  
  
## <a name="denying-permission-to-create-an-xml-schema-collection"></a>Verweigern der Berechtigung zum Erstellen einer XML-Schemaauflistung  
 Es gibt folgende Möglichkeiten, um die Berechtigung zum Erstellen einer XML-Schemaauflistung zu verweigern:  
  
-   Verweigern der ALTER-Berechtigung für das relationale Schema.  
  
-   Verweigern der CONTROL-Berechtigung für das relationale Schema, um alle Berechtigungen für das relationale Schema und alle darin enthaltenen Objekte zu verweigern.  
  
-   Verweigern der ALTER ANY SCHEMA-Berechtigung für die Datenbank. In diesem Fall kann der Prinzipal keine XML-Schemaauflistung in der gesamten Datenbank erstellen. Beachten Sie, dass das Verweigern der ALTER- oder CONTROL-Berechtigung für die Datenbank alle Berechtigungen für alle Objekte in der Datenbank verweigert.  
  
## <a name="denying-permissions-on-an-xml-schema-collection-object"></a>Verweigern von Berechtigungen für ein XML-Schemaauflistungsobjekt  
 Die folgenden Berechtigungen können mit den aufgeführten Ergebnissen für eine vorhandene XML-Schemaauflistung verweigert werden:  
  
-   Durch das Verweigern der ALTER-Berechtigung wird einem Prinzipal die Fähigkeit zum Ändern des Inhalts der XML-Schemaauflistung abgesprochen.  
  
-   Durch das Verweigern der CONTROL-Berechtigung wird einem Prinzipal die Fähigkeit zum Ausführen beliebiger Vorgänge mit der XML-Schemaauflistung abgesprochen.  
  
-   Durch das Verweigern der REFERENCES-Berechtigung wird einem Prinzipal die Fähigkeit zum Typisieren oder Einschränken von Spalten und Parametern vom Typ xml mithilfe der XML-Schemaauflistung abgesprochen. Außerdem wird dem Prinzipal die Möglichkeit zum Verweisen auf diese XML-Schemaauflistung aus anderen XML-Schemaauflistungen verweigert.  
  
-   Durch das Verweigern der VIEW DEFINITION-Berechtigung wird einem Prinzipal die Fähigkeit zum Anzeigen des Inhalts einer XML-Schemaauflistung abgesprochen.  
  
-   Durch das Verweigern der EXECUTE-Berechtigung wird dem Prinzipal die Fähigkeit zum Einfügen oder Aktualisieren von Werten in Spalten, Variablen und Parametern abgesprochen, die durch die XML-Auflistung typisiert oder eingeschränkt werden. Außerdem wird dem Prinzipal die Möglichkeit zum Abfragen der Werte in diesen Spalten und Variablen vom Typ xml abgesprochen.  
  
## <a name="examples"></a>Beispiele  
 Die Szenarien in den folgenden Beispielen veranschaulichen, wie XML-Schemaberechtigungen funktionieren. Jedes dieser Beispiele erstellt die erforderliche Testdatenbank, die relationalen Schemas und Anmeldungen. Diesen Anmeldenamen werden die erforderlichen Berechtigungen für XML-Schemaauflistungen erteilt. Jedes der Beispiele führt am Ende den erforderlichen Cleanup aus.  
  
### <a name="a-preventing-a-user-from-creating-an-xml-schema-collection"></a>A. Verhindern, dass ein Benutzer eine XML-Schemaauflistung erstellen kann  
 Wenn Sie verhindern möchten, dass ein Benutzer eine XML-Schemaauflistung erstellen kann, können Sie z. B. die ALTER-Berechtigung für ein relationales Schema verweigern. Dies wird im folgenden Beispiel gezeigt.  
  
 Dieses Beispiel erstellt einen Benutzer, `TestLogin1`, und eine Datenbank. Außerdem wird neben dem `dbo` -Schema ein relationales Schema in der Datenbank erstellt. Anfangs ermöglicht die `CREATE XML SCHEMA` -Berechtigung dem Benutzer das Erstellen einer Schemaauflistung in der gesamten Datenbank. Das Beispiel verweigert dann die `ALTER` -Berechtigung für den Benutzer für eines der relationalen Schemas. Dies verhindert, dass der Benutzer eine XML-Schemaauflistung in diesem relationalen Schema erstellen kann.  
  
```  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
-- Create another relational schema in the database.  
CREATE SCHEMA myOtherDBSchema  
GO  
CREATE USER TestLogin1  
GO  
-- For TestLogin1 to create/import XML schema collection, following  
-- permission needed.  
-- Database-level permissions  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
GO  
GRANT ALTER ANY SCHEMA TO TestLogin1  
GO  
-- Now TestLogin1 can import an XML schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
DROP XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection  
GO  
-- Now deny permission from TestLogin1 to alter myOtherDBSchema.  
setuser  
GO  
DENY ALTER ON SCHEMA::myOtherDBSchema TO TestLogin1  
GO  
-- Now TestLogin1 cannot create xml schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
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
  
### <a name="b-denying-permissions-on-an-xml-schema-collection"></a>B. Verweigern von Berechtigungen für eine XML-Schemaauflistung  
 Das folgende Beispiel zeigt, wie einem Anmeldenamen eine bestimmte Berechtigung für eine vorhandene XML-Schemaauflistung verweigert werden kann. In diesem Beispiel wird einem Testanmeldenamen die REFERENCES-Berechtigung für eine vorhandene XML-Schemaauflistung verweigert.  
  
 Dieses Beispiel erstellt einen Benutzer, `TestLogin1`, und eine Datenbank. Außerdem wird neben dem `dbo` -Schema ein relationales Schema in der Datenbank erstellt. Anfangs ermöglicht die `CREATE XML SCHEMA` -Berechtigung dem Benutzer das Erstellen einer Schemaauflistung in der gesamten Datenbank.  
  
 Durch die `REFERENCES` -Berechtigung für die XML-Schemaauflistung kann `TestLogin1` das Schema beim Erstellen einer typisierten `xml` -Spalte in einer Tabelle verwenden. Wenn die `REFERENCES` -Berechtigung für die XML-Schemaauflistung verweigert wird, kann `TestLogin1` die XML-Schemaauflistung nicht verwenden.  
  
```  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
-- Create another relational schema in the database.  
CREATE SCHEMA myOtherDBSchema  
GO  
CREATE USER TestLogin1  
GO  
-- For TestLogin1 to create/import XML schema collection, the following  
-- permission is required.  
-- Database-level permissions  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
GO  
GRANT ALTER ANY SCHEMA TO TestLogin1  
GO  
-- Now TestLogin1 can import an XML schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
-- Grant permission to TestLogin1 to create a table and reference the XML schema collection.  
SETUSER  
GO  
GRANT CREATE TABLE TO TestLogin1  
GO  
-- The user also needs REFERENCES permission to use the XML schema collection  
-- to create a typed XML column (REFERENCES permission on the schema   
-- collection is not needed).  
GRANT REFERENCES ON XML SCHEMA COLLECTION::myOtherDBSchema.myTestSchemaCollection   
TO TestLogin1  
GO  
  
--TestLogin1 can use the schema.  
CREATE TABLE T(i int, x xml (myOtherDBSchema.myTestSchemaCollection))  
GO  
-- Drop the table.  
DROP TABLE T  
GO  
-- Now deny REFERENCES permission to TestLogin1 on the schema created previously.  
SETUSER  
GO  
DENY REFERENCES ON XML SCHEMA COLLECTION::myOtherDBSchema.myTestSchemaCollection TO TestLogin1  
  
GO  
-- Now TestLogin1 cannot create xml schema collection  
SETUSER 'TestLogin1'  
GO  
-- Following statement fails. TestLogin1 does not have REFERENCES   
-- permission on the XML schema collection.  
CREATE TABLE T(i int, x xml (myOtherDBSchema.myTestSchemaCollection))  
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
  
## <a name="see-also"></a>Siehe auch  
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML-Schemaauflistungen &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [Anforderungen und Einschränkungen für XML-Schemaauflistungen auf dem Server](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)   
 [DENY (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)   
 [GRANT (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)   
 [XML-Daten &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
