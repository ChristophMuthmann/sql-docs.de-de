---
title: SQL Server Integration Services Scale Out-Manager | Microsoft-Dokumentation
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
ms.openlocfilehash: 84fe58d4dc7894728c43cb19d17d3444b5b84820
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="integration-services-scale-out-manager"></a>Integration Services Scale Out-Manager

Scale Out-Manager ist ein Verwaltungstool, mit dem Sie Ihre vollständige SSIS Scale Out-Topologie von einem einzigen Ort aus verwalten können. Sie müssen nicht mehr an mehreren Computern arbeiten und keine TSQL-Befehle mehr verwenden. 

Es gibt zwei Möglichkeiten, um Scale Out-Manager zu starten.

## <a name="1-open-scale-out-manager-from-sql-server-management-studio"></a>1. Öffnen Sie Scale Out-Manager über SQL Server Management Studio.
Öffnen Sie SQL Server Management Studio, und stellen Sie eine Verbindung mit der SQL Server-Instanz von Scale Out-Master her.

Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf **SSISDB**, und wählen Sie **Scale Out verwalten...** aus. ![Scale Out verwalten](media/manage-scale-out.PNG)

> [!NOTE]
> Es wird empfohlen, SQL Server Management Studio als Administrator auszuführen, da manche der Scale Out-Verwaltungsvorgänge (z.B. das Hinzufügen des Scale Out-Workers) Administratorrechte erfordern.


## <a name="2-open-scale-out-manager-by-runing-ismanagerexe-directly"></a>2. Öffnen von Scale Out-Manager, indem „ISManager.exe“ direkt ausgeführt wird

„ISManager.exe“ befindet sich unter %SystemDrive%\Programme (x86)\Microsoft SQL Server\140\DTS\Binn\Management. Klicken Sie mit der rechten Maustaste auf **ISManager.exe**, und wählen Sie „Als Administrator ausführen“ aus. 

Nach dem Öffnen müssen Sie den SQL-Servernamen von Scale Out-Master eingeben und eine Verbindung herstellen, bevor Sie Scale Out verwalten können.

![Portal: Verbindung herstellen](media/portal-connect.PNG)

Im Folgenden werden die verschiedenen Funktionen von Scale Out-Manager beschrieben. 

## <a name="enable-scale-out"></a>Aktivieren von Scale Out
Wenn Scale Out deaktiviert ist, können Sie zum Aktivieren auf „Aktivieren“ klicken, nachdem Sie eine Verbindung mit SQL Server hergestellt haben.

![Portal: Aktivieren von Scale Out](media/portal-enable-scale-out.PNG) 
## <a name="view-scale-out-master-status"></a>Anzeigen des Status von Scale Out-Master
Der Status von Scale Out-Master wird auf der **Dashboard**-Seite angezeigt.

![Portal: Dashboard](media/portal-dashboard.PNG)
## <a name="view-scale-out-worker-status"></a>Anzeigen des Status des Scale Out-Workers
Der Status des Scale Out-Workers wird auf der Seite **Worker-Manager** angezeigt. Sie können auf jeden Worker klicken, um den jeweiligen Status anzuzeigen.

![Portal: Worker-Manager](media/portal-worker-manager.PNG)

## <a name="add-scale-out-worker"></a>Hinzufügen des Scale Out-Workers
Klicken Sie auf „+“ im unteren Bereich der Liste „Scale Out-Worker“, um einen Scale Out-Worker hinzuzufügen. 

Geben Sie den Computernamen des Scale Out-Workers ein, den Sie hinzufügen möchten, und klicken Sie auf „Überprüfen“. Der Scale Out-Manager überprüft, ob der aktuelle Benutzer Zugriff auf die Zertifikatspeicher der Computer des Scale Out-Masters und des Scale Out-Workers hat.

![Verbindung herstellen: Worker](media/connect-worker.PNG)

Wenn die Überprüfung erfolgreich ist, versucht der Scale Out-Manager, die Konfigurationsdatei des Workers zu lesen und den Zertifikatfingerabdruck des Workers abzurufen. Weitere Informationen finden Sie unter [Scale Out-Worker](integration-services-ssis-scale-out-worker.md). Wenn die Konfigurationsdatei des Workers nicht gelesen werden kann, gibt es zwei Alternativen, um das Workerzertifikat bereitzustellen. 

Sie können entweder den Fingerabdruck des Workerzertifikats direkt eingeben 

![Workerzertifikat (1)](media/portal-cert1.PNG)

oder die Zertifikatdatei bereitstellen. 

![Workerzertifikat (2)](media/portal-cert2.PNG)

Nachdem alle Informationen erfasst wurden, stellt der Scale Out-Manager die Aktionen bereit, die ausgeführt werden sollen. Üblicherweise schließt dies die Installation des Zertifikats, ein Update der Konfigurationsdatei des Workers und einen Neustart des Workerdiensts ein. 

![Portal: Hinzufügen bestätigen (1)](media/portal-add-confirm1.PNG)

Falls auf den Worker nicht zugegriffen werden kann, müssen Sie diesen manuell aktualisieren und den Workerdienst neu starten.

![Portal: Hinzufügen bestätigen (2)](media/portal-add-confirm2.PNG)

Aktivieren Sie das Kontrollkästchen „Bestätigen“, und beginnen Sie damit, den Scale Out-Worker hinzuzufügen.

## <a name="delete-scale-out-worker"></a>Löschen eines Scale Out-Workers
Wählen Sie einen Scale Out-Worker, und klicken Sie im unteren Bereich der Liste „Scale Out-Worker“ auf „–“, um einen Scale Out-Worker zu löschen.


## <a name="enabledisable-scale-out"></a>Aktivieren/Deaktivieren von Scale Out
Wählen Sie einen Scale Out-Worker aus, und klicken Sie auf die Schaltfläche „Worker aktivieren“ oder „Worker deaktivieren“, um einen Scale Out-Worker zu aktivieren oder zu deaktivieren. Der Workerstatus des Scale Out-Managers ändert sich entsprechend, wenn der Worker nicht offline ist.

## <a name="edit-scale-out-worker-description"></a>Bearbeiten der Beschreibung des Scale Out-Workers
Wählen Sie einen Scale Out-Worker aus, und klicken Sie auf die Schaltfläche „Bearbeiten“, um die Beschreibung eines Scale Out-Workers zu bearbeiten. Klicken Sie auf die Schaltfläche „Speichern“, wenn Sie die Bearbeitung abgeschlossen haben.

![Portal: Worker speichern](media/portal-save-worker.PNG)

