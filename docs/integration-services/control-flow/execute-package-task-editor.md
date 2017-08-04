---
title: "Editor für den Task Paket ausführen | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.executepackagetask.package.f1
- sql13.dts.designer.executepackagetask.parameter.F1
- sql13.dts.designer.executepackagetask.general.f1
ms.assetid: c2c96b4f-eb10-4d8b-be34-88edfd0785fb
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a2e3655bedbb24f2174a62c8792cd168e7642592
ms.openlocfilehash: 6f03d1bb15f1513a7683c6719c42e9cd7f440a71
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="execute-package-task-editor"></a>Editor für den Task 'Paket ausführen'
  Mit dem Editor für den Task "Paket ausführen" können Sie Task "Paket ausführen" konfigurieren. Der Task Paket ausführen erweitert die Unternehmensfunktionen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , indem Paketen das Ausführen anderer Pakete als Teil eines Workflows ermöglicht wird.  
  
 **Was möchten Sie tun?**  
  
-   [Öffnen des Editors für den Task "Paket ausführen"](#open)  
  
-   [Festlegen der Optionen auf der Seite „Allgemein“](#general)  
  
-   [Festlegen der Optionen auf der Seite "Paket"](#package)  
  
-   [Festlegen der Optionen auf der Seite "Parameterbindungen"](#parameter)  
  
##  <a name="open"></a> Öffnen des Editors für den Task "Paket ausführen"  
  
1.  Öffnen Sie in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ein [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] -Projekt, das einen Task „Paket ausführen“ enthält.  
  
2.  Klicken Sie im SSIS-Designer mit der rechten Maustaste auf den Task, und klicken Sie dann auf **Bearbeiten**.  
  
##  <a name="general"></a> Festlegen der Optionen auf der Seite „Allgemein“  
 **Name**  
 Geben Sie einen eindeutigen Namen für den Task "Paket ausführen" an. Dieser Name wird im Tasksymbol als Bezeichnung verwendet.  
  
> [!NOTE]  
>  Tasknamen müssen innerhalb eines Pakets eindeutig sein.  
  
 **Description**  
 Geben Sie eine Beschreibung des Tasks "Paket ausführen" ein.  
  
##  <a name="package"></a> Festlegen der Optionen auf der Seite "Paket"  
 **ReferenceType**  
 Wählen Sie **Projektverweis** für untergeordnete Pakete im Projekt aus. Wählen Sie **Externer Verweis** für untergeordnete Pakete aus, die sich außerhalb des Pakets befinden.  
  
> [!NOTE]  
>  Die Option **ReferenceType** ist schreibgeschützt und auf **Externer Verweis** festgelegt, wenn das Projekt, das das Paket enthält, nicht in das Projektbereitstellungsmodell konvertiert wurde. [Bereitstellen von Integrationsservices (SSIS)-Projekten und Paketen](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 **Kennwort**  
 Wenn das untergeordnete Paket kennwortgeschützt ist, stellen Sie das Kennwort für das untergeordnete Paket bereit, oder klicken Sie auf die Schaltfläche mit den drei Punkten (...), und erstellen Sie ein neues Kennwort für das untergeordnete Paket.  
  
 **ExecuteOutOfProcess**  
 Geben Sie an, ob das untergeordnete Paket im Prozess des übergeordneten Pakets oder in einem separaten Prozess ausgeführt wird. Die ExecuteOutOfProcess-Eigenschaft des Tasks „Paket ausführen“ ist standardmäßig auf **FALSE**festgelegt, und das untergeordnete Paket wird im selben Prozess wie das übergeordnete Paket ausgeführt. Wenn Sie diese Eigenschaft auf **TRUE**festlegen, wird das untergeordnete Paket in einem separaten Prozess ausgeführt. Dadurch kann sich der Start des untergeordneten Pakets verlangsamen. Wenn die Eigenschaft auf **TRUE**festgelegt wurde, ist außerdem das Debuggen des Pakets in einer Installation, die nur die Tools enthält, nicht möglich. Das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Produkt muss von Ihnen installiert werden. Weitere Informationen finden Sie unter [Installieren von Integration Services](../../integration-services/install-windows/install-integration-services.md).  
  
### <a name="referencetype-dynamic-options"></a>Dynamische Optionen für ReferenceType  
  
#### <a name="referencetype--external-reference"></a>ReferenceType = Externer Verweis  
 **Speicherort**  
 Wählen Sie den Speicherort des untergeordneten Pakets aus. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**SQL Server**|Legt den Speicherort als Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]fest.|  
|**File system**|Legen Sie als Speicherort das Dateisystem fest.|  
  
 **Verbindung**  
 Wählen Sie den Typ des Speicherorts für das untergeordnete Paket aus.  
  
 **PackageNameReadOnly**  
 Zeigt den Paketnamen an.  
  
#### <a name="referencetype--project-reference"></a>ReferenceType = Projektverweis  
 **PackageNameFromProjectReference**  
 Wählen Sie ein im Projekt enthaltenes Paket als untergeordnetes Paket aus.  
  
### <a name="location-dynamic-options"></a>Dynamische Optionen für Location  
  
#### <a name="location--sql-server"></a>Location = SQL Server  
 **Verbindung**  
 Wählen Sie einen OLE DB-Verbindungs-Manager in der Liste aus, oder klicken Sie auf \< **neue Verbindung...** > um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [OLE DB-Verbindungs-Manager](../../integration-services/connection-manager/ole-db-connection-manager.md), [OLE DB-Verbindungs-Manager konfigurieren](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)  
  
 **PackageName**  
 Geben Sie den Namen des untergeordneten Pakets an, oder klicken Sie auf die Schaltfläche mit den drei Punkten, um nach dem Paket zu suchen.  
  
#### <a name="location--file-system"></a>Location = File system  
 **Verbindung**  
 Wählen Sie einen Dateiverbindungs-Manager in der Liste aus, oder klicken Sie auf \< **neue Verbindung...** > um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **PackageNameReadOnly**  
 Zeigt den Paketnamen an.  
  
##  <a name="parameter"></a> Festlegen der Optionen auf der Seite "Parameterbindungen"  
 Sie können Werte aus dem übergeordneten Paket oder dem Projekt an das untergeordnete Paket übergeben. Das Projekt muss das Projektbereitstellungsmodell verwenden, und das untergeordnete Paket muss im gleichen Projekt enthalten sein wie das übergeordnete Paket.  
  
 Informationen zum Konvertieren von Projekten in das projektbereitstellungsmodell finden Sie unter [Bereitstellen von Integration Services (SSIS)-Projekten und Paketen](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 **Untergeordneter Paketparameter**  
 Geben Sie einen Namen für den untergeordneten Paketparameter ein, oder wählen Sie diesen aus.  
  
 **Bindungsparameter oder Variable**  
 Wählen Sie den Parameter oder die Variable mit dem Wert aus, den Sie an das untergeordnete Paket übergeben möchten.  
  
 **Hinzufügen**  
 Klicken Sie, um einen Parameter oder eine Variable einem untergeordneten Paketparameter zuzuordnen.  
  
 **Entfernen**  
 Klicken Sie, um eine Zuordnung zwischen einem Parameter oder einer Variable und einem untergeordneten Paketparameter zu entfernen.  
  
  
