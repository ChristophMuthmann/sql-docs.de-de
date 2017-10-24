---
title: RECONFIGURE-Anweisung (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/20/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RECONFIGURE
- RECONFIGURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- reconfiguring configuration options
- configuration options [SQL Server], reconfiguring
- updating configuration options
- RECONFIGURE, RECONFIGURE statement
- RECONFIGURE
- RECONFIGURE, WITH OVERRIDE statement
ms.assetid: 2e6e4eeb-b70b-4f45-a253-28ac4e595d75
caps.latest.revision: 50
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 32039a4077f028a078e9265c6d18f5cbb6187e3f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="reconfigure-transact-sql"></a>RECONFIGURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aktualisiert den derzeit konfigurierten Wert (der **Config_value** Spalte in der **Sp_configure** Resultset) einer Konfigurationsoption geändert, mit der **Sp_configure** System gespeicherte Prozedur. Da einige Konfigurationsoptionen einen Serverstopp und Neustart für das aktuell ausgeführte update erfordern, RECONFIGURE nicht immer aktualisiert den derzeit ausgeführten Wert (der **Run_value** Spalte in der **Sp_configure**  Resultset) für einen geänderten Konfigurationswert.    
    
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Syntax    
    
```    
    
RECONFIGURE [ WITH OVERRIDE ]    
```    
    
## <a name="arguments"></a>Argumente    
 RECONFIGURE    
 Gibt an, dass der derzeit wirksame Wert aktualisiert werden soll, wenn die Konfigurationseinstellung keinen Serverstopp und Neustart erfordert. RECONFIGURE überprüft auch die neuen Konfigurationswerte entweder Werte, die nicht gültig sind (z. B. einen Sortierreihenfolgenwert, die nicht in existiert **Syscharsets**) oder Konfigurationswerts Werte. Bei den Konfigurationsoptionen, die keinen Serverstopp und -neustart erfordern, sollten der derzeit wirksame Wert und der derzeit konfigurierte Wert der Konfigurationsoption nach Angabe von RECONFIGURE identisch sein.    
    
 WITH OVERRIDE    
 Deaktiviert die konfigurationswertüberprüfung (für Werte, die ungültig sind oder Konfigurationswerts Werte) für die **Wiederherstellungsintervall** erweiterte Konfigurationsoption.    
    
 Nahezu jede Konfigurationsoption kann neu konfiguriert werden, mithilfe der Option WITH OVERRIDE, jedoch einige schwerwiegende Fehler weiterhin verhindert werden. Z. B. die **Min. Serverarbeitsspeicher** Konfigurationsoption kann nicht konfiguriert werden, mit einem Wert größer als der Wert der **Max. Serverarbeitsspeicher** Konfigurationsoption.
      
## <a name="remarks"></a>Hinweise    
 **Sp_configure** akzeptiert keine neuen Werte für eine Konfigurationsoption außerhalb der dokumentierten gültigen Bereiche für jede Konfigurationsoption.    
    
 RECONFIGURE ist in einer expliziten oder impliziten Transaktion nicht zulässig. Wenn Sie mehrere Optionen gleichzeitig neu konfigurieren und bei einem der Neukonfigurierungsvorgänge ein Fehler auftritt, wird keine der Neukonfigurierungen wirksam.    
    
 Wenn die Ressourcenkontrolle neu konfiguriert wird, finden Sie unter der Option RECONFIGURE [ALTER RESOURCE GOVERNOR &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-resource-governor-transact-sql.md).    
    
## <a name="permissions"></a>Berechtigungen    
 RECONFIGURE-Berechtigungen erhalten standardmäßig ALTER SETTINGS-Berechtigte. Die **Sysadmin** und **Serveradmin** festen Serverrollen diese Berechtigung erhalten implizit.    
    
## <a name="examples"></a>Beispiele    
 Im folgenden Beispiel wird der obere Grenzwert für die Konfigurationsoption `recovery interval` auf `75` Minuten festgelegt und mithilfe von `RECONFIGURE WITH OVERRIDE` installiert. Wiederherstellungsintervalle über 60 Minuten werden nicht empfohlen und sind standardmäßig nicht zulässig. Da jedoch die Option `WITH OVERRIDE` angegeben wurde, wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht überprüft, ob es sich beim angegebenen Wert (`90`) um einen gültigen Wert für die Konfigurationsoption `recovery interval` handelt.    
    
```    
EXEC sp_configure 'recovery interval', 75'    
RECONFIGURE WITH OVERRIDE;    
GO    
```    
    
## <a name="see-also"></a>Siehe auch    
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)    
    
  

