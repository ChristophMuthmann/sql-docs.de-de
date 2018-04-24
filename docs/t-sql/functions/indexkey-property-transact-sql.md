---
title: INDEXKEY_PROPERTY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- INDEXKEY_PROPERTY_TSQL
- INDEXKEY_PROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- index keys [SQL Server]
- INDEXKEY_PROPERTY function
- viewing index keys
- displaying index keys
- keys [SQL Server], index
ms.assetid: 87c0c385-6b2d-4716-ac8c-a3ce6e8d89e9
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7cef50b919c2c5700331779d602f2257a0502c20
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="indexkeyproperty-transact-sql"></a>INDEXKEY_PROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen über den Indexschlüssel zurück. Gibt für XML-Indizes NULL zurück.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
INDEXKEY_PROPERTY ( object_ID ,index_ID ,key_ID ,property )  
```  
  
## <a name="arguments"></a>Argumente  
 *object_ID*  
 Die Objekt-ID der Tabelle oder der indizierten Sicht. *object_id* ist vom Datentyp **int**.  
  
 *index_ID*  
 Die ID-Nummer für den Index. *index_ID* ist vom Datentyp **int**.  
  
 *key_ID*  
 Die Position der Indexschlüsselspalte. *key_ID* ist vom Datentyp **int**.  
  
 *property*  
 Der Name der Eigenschaft, für die Informationen zurückgegeben werden. *property* ist eine Zeichenfolge und kann einen der folgenden Werte aufweisen.  
  
|value|Description|  
|-----------|-----------------|  
|**ColumnId**|Die Spalten-ID an der *key_ID*-Position des Index.|  
|**IsDescending**|Die Reihenfolge, in der die Indexspalte gespeichert wird.<br /><br /> 1 = Absteigend 0 = Aufsteigend|  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="exceptions"></a>Ausnahmen  
 Gibt NULL bei einem Fehler zurück oder wenn ein Aufrufer nicht über Berechtigungen zum Anzeigen des Objekts verfügt.  
  
 Ein Benutzer kann nur die Metadaten sicherungsfähiger Elemente anzeigen, bei denen der Benutzer entweder der Besitzer ist oder für die dem Benutzer eine Berechtigung erteilt wurde. Dies bedeutet, dass Metadaten ausgebende integrierte Funktionen, z. B. INDEXKEY_PROPERTY, möglicherweise NULL zurückgeben, wenn dem Benutzer für das Objekt keine Berechtigung erteilt wurde. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden beide Eigenschaften für Index-ID `1`, Schlüsselspalte `1`, in der `Production.Location`-Tabelle zurückgegeben.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT   
    INDEXKEY_PROPERTY(OBJECT_ID('Production.Location', 'U'),  
        1,1,'ColumnId') AS [Column ID],  
    INDEXKEY_PROPERTY(OBJECT_ID('Production.Location', 'U'),  
        1,1,'IsDescending') AS [Asc or Desc order];  
```  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
```  
Column ID   Asc or Desc order   
----------- -----------------   
1           0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [INDEX_COL &#40;Transact-SQL&#41;](../../t-sql/functions/index-col-transact-sql.md)   
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
