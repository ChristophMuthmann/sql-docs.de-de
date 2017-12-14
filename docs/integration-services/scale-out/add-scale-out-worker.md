---
title: "Hinzufügen eines SSIS Scale Out-Workers mit dem Manager für horizontales Hochskalieren | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ef11448d03bd188aaea425225312af9f681f530c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="add-a-scale-out-worker-with-scale-out-manager"></a>Hinzufügen eines SSIS Scale Out-Workers mit dem Manager für horizontales Hochskalieren

Der Manager für horizontales Hochskalieren der Integration Services vereinfacht das Hinzufügen des Workers für horizontales Hochskalieren zu Ihrer vorhandenen Umgebung für horizontales Hochskalieren erheblich. 

Mit den unten aufgeführten Schritten können Sie Ihrer Topologie für horizontales Hochskalieren einen SSIS Scale Out-Worker hinzufügen:

## <a name="1-install-scale-out-worker"></a>1. Installieren des SSIS Scale Out-Workers
Wählen Sie im Assistenten zum Installieren von SQL Server auf der Seite **Funktionsauswahl** „Integration Services“ und „Worker für horizontales Hochskalieren“ aus. 
![Komponentenauswahl Worker](media/feature-select-worker.PNG)

Auf der Seite **Integration Services-Konfiguration für horizontales Hochskalieren – Workerknoten** können Sie einfach auf „Weiter“ klicken, um die Konfiguration hier zu überspringen und mit **Manager für horizontales Hochskalieren** die Konfiguration nach der Installation auszuführen.

Schließen Sie den Installations-Assistenten ab.

## <a name="2-open-firewall-on-scale-out-master-computer"></a>2. Öffnen der Firewall auf dem Mastercomputer für horizontales Hochskalieren
Öffnen Sie mithilfe der Windows-Firewall auf dem Mastercomputer für horizontales Hochskalieren den Port, der während der Installation des Masters für horizontales Hochskalieren angegeben wurde (standardmäßig 8391), sowie den Port von SQL Server (standardmäßig 1433).

## <a name="3-add-scale-out-worker-with-scale-out-manager"></a>3. Hinzufügen eines SSIS Scale Out-Workers mit dem Manager für horizontales Hochskalieren
Führen Sie SQL Server Management Studio als Administrator aus, und stellen Sie eine Verbindung mit der SQL Server-Instanz des Masters für horizontales Hochskalieren her.

Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf **SSISDB**, und wählen Sie **Zentrales Hochskalieren verwalten...** aus. 

![Zentrales Hochskalieren verwalten](media/manage-scale-out.PNG)

Wechseln Sie im daraufhin angezeigten Dialogfeld **Manager für horizontales Hochskalieren** zu **Worker-Manager**. Klicken Sie auf die „+“-Schaltfläche, und befolgen Sie die Anweisungen im Dialogfeld „Worker verbinden“. Weitere Informationen finden Sie unter [Integration Services Scale Out Manager](integration-services-ssis-scale-out-manager.md) (Integration Services: Manager für horizontales Hochskalieren).
