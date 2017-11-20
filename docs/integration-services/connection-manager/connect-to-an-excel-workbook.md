---
title: Herstellen einer Verbindung mit einer Excel-Arbeitsmappe | Microsoft Docs
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
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2800075091835b2d6f2b07ee34e9b897fe86634e
ms.openlocfilehash: f8fb1db80ac1b750950a3401516b54af5ee29686
ms.contentlocale: de-de
ms.lasthandoff: 08/17/2017

---
# <a name="connect-to-an-excel-workbook"></a>Herstellen einer Verbindung mit einer Excel-Arbeitsmappe
  Um ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket mit einer Microsoft Office Excel-Arbeitsmappe zu verbinden, ist ein Excel-Verbindungs-Manager erforderlich.  
  
 Sie können diese Verbindungs-Manager entweder im Bereich "Verbindungs-Manager" im [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer oder im Import/Export-Assistenten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellen.  
 
## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Konnektivitätskomponenten für Microsoft Excel- und Access-Dateien
  
Sie müssen möglicherweise die Konnektivitätskomponenten für Microsoft Office-Dateien herunterladen, sofern diese nicht bereits installiert sind. Die neueste Version der datenkonnektivitätskomponenten für Excel- und Access-Dateien hier herunterladen: [Microsoft Access Database Engine 2016 Redistributable](https://www.microsoft.com/download/details.aspx?id=54920).
  
Die neueste Version der Komponenten kann von früheren Versionen von Excel erstellte Dateien öffnen.

Verfügt der Computer eine 32-Bit-Version von Office, dann müssen Sie die 32-Bit-Version der Komponenten zu installieren, und außerdem müssen Sie sicherstellen, dass Sie das Paket im 32-Bit-Modus ausführen.

Wenn Sie ein Office 365-Abonnement verfügen, stellen Sie sicher, dass Sie Access-Datenbank-Engine 2016 Redistributable und nicht die Microsoft Access 2016 Runtime herunterladen. Wenn Sie das Installationsprogramm ausführen, sehen Sie eine Fehlermeldung angezeigt, dass Sie die Download-Seite-an-Seite mit den Office-Klick-und-Los-Komponenten installieren können. Um diese Fehlermeldung umgehen und die Komponenten erfolgreich installiert haben, führen Sie die Installation im stillen Modus, indem Sie ein Eingabeaufforderungsfenster öffnen und Ausführen der. EXE-Datei, die Sie heruntergeladen, mit der `/quiet` wechseln. Beispiel:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="create-an-excel-connection-manager"></a>Erstellen Sie eine Excel-Verbindungs-manager

### <a name="to-create-an-excel-connection-manager-from-the-connection-managers-area"></a>So erstellen Sie einen Excel-Verbindungs-Manager im Bereich "Verbindungs-Manager"  
  
1.  Öffnen Sie das Paket in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Klicken Sie mit der rechten Maustaste auf eine beliebige Stelle im Bereich **Verbindungs-Manager** , und klicken Sie dann auf **Neue Verbindung**.  
  
3.  Wählen Sie im Dialogfeld **SSIS-Verbindungs-Manager hinzufügen** die Option **Excel**aus, und konfigurieren Sie anschließend den Verbindungs-Manager.  
  
     Weitere Informationen zu den für diesen Verbindungs-Manager verfügbaren Konfigurationsoptionen finden Sie unter [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
### <a name="to-create-an-excel-connection-from-the-sql-server-import-and-export-wizard"></a>So erstellen Sie eine Excel-Verbindung mit dem SQL Server-Import/Export-Assistenten  
  
1.  Starten Sie die 32-Bit-Version des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistenten.  
  
2.  Wählen Sie auf der Seite **Datenquelle auswählen** für **Datenquelle**die Option **Microsoft Excel**aus, und konfigurieren Sie anschließend die Excel-Verbindung.  
  
     Weitere Informationen zu den für diesen Verbindungstyp verfügbaren Konfigurationsoptionen finden Sie unter [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Herstellen einer Verbindung zu einer Access-Datenbank](../../integration-services/connection-manager/connect-to-an-access-database.md)  
  
  

