---
title: Erste Schritte mit SSIS Scale Out auf einem einzelnen Computer | Microsoft-Dokumentation
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
ms.openlocfilehash: 8514cd548b003a39bf198b83b6b80d775a55384b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="get-started-with-integration-services-ssis-scale-out-on-a-single-computer"></a>Erste Schritte mit Integration Services (SSIS) Scale Out auf einem einzelnen Computer
In diesem Artikel finden Sie eine Anleitung zum Einrichten von Integration Services Scale Out in einer „Ein-Computer“-Umgebung mithilfe von Standardeinstellungen.

## <a name="1-install-sql-server-features"></a>1. Installieren von SQL Server-Funktionen
Wählen Sie im Assistenten zum Installieren von SQL Server „Database Engine Services“, „Integration Services“, „Scale Out-Master“ und „Scale Out-Worker“ auf der Seite **Funktionsauswahl** aus.

![Funktionsauswahl „Onebox 1“](media/feature-select-onebox1.PNG)

![Funktionsauswahl „Onebox 2“](media/feature-select-onebox2.PNG)

Klicken Sie auf der Seite **Server-Konfiguration** einfach auf „Weiter“, um Standarddienstkonten und -starttypen zu verwenden.

Wählen Sie auf der Seite **Datenbankmodulkonfiguration** **gemischter Modus** aus, und klicken Sie auf die Schaltfläche **Aktuellen Benutzer hinzufügen**. 

![Modulkonfiguration](media/engine-config.PNG)

Klicken Sie auf den Seiten **Integration Services Scale Out-Konfiguration – Masterknoten** und **Integration Services Scale Out-Konfiguration – Workerknoten** einfach auf „Weiter“, um die Standardeinstellungen des Ports und der Zertifikate anzuwenden.

Stellen Sie den Assistenten zum Installieren von SQL Server fertig.

## <a name="2-install-sql-server-management-studio"></a>2. Installieren von SQL Server Management Studio

[Laden](../../ssms/download-sql-server-management-studio-ssms.md) Sie SQL Server Management Studio herunter, und führen Sie eine Installation durch.

## <a name="3-enable-scale-out"></a>3. Aktivieren von Scale Out
Öffnen Sie SSMS, und stellen Sie eine Verbindung mit einer lokalen SQL Server-Instanz her.
Klicken Sie im Objekt-Explorer auf **Integration Services-Kataloge**, und wählen Sie **Katalog erstellen** aus.

Im Dialogfeld **Katalog erstellen** ist standardmäßig die Option **Diesen Server als SSIS Scale Out-Master aktivieren** ausgewählt. Erstellen Sie den Katalog einfach wie gewohnt. 

## <a name="4-enable-scale-out-worker"></a>4. Aktivieren des Scale Out-Workers
Klicken Sie in SSMS auf **SSISDB**, und wählen Sie **Manage Scale Out...** (Scale Out Verwalten...) aus. ![Scale Out verwalten](media/manage-scale-out.PNG)

Der Integration Services Scale Out-Manager wird angezeigt. Mithilfe dieses Managers können Sie Scale Out verwalten. Weitere Informationen finden Sie unter [Integration Services Scale Out Manager (Integration Services Scale Out-Manager)](integration-services-ssis-scale-out-manager.md).

Wechseln Sie zu **Worker-Manager**, und wählen Sie den gewünschten Worker aus, um den Scale Out-Worker zu aktivieren. Standardmäßig ist der Worker deaktiviert. Klicken Sie zur Aktivierung auf **Worker aktivieren**.

## <a name="5-run-packages-in-scale-out"></a>5. Ausführen von Paketen in horizontaler Hochskalierung
Jetzt können Sie SSIS-Pakete in Scale Out ausführen. Vgl. [Run Packages in Integration Services (SSIS) Scale Out (Ausführen von Paketen Integration Services (SSIS) Scale Out)](run-packages-in-integration-services-ssis-scale-out.md).


Informationen zum Hinzufügen von weiteren Scale Out-Workers finden Sie unter [Add a Scale Out Worker with Scale Out Manager (Hinzufügen eines Scale Out-Workers mit dem Scale Out-Manager)](add-scale-out-worker.md).
