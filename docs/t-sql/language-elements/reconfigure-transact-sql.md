---
title: RECONFIGURE-Anweisung (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/20/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 432e5157969a10f36273db3bbd8990fa9e332b68
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="reconfigure-transact-sql"></a>RECONFIGURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aktualisiert den derzeit konfigurierten Wert (Spalte **config_value** im Resultset **sp_configure**) einer Konfigurationsoption mit der gespeicherten Systemprozedur **sp_configure**. Da einige Konfigurationsoptionen das Beenden und erneute Starten des Servers für die Aktualisierung des aktuell ausgeführten Werts erfordern, aktualisiert RECONFIGURE bei Änderung des Konfigurationswerts nicht immer den aktuell ausgeführten Wert (Spalte **run_value** im Resultset **sp_configure**).     
    
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Syntax    
    
```    
    
RECONFIGURE [ WITH OVERRIDE ]    
```    
    
## <a name="arguments"></a>Argumente    
 RECONFIGURE    
 Gibt an, dass der derzeit wirksame Wert aktualisiert werden soll, wenn die Konfigurationseinstellung keinen Serverstopp und Neustart erfordert. RECONFIGURE überprüft auch die neuen Konfigurationswerte entweder Werte, die nicht gültig sind (z. B. einen Sortierreihenfolgenwert, die nicht in existiert **Syscharsets**) oder nicht empfehlenswerte Konfigurationswertswerte. Bei den Konfigurationsoptionen, die keinen Serverstopp und -neustart erfordern, sollten der derzeit wirksame Wert und der derzeit konfigurierte Wert der Konfigurationsoption nach Angabe von RECONFIGURE identisch sein.    
    
 WITH OVERRIDE    
 Deaktiviert die Konfigurationswertüberprüfung (für ungültige oder nicht empfohlene Werte) für die erweiterte Konfigurationsoption **recovery interval**.   
    
 Nahezu jede Konfigurationsoption kann mithilfe der Option WITH OVERRIDE neu konfiguriert werden. Allerdings werden einige schwerwiegende Fehler auch weiterhin verhindert. So kann etwa für die Konfigurationsoption **min server memory** kein Wert konfiguriert werden ,der größer ist als der Wert der Konfigurationsoption **max server memory**.
      
## <a name="remarks"></a>Hinweise    
 **Sp_configure** akzeptiert keine neuen Werte für eine Konfigurationsoption außerhalb der dokumentierten gültigen Bereiche für jede Konfigurationsoption.    
    
 RECONFIGURE ist in einer expliziten oder impliziten Transaktion nicht zulässig. Wenn Sie mehrere Optionen gleichzeitig neu konfigurieren und bei einem der Neukonfigurierungsvorgänge ein Fehler auftritt, wird keine der Neukonfigurierungen wirksam.    
    
 Wenn die Ressourcenkontrolle neu konfiguriert wird, finden Sie unter der Option RECONFIGURE [ALTER RESOURCE GOVERNOR &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-resource-governor-transact-sql.md).    
    
## <a name="permissions"></a>Berechtigungen    
 RECONFIGURE-Berechtigungen erhalten standardmäßig ALTER SETTINGS-Berechtigte. Die **Sysadmin** und **Serveradmin** festen Serverrollen diese Berechtigung erhalten implizit.    
    
## <a name="examples"></a>Beispiele    
 Im folgenden Beispiel wird der obere Grenzwert für die Konfigurationsoption `recovery interval` auf `75` Minuten festgelegt und mithilfe von `RECONFIGURE WITH OVERRIDE` installiert. Wiederherstellungsintervalle über 60 Minuten werden nicht empfohlen und sind standardmäßig nicht zulässig. Da jedoch die Option `WITH OVERRIDE` angegeben wurde, wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht überprüft, ob es sich beim angegebenen Wert (`75`) um einen gültigen Wert für die Konfigurationsoption `recovery interval` handelt.    
    
```    
EXEC sp_configure 'recovery interval', 75'    
RECONFIGURE WITH OVERRIDE;    
GO    
```    
    
## <a name="see-also"></a>Siehe auch    
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)    
    
  
