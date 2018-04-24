---
title: xml_schema_namespace (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xml_schema_namespace_TSQL
- xml_schema_namespace
dev_langs:
- TSQL
helpviewer_keywords:
- XML schema collections [SQL Server], reconstructing schemas
- xml_schema_namespace function
- reconstructing schemas
- schemas [SQL Server], XML
- schema collections [SQL Server], reconstructing schemas
ms.assetid: ee9873d8-dd3a-4bff-a10c-68bbadbdf1a6
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9706fc510b6bc731539809ec492dba2a8b933e04
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="xmlschemanamespace"></a>xml_schema_namespace
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rekonstruiert alle Schemas oder ein bestimmtes Schema in der angegebenen XML-Schemaauflistung. Diese Funktion gibt eine Instanz vom Datentyp **xml** zurück.  
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```  
  
xml_schema_namespace( Relational_schema , XML_schema_collection_name , [ Namespace ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Relational_schema*  
 Der Name des relationalen Schemas. *Relational_schema* ist vom Datentyp **sysname**.  
  
 *XML_schema_collection_name*  
 Der Name der XML-Schemaauflistung, die rekonstruiert werden soll. *XML_schema_collection_name* ist vom Datentyp **sysname**.  
  
 *Namespace*  
 Der Namespace-URI des zu rekonstruierenden XML-Schemas. Die Eingabe ist auf 1.000 Zeichen beschränkt. Wenn kein Namespace-URI bereitgestellt wurde, wird die gesamte XML-Schemaauflistung rekonstruiert. *Namespace* ist vom Datentyp **nvarchar(4000)**.  
  
## <a name="return-types"></a>Rückgabetypen  
 **xml**  
  
## <a name="remarks"></a>Remarks  
 Wenn Sie XML-Schemakomponenten in der Datenbank mithilfe von [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) oder [ALTER XML SCHEMA COLLECTION](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md) importieren, bleiben Aspekte des Schemas erhalten, die zur Überprüfung verwendet werden. Deshalb kann es sein, dass das rekonstruierte Schema lexikalisch nicht mit dem ursprünglichen Schemadokument identisch ist. Insbesondere Kommentare, Leerzeichen und Anmerkungen gehen verloren; und implizite Informationen werden zu expliziten Informationen. Beispielsweise wird \<xs:element name="e1" /> zu \<xs:element name="e1" type="xs:anyType"/>. Außerdem werden Namespacepräfixe nicht beibehalten.  
  
 Wenn Sie einen Namespaceparameter angeben, enthält das resultierende Schemadokument Definitionen für alle Schemakomponenten in diesem Namespace, selbst wenn sie in verschiedenen Schemadokumenten und/oder DDL-Schritten hinzugefügt wurden.  
  
 Mit dieser Funktion können keine XML-Schemadokumente von der XML-Schemaauflistung **sys.sys** erstellt werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die XML-Schemaauflistung `ProductDescriptionSchemaCollection` vom relationalen Schema Production in der `AdventureWorks`-Datenbank abgerufen.  
  
```  
USE AdventureWorks;  
GO  
SELECT xml_schema_namespace(N'production',N'ProductDescriptionSchemaCollection');  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Anzeigen einer gespeicherten XML-Schemaauflistung](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)   
 [XML-Schemaauflistungen &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
