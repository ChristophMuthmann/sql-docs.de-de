---
title: Sp_dropanonymousagent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_dropanonymousagent
- sp_dropanonymousagent_TSQL
helpviewer_keywords:
- sp_dropanonymousagent
ms.assetid: 4cb96efa-9358-44a3-a8ee-a7e181bed089
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 10b75c7c2e083a09dbebfc720487511397a1af90
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spdropanonymousagent-transact-sql"></a>sp_dropanonymousagent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht einen anonymen Agent für die Replikationsüberwachung auf dem Verteiler vom Verleger. Diese gespeicherte Prozedur wird auf dem Verleger für jede Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_dropanonymousagent [ @subid= ] sub_id    , [ @type= ] type  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@subid=**] *Sub_id*  
 Die globale ID für ein anonymes Abonnement. *Sub_id* ist **"uniqueidentifier"**, hat keinen Standardwert. Dieser Bezeichner kann abgerufen werden, auf dem Abonnenten mit **Sp_helppullsubscription**. Der Wert in der **Subid** Feld des zurückgegebenen Resultsets stellt diesen globalen Bezeichner.  
  
 [  **@type=**] *Typ*  
 Ist der Typ des Abonnements. *Typ* ist **Int**, hat keinen Standardwert. Gültige Werte sind **1** oder **2**. Geben Sie **1**, wenn die momentaufnahmereplikation oder Transaktionsreplikation mit der Verteilungs-Agent eine Momentaufnahme. Geben Sie **2**, wenn der Merge-Agent mithilfe der Mergereplikation.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_dropanonymousagent** wird für alle Replikationstypen verwendet.  
  
 Diese gespeicherte Prozedur wird nur verwendet, um anonyme Abonnement-Agents zu löschen, und kann nicht verwendet werden, um bekannte Abonnements zu löschen.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Db_owner** festen Datenbankrolle "" in der Verteilungsdatenbank kann ausführen **Sp_dropanonymousagent**.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
