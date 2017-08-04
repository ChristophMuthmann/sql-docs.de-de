---
title: Herstellen einer Verbindung mit einer Excel-Arbeitsmappe | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
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
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b36b92c9beb840f6a2ea66250a5a025aa587acef
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-an-excel-workbook"></a>Herstellen einer Verbindung mit einer Excel-Arbeitsmappe
  Um ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket mit einer Microsoft Office Excel-Arbeitsmappe zu verbinden, ist ein Excel-Verbindungs-Manager erforderlich.  
  
 Sie können diese Verbindungs-Manager entweder im Bereich "Verbindungs-Manager" im [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer oder im Import/Export-Assistenten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellen.  
  
 **Anbieter und Treiber für Microsoft Excel- und Access-Dateien**  
  
 Möglicherweise müssen Sie die OLE DB-Anbieter und -Treiber für Microsoft Office-Dateien herunterladen, sofern diese nicht bereits installiert sind. Spätere Versionen des Anbieters dienen zum Öffnen von Dateien, die in früheren Versionen von Excel erstellt wurden.  
  
 Wenn der Computer über eine 32-Bit-Version von Office verfügt, müssen Sie die 32-Bit-Version der Treiber installieren. Sie müssen zudem sicherstellen, dass Sie den Assistenten oder das Integration Services-Paket ausführen, das den Treiber im 32-Bit-Modus erstellt.  
  
|Microsoft Office-Version|Herunterladen|  
|------------------------------|--------------|  
|2007|[2007 Office System-Treiber: Datenkonnektivitätskomponenten](https://www.microsoft.com/en-us/download/details.aspx?id=23734)|  
|2010|[Microsoft Access 2010 Runtime](https://www.microsoft.com/en-us/download/details.aspx?id=10910)|  
|2013|[Microsoft Access 2013 Runtime](http://www.microsoft.com/en-us/download/details.aspx?id=39358)|  
  
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
  
  
