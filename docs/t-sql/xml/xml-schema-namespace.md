---
title: xml_schema_namespace (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 19f4701bc26e115c7f6b78d01feef876665763df
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
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
 Der Name des relationalen Schemas. *Relational_schema* ist **Sysname**.  
  
 *XML_schema_collection_name*  
 Der Name der XML-Schemaauflistung, die rekonstruiert werden soll. *XML_schema_collection_name* ist **Sysname**.  
  
 *Namespace*  
 Der Namespace-URI des zu rekonstruierenden XML-Schemas. Die Eingabe ist auf 1.000 Zeichen beschränkt. Wenn kein Namespace-URI bereitgestellt wurde, wird die gesamte XML-Schemaauflistung rekonstruiert. *Namespace* ist **nvarchar(4000)**.  
  
## <a name="return-types"></a>Rückgabetypen  
 **xml**  
  
## <a name="remarks"></a>Hinweise  
 Beim Importieren von XML-Schemakomponenten in der Datenbank mithilfe von [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) oder [ALTER XML SCHEMA COLLECTION](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md), Aspekte des für die Validierung verwendeten Schemas werden beibehalten. Deshalb kann es sein, dass das rekonstruierte Schema lexikalisch nicht mit dem ursprünglichen Schemadokument identisch ist. Insbesondere Kommentare, Leerzeichen und Anmerkungen gehen verloren; und implizite Informationen werden zu expliziten Informationen. Beispielsweise \<xs: Element Name = "e1" / > wird \<xs: Element Name = "e1" Type = "xs: anyType" / >. Außerdem werden Namespacepräfixe nicht beibehalten.  
  
 Wenn Sie einen Namespaceparameter angeben, enthält das resultierende Schemadokument Definitionen für alle Schemakomponenten in diesem Namespace, selbst wenn sie in verschiedenen Schemadokumenten und/oder DDL-Schritten hinzugefügt wurden.  
  
 Sie können nicht diese Funktion verwenden, um die XML-Schemadokumente von der **sys.sys** XML-schemaauflistung.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die XML-Schemaauflistung `ProductDescriptionSchemaCollection` vom relationalen Schema Production in der `AdventureWorks2012`-Datenbank abgerufen.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT xml_schema_namespace(N'production',N'ProductDescriptionSchemaCollection');  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen einer gespeicherten XML-Schemaauflistung](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)   
 [XML-Schemaauflistungen &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
