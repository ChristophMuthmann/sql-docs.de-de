---
title: '@@SPID (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@SPID'
- '@@SPID_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@SPID function'
- session_id
- server process IDs [SQL Server]
- IDs [SQL Server], user processes
- SPID
- session IDs [SQL Server]
- process ID of current user process
ms.assetid: df955d32-8194-438e-abee-387eebebcbb7
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 69413cf65e25d2ee962e4e3a7325a019e321c164
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="spid-transact-sql"></a>@@SPID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt die Sitzungs-ID des aktuellen Benutzerprozesses zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
@@SPID  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **smallint**  
  
## <a name="remarks"></a>Hinweise  
 @@SPID dienen zum Identifizieren des aktuellen Benutzerprozesses in der Ausgabe von **Sp_who**.  
  
## <a name="examples"></a>Beispiele  
 Dieses Beispiel gibt die Sitzungs-ID, den Anmeldenamen und den Benutzernamen für den aktuellen Benutzerprozess zurück.  
  
```  
SELECT @@SPID AS 'ID', SYSTEM_USER AS 'Login Name', USER AS 'User Name';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
ID     Login Name                     User Name                       
------ ------------------------------ ------------------------------  
54     SEATTLE\joanna                 dbo                             
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 In diesem Beispiel gibt die [!INCLUDE[ssDW](../../includes/ssdw-md.md)] Sitzungs-ID, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sitzungs-ID von Knoten, Anmeldename und Benutzernamen für den aktuellen Benutzerprozess zu steuern.  
  
```  
SELECT SESSION_ID() AS ID, @@SPID AS 'Control ID', SYSTEM_USER AS 'Login Name', USER AS 'User Name';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurationsfunktionen](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [' sp_lock ' &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
  
  


