---
title: "Aufheben der Berechtigungen für eine XML-Schemaauflistung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: revoking permissions [SQL Server]
ms.assetid: 4e542b70-2d56-4a65-8a39-96a1ed477ca6
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3daaadf50d221b5f5b4fc2f580990a3e849a0c60
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="revoke-permissions-on-an-xml-schema-collection"></a>Aufheben der Berechtigungen für eine XML-Schemaauflistung
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] Die Berechtigung zum Erstellen einer XML-Schemaauflistung kann mithilfe eines der folgenden Verfahren aufgehoben werden:  
  
-   Aufheben der ALTER-Berechtigung für das relationale Schema. Der Prinzipal kann in diesem Fall keine XML-Schemaauflistung im relationalen Schema erstellen. Der Prinzipal kann dies jedoch auch weiterhin in anderen relationalen Schemas in der gleichen Datenbank.  
  
-   Aufheben der ALTER ANY SCHEMA-Berechtigung für die Datenbank für den Prinzipal. Der Prinzipal kann in diesem Fall keine XML-Schemaauflistung in der gesamten Datenbank erstellen.  
  
-   Aufheben der CREATE XML SCHEMA COLLECTION- oder ALTER XML SCHEMA COLLECTION-Berechtigung für die Datenbank für den Prinzipal. Dies verhindert, dass der Prinzipal eine XML-Schemaauflistung innerhalb der Datenbank importieren kann. Das Aufheben der ALTER- oder CONTROL-Berechtigung für die Datenbank besitzt die gleichen Auswirkungen.  
  
## <a name="revoking-permissions-on-an-existing-xml-schema-collection-object"></a>Aufheben der Berechtigungen für ein vorhandenes XML-Schemaauflistungsobjekt  
 Im Folgenden finden Sie die Berechtigungen, die für eine XML-Schemaauflistung aufgehoben werden können, sowie die Ergebnisse:  
  
-   Durch das Aufheben der ALTER-Berechtigung wird die Fähigkeit eines Prinzipals zum Ändern des Inhalts der XML-Schemaauflistung aufgehoben.  
  
-   Durch das Aufheben der TAKE OWNERSHIP-Berechtigung wird die Fähigkeit eines Prinzipals zum Übertragen des Besitzes der XML-Schemaauflistung aufgehoben.  
  
-   Durch das Aufheben der REFERENCES-Berechtigung wird die Fähigkeit eines Prinzipals zum Verwenden der XML-Schemaauflistung zum Typisieren oder Einschränken von Spalten des xml-Typs in Tabellen und Sichten sowie Parametern aufgehoben. Außerdem wird die Berechtigung zum Verweisen auf diese Schemaauflistung aus anderen XML-Schemaauflistungen aufgehoben.  
  
-   Durch das Aufheben der VIEW DEFINITION-Berechtigung wird die Fähigkeit eines Prinzipals zum Anzeigen des Inhalts einer XML-Schemaauflistung aufgehoben.  
  
-   Durch das Aufheben der EXECUTE-Berechtigung wird die Fähigkeit eines Prinzipals zum Einfügen oder Aktualisieren von Werten in Spalten, Variablen und Parametern aufgehoben, die durch die XML-Auflistung typisiert oder eingeschränkt werden. Außerdem wird die Fähigkeit zum Abfragen solcher Spalten, Variablen oder Parameter vom Typ **xml** aufgehoben.  
  
## <a name="examples"></a>Beispiele  
 Die Szenarien in den folgenden Beispielen veranschaulichen, wie XML-Schemaberechtigungen funktionieren. Jedes dieser Beispiele erstellt die erforderliche Testdatenbank, die relationalen Schemas und Anmeldungen. Diesen Anmeldenamen werden die erforderlichen Berechtigungen für XML-Schemaauflistungen erteilt. Jedes der Beispiele führt am Ende den erforderlichen Cleanup aus.  
  
### <a name="a-revoking-permissions-to-create-an-xml-schema-collection"></a>A. Aufheben der Berechtigungen zum Erstellen einer XML-Schemaauflistung  
 Dieses Beispiel erstellt eine Anmeldung und eine Beispieldatenbank. Darüber hinaus wird in der Datenbank ein relationales Schema hinzugefügt. Anfangs werden dem Anmeldenamen die ALTER-Berechtigung für relationale Schemas und andere erforderliche Berechtigungen zum Erstellen von XML-Schemaauflistungen erteilt. Das Beispiel hebt dann die ALTER-Berechtigung für eines der relationalen Schemas in der Datenbank auf. Dies verhindert, dass der Anmeldename eine XML-Schemaauflistung erstellen kann.  
  
```  
setuser  
go  
create login TestLogin1 with password='SQLSvrPwd1'  
go  
create database SampleDBForSchemaPermissions  
go  
use SampleDBForSchemaPermissions  
go  
-- Create another relational schema in the db (in addition to dbo schema)  
CREATE SCHEMA myOtherDBSchema  
go  
CREATE USER TestLogin1  
go  
-- For TestLogin1 to create/import XML schema collection, following  
-- permission needed  
-- CREATE XML SCHEMA is a database level permission  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
go  
GRANT ALTER ON SCHEMA::myOtherDBSchema TO TestLogin1  
go  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
go  
-- Now TestLogin1 can import an XML schema collection in both relational schemas.  
setuser 'TestLogin1'  
go  
CREATE XML SCHEMA COLLECTION dbo.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
-- TestLogin1 can create XML schema collection in myOtherDBSchema relational schema  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
-- Let us drop XML schema collections from both relational schemas  
DROP XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection  
go  
DROP XML SCHEMA COLLECTION dbo.myTestSchemaCollection  
go  
-- now REVOKE permission from TestLogin1 to alter myOtherDBSchema  
setuser  
go  
REVOKE ALTER ON SCHEMA::myOtherDBSchema FROM TestLogin1  
go  
-- now TestLogin1 cannot create xml schema collection in myOtherDBSchema  
setuser 'TestLogin1'  
go  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
  
-- TestLogin1 can still create XML schema collections in dbo  
-- It cannot create XML schema collections anywhere in the database  
-- if we REVOKE CREATE XML SCHEMA COLLECTION permission  
SETUSER  
go  
REVOKE CREATE XML SCHEMA COLLECTION FROM TestLogin1  
go  
  
setuser 'TestLogin1'  
go  
-- the following now should fail  
CREATE XML SCHEMA COLLECTION dbo.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
  
-- Final cleanup  
SETUSER  
go  
USE master  
go  
DROP DATABASE SampleDBForSchemaPermissions  
go  
DROP LOGIN TestLogin1  
Go  
```  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Daten &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)   
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML-Schemaauflistungen &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [Anforderungen und Einschränkungen für XML-Schemaauflistungen auf dem Server](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
