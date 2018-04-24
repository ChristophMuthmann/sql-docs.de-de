---
title: SET TEXTSIZE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- TEXTSIZE_TSQL
- TEXTSIZE
- SET_TEXTSIZE_TSQL
- SET TEXTSIZE
dev_langs:
- TSQL
helpviewer_keywords:
- SET TEXTSIZE statement
- SELECT statement [SQL Server], text size returned
- size [SQL Server], text and image data
- TEXTSIZE option
- text size returned [SQL Server]
ms.assetid: 787154a6-39a6-4dd6-a6d0-67b4364f95d5
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 84bfce7530886844d548c9ec3038328482939905
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="set-textsize-transact-sql"></a>SET TEXTSIZE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt die Größe der **varchar(max)**-, **nvarchar(max)**-, **varbinary(max)**-, **text**-, **ntext**- und **image**-Daten an, die von einer SELECT-Anweisung zurückgegeben werden.  
  
> [!IMPORTANT]  
>  Die Datentypen **ntext**, **text** und **image** werden in einer zukünftigen Version von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt. Vermeiden Sie die Verwendung dieser Datentypen bei neuen Entwicklungen, und planen Sie die Änderung von Anwendungen, in denen sie aktuell verwendet werden. Verwenden Sie stattdessen **nvarchar(max)**, **varchar(max)** und **varbinary(max)** .  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SET TEXTSIZE { number }   
```  
  
## <a name="arguments"></a>Argumente  
 *number*  
 Entspricht der Länge der **varchar(max)**-, **nvarchar(max)**-, **varbinary(max)**-, **text**-, **ntext**- oder **image**-Daten in Byte. *number* entspricht einer ganzen Zahl mit einem maximalen Wert von 2.147.483.647 (2 GB).  Ein Wert von –1 gibt eine unbegrenzte Größe an. Ein Wert von 0 setzt die Größe auf den Standardwert von 4 KB zurück.  
  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (10.0 und höher) und der ODBC-Treiber für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geben beim Herstellen einer Verbindung automatisch `-1` (unbegrenzt) an.  
  
 **Ältere Treiber als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008:** Der ODBC-Treiber von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client und der OLE DB-Anbieter (Version 9) von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] legen beim Herstellen einer Verbindung für TEXTSIZE automatisch den Wert 2.147.483.647 fest.  
  
## <a name="remarks"></a>Remarks  
 Das Festlegen von SET TEXTSIZE wirkt sich auf die @@TEXTSIZE-Funktion aus.  
  
 Die Einstellung von TEXTSIZE wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [@@TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
