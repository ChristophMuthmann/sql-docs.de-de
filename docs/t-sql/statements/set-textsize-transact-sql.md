---
title: SET TEXTSIZE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/12/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2d9925b382a7d09722846ca7da583fb92fe4609c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-textsize-transact-sql"></a>SET TEXTSIZE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt die Größe des **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **Text**, **Ntext** , und **Image** von einer SELECT-Anweisung zurückgegebenen Daten.  
  
> [!IMPORTANT]  
>  **Ntext**, **Text**, und **Image** Datentypen werden in einer zukünftigen Version von entfernt [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Vermeiden Sie die Verwendung dieser Datentypen bei neuen Entwicklungen, und planen Sie die Änderung von Anwendungen, in denen sie aktuell verwendet werden. Verwenden Sie stattdessen **nvarchar(max)**, **varchar(max)**und **varbinary(max)** .  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
SET TEXTSIZE { number }   
```  
  
## <a name="arguments"></a>Argumente  
 *number*  
 Die Länge des **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **Text**, **Ntext**, oder **Image** Daten in Bytes. *Anzahl* ist eine ganze Zahl mit einem maximalen Wert von 2147483647 (2 GB).  Der Wert-1 gibt eine unbegrenzte Größe an. Der Wert 0 setzt die Größe auf den Standardwert von 4 KB zurück.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (10.0 und höher) und ODBC-Treiber für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatisch `-1` (unbegrenzt) beim Herstellen einer Verbindung.  
  
 **Treiber, die älter sind als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008:** der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter (Version 9) für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] TEXTSIZE automatisch auf 2147483647 festgelegt wird, beim Herstellen einer Verbindung.  
  
## <a name="remarks"></a>Hinweise  
 Festlegen von SET TEXTSIZE wirkt sich auf den @@TEXTSIZE Funktion.  
  
 Die Einstellung von TEXTSIZE wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="see-also"></a>Siehe auch  
 [@@TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

