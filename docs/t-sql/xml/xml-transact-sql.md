---
title: xml (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xml_TSQL
- xml
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], about xml data type
ms.assetid: 9198f671-8e61-4ca4-9c3a-859f84020e62
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6b9d3c8c512611ea9d8d0482acb7fd848c04629b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="xml-transact-sql"></a>xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Der Datentyp, in dem XML-Daten gespeichert sind. **xml**-Instanzen können in einer Spalte oder in einer Variablen vom Typ **xml** gespeichert werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
xml ( [ CONTENT | DOCUMENT ] xml_schema_collection )  
```  
  
## <a name="arguments"></a>Argumente  
 CONTENT  
 Schränkt die **xml**-Instanz auf ein wohlgeformtes XML-Fragment ein. Die XML-Daten können keine oder auch mehrere Elemente auf der obersten Ebene enthalten. Textknoten sind auf der obersten Ebene ebenfalls zulässig.  
  
 Dies ist das Standardverhalten.  
  
 DOCUMENT  
 Schränkt die **xml**-Instanz auf ein wohlgeformtes XML-Dokument ein. Die XML-Daten müssen genau ein Stammelement aufweisen. Textknoten sind auf der obersten Ebene nicht zulässig.  
  
 *xml_schema_collection*  
 Der Name einer XML-Schemaauflistung. Zum Erstellen einer Spalte oder Variablen vom Typ **xml** können Sie optional den Namen der XML-Schemaauflistung angeben. Weitere Informationen zu typisierten und nicht typisierten XML-Dokumenten finden Sie unter [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
## <a name="remarks"></a>Remarks  
 Die gespeicherte Darstellung von Instanzen vom Datentyp **xml** darf die Größe von 2 Gigabyte (GB) nicht überschreiten.  
  
 Die Facets CONTENT und DOCUMENT beziehen sich nur auf typisierte XML-Daten. Weitere Informationen finden Sie unter [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
## <a name="examples"></a>Beispiele  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @y xml (Sales.IndividualSurveySchemaCollection);  
SET @y =  (SELECT TOP 1 Demographics FROM Sales.Individual);  
SELECT @y;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datentypkonvertierung &#40;Datenbank-Engine&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [XML-Datentypmethoden](../../t-sql/xml/xml-data-type-methods.md)   
 [XQuery-Sprachreferenz &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
