---
title: Synonyme (Transact-SQL) "Datentyp" | Microsoft Docs
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
# <a name="data-type-synonyms-transact-sql"></a>Synonyme für Datentypen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Synonyme für Datentypen werden für die ISO-Kompatibilität in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt. In der folgenden Tabelle sind die Synonyme und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentypen aufgeführt, denen sie zugeordnet werden.
  
|Synonym|SQL Server-Systemdatentyp|  
|---|---|
|**Binary varying**|**varbinary**|  
|**Char varying**|**varchar**|  
|**Zeichen**|**char**|  
|**Zeichen**|**char(1)**|  
|**Zeichen (**  *n*  **)**|**char(n)**|  
|**unterschiedliche Zeichen (**  *n*  **)**|**varchar(n)**|  
|**DEC**|**decimal**|  
|**Mit doppelter Genauigkeit**|**float**|  
|**"float"**[**(***n***)**] für  *n*  = 1 bis 7|**real**|  
|**"float"**[**(***n***)**] für  *n*  = 8-15|**float**|  
|**integer**|**int**|  
|**nationale Zeichensätze (**  *n*  **)**|**NCHAR (n)**|  
|**National Char (**  *n*  **)**|**NCHAR (n)**|  
|**nationale Zeichensätze varying (**  *n*  **)**|**nvarchar (n)**|  
|**National Char varying (**  *n*  **)**|**nvarchar (n)**|  
|**National text**|**ntext**|  
|**timestamp**|rowversion|  
  
Synonyme für Datentypen kann anstelle der entsprechenden basisdatentypnamen in die Anweisungen der Data Definition Language (DDL), z. B. CREATE TABLE, CREATE PROCEDURE verwendet werden, oder deklarieren Sie  *@variable* . Die Synonyme sind allerdings nicht sichtbar, nachdem die Objekte erstellt wurden. Wenn ein Objekt erstellt wird, wird ihm der Basisdatentyp zugewiesen, der dem Synonym zugeordnet ist. Es gibt keinen Protokolleintrag, dem entnommen werden kann, dass das Synonym in der Anweisung angegeben wurde, mit der das Objekt erstellt wurde.
  
Allen Objekten, die von einem Originalobjekt abgeleitet wurden, wie z. B. Spalten eines Resultsets oder Ausdrücke, ist der Basisdatentyp zugewiesen. Alle Metadatenfunktionen, die später für das Originalobjekt oder für eines der abgeleiteten Objekte ausgeführt werden, melden den Basisdatentyp, nicht das Synonym. Dieses Verhalten tritt bei Metadatenoperationen, wie z. B. **Sp_help** und anderen gespeicherten Prozeduren, die Informationsschemasichten oder die verschiedenen API-Metadaten Datenzugriffsvorgänge, die die Datentypen der Tabelle oder des Resultsets zu melden Spalten.
  
Sie können z. B. eine Tabelle durch Angabe von `national character varying` erstellen:
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, VarCharCol national character varying(10))  
```  
  
`VarCharCol`zugewiesen ist tatsächlich eine **nvarchar(10)** -Datentyp, und alle später ausgeführten Metadatenfunktionen melden die Spalte als ein **nvarchar(10)** Spalte. Die Metadatenfunktionen melden sie nie als eine **nationaler Zeichensätze varying(10)** Spalte.
  
## <a name="see-also"></a>Siehe auch
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
