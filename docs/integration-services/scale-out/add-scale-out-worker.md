---
title: "Hinzufügen eines SSIS Scale Out-Workers mit dem Manager für horizontales Hochskalieren | Microsoft-Dokumentation"
ms.description: This article describes how to add an SSIS Scale Out Worker to an existing Scale Out environment by using Scale Out Manager.
ms.custom: 
ms.date: 12/19/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 
author: haoqian
ms.author: haoqian
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9fb097365def44d943a7fe6193a4a6498f4d9e37
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="add-a-scale-out-worker-with-scale-out-manager"></a>Hinzufügen eines SSIS Scale Out-Workers mit dem Manager für horizontales Hochskalieren

Der Scale Out-Manager für Integration Services vereinfacht das Hinzufügen des Scale Out-Workers zu Ihrer bereits bestehenden Scale Out-Umgebung. 

Führen Sie die folgenden Schritte aus, um Ihrer Scale Out-Topologie einen Scale Out-Worker hinzufügen:

## <a name="1-install-scale-out-worker"></a>1. Installieren des SSIS Scale Out-Workers
Wählen Sie im Assistenten zum Installieren von SQL Server auf der Seite **Funktionsauswahl** „Integration Services“ und „Worker für horizontales Hochskalieren“ aus. 
![Komponentenauswahl Worker](media/feature-select-worker.PNG)

Auf der Seite **Integration Services Scale Out-Konfiguration – Workerknoten** können Sie auf **Weiter** klicken, um die Konfiguration an dieser Stelle zu überspringen, und den **Scale Out-Manager** verwenden, um die Konfiguration nach der Installation durchzuführen.

Schließen Sie den Installations-Assistenten ab.

## <a name="2-open-the-firewall-on-the-scale-out-master-computer"></a>2. Öffnen Sie die Firewall auf dem Scale Out-Mastercomputer.
Öffnen Sie in der Windows-Firewall auf dem Scale Out-Mastercomputer den Port, der während der Installation des Scale Out-Masters angegeben wurde (standardmäßig 8391), sowie den Port für SQL Server (standardmäßig 1433).

## <a name="3-add-a-scale-out-worker-with-scale-out-manager"></a>3. Hinzufügen eines SSIS Scale Out-Workers mit dem Manager für horizontales Hochskalieren
Führen Sie SQL Server Management Studio als Administrator aus, und stellen Sie eine Verbindung mit der SQL Server-Instanz des Masters für horizontales Hochskalieren her.

Klicken Sie in Objekt-Explorer mit der rechten Maustaste auf **SSISDB**, und wählen Sie **Manage Scale Out** (Scale Out verwalten) aus. 

![Zentrales Hochskalieren verwalten](media/manage-scale-out.PNG)

Wechseln Sie im Dialogfeld **Scale Out-Manager** zu **Worker-Manager**. Klicken Sie auf die **+**, und befolgen Sie die Anweisungen im Dialogfeld **Connect Worker** (Worker verbinden). 

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen finden Sie unter [Scale Out-Manager](integration-services-ssis-scale-out-manager.md).