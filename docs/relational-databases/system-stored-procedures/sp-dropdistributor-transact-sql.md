---
title: Sp_dropdistributor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_dropdistributor
- sp_dropdistributor_TSQL
helpviewer_keywords:
- sp_dropdistributor
ms.assetid: 0644032f-5ff0-4718-8dde-321bc9967a03
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dfb681d5022e5a5f9ada3f0815513ce020250e79
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spdropdistributor-transact-sql"></a>sp_dropdistributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Deinstalliert den Verteiler. Diese gespeicherte Prozedur wird auf dem Verteiler für jede Datenbank mit Ausnahme der Verteilungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_dropdistributor [ [ @no_checks= ] no_checks ]   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@no_checks=**] *No_checks*  
 Gibt an, ob vor dem Löschen des Verteilers auf abhängige Objekte überprüft werden soll. *No_checks* ist **Bit**, hat den Standardwert 0.  
  
 Wenn **0**, **Sp_dropdistributor** überprüft, um sicherzustellen, dass alle Veröffentlichungs- und Verteilungsobjekte Objekte zusätzlich zum Verteiler gelöscht wurden.  
  
 Wenn **1**, **Sp_dropdistributor** löscht alle Veröffentlichungs- und Verteilungsobjekte vor dem Deinstallieren des Verteilers.  
  
 [  **@ignore_distributor=**] *Ignore_distributor*  
 Gibt an, ob diese gespeicherte Prozedur ausgeführt wird, ohne eine Verbindung mit dem Verteiler herzustellen. *Ignore_distributor* ist **Bit**, hat den Standardwert **0**.  
  
 Wenn **0**, **Sp_dropdistributor** eine Verbindung mit dem Verteiler her und entfernt alle Replikationsobjekte. Wenn **Sp_dropdistributor** ist keine Verbindung mit dem Verteiler, schlägt die gespeicherte Prozedur fehl.  
  
 Wenn **1**, keine Verbindung mit dem Verteiler hergestellt wird und die Replikationsobjekte werden nicht entfernt. Diese Möglichkeit wird verwendet, wenn der Verteiler deinstalliert wird oder dauerhaft offline ist. Die Objekte für diesen Verleger werden auf dem Verteiler nicht entfernt, bis der Verteiler zu einem späteren Zeitpunkt neu installiert wird.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_dropdistributor** wird für alle Replikationstypen verwendet.  
  
 Wenn andere Verleger- oder Verteilungsobjekte Objekte auf dem Server vorhanden sind **Sp_dropdistributor** schlägt fehl, es sei denn, **@no_checks** festgelegt ist, um **1**.  
  
 Diese gespeicherte Prozedur muss ausgeführt werden, nachdem die Verteilungsdatenbank gelöscht, durch das Ausführen **Sp_dropdistributiondb**.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistributor-trans_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle kann ausführen **Sp_dropdistributor**.  
  
## <a name="see-also"></a>Siehe auch  
 [Deaktivieren der Veröffentlichung und Verteilung](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [Sp_adddistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)   
 [Sp_changedistributor_property &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
