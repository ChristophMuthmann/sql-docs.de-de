---
title: Einschließen von NULL-Werten in die JSON-Ausgabe mit der Option INCLUDE_NULL_VALUES | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- INCLUDE_NULL_VALUES (FOR JSON)
ms.assetid: 06873768-3778-4ed8-a1db-61758726bda0
caps.latest.revision: 14
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cc18e05090f124df2c97aa4f721bab1591690ad5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="include-null-values-in-json---includenullvalues-option"></a>Einschließen von NULL-Werten in die JSON-Ausgabe mit der Option INCLUDE_NULL_VALUES
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Geben Sie die Option **INCLUDE_NULL_VALUES** an, um NULL-Werte in die JSON-Ausgabe einer **FOR JSON** -Klausel einzuschließen.  
  
 Wenn Sie die Option **INCLUDE_NULL_VALUES** nicht angeben, enthält die JSON-Ausgabe in den Abfrageergebnissen keine Eigenschaften für NULL-Werte.  
  
## <a name="examples"></a>Beispiele  
 Die folgende Tabelle zeigt die Ausgabe der **FOR JSON** -Klausel mit und ohne die Option **INCLUDE_NULL_VALUES** an.  
  
|Ohne die Option **INCLUDE_NULL_VALUES**|Mit der Option **INCLUDE_NULL_VALUES**|  
|--------------------------------------------------|-----------------------------------------------|  
|`{    "name": "John",    "surname": "Doe" }`|`{    "name": "John",    "surname": "Doe",    "age": null,    "phone": null }`|  
  
 Hier ist ein weiteres Beispiel für eine **FOR JSON** -Klausel mit der Option **INCLUDE_NULL_VALUES** .  
  
 **Dataseteigenschaften**  
  
```sql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO, INCLUDE_NULL_VALUES    
```  
  
 **Ergebnis**  
  
```json  
[{
    "name": "John",
    "surname": null
}, {
    "name": "Jane",
    "surname": "Doe"
}] 
```  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Weitere Informationen zu JSON in SQL Server und Azure SQL-Datenbank  
  
### <a name="microsoft-blog-posts"></a>Microsoft-Blogbeiträge  
  
Spezielle Lösungen, Anwendungsfälle und Empfehlungen finden Sie in den [Blogbeiträgen über die integrierte JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) in SQL-Server und in Azure SQL-Datenbank.  

### <a name="microsoft-videos"></a>Microsoft-Videos

Eine visuelle Einführung in die JSON-Unterstützung, die in SQL Server und Azure SQL-Datenbank integriert ist, finden Sie in den folgenden Videos:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)

## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [FOR-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  
