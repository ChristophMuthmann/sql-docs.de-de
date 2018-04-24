---
title: RECONFIGURE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/20/2016
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a2aa82bf7e34fb4ed7a2dcc083055d49e64c14a9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="reconfigure-transact-sql"></a>RECONFIGURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aktualisiert den derzeit konfigurierten Wert (die **config_value**-Spalte im **sp_configure**-Resultset) einer Konfigurationsoption, die mit der gespeicherten Systemprozedur **sp_configure** geändert wurde. Da einige Konfigurationsoptionen einen Serverstopp und -neustart erfordern, um den derzeit wirksamen Wert zu aktualisieren, aktualisiert RECONFIGURE nicht immer den derzeit wirksamen Wert (die **run_value**-Spalte im **sp_configure**-Resultset) mit einem geänderten Konfigurationswert.    
    
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Syntax    
    
```    
    
RECONFIGURE [ WITH OVERRIDE ]    
```    
    
## <a name="arguments"></a>Argumente    
 RECONFIGURE    
 Gibt an, dass der derzeit wirksame Wert aktualisiert werden soll, wenn die Konfigurationseinstellung keinen Serverstopp und Neustart erfordert. RECONFIGURE überprüft darüber hinaus die neuen Konfigurationswerte entweder auf ungültige Werte (z.B. einen Sortierreihenfolgenwert, der nicht in **syscharsets** vorhanden ist) oder auf nicht empfohlene Werte. Bei den Konfigurationsoptionen, die keinen Serverstopp und -neustart erfordern, sollten der derzeit wirksame Wert und der derzeit konfigurierte Wert der Konfigurationsoption nach Angabe von RECONFIGURE identisch sein.    
    
 WITH OVERRIDE    
 Deaktiviert die Überprüfung des Konfigurationswerts (auf ungültige oder nicht empfohlene Werte) für die erweiterte Konfigurationsoption **recovery interval**.    
    
 Fast alle Konfigurationsoptionen können mithilfe der Option WITH OVERRIDE neu konfiguriert werden. Einige schwerwiegende Fehler werden jedoch weiterhin verhindert. So kann beispielsweise der Wert der Konfigurationsoption **min server memory** nicht mit einem höheren Wert konfiguriert werden als der in der Konfigurationsoption **max server memory** angegebene Wert.
      
## <a name="remarks"></a>Remarks    
 **sp_configure** akzeptiert keine neuen Werte für eine Konfigurationsoption, die für diese Konfigurationsoption außerhalb der dokumentierten gültigen Bereiche liegen.    
    
 RECONFIGURE ist in einer expliziten oder impliziten Transaktion nicht zulässig. Wenn Sie mehrere Optionen gleichzeitig neu konfigurieren und bei einem der Neukonfigurierungsvorgänge ein Fehler auftritt, wird keine der Neukonfigurierungen wirksam.    
    
 Beachte Sie beim Konfigurieren von Resource Governor die Option RECONFIGURE von [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md).    
    
## <a name="permissions"></a>Berechtigungen    
 RECONFIGURE-Berechtigungen erhalten standardmäßig ALTER SETTINGS-Berechtigte. Diese Berechtigung erhalten implizit die festen Serverrollen **sysadmin** und **serveradmin**.    
    
## <a name="examples"></a>Beispiele    
 Im folgenden Beispiel wird der obere Grenzwert für die Konfigurationsoption `recovery interval` auf `75` Minuten festgelegt und mithilfe von `RECONFIGURE WITH OVERRIDE` installiert. Wiederherstellungsintervalle über 60 Minuten werden nicht empfohlen und sind standardmäßig nicht zulässig. Da jedoch die Option `WITH OVERRIDE` angegeben wurde, wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht überprüft, ob es sich beim angegebenen Wert (`90`) um einen gültigen Wert für die Konfigurationsoption `recovery interval` handelt.    
    
```    
EXEC sp_configure 'recovery interval', 75'    
RECONFIGURE WITH OVERRIDE;    
GO    
```    
    
## <a name="see-also"></a>Weitere Informationen finden Sie unter    
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)    
    
  
