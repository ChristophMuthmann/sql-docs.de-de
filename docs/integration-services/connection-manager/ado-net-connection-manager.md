---
title: ADO.NET-Verbindungs-Manager | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection managers [Integration Services], ADO.NET
- ADO.NET connection manager [Integration Services]
- connections [Integration Services], ADO.NET
ms.assetid: fc5daa2f-0159-4bda-9402-c87f1035a96f
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 41363d15ebb18431c658c4f990d10a1fa67260ae
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="adonet-connection-manager"></a>ADO.NET-Verbindungs-Manager
  Ein [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager ermöglicht einem Paket den Zugriff auf Datenquellen mithilfe eines .NET-Anbieters. Dieser Verbindungs-Manager dient in der Regel für den Zugriff auf Datenquellen, z.B. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sowie Datenquellen, die durch OLE DB und XML in benutzerdefinierten Tasks verfügbar gemacht werden, die mit einer Programmiersprache wie C# in verwaltetem Code geschrieben sind.  
  
 Wenn Sie einem Paket einen [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager hinzufügen, erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einen Verbindungs-Manager, der zur Laufzeit als [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindung aufgelöst wird, die Eigenschaften des Verbindungs-Managers festlegt und der **Connections** -Sammlung im Paket den Verbindungs-Manager hinzufügt.  
  
 Die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers ist auf **ADO.NET**festgelegt. Der Wert von **ConnectionManagerType** ist qualifiziert, um den Namen des .NET-Anbieters einzuschließen, der vom Verbindungs-Manager verwendet wird.  
  
## <a name="adonet-connection-manager-troubleshooting"></a>Problembehandlung des ADO.NET-Verbindungs-Managers  
 Sie können die vom [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager an externe Datenanbieter gerichteten Aufrufe protokollieren. Mithilfe dieser Protokollierungsfunktionen können Sie Probleme bei Verbindungen behandeln, die vom [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager mit externen Datenquellen hergestellt werden. Aktivieren Sie zum Protokollieren der vom [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager an externe Datenprovider gerichteten Aufrufe die Paketprotokollierung, und wählen Sie das **Diagnostic** -Ereignis auf Paketebene aus. Weitere Informationen finden Sie unter [Behandeln von Problemen mit Paketausführungstools](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
 Daten bestimmter [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Datumsdatentypen generieren beim Lesen durch einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verbindungs-Manager die in der folgenden Tabelle dargestellten Ergebnisse.  
  
|SQL Server-Datentyp|Ergebnis|  
|--------------------------|------------|  
|**time**, **datetimeoffset**|Das Paket erzeugt einen Fehler, sofern das Paket keine parametrisierten SQL-Befehle verwendet. Um parametrisierte SQL-Befehle zu verwenden, verwenden Sie den Task SQL ausführen im Paket. Weitere Informationen finden Sie unter [SQL ausführen (Task)](../../integration-services/control-flow/execute-sql-task.md) und [Parameter und Rückgabecodes im Task „SQL ausführen“](http://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663).|  
|**datetime2**|Der [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager schneidet den Millisekundenwert ab.|  
  
> [!NOTE]  
>  Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentypen sowie deren Zuordnung zu [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Datentypen finden Sie unter [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) und [SQL Server Integration Services-Datentypen](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="adonet-connection-manager-configuration"></a>Konfiguration des ADO.NET-Verbindungs-Managers  
 Es gibt folgende Möglichkeiten, um einen [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager zu konfigurieren:  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
-   Stellen Sie eine Verbindungszeichenfolge bereit, die die Anforderungen des ausgewählten .NET-Anbieters erfüllt.  
  
-   Schließen Sie in Abhängigkeit vom Anbieter den Namen der Datenquelle ein, mit der eine Verbindung hergestellt werden soll.  
  
-   Stellen Sie entsprechende Sicherheitsanmeldeinformationen für den ausgewählten Anbieter bereit.  
  
-   Geben Sie an, ob die im Verbindungs-Manager erstellte Verbindung zur Laufzeit beibehalten wird.  
  
 Viele der Konfigurationsoptionen des [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Managers hängen vom .NET-Anbieter ab, der vom Verbindungs-Manager verwendet wird.  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [ADO.NET-Verbindungs-Manager konfigurieren](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> und [Programmgesteuertes Hinzufügen von Verbindungen](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)festgelegt.  
  
## <a name="see-also"></a>Siehe auch  
 [Integration Services-Verbindungen &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
