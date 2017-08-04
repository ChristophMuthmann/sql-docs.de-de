---
title: SQL Serverintegration Services-Dezentrales Skalieren Manager | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 96748296acd1b2f5ba98558335fece9637eadb87
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-scale-out-manager"></a>Integration Services Dezentrales Skalieren Manager

Scale-Out-Manager ist ein Management-Tool, das Ihnen ermöglicht, Ihre vollständige Horizontales Skalieren SSIS-Topologie an einem zentralen Ort zu verwalten. Entfernt die Last auf mehreren Computern ausgeführt und der Umgang mit t-SQL-Befehle. 

Es gibt zwei Möglichkeiten zum Auslösen der Scale-Out-Manager.

## <a name="1-open-scale-out-manager-from-sql-server-management-studio"></a>1. Öffnen Sie Dezentrales Skalieren Manager von SQL Server Management Studio
Öffnen Sie SQL Server Management Studio, und Verbinden mit SQL Server-Instanz des Scale-Out-Master.

Mit der rechten Maustaste **SSISDB** im Objekt-Explorer, und wählen **verwalten horizontal skalieren...** . 
![Verwalten für horizontales Skalieren](media/manage-scale-out.PNG)

> [!NOTE]
> Es wird empfohlen, zum Ausführen von SQL Server Management Studio als Administrator als Teil der Verwaltungsvorgänge horizontal skalieren, z. B. "horizontales hochskalieren Worker hinzufügen" Administratorberechtigungen benötigen.


## <a name="2-open-scale-out-manager-by-runing-ismanagerexe-directly"></a>2. Öffnen Sie Scale-Out-Manager, indem auf ISManager.exe direkt

ISManager.exe sucht unter %SystemDrive%\Programme\Microsoft Dateien (x86) \Microsoft SQL Server\140\DTS\Binn\Management. Klicken Sie mit der rechten Maustaste auf **ISManager.exe** , und wählen Sie "Als Administrator ausführen". 

Nachdem er geöffnet wird, müssen Sie den Sql Server-Namen Scale-Out-Master eingeben und herstellen, wenn sie vor dem Verwalten Ihrer horizontal skalieren.

![Verwaltungsportal – Connect](media/portal-connect.PNG)

Scale-Out-Manager bietet verschiedene Funktionen wie unten beschrieben. 

## <a name="enable-scale-out"></a>Aktivieren Sie für horizontales Skalieren
Nach dem Herstellen einer Verbindung mit SQL Server, wenn horizontal skalieren nicht aktiviert ist, können Sie die Schaltfläche "Aktivieren", um ihn zu aktivieren klicken Sie auf.

![Portal aktivieren für horizontales Skalieren](media/portal-enable-scale-out.PNG) 
## <a name="view-scale-out-master-status"></a>Scale-Out-Master-Anzeigestatus
Der Status der Scale-Out-Master wird angezeigt, auf die **Dashboard** Seite.

![Projektportal-Dashboards](media/portal-dashboard.PNG)
## <a name="view-scale-out-worker-status"></a>Scale-Out-Worker-Anzeigestatus
Der Status der Scale-Out-Worker wird angezeigt, auf die **Worker-Manager** Seite. Sie können für jeden Arbeitsthread auf den einzelnen Status anzeigen klicken.

![Portal-Worker-Manager](media/portal-worker-manager.PNG)

## <a name="add-scale-out-worker"></a>Dezentrales Skalieren Worker hinzufügen
Um einen Maßstab Out Worker hinzuzufügen, klicken Sie auf die Schaltfläche "+" am unteren Rand Scale-Out-Worker-Liste. 

Geben Sie den Computernamen des der Skalierung Out Worker Sie hinzufügen möchten und klicken Sie auf "Überprüfen". Scale-Out-Manager überprüft, ob der aktuelle Benutzer Zugriff auf den Zertifikatspeicher auf den Computern der Scale-Out-Master "und" Scale-Out-Worker verfügt.

![Verbinden von Arbeitsthreads](media/connect-worker.PNG)

Wenn die Überprüfung erfolgreich ist, versucht Scale-Out-Manager, die Worker-Datei "App.config" gelesen und erhalten den Fingerabdruck des Zertifikats des Arbeitsthreads. Weitere Informationen finden Sie unter [Scale-Out-Worker](integration-services-ssis-scale-out-worker.md). Ist dies nicht der Arbeitsthread Config-Datei lesen, gibt es zwei alternative Methoden zur Bereitstellung des Zertifikats Worker. 

Sie können entweder den Fingerabdruck des Zertifikats Worker direkt eingeben 

![Das Workerzertifikat 1](media/portal-cert1.PNG)

oder geben Sie die Zertifikatdatei an. 

![Das Workerzertifikat 2](media/portal-cert2.PNG)

Nachdem Sie alle Informationen erfasst, gebe Scale-Out-Manager die Aktionen ausgeführt werden. Tyically, enthält es Zertifikatinstallation "," Worker Update der Serverkonfigurationsdatei "und" Worker-Dienst neu starten. 

![Portal hinzufügen 1 bestätigen](media/portal-add-confirm1.PNG)

Für den Fall, dass das workerzertifikat nicht zugänglich ist, müssen Sie selbst manuell aktualisieren und den Worker-Dienst neu.

![Portal hinzufügen 2 bestätigen](media/portal-add-confirm2.PNG)

Klicken Sie auf das Kontrollkästchen bestätigen, und starten Sie die Scale-Out-Worker hinzufügen.

## <a name="delete-scale-out-worker"></a>Dezentrales Skalieren Worker löschen
Um eine Skala, Worker zu löschen, wählen Sie die Skalierung Out Arbeitskraft, und klicken Sie auf der "-" am unteren Rand der Liste Scale-Out-Worker-Schaltfläche.


## <a name="enabledisable-scale-out"></a>Horizontales Skalieren aktivieren/deaktivieren
Zum Aktivieren oder Deaktivieren einer Skala Out Worker, wählen Sie die Skalierung, Worker, und klicken Sie auf die "Workerrollen aktivieren" oder "Workerrollen deaktivieren". Der Worker-Status für den Scale-Out-Manager entsprechend geändert werden, wenn sich der Arbeitsthread nicht offline ist.

## <a name="edit-scale-out-worker-description"></a>Scale-Out-Worker-Beschreibung bearbeiten
Um die Beschreibung des eine Skala, Worker zu bearbeiten, wählen Sie die Skalierung, Worker, und klicken Sie auf die Schaltfläche "Bearbeiten". Nachdem Sie die Bearbeitung abgeschlossen haben, klicken Sie auf die Schaltfläche "Speichern".

![Portal speichern Worker](media/portal-save-worker.PNG)


