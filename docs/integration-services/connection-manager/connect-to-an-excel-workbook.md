---
title: Herstellen einer Verbindung mit einer Excel-Arbeitsmappe | Microsoft-Dokumentation
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Excel [Integration Services]
ms.assetid: d9746318-3669-4ce2-bbb0-4a1bd471c9dd
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3ece6c4ef032f7b60f82f3f58ee602d0a4ac1196
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="connect-to-an-excel-workbook"></a>Herstellen einer Verbindung mit einer Excel-Arbeitsmappe
  Um ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket mit einer Microsoft Office Excel-Arbeitsmappe zu verbinden, ist ein Excel-Verbindungs-Manager erforderlich.  
  
 Sie können diese Verbindungs-Manager entweder im Bereich "Verbindungs-Manager" im [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer oder im Import/Export-Assistenten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellen.  
 
## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Konnektivitätskomponenten für Microsoft Excel- und Access-Dateien
  
Sie müssen möglicherweise die Konnektivitätskomponenten für Microsoft Office-Dateien herunterladen, wenn diese nicht bereits installiert sind. Laden Sie die neueste Version der Konnektivitätskomponenten für Excel- und Access-Dateien hier herunter: [Microsoft Access Database Engine 2016 Redistributable](https://www.microsoft.com/download/details.aspx?id=54920).
  
Die aktuelle Version der Komponenten dient zum Öffnen von Dateien, die in früheren Versionen von Excel erstellt wurden.

Wenn der Computer über eine 32-Bit-Version von Office verfügt, müssen Sie die 32-Bit-Version der Komponenten installieren. Sie müssen zudem sicherstellen, dass Sie das Paket im 32-Bit-Modus ausführen.

Wenn Sie über ein Office 365-Abonnement verfügen, stellen Sie sicher, dass Sie die weitervertreibbare Komponente von Access Database Engine 2016 und nicht Microsoft Access 2016 Runtime herunterladen. Wenn Sie das Installationsprogramm ausführen, wird vielleicht eine Fehlermeldung angezeigt, dass Sie den Download nicht parallel mit Klick-und-Los-Komponenten von Office installieren können. Um diese Fehlermeldung zu umgehen und die Komponenten erfolgreich zu installieren, führen Sie die Installation im stillen Modus durch, indem Sie ein Eingabeaufforderungsfenster öffnen und die EXE-Datei, die Sie heruntergeladen haben, mit der Befehlszeilenoption `/quiet` ausführen. Zum Beispiel:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="create-an-excel-connection-manager"></a>Erstellen eines Excel-Verbindungs-Managers

### <a name="to-create-an-excel-connection-manager-from-the-connection-managers-area"></a>So erstellen Sie einen Excel-Verbindungs-Manager im Bereich "Verbindungs-Manager"  
  
1.  Öffnen Sie das Paket in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Klicken Sie mit der rechten Maustaste auf eine beliebige Stelle im Bereich **Verbindungs-Manager** , und klicken Sie dann auf **Neue Verbindung**.  
  
3.  Wählen Sie im Dialogfeld **SSIS-Verbindungs-Manager hinzufügen** die Option **Excel**aus, und konfigurieren Sie anschließend den Verbindungs-Manager.  
  
     Weitere Informationen zu den für diesen Verbindungs-Manager verfügbaren Konfigurationsoptionen finden Sie unter [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
### <a name="to-create-an-excel-connection-from-the-sql-server-import-and-export-wizard"></a>So erstellen Sie eine Excel-Verbindung mit dem SQL Server-Import/Export-Assistenten  
  
1.  Starten Sie die 32-Bit-Version des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistenten.  
  
2.  Wählen Sie auf der Seite **Datenquelle auswählen** für **Datenquelle**die Option **Microsoft Excel**aus, und konfigurieren Sie anschließend die Excel-Verbindung.  
  
     Weitere Informationen zu den für diesen Verbindungstyp verfügbaren Konfigurationsoptionen finden Sie unter [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Herstellen einer Verbindung zu einer Access-Datenbank](../../integration-services/connection-manager/connect-to-an-access-database.md)  
  
  
