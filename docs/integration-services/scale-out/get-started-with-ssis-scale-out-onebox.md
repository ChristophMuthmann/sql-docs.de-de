---
title: Erste Schritte mit SSIS Skalierung auf einem einzelnen Computer Out | Microsoft Docs
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
ms.openlocfilehash: 7175c63be4c0e15e50f2020f75d283ac0e3dfdbf
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="get-started-with-integration-services-ssis-scale-out-on-a-single-computer"></a>Erste Schritte mit Integration Services (SSIS) horizontal skalieren auf einem einzelnen computer
Dieser Abschnitt enthält die Anleitung zum Einrichten Integration Services horizontal skalieren, in einer 1-Box-Umgebung mit Standardeinstellungen.

## <a name="1-install-sql-server-features"></a>1. Installieren von SQL Server-Funktionen
Wählen Sie im Installations-Assistenten von SQL Server Database Engine Services, Integration Services, Scale-Out-Master und Scale-Out-Worker auf die **Funktionsauswahl** Seite.

![Funktion auswählen Onebox 1](media/feature-select-onebox1.PNG)

![Funktion auswählen Onebox 2](media/feature-select-onebox2.PNG)

Auf der **Serverkonfiguration** einfach auf "Weiter", um die Standard-Dienstkonten und Starttypen verwenden.

Auf der **Datenbankmodulkonfiguration** Seite "**im gemischten Modus**"und klicken Sie auf"**aktuellen Benutzer hinzufügen**" Schaltfläche. 

![Konfiguration des Datenbankmoduls](media/engine-config.PNG)

Einer der **Scale Out Konfiguration von Integration Services - Master Knoten** und **Scale Out Konfiguration von Integration Services - Worker-Knoten** Seiten, klicken Sie einfach auf "Weiter", um die Standardeinstellungen des Ports und Zertifikate gelten.

Beenden Sie den SQL Server-Installations-Assistenten.

## <a name="2-install-sql-server-management-studio"></a>2. Installieren von SQL Server Management Studio

[Herunterladen](../../ssms/download-sql-server-management-studio-ssms.md) SQL Server Management Studio, und installieren Sie es.

## <a name="3-enable-scale-out"></a>3. Aktivieren Sie für horizontales Skalieren
Öffnen Sie SSMS und Herstellen einer Verbindung mit der lokalen Sql Server-Instanz.
Mit der rechten Maustaste **Integration Services-Kataloge** im Objekt-Explorer, und wählen **Katalog erstellen**.

In der **Katalog erstellen** Dialogfeld **aktivieren Sie diesen Server als SSIS Dezentrales Skalieren Master** ist standardmäßig aktiviert. Erstellen Sie den Katalog einfach wie gewohnt. 

## <a name="4-enable-scale-out-worker"></a>4. Dezentrales Skalieren Worker aktivieren
In SSMS mit der Maustaste **SSISDB** , und wählen Sie **verwalten horizontal skalieren...** . 
![Verwalten für horizontales Skalieren](media/manage-scale-out.PNG)

Der Integration Services-Skalierung Out-Manager wird angezeigt. Sie können horizontal skalieren mit verwalten. Weitere Informationen finden Sie unter [Integration Services Scale Out Manager](integration-services-ssis-scale-out-manager.md).

Um die Skalierung, Worker zu aktivieren, wechseln Sie zur **Worker-Manager** , und wählen Sie den Worker, die Sie aktivieren möchten. Der Worker ist ursprünglich deaktiviert. Klicken Sie auf **aktivieren Worker** zu aktivieren.

## <a name="5-run-packages-in-scale-out"></a>5. Ausführen von Paketen in horizontaler Hochskalierung
Jetzt sind Sie bereit zum Ausführen von SSIS-Paketen in horizontal skalieren. Finden Sie unter [Horizontales Skalieren Ausführen von Paketen in Integrationsservices (SSIS)](run-packages-in-integration-services-ssis-scale-out.md).


Um mehr horizontal skalieren Worker hinzufügen zu können, finden Sie unter [eine Skala Out Worker mit Scale-Out-Manager hinzufügen](add-scale-out-worker.md).
