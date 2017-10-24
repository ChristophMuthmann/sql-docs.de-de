---
title: '@@REMSERVER (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@REMSERVER'
- '@@REMSERVER_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], remote servers
- remote servers [SQL Server], logins
- '@@REMSERVER function'
ms.assetid: 0bb451a9-3866-4064-963d-b74a2f864049
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: fd32b0c7ebc6da51fe50787a8492d52928dd7d32
ms.contentlocale: de-de
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40remserver-transact-sql"></a>& #x 40; & #x 40; REMSERVER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Verwenden Sie stattdessen Verbindungsserver und gespeicherte Prozeduren, die über Verbindungsserver ausgeführt werden.  
  
 Gibt den Namen des Remote-Datenbankservers mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück, wie er im Anmeldedatensatz enthalten ist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@REMSERVER  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **vom Datentyp nvarchar(128)**  
  
## <a name="remarks"></a>Hinweise  
 @@REMSERVER ermöglicht eine gespeicherten Prozedur den Namen des Datenbankservers zu überprüfen, von dem die Prozedur ausgeführt wird.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die `usp_CheckServer`-Prozedur erstellt, die den Namen des Remoteservers zurückgibt.  
  
```  
CREATE PROCEDURE usp_CheckServer  
AS  
SELECT @@REMSERVER;  
```  
  
 Die folgende gespeicherte Prozedur wird auf dem lokalen Server `SEATTLE1` erstellt. Der Benutzer meldet sich am Remoteserver `LONDON2` an und führt `usp_CheckServer` aus.  
  
```  
EXEC SEATTLE1...usp_CheckServer;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------------  
LONDON2  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurationsfunktionen (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [Remoteserver](../../database-engine/configure-windows/remote-servers.md)  
  
  

