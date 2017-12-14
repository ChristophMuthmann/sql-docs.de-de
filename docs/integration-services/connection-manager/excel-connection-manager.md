---
title: Excel-Verbindungs-Manager | Microsoft-Dokumentation
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.designer.excelconnection.f1
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
caps.latest.revision: "41"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5785a2753b61cde59a5ed157d697b05a93796fc7
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="excel-connection-manager"></a>Excel-Verbindungs-Manager
  Mit einem Excel-Verbindungs-Manager kann ein Paket eine Verbindung mit einer vorhandenen [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel-Arbeitsmappendatei herstellen. Die Excel-Quelle und das Excel-Ziel von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwenden den Excel-Verbindungs-Manager.  
  
 Wenn Sie einem Paket einen Excel-Verbindungs-Manager hinzufügen, erstellt [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einen Verbindungs-Manager, der zur Laufzeit als Excel-Verbindung aufgelöst wird, die Eigenschaften des Verbindungs-Managers festlegt und der Sammlung **Verbindungen** im Paket den Verbindungs-Manager hinzufügt.  
  
 Die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers ist auf **EXCEL**festgelegt.  
  
## <a name="configuration-of-the-excel-connection-manager"></a>Konfiguration des Excel-Verbindungs-Managers  
 Es gibt folgende Möglichkeiten, um den Excel-Verbindungs-Manager zu konfigurieren:  
  
-   Geben Sie den Pfad der Excel-Arbeitsmappendatei an.  
  
    > [!NOTE]  
    >  Es ist nicht möglich, eine Verbindung mit einer kennwortgeschützten Excel-Datei herzustellen.  
  
-   Geben Sie die Excel-Version an, die zum Erstellen der Datei verwendet wurde.  
  
-   Zeigen Sie an, ob die erste Zeile der abgerufenen Daten in den ausgewählten Arbeitsmappen oder Bereichen Spaltennamen enthält.  
  
 Wenn der Excel-Verbindungs-Manager von einer Excel-Quelle verwendet wird, sind die Spaltennamen in den extrahierten Daten enthalten. Wird dieser von einem Excel-Ziel verwendet, sind die Spaltennamen in den geschriebenen Daten enthalten.  
  
 Weitere Informationen zum Verhalten von Excel-Quellen und Excel-Zielen finden Sie unter [Excel Source](../../integration-services/data-flow/excel-source.md) und [Excel Destination](../../integration-services/data-flow/excel-destination.md).  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können, finden Sie unter [Verbindungs-Manager-Editor für Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> und [Programmgesteuertes Hinzufügen von Verbindungen](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)festgelegt.  
  
 Informationen zum Durchlaufen einer Gruppe von Excel-Dateien finden Sie unter [Schleife durch Excel-Dateien und Tabellen mit einem Foreach-Schleifencontainer](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md).  
  
## <a name="excel-connection-manager-editor"></a>Verbindungs-Manager-Editor für Excel
  Mithilfe des Dialogfelds **Verbindungs-Manager-Editor für Excel** können Sie einer vorhandenen oder neuen [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] -Arbeitsmappendatei eine Verbindung hinzufügen.  
  
 Weitere Informationen zum Excel-Verbindungs-Manager finden Sie unter [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md).  
  
### <a name="options"></a>enthalten  
 **Excel-Dateipfad**  
 Geben Sie den Pfad und den Dateinamen einer vorhandenen oder neuen Excel-Arbeitsmappendatei (XLS-Datei) ein.  
  
> [!NOTE]  
>  Es ist nicht möglich, eine Verbindung mit einer kennwortgeschützten Excel-Datei herzustellen.  
  
> [!WARNING]  
>  Der **Ziel-Editor für Excel** erstellt die Excel-Datei automatisch, wenn Sie eine **Excel-Verbindung** auswählen, die zu einer neuen oder nicht vorhandenen Datei zeigt, und dann auf **Neu** für **Name der Excel-Tabelle**klicken.  
  
 **Durchsuchen**  
 Verwenden Sie das Dialogfeld **Öffnen** , um zum Ordner zu navigieren, in dem die Excel-Datei enthalten ist bzw. in dem Sie die neue Datei erstellen möchten.  
  
 **Excel-Version**  
 Geben Sie die Version von Microsoft Excel an, die zum Erstellen der Datei verwendet wurde.  
  
 **Erste Zeile enthält Spaltennamen**  
 Geben Sie an, ob die erste Zeile der Daten in der ausgewählten Arbeitsmappe Spaltennamen enthält. Der Standardwert für diese Option ist **True**.  
  
## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Konnektivitätskomponenten für Microsoft Excel- und Access-Dateien
  
Sie müssen möglicherweise die Konnektivitätskomponenten für Microsoft Office-Dateien herunterladen, wenn diese nicht bereits installiert sind. Laden Sie die neueste Version der Konnektivitätskomponenten für Excel- und Access-Dateien hier herunter: [Microsoft Access Database Engine 2016 Redistributable](https://www.microsoft.com/download/details.aspx?id=54920).
  
Die aktuelle Version der Komponenten dient zum Öffnen von Dateien, die in früheren Versionen von Excel erstellt wurden.

Wenn der Computer über eine 32-Bit-Version von Office verfügt, müssen Sie die 32-Bit-Version der Komponenten installieren. Sie müssen zudem sicherstellen, dass Sie das Paket im 32-Bit-Modus ausführen.

Wenn Sie über ein Office 365-Abonnement verfügen, stellen Sie sicher, dass Sie die Access Database Engine 2016 Redistributable und nicht die Microsoft Access 2016 Runtime herunterladen. Wenn Sie das Installationsprogramm ausführen, wird vielleicht eine Fehlermeldung angezeigt, dass Sie den Download nicht parallel mit Klick-und-Los-Komponenten von Office installieren können. Um diese Fehlermeldung zu umgehen, führen Sie die Installation im stillen Modus durch, indem Sie ein Eingabeaufforderungsfenster öffnen und die EXE-Datei, die Sie heruntergeladen haben, mit der Befehlszeilenoption `/quiet` ausführen. Beispiel:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
-   [Schleife durch Excel-Dateien und Tabellen mit einem Foreach-Schleifencontainer](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
-   [Herstellen einer Verbindung mit einer Excel-Arbeitsmappe](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
  
