---
title: Aktivieren der CLR-Integration | Microsoft Docs
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- clr enabled option
- common language runtime [SQL Server], enabling
ms.assetid: eb3e9c64-7486-42e7-baf6-c956fb311a2c
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: d66238df770dfd647c3013441024409f15fdef9b
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="clr-integration---enabling"></a>CLR-Integration - Aktivierung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Die common Language Runtime (CLR)-Integrationsfunktion ist standardmäßig deaktiviert und muss aktiviert werden, um Objekte zu verwenden, die mit CLR-Integration implementiert werden. Verwenden Sie zum Aktivieren der CLR-Integration die **Clr-fähig** -Option von der **Sp_configure** gespeicherte Prozedur in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
```sql  
  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'clr enabled', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
 Sie können den CLR-Integration deaktivieren, indem die **Clr-fähig** -Option auf 0. Wenn Sie die CLR-Integration deaktivieren, stoppt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Ausführung aller CLR-Routinen und entlädt alle Anwendungsdomänen.  
  
> [!NOTE]  
>  Um CLR-Integration zu aktivieren, benötigen Sie ALTER SETTINGS Serverberechtigung, die implizit von Mitgliedern der erhalten die **Sysadmin** und **Serveradmin** festen Serverrollen.  
  
> [!NOTE]  
>  Computer, die mit großen Mengen an Arbeitsspeicher und einer großen Anzahl von Prozessoren konfiguriert sind, können das SQL Server-Funktion zur CLR-Integration beim Serverstart möglicherweise nicht laden. Um dieses Problem zu beheben, starten Sie den Server mithilfe der **-Gmemory_to_reserve** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Dienststartoption, und geben Sie einen ausreichend großen Speicherwert. Weitere Informationen finden Sie unter [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
> [!NOTE]  
>  CLR (Common Language Runtime) wird beim Lightweightpooling nicht unterstützt. Vor dem Aktivieren der CLR-Integration müssen Sie Lightweightpooling deaktivieren. Weitere Informationen finden Sie unter [Lightweightpooling (Serverkonfigurationsoption)](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md).  
  
## <a name="see-also"></a>Siehe auch  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CLR-fähig (Serverkonfigurationsoption)](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Rollen auf Serverebene](../../relational-databases/security/authentication-access/server-level-roles.md)  
  
  
