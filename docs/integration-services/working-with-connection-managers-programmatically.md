---
title: Programmgesteuertes Arbeiten mit Verbindungs-Manager | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- connection managers [Integration Services], programming
ms.assetid: 2686fe84-1ecc-48b8-9160-e7122274bd84
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9093b9eadce231aea248cd04c2b57dc5dd5e1a76
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="working-with-connection-managers-programmatically"></a>Programmgesteuertes Arbeiten mit Verbindungs-Managern
  In [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], die AcquireConnection-Methode der zugeordneten Verbindungs-Manager-Klasse ist die Methode, die am häufigsten bei der Arbeit mit Verbindungs-Managern in verwaltetem Code aufgerufen. Wenn Sie verwalteten Code schreiben, müssen Sie die AcquireConnection-Methode zur Verwendung der Funktionen einer Verbindung-Manager aufrufen. Sie müssen diese Methode unabhängig davon, ob Sie einen verwalteten Code in einem Skripttask, einer Skriptkomponente, einem benutzerdefinierten Objekt oder einer benutzerdefinierten Anwendung schreiben, aufrufen.  
  
 Zum erfolgreichen Aufrufen die AcquireConnection-Methode müssen Sie die folgenden Fragen beantworten:  
  
-   **Welche Verbindungs-Manager von der AcquireConnection-Methode ein verwaltetes Objekt zurückgeben?**  
  
     Viele Verbindungs-Manager zurück, dass nicht verwaltete COM-Objekte (__ComObject) und diese Objekte einfach aus verwaltetem Code verwendet werden können. Zu diesen Verbindungs-Managern gehört der häufig verwendete OLE DB-Verbindungs-Manager.  
  
-   **Für den Verbindungs-Managern, die ein verwaltetes Objekt zurückgeben, führen Sie welche Objekte die AcquireConnection-Methoden zurückgeben?**  
  
     Um den Rückgabewert in den entsprechenden Typ umwandeln möchten, müssen Sie den Typ des Objekts kennen, die die AcquireConnection-Methode zurückgegeben. Z. B. der AcquireConnection-Methode für die [!INCLUDE[vstecado](../includes/vstecado-md.md)] Verbindungs-Manager gibt ein offenen SqlConnection-Objekt zurück, bei der Verwendung des SqlClient-Anbieters. Die AcquireConnection-Methode für den Dateiverbindungs-Manager gibt jedoch nur eine Zeichenfolge zurück.  
  
 In diesem Thema werden diese Fragen für die in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] enthaltenen Verbindungs-Manager beantwortet.  
  
## <a name="connection-managers-that-do-not-return-a-managed-object"></a>Verbindungs-Manager, die kein verwaltetes Objekt zurückgeben  
 Die folgende Tabelle enthält die Verbindungs-Manager, die ein systemeigenes COM-Objekt (__ComObject) von der AcquireConnection-Methode zurückgegeben. Diese nicht verwalteten Objekte können nicht ohne Weiteres in verwaltetem Code verwendet werden.  
  
|Typ des Verbindungs-Managers|Name des Verbindungs-Manager|  
|-----------------------------|-----------------------------|  
|ADO|ADO-Verbindungs-Manager|  
|MSOLAP90|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]Verbindungs-Manager|  
|EXCEL|Excel-Verbindungs-Manager|  
|FTP|FTP-Verbindungs-Manager|  
|HTTP|HTTP-Verbindungs-Manager|  
|ODBC|ODBC-Verbindungs-Manager|  
|OLEDB|OLE DB-Verbindungs-Manager|  
  
 In der Regel können Sie eine [!INCLUDE[vstecado](../includes/vstecado-md.md)] Verbindungs-Manager aus verwaltetem Code zum Herstellen einer ADO, Excel, ODBC oder OLE DB-Datenquelle.  
  
## <a name="return-values-from-the-acquireconnection-method"></a>Rückgabewerte von der AcquireConnection-Methode  
 Die folgende Tabelle enthält die Verbindungs-Manager, die ein verwaltetes Objekt von der AcquireConnection-Methode zurückgegeben. Diese verwalteten Objekte können einfach in verwaltetem Code verwendet werden.  
  
|Typ des Verbindungs-Managers|Name des Verbindungs-Manager|Typ des Rückgabewerts|Zusätzliche Informationen|  
|-----------------------------|-----------------------------|--------------------------|----------------------------|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|[!INCLUDE[vstecado](../includes/vstecado-md.md)]Verbindungs-Manager|**System.Data.SqlClient.SqlConnection**||  
|FILE|Dateiverbindungs-Manager|**System.String**|Pfad zur Datei.|  
|FLATFILE|Verbindungs-Manager für Flatfiles|**System.String**|Pfad zur Datei.|  
|MSMQ|MSMQ-Verbindungs-Manager|**System.Messaging.MessageQueue**||  
|MULTIFILE|Verbindungs-Manager für mehrere Dateien|**System.String**|Pfad zu einer der Dateien.|  
|MULTIFLATFILE|Verbindungs-Manager für mehrere Flatfiles|**System.String**|Pfad zu einer der Dateien.|  
|SMOServer|SMO-Verbindungs-Manager|**Microsoft.SqlServer.Management.Smo.Server**||  
|SMTP|SMTP-Verbindungs-Manager|**System.String**|Beispiel: `SmtpServer=<server name>;UseWindowsAuthentication=True;EnableSsl=False;`|  
|WMI|WMI-Verbindungs-Manager|**System.Management.ManagementScope**||  
|SQLMOBILE|SQL Server Compact Verbindungs-Manager|**Dokumentaiton zur System.Data.SqlServerCe.SqlCeConnection**||  
  
## <a name="see-also"></a>Siehe auch  
 [Connecting to Data Sources in the Script Task](../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)   
 [Herstellen einer Verbindung mit Datenquellen in der Skriptkomponente](../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)   
 [Herstellen einer Verbindung mit Datenquellen in einem benutzerdefinierten Task](../integration-services/extending-packages-custom-objects/task/connecting-to-data-sources-in-a-custom-task.md)  
  
  
