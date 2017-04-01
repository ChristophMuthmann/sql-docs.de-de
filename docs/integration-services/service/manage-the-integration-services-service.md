---
title: "Verwalten des Integration Services-Diensts | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Integration Services-Dienst, konfigurieren"
  - "Dienste [Integration Services], konfigurieren"
ms.assetid: 45554117-a0df-4830-b41c-5ebb33b764a5
caps.latest.revision: 63
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 63
---
# Verwalten des Integration Services-Diensts
    
> **WICHTIG!** In diesem Thema wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst beschrieben, ein Windows-Dienst zur Verwaltung von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketen. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] unterstützt den Dienst für die Abwärtskompatibilität mit früheren Versionen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]können Sie Objekte, z. B. Pakete, auf dem Integration Services-Server verwalten.  
  
 Wenn Sie die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponente von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installieren, wird auch der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst installiert. Standardmäßig wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst gestartet, und der Starttyp des Dienstes ist auf automatisch festgelegt. Sie müssen jedoch auch [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] installieren, um den Dienst zur Verwaltung gespeicherter und ausgeführter [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete verwenden zu können.  
  
> **HINWEIS:** Die verwendete Version von SQL Server Management Studio (SSMS) muss mit der SQL Server-Version kompatibel sein, unter der Integration Services ausgeführt wird, damit eine direkte Verbindung zu einer Instanz einer älteren Version von Integration Services hergestellt werden kann. Sie benötigen z.B. die für SQL Server 2016 veröffentlichte SSMS-Version, um eine Verbindung mit der Vorgängerversion von Integration Services herzustellen, die auf einer SQL Server 2016-Instanz ausgeführt wird. [Herunterladen von SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)
>
>   Im Dialogfeld **Verbindung mit Server herstellen** in SSMS können Sie nicht den Namen eines Servers eingeben, auf dem eine ältere Version des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Diensts ausgeführt wird. Sie müssen jedoch zum Verwalten von Paketen auf einem Remoteserver keine Verbindung mit der Instanz des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Diensts auf dem betreffenden Remoteserver herstellen. Bearbeiten Sie stattdessen die Konfigurationsdatei für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst, sodass die auf dem Remoteserver gespeicherten Pakete von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] angezeigt werden. Weitere Informationen finden Sie unter [Konfigurieren des Integration Services-Diensts &#40;SSIS-Dienst&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md).  
  
 Es kann nur eine einzige Instanz des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienstes auf einem Computer installiert werden. Der Dienst ist nicht spezifisch für eine bestimmte Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Sie melden sich beim Dienst mit dem Namen des Computers an, auf dem er ausgeführt wird.  
  
 Sie können den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst mithilfe eines der folgenden Snap-Ins für Microsoft Management Console (MMC) verwalten: SQL Server-Konfigurations-Manager oder -Dienste. Bevor Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Pakete verwalten können, muss der Dienst gestartet werden.  
  
 Standardmäßig wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst für die Verwaltung von Paketen in der msdb-Datenbank der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] konfiguriert, die zur selben Zeit wie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installiert wird. Wenn eine Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] nicht zur selben Zeit installiert wird, wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst so konfiguriert, dass Pakete in der msdb-Datenbank der lokalen Standardinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] verwaltet werden. Zur Verwaltung von Paketen, die in einer benannten Instanz oder einer Remoteinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]bzw. in mehreren Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)]gespeichert sind, müssen Sie die Konfigurationsdatei ändern. Weitere Informationen finden Sie unter [Konfigurieren des Integration Services-Diensts &#40;SSIS-Dienst&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md).  
  
 Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst ist standardmäßig so konfiguriert, dass ausgeführte Pakete angehalten werden, sobald der Dienst angehalten wird. Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst wartet jedoch nicht darauf, dass die Pakete angehalten werden, und einige Pakete können weiterhin ausgeführt werden, nachdem der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst angehalten wurde.  
  
 Wenn der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst angehalten wird, können Sie weiterhin Pakete mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Import/Export-Assistenten, dem [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer, dem Paketausführungsprogramm und der **dtexec**-Eingabeaufforderung (dtexec.exe) ausführen. Sie können die ausgeführten Pakete jedoch nicht überwachen.  
  
 Standardmäßig wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst im Kontext des NETWORK SERVICE-Kontos ausgeführt.  
  
 Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst schreibt in das Windows-Ereignisprotokoll. Sie können Dienstereignisse in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]anzeigen. Sie können Dienstereignisse auch mithilfe der Windows-Ereignisanzeige anzeigen.  
  
### So legen Sie die Eigenschaften des Integration Services-Dienstes mit dem Dienste-Snap-In fest  
  
-   [Festlegen der Eigenschaften des Integration Services-Diensts](../../integration-services/service/set-the-properties-of-the-integration-services-service.md)  
  
### So zeigen Sie Dienstereignisse für den Integration Services-Dienst an  
  
-   [Anzeigen von Ereignissen für den Integration Services-Dienst](../../integration-services/service/view-events-for-the-integration-services-service.md)  
  
## Siehe auch  
 [Integration Services-Dienst &#40;SSIS-Dienst&#41;](../../integration-services/service/integration-services-service-ssis-service.md)   
 [Konfigurieren des Integration Services-Diensts &#40;SSIS-Dienst&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md)   
 [SQL Server-Import/Export-Assistent](../Topic/SQL%20Server%20Import%20and%20Export%20Wizard.md)   
 [dtexec (Hilfsprogramm)](../../integration-services/packages/dtexec-utility.md)   
 [Ausführung von Projekten und Paketen](https://msdn.microsoft.com/library/ms141708(v=sql.130).aspx)  
  
  