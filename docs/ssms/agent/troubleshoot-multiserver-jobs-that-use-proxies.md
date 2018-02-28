---
title: "Problembehandlung von proxybasierten Multiserveraufträgen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- proxies [SQL Server Agent], multiserver jobs
- jobs [SQL Server Agent], multiserver jobs using proxies
ms.assetid: fc579bd3-010c-4f72-8b5c-d0cc18a1f280
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ccf7f0b4eb9817aef38420111bb0ac2e7ce7bf2a
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="troubleshoot-multiserver-jobs-that-use-proxies"></a>Problembehandlung von proxybasierten Multiserveraufträgen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Verteilte Aufträge mit Schritten, die einem Proxy zugeordnet sind, werden unter dem Kontext des Proxykontos auf dem Zielserver ausgeführt. Wenn Auftragsschritte, die Proxykonten verwenden, beim Herunterladen vom Masterserver einen Fehler erzeugen, überprüfen Sie die **error_message** -Spalte in der **sysdownloadlist** -Tabelle der **msdb** -Datenbank auf folgende Fehlermeldungen:  
  
-   "Für den Auftragsschritt ist ein Proxykonto erforderlich, das Proxyabgleichen ist auf dem Zielserver aber deaktiviert."  
  
    Um diesen Fehler zu beheben, legen Sie den Registrierungsunterschlüssel **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL.***\<n*>**\SQLServerAgent\AllowDownloadedJobsToMatchProxyName auf **1 (TRUE)** fest. Dieser Unterschlüssel ist standardmäßig auf **0** (**falsch**) festgelegt. Der Wert von **MSSQL.**\<*n*> ist der Instanzname, z.B. **MSSQL.1** oder **MSSQL.3**.  
  
-   "Proxy nicht gefunden."  
  
    Zum Beheben dieses Fehlers stellen Sie sicher, dass auf dem Zielserver ein Proxykonto vorhanden ist, das den gleichen Namen wie das Proxykonto des Masterservers hat, unter dem der Auftragsschritt ausgeführt wird.  
  
> [!CAUTION]  
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry_md.md)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Erstellen einer Multiserverumgebung](../../ssms/agent/create-a-multiserver-environment.md)  
  
