---
title: SQL Server Integration Services Scale Out-Manager | Microsoft-Dokumentation
ms.description: This article describes the Scale Out Manager tool which you can use to manager SSIS Scale Out
ms.custom: ''
ms.date: 12/19/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: scale-out
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5e7d9120273330d4beab9e859fa17dde4caa0b04
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="integration-services-scale-out-manager"></a>Integration Services Scale Out-Manager

Der Scale Out-Manager ist ein Verwaltungstool, mit dem Sie Ihre gesamte SSIS Scale Out-Topologie mithilfe einer einzigen App verwalten können. Dadurch müssen Sie keine Verwaltungsaufgaben mehr erledigen und keine Transact-SQL-Befehle mehr auf mehreren Computern ausführen.

## <a name="open-scale-out-manager"></a>Öffnen des Scale Out-Managers

Es gibt zwei Möglichkeiten, den Scale Out-Manager zu öffnen.

### <a name="1-open-scale-out-manager-from-sql-server-management-studio"></a>1. Öffnen Sie Scale Out-Manager über SQL Server Management Studio.
Öffnen Sie SQL Server Management Studio (SSMS), und stellen Sie eine Verbindung mit der SQL Server-Instanz von Scale Out-Master her.

Klicken Sie in Objekt-Explorer mit der rechten Maustaste auf **SSISDB**, und wählen Sie **Scale Out verwalten** aus.

![Zentrales Hochskalieren verwalten](media/manage-scale-out.PNG)

> [!NOTE]
> Es wird empfohlen, SSMS als Administrator auszuführen, da Sie für einige Verwaltungsoptionen für Scale Out wie das Hinzufügen eines Scale Out-Workers Administratorrechte benötigen.

### <a name="2-open-scale-out-manager-by-running-ismanagerexe"></a>2. Öffnen Sie den Scale Out-Manager, indem Sie „ISManager.exe“ ausführen

Suchen Sie `ISManager.exe` unter `%SystemDrive%\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn\Management`. Klicken Sie mit der rechten Maustaste auf **ISManager.exe**, und wählen Sie **Als Administrator ausführen** aus. 

Nachdem sich der Scale Out-Manager geöffnet hat, geben Sie den Namen der SQL Server-Instanz des Scale Out-Masters ein, und stellen Sie eine Verbindung mit dieser Instanz her, um die Scale Out-Umgebung zu verwalten.

![Portal: Verbindung herstellen](media/portal-connect.PNG)

## <a name="tasks-available-in-scale-out-manager"></a>Verfügbare Aufgaben im Scale Out-Manager
Im Scale Out-Manager können Sie folgende Schritte ausführen:

### <a name="enable-scale-out"></a>Aktivieren von Scale Out
Wenn Scale Out deaktiviert ist, können Sie zum Aktivieren auf **Aktivieren** klicken, nachdem Sie eine Verbindung mit SQL Server hergestellt haben.

![Portal: Aktivieren von Scale Out](media/portal-enable-scale-out.PNG) 

### <a name="view-scale-out-master-status"></a>Anzeigen des Status von Scale Out-Master
Der Status von Scale Out-Master wird auf der **Dashboard**-Seite angezeigt.

![Portal: Dashboard](media/portal-dashboard.PNG)

### <a name="view-scale-out-worker-status"></a>Anzeigen des Status des Scale Out-Workers
Der Status des Scale Out-Workers wird auf der Seite **Worker-Manager** angezeigt. Sie können einen beliebigen Worker auswählen, um den jeweiligen Status anzuzeigen.

![Portal: Worker-Manager](media/portal-worker-manager.PNG)

### <a name="add-a-scale-out-worker"></a>Hinzufügen eines Scale Out-Workers
Klicken Sie im unteren Bereich der Liste „Scale Out-Worker“ auf **+**, um einen Scale Out-Worker hinzuzufügen. 

Geben Sie den Computernamen des Scale Out-Workers ein, den Sie hinzufügen möchten, und klicken Sie auf **Überprüfen**. Der Scale Out-Manager überprüft, ob der aktuelle Benutzer Zugriff auf die Zertifikatspeicher der Computer des Scale Out-Masters und des Scale Out-Workers hat.

![Verbindung herstellen: Worker](media/connect-worker.PNG)

Wenn die Überprüfung erfolgreich ist, versucht der Scale Out-Manager, die Konfigurationsdatei des Servers des Workers zu lesen und den Zertifikatfingerabdruck des Workers abzurufen. Weitere Informationen finden Sie unter [Scale Out-Worker](integration-services-ssis-scale-out-worker.md). Wenn der Scale Out-Manager die Konfigurationsdatei des Workerdiensts nicht lesen kann, gibt es zwei Alternativen, um das Workerzertifikat bereitzustellen. 

1.  Sie können entweder den Fingerabdruck des Workerzertifikats direkt eingeben

    ![Workerzertifikat (1)](media/portal-cert1.PNG)

2.  oder die Zertifikatdatei bereitstellen. 

    ![Workerzertifikat (2)](media/portal-cert2.PNG)

Nachdem Informationen erfasst wurden, beschreibt der Scale Out-Manager die Aktionen, die ausgeführt werden sollen. In der Regel handelt es sich bei diesen Optionen um die Installation des Zertifikats, die Aktualisierung der Konfigurationsdatei des Workers und den Neustart des Workerdiensts.

![Portal: Hinzufügen bestätigen (1)](media/portal-add-confirm1.PNG)

Falls nicht auf den Worker zugegriffen werden kann, müssen Sie diesen manuell aktualisieren und den Workerdienst neu starten.

![Portal: Hinzufügen bestätigen (2)](media/portal-add-confirm2.PNG)

Aktivieren Sie das Kontrollkästchen **Bestätigen**, und klicken Sie dann auf **OK**, um den Vorgang zum Hinzufügen eines Scale Out-Workers zu starten.

### <a name="delete-a-scale-out-worker"></a>Löschen eines Scale Out-Workers
Wählen Sie einen Scale Out-Worker aus, und klicken Sie im unteren Bereich der Liste „Scale Out-Worker“ auf **-**, um einen Scale Out-Worker zu löschen.

### <a name="enable-or-disable-a-scale-out-worker"></a>Aktivieren oder Deaktivieren eines Scale Out-Workers
Wählen Sie einen Scale Out-Worker aus, und klicken Sie auf die Schaltfläche **Worker aktivieren** oder **Worker deaktivieren**, um einen Scale Out-Worker zu aktivieren bzw. zu deaktivieren. Wenn der Worker online ist, ändert sich dessen Status, der im Scale Out-Manager angezeigt wird, umgehend.

## <a name="edit-a-scale-out-worker-description"></a>Bearbeiten der Beschreibung eines Scale Out-Workers
Wählen Sie einen Scale Out-Worker aus, und klicken Sie auf die Schaltfläche **Bearbeiten**, um die Beschreibung eines Scale Out-Workers zu bearbeiten. Klicken Sie auf **Speichern**, nachdem Sie die Beschreibung vollständig bearbeitet haben.

![Portal: Worker speichern](media/portal-save-worker.PNG)

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen finden Sie in den folgenden Artikeln:
-   [Scale Out-Master von Integration Services (SSIS)](integration-services-ssis-scale-out-master.md)
-   [Scale Out-Worker von Integration Services (SSIS)](integration-services-ssis-scale-out-worker.md)