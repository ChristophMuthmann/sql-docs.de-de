---
title: Sp_OADestroy (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_OADestroy_TSQL
- sp_OADestroy
dev_langs: TSQL
helpviewer_keywords: sp_OADestroy
ms.assetid: 0bd1cff4-ceff-4095-9ae4-e1e65a80f5d6
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cadadd9ac5c5c99748a21f4e6c38a6f22b1e96e5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spoadestroy-transact-sql"></a>sp_OADestroy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zerstört ein zuvor erstelltes OLE-Objekt.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_OADestroy objecttoken      
```  
  
## <a name="arguments"></a>Argumente  
 *objecttoken*  
 Das Objekttoken eines zuvor mit **sp_OACreate**erstellten OLE-Objekts.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder eine Zahl ungleich Null (Fehler), die dem ganzzahligen Wert von HRESULT entspricht, der vom OLE-Automatisierungsobjekt zurückgegeben wird.  
  
 Weitere Informationen zu HRESULT-Rückgabecodes finden Sie unter [OLE-Automatisierung Rückgabecodes und Fehlerinformationen](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="remarks"></a>Hinweise  
 Wird **sp_OADestroy** nicht aufgerufen, wird das erstellte OLE-Objekt am Ende des Batches automatisch gelöscht.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird das zuvor erstellte **SQLServer** -Objekt zerstört.  
  
```  
EXEC @hr = sp_OADestroy @object;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [OLE-Automatisierung gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE-Automatisierungsbeispielskript](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
