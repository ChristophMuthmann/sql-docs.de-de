---
title: Angeben des ersten und des letzten Triggers | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: triggers
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-dml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- first triggers [SQL Server]
- last triggers
- DML triggers, first or last triggers
- INSTEAD OF triggers
- AFTER triggers
ms.assetid: 9e6c7684-3dd3-46bb-b7be-523b33fae4d5
caps.latest.revision: 24
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 33d3488d20be5196a9dc9a7f13db334c3b94fd57
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="specify-first-and-last-triggers"></a>Angeben des ersten und des letzten Triggers
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  Sie können angeben, dass einer der AFTER-Trigger, der einer Tabelle zugeordnet ist, der erste oder der letzte AFTER-Trigger ist, der für jede der auslösenden INSERT-, DELETE- und UPDATE-Aktionen ausgelöst wird. Die AFTER-Trigger, die zwischen dem ersten und letzten Trigger ausgelöst werden, werden in einer nicht definierten Reihenfolge ausgeführt.  
  
 Um die Ausführungsreihenfolge für einen AFTER-Trigger anzugeben, verwenden Sie die gespeicherte Prozedur **sp_settriggerorder** . **sp_settriggerorder** besitzt die folgenden Optionen.  
  
|Option|Description|  
|------------|-----------------|  
|**Erster**|Gibt an, dass der DML-Trigger der erste AFTER-Trigger ist, der für eine Triggeraktion ausgelöst wird.|  
|**Letzter**|Gibt an, dass der DML-Trigger der letzte AFTER-Trigger ist, der für eine Triggeraktion ausgelöst wird.|  
|**Keine**|Gibt an, dass keine besondere Reihenfolge vorhanden ist, in der der DML-Trigger ausgelöst werden soll. Diese Option wird hauptsächlich verwendet, um einen ersten oder letzten Trigger zurückzusetzen.|  
  
 Das folgende Beispiel zeigt die Verwendung von **sp_settriggerorder**:  
  
```  
sp_settriggerorder @triggername = 'MyTrigger', @order = 'first', @stmttype = 'UPDATE'  
```  
  
> [!IMPORTANT]  
>  Der erste und der letzte Trigger müssen zwei unterschiedliche Trigger sein.  
  
 Für eine Tabelle können gleichzeitig INSERT-, UPDATE- und DELETE-Trigger definiert sein. Jeder Anweisungstyp kann über eigene erste und letzte Trigger verfügen; es darf sich dabei jedoch nicht um dieselben Trigger handeln.  
  
 Wenn der für eine Tabelle definierte erste oder letzte Trigger keine Triggeraktion abdeckt, wie beispielsweise FOR UPDATE, FOR DELETE oder FOR INSERT, gibt es keinen ersten oder letzten Trigger für die fehlenden Aktionen.  
  
 INSTEAD OF-Trigger können nicht als erste oder letzte Trigger angegeben werden. INSTEAD OF-Trigger werden ausgelöst, bevor Updates an den zugrunde liegenden Tabellen vorgenommen werden. Wenn die Updates an zugrunde liegenden Tabellen durch einen INSTEAD OF-Trigger vorgenommen werden, erfolgen die Updates, bevor einer der für die Tabelle definierten AFTER-Trigger ausgelöst wird. Wenn z. B. ein INSTEAD OF INSERT-Trigger für eine Sicht Daten in eine Basistabelle einfügt und die Basistabelle selbst einen INSTEAD OF INSERT-Trigger und drei AFTER INSERT-Trigger enthält, wird der INSTEAD OF INSERT-Trigger für die Basistabelle statt der Einfügeaktion ausgelöst, und die AFTER-Trigger für die Basistabelle werden nach einer Einfügeaktion für die Basistabelle ausgelöst. Weitere Informationen finden Sie unter [DML Triggers](../../relational-databases/triggers/dml-triggers.md).  
  
 Wenn eine ALTER TRIGGER-Anweisung den ersten oder letzten Trigger ändert, wird das **First** - oder **Last** -Attribut gelöscht, und der Reihenfolgewert wird auf **None**festgelegt. Die Reihenfolge muss mit **sp_settriggerorder**zurückgesetzt werden.  
  
 Die Funktion OBJECTPROPERTY meldet mithilfe folgender Eigenschaften, ob es sich bei einem Trigger um den ersten oder den letzten Trigger handelt: **ExecIsFirstInsertTrigger**, **ExecIsFirstUpdateTrigger**, **ExecIsFirstDeleteTrigger**, **ExecIsLastInsertTrigger**, **ExecIsLastUpdateTrigger** und **ExecIsLastDeleteTrigger**.  
  
 Die Replikation generiert automatisch einen ersten Trigger für alle Tabellen, die in einem Abonnement mit sofortigem Update oder verzögertem Update über eine Warteschlange enthalten sind. Für die Replikation gilt, dass ihr Trigger der erste Trigger sein muss. Die Replikation meldet einen Fehler, wenn Sie versuchen, eine Tabelle, die einen ersten Trigger aufweist, in ein Abonnement mit sofortigem Update bzw. verzögertem Update über eine Warteschlange einzufügen. Wenn Sie versuchen, einen Trigger zum ersten Trigger zu erklären, nachdem eine Tabelle in ein Abonnement aufgenommen wurde, gibt **sp_settriggerorder** einen Fehler zurück. Wenn Sie ALTER für den Replikationstrigger verwenden oder **sp_settriggerorder** verwenden, um den Replikationstrigger auf einen Trigger vom Typ LAST oder NONE festzulegen, funktioniert das Abonnement nicht ordnungsgemäß.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_settriggerorder &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql.md)  
  
  
