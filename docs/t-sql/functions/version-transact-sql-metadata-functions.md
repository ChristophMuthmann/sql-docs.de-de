---
title: VERSION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 95a79b33-98f2-4929-a1a5-93b522a9e152
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aa9dec84a07189eb3b2c6c9c3d9342db4eac1df6
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="version---transact-sql-metadata-functions"></a>Version - Transact-SQL-Metadaten-Funktionen
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

 Gibt die Version des [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] oder [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)] auf dem Gerät ausgeführt wird.  
  
![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
VERSION ( )  
```  
  
## <a name="arguments"></a>Argumente  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
Ein Tabellenname muss angegeben werden, einem [FROM](../../t-sql/queries/from-transact-sql.md) -Klausel für diese Funktion, um Ergebnisse zurückzugeben. Eine Ergebniszeile wird für jede Zeile im Resultset der Abfrage zurückgegeben werden. Verwenden Sie [TOP (Transact-SQL)](../../t-sql/queries/top-transact-sql.md) um die Anzahl der zurückgegebenen Zeilen einzuschränken.  
  
## <a name="examples"></a>Beispiele  
Im folgende Beispiel gibt die Versionsnummer.  
  
```  
SELECT VERSION();  
```  
  
## <a name="see-also"></a>Siehe auch 
[SESSION_ID (Transact-SQL)](../../t-sql/functions/session-id-transact-sql.md)  
[Db_name &#40; Transact-SQL &#41;](../../t-sql/functions/db-name-transact-sql.md)  
  
  
