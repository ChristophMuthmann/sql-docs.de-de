---
title: "Ändern von XML-Indizes | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML indexes [SQL Server], modifying
- modifying indexes
ms.assetid: 24d50fe1-c6ec-49e6-91a3-9791851ba53d
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2351a96c293395370afc4e20a6e65f93b900d121
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="modify-xml-indexes"></a>Ändern von XML-Indizes
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] Die [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)]-DDL-Anweisung kann zum Ändern vorhandener XML-Indizes und Nicht-XML-Indizes verwendet werden. Nicht alle ALTER INDEX-Optionen sind jedoch für XML-Indizes verfügbar. Die folgenden Optionen sind beim Ändern von XML-Indizes nicht zulässig:  
  
-   Die REBUILD- und SET-Option IGNORE_DUP_KEY ist für XML-Indizes nicht zulässig. Die REBUILD-Option ONLINE muss für sekundäre XML-Indizes auf OFF festgelegt werden. Die Option DROP_EXISTING ist in der ALTER INDEX-Anweisung nicht zulässig.  
  
-   Die Änderungen der primary key-Einschränkung in der user-Tabelle werden nicht automatisch an XML-Indizes weitergegeben. Der Benutzer muss die XML-Indizes zuerst löschen und dann neu erstellen.  
  
-   Wenn ALTER INDEX ALL angegeben wird, gilt dies für Nicht-XML- und XML-Indizes. Möglicherweise werden Indizierungsoptionen angegeben, die nicht für beide Indextypen zulässig sind. In diesem Fall schlägt die gesamte Anweisung fehl.  
  
## <a name="example-modifying-an-xml-index"></a>Beispiel: Ändern eines XML-Index  
 Im folgenden Beispiel wird ein XML-Index erstellt und dann durch Festlegen der Option `ALLOW_ROW_LOCKS` auf `OFF`geändert. Wenn `ALLOW_ROW_LOCKS` auf `OFF`festgelegt wurde, sind die Zeilen gesperrt, und der Zugriff auf die angegebenen Indizes erfolgt über die Sperren auf Seiten- und Tabellenebene.  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
-- Create primary XML index.   
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol)  
GO  
-- Note the type 3 is index on XML type.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'  
  
-- Modify and set an index option.  
ALTER INDEX PIdx_T_XmlCol on T   
SET (ALLOW_ROW_LOCKS = OFF)  
```  
  
## <a name="example-disabling-and-enabling-an-xml-index"></a>Beispiel: Deaktivieren und Aktivieren eines XML-Index  
 Standardmäßig ist ein XML-Index aktiviert. Wenn ein XML-Index deaktiviert ist, verwenden die Abfragen, die für eine XML-Spalte ausgeführt werden, den XML-Index nicht. Verwenden Sie `ALTER INDEX` mit der Option `REBUILD` , um einen XML-Index zu aktivieren.  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol ON T(XmlCol)  
GO  
ALTER INDEX PIdx_T_XmlCol on T DISABLE  
Go  
-- Verify index is disabled.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'  
-- Rebuild the index.  
ALTER INDEX PIdx_T_XmlCol on T REBUILD  
Go  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [XML-Indizes &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  
