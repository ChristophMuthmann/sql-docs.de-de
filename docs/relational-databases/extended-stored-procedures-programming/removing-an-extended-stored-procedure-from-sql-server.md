---
title: Entfernen eine erweiterte gespeicherte Prozedur von SQLServer | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- deleting extended stored procedures
- removing extended stored procedures
- extended stored procedures [SQL Server], removing
- dropping extended stored procedures
ms.assetid: 7827e574-3f59-4279-9a9b-532582e041cb
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b602181f3aec43aa37e61d0c20457037a133a67c
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>Entfernen einer erweiterten gespeicherten Prozedur aus SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Verwenden Sie stattdessen die CLR-Integration.  
  
 So löschen Sie jede Funktion der erweiterten gespeicherten Prozedur in einer benutzerdefinierten erweiterten gespeicherten Prozedur DLL eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss vom Systemadministrator ausgeführt der **Sp_dropextendedproc** gespeicherte Systemprozedur, Angeben des Namens der Funktion und den Namen der DLL, in dem sich die Funktion befindet. Dieser Befehl entfernt z. B. die Funktion **Xp_hello**befindet sich in einer DLL, die mit dem Namen xp_hello.dll befindet, vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 Beginnend mit [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], **Sp_dropextendedproc** erweiterte gespeicherte Systemprozeduren nicht gelöscht. Stattdessen sollte der Systemadministrator EXECUTE-Berechtigung für die erweiterte gespeicherte Prozedur zum Verweigern der **öffentlichen** Rolle.  
  
## <a name="see-also"></a>Siehe auch  
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
