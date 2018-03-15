---
title: Datentypsynonyme (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], synonyms
- alternate names [SQL Server]
- synonyms [SQL Server], data types
ms.assetid: 390eef67-1a49-4185-a971-e07765be9717
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 07b4ada74ee54bf1c892e0938dd794e17ea4c0cb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="data-type-synonyms-transact-sql"></a>Datentypsynonyme (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Synonyme für Datentypen werden für die ISO-Kompatibilität in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt. In der folgenden Tabelle sind die Synonyme und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentypen aufgeführt, denen sie zugeordnet werden.
  
|Synonym|SQL Server-Systemdatentyp|  
|---|---|
|**Binary varying**|**varbinary**|  
|**char varying**|**varchar**|  
|**character**|**char**|  
|**character**|**char(1)**|  
|**character(** *n* **)**|**char(n)**|  
|**character varying(** *n* **)**|**varchar(n)**|  
|**Dec**|**decimal**|  
|**Double precision**|**float**|  
|**float**[**(***n***)**] für *n* = 1-7|**real**|  
|**float**[**(***n***)**] für *n* = 8-15|**float**|  
|**integer**|**int**|  
|**national character(** *n* **)**|**nchar(n)**|  
|**national char(** *n* **)**|**nchar(n)**|  
|**national character varying(** *n* **)**|**nvarchar(n)**|  
|**national char varying(** *n* **)**|**nvarchar(n)**|  
|**national text**|**ntext**|  
|**timestamp**|rowversion|  
  
Synonyme für Datentypen können in DDL-Anweisungen (Data Definition Language, Datendefinitionssprache), wie z.B. CREATE TABLE, CREATE PROCEDURE oder DECLARE *@variable*, statt der entsprechenden Basisdatentypnamen verwendet werden. Die Synonyme sind allerdings nicht sichtbar, nachdem die Objekte erstellt wurden. Wenn ein Objekt erstellt wird, wird ihm der Basisdatentyp zugewiesen, der dem Synonym zugeordnet ist. Es gibt keinen Protokolleintrag, dem entnommen werden kann, dass das Synonym in der Anweisung angegeben wurde, mit der das Objekt erstellt wurde.
  
Allen Objekten, die von einem Originalobjekt abgeleitet wurden, wie z. B. Spalten eines Resultsets oder Ausdrücke, ist der Basisdatentyp zugewiesen. Alle Metadatenfunktionen, die später für das Originalobjekt oder für eines der abgeleiteten Objekte ausgeführt werden, melden den Basisdatentyp, nicht das Synonym. Dieses Verhalten tritt bei Metadatenoperationen, wie z.B. **sp_help**, und bei anderen gespeicherten Systemprozeduren, den Informationsschemasichten oder den verschiedenen Datenzugriff-API-Metadatenoperationen auf, die die Datentypen von Tabellen- oder Resultsetspalten zurückgeben.
  
Sie können z. B. eine Tabelle durch Angabe von `national character varying` erstellen:
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, VarCharCol national character varying(10))  
```  
  
`VarCharCol` wird tatsächlich ein **nvarchar(10)**-Datentyp zugewiesen, und alle später ausgeführten Metadatenfunktionen melden die Spalte als **nvarchar(10)**-Spalte. Die Metadatenfunktionen melden sie nie als **national character varying(10)**-Spalte.
  
## <a name="see-also"></a>Siehe auch
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
