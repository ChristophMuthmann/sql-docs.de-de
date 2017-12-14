---
title: WMI-Verbindungs-Manager | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.designer.wmiconnection.f1
helpviewer_keywords:
- connections [Integration Services], WMI
- connection managers [Integration Services], WMI
- WMI connection manager [Integration Services]
ms.assetid: fbfa4ba7-3d0d-4d6b-94ad-50741a88d03d
caps.latest.revision: "39"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a3043e761402ae70369990d281bedede9c7bc39b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="wmi-connection-manager"></a>WMI-Verbindungs-Manager
  Mit einem WMI-Verbindungs-Manager kann ein Paket mithilfe der Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) Informationen in einer Unternehmensumgebung verwalten. Der Task Webdienst von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwendet einen WMI-Verbindungs-Manager.  
  
 Wenn Sie einem Paket einen WMI-Verbindungs-Manager hinzufügen, erstellt [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einen Verbindungs-Manager, der zur Laufzeit in eine WMI-Verbindung aufgelöst wird, die Eigenschaften des Verbindungs-Managers festlegt und der **Connections** -Sammlung im Paket den Verbindungs-Manager hinzufügt. Die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers ist auf **WMI**festgelegt.  
  
## <a name="configuration-of-the-wmi-connection-manager"></a>Konfiguration des WMI-Verbindungs-Managers  
 Es gibt folgende Möglichkeiten, um einen WMI-Verbindungs-Manager zu konfigurieren:  
  
-   Geben Sie den Namen eines Servers an.  
  
-   Geben Sie einen Namespace auf dem Server an.  
  
-   Wählen Sie den Authentifizierungsmodus zum Herstellen einer Verbindung mit dem Server aus.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können, finden Sie unter [WMI-Verbindungs-Manager-Editor](../../integration-services/connection-manager/wmi-connection-manager-editor.md).  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> und [Programmgesteuertes Hinzufügen von Verbindungen](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)festgelegt.  
  
## <a name="wmi-connection-manager-editor"></a>WMI-Verbindungs-Manager-Editor
  Mithilfe des Dialogfelds **WMI-Verbindungs-Manager** geben Sie eine WMI-Verbindung (Microsoft Windows Management Instrumentation) mit einem Server an.  
  
 Weitere Informationen zum WMI-Verbindungs-Manager finden Sie unter [WMI Connection Manager](../../integration-services/connection-manager/wmi-connection-manager.md).  
  
### <a name="options"></a>enthalten  
 **Name**  
 Geben Sie einen eindeutigen Namen für den Verbindungs-Manager an.  
  
 **Description**  
 Beschreiben Sie den Verbindungs-Manager. Die bewährte Methode ist hierbei, den Verbindungs-Manager zweckbezogen zu beschreiben, sodass Pakete selbsterklärend und leichter zu verwalten sind.  
  
 **Servername**  
 Geben Sie den Namen des Servers an, zu dem die WMI-Verbindung hergestellt werden soll.  
  
 **Namespace**  
 Geben Sie den WMI-Namespace an.  
  
 **Windows-Authentifizierung verwenden**  
 Wählen Sie diese Option aus, wenn Windows-Authentifizierung verwendet werden soll. Wenn Sie Windows-Authentifizierung verwenden, müssen Sie keinen Benutzernamen und kein Kennwort für die Verbindung angeben.  
  
 **Benutzername**  
 Wenn Sie Windows-Authentifizierung nicht verwenden, müssen Sie für die Verbindung einen Benutzernamen angeben.  
  
 **Kennwort**  
 Wenn Sie Windows-Authentifizierung nicht verwenden, müssen Sie für die Verbindung das Kennwort angeben.  
  
 **Test**  
 Testen Sie die Verbindungs-Manager-Einstellungen.  
  
## <a name="see-also"></a>Siehe auch  
 [Webdienst (Task)](../../integration-services/control-flow/web-service-task.md)   
 [Integration Services-Verbindungen &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
