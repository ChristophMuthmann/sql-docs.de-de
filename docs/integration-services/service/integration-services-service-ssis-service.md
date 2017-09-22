---
title: SQL Server Integration Services (SSIS-Dienst) | Microsoft Docs
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
- sql13.ssiseditserverregistration.connectionproperties.f1
- sql13.swb.connecttodts.connectionproperties.f1
- sql13.swb.connection.login.dtsserver.f1
- sql13.swb.connecttodts.login.f1
- sql13.swb.connecttodtsserver.login.f1
helpviewer_keywords:
- Integration Services service, about Integration Services service
- SQL Server Integration Services service
- service [Integration Services],about Integration Services service
- service [Integration Services]
- SQL Server Integration Services, service
ms.assetid: 2c785b3b-4a0c-4df7-b5cd-23756dc87842
caps.latest.revision: 61
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 0ec83d1e567c44abba880716bbd700af2810be60
ms.contentlocale: de-de
ms.lasthandoff: 09/21/2017

---
# <a name="integration-services-service-ssis-service"></a>Integration Services-Dienst (SSIS-Dienst)
  In den Themen in diesem Abschnitt wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst, ein Windows-Dienst zum Verwalten von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketen, erläutert. Dieser Dienst ist nicht erforderlich, um Integration Services-Pakete zu erstellen, zu speichern und auszuführen. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] unterstützt den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst für die Abwärtskompatibilität mit früheren Versionen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]speichert [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Objekte, Einstellungen und operative Daten in der **SSISDB** -Datenbank für Projekte, die mithilfe des Projektbereitstellungsmodells auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitgestellt wurden. Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server, bei dem es sich um eine Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankmoduls handelt, hostet die Datenbank. Weitere Informationen zur Verschlüsselung finden Sie unter [SSIS-Katalog](../../integration-services/service/ssis-catalog.md). Weitere Informationen zum Bereitstellen von Projekten auf die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Server, finden Sie unter [Bereitstellen von Integration Services (SSIS)-Projekten und Paketen](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
## <a name="management-capabilities"></a>Managementfunktionen  
 Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst ist ein Windows-Dienst zur Verwaltung von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketen. Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst steht nur in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]zur Verfügung.  
  
 Beim Ausführen des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienstes stehen folgende Verwaltungsfunktionen zur Verfügung:  
  
-   Starten von lokal und remote gespeicherten Paketen  
  
-   Beenden von lokal und remote ausgeführten Paketen  
  
-   Überwachen von lokal und remote ausgeführten Paketen  
  
-   Importieren und Exportieren von Paketen  
  
-   Verwalten des Paketspeichers  
  
-   Anpassen von Speicherordnern  
  
-   Beenden von ausgeführten Paketen beim Beenden des Dienstes  
  
-   Anzeigen des Windows-Ereignisprotokolls  
  
-   Herstellen von Verbindungen mit mehreren [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Servern  
  
## <a name="startup-type"></a>Starttyp
 Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst wird zusammen mit der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponente von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installiert. Standardmäßig wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst gestartet, und der Starttyp des Dienstes ist auf automatisch festgelegt. Der Dienst muss ausgeführt werden, damit die im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher gespeicherten Pakete überwacht werden. Als [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher können entweder die msdb-Datenbank einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder die dazu bestimmten Ordner des Dateisystems dienen.  
  
 Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst ist nicht erforderlich, wenn Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete lediglich entwerfen und ausführen möchten. Der Dienst ist jedoch zum Auflisten und Überwachen von Paketen in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]erforderlich.  

## <a name="manage-the-service"></a>Verwalten des Diensts
  
 Wenn Sie die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponente von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installieren, wird auch der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst installiert. Standardmäßig wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst gestartet, und der Starttyp des Dienstes ist auf automatisch festgelegt. Sie müssen jedoch auch [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] installieren, um den Dienst zur Verwaltung gespeicherter und ausgeführter [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete verwenden zu können.  
  
> [!NOTE]
> Die verwendete Version von SQL Server Management Studio (SSMS) muss mit der SQL Server-Version kompatibel sein, unter der Integration Services ausgeführt wird, damit eine direkte Verbindung zu einer Instanz einer älteren Version von Integration Services hergestellt werden kann. Sie benötigen z.B. die für SQL Server 2016 veröffentlichte SSMS-Version, um eine Verbindung mit der Vorgängerversion von Integration Services herzustellen, die auf einer SQL Server 2016-Instanz ausgeführt wird. [Herunterladen von SQL Server Management Studio (SSMS)](/sql-docs/docs/ssms/download-sql-server-management-studio-ssms)
>
>   Im Dialogfeld **Verbindung mit Server herstellen** in SSMS können Sie nicht den Namen eines Servers eingeben, auf dem eine ältere Version des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts ausgeführt wird. Sie müssen jedoch zum Verwalten von Paketen auf einem Remoteserver keine Verbindung mit der Instanz des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts auf dem betreffenden Remoteserver herstellen. Bearbeiten Sie stattdessen die Konfigurationsdatei für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst, sodass die auf dem Remoteserver gespeicherten Pakete von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] angezeigt werden.   
  
 Es kann nur eine einzige Instanz des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienstes auf einem Computer installiert werden. Der Dienst ist nicht spezifisch für eine bestimmte Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Sie melden sich beim Dienst mit dem Namen des Computers an, auf dem er ausgeführt wird.  
  
 Sie können den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst mithilfe eines der folgenden Snap-Ins für Microsoft Management Console (MMC) verwalten: SQL Server-Konfigurations-Manager oder -Dienste. Bevor Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Pakete verwalten können, muss der Dienst gestartet werden.  
  
 Standardmäßig wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst für die Verwaltung von Paketen in der msdb-Datenbank der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] konfiguriert, die zur selben Zeit wie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]installiert wird. Wenn eine Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] nicht zur selben Zeit installiert wird, wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst so konfiguriert, dass Pakete in der msdb-Datenbank der lokalen Standardinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]verwaltet werden. Zur Verwaltung von Paketen, die in einer benannten Instanz oder einer Remoteinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]bzw. in mehreren Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)]gespeichert sind, müssen Sie die Konfigurationsdatei ändern.
  
 Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst ist standardmäßig so konfiguriert, dass ausgeführte Pakete angehalten werden, sobald der Dienst angehalten wird. Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst wartet jedoch nicht darauf, dass die Pakete angehalten werden, und einige Pakete können weiterhin ausgeführt werden, nachdem der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst angehalten wurde.  
  
 Wenn der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst angehalten wird, können Sie weiterhin Pakete mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistenten, dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer, dem Paketausführungsprogramm und der **dtexec** -Eingabeaufforderung (dtexec.exe) ausführen. Sie können die ausgeführten Pakete jedoch nicht überwachen.  
  
 Standardmäßig wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst im Kontext des NETWORK SERVICE-Kontos ausgeführt.  
  
 Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst schreibt in das Windows-Ereignisprotokoll. Sie können Dienstereignisse in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]anzeigen. Sie können Dienstereignisse auch mithilfe der Windows-Ereignisanzeige anzeigen.  
  
## <a name="set-the-properties-of-the-service"></a>Legen Sie die Eigenschaften des Diensts
  
 Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst überwacht und verwaltet Pakete in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Bei der erstmaligen Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst gestartet und der Starttyp des Dienstes auf automatisch festgelegt.  
  
 Nach der Installation des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts können Sie die Eigenschaften des Dienstes entweder mit dem SQL Server-Konfigurations-Manager oder mit dem MMC-Snap-In „Dienste“ festlegen.  
  
 Zur Konfiguration anderer wichtiger Funktionen des Dienstes, wie die Verzeichnisse für die Speicherung und Verwaltung von Paketen, müssen Sie die Konfigurationsdatei des Dienstes ändern.
  
### <a name="to-set-properties-of-the-integration-services-service-by-using-sql-server-configuration-manager"></a>So legen Sie Eigenschaften des Integration Services-Dienstes mit dem SQL Server-Konfigurations-Manager fest  
  
1.  Zeigen Sie im Menü **Start** auf **Alle Programme**, **Microsoft SQL Server**, **Konfigurationstools**, und klicken Sie dann auf **SQL Server-Konfigurations-Manager**.  
  
2.  Suchen Sie im **SQL Server-Konfigurations-Manager** -Snap-In in der Diensteliste nach **SQL Server Integration Services** , klicken Sie mit der rechten Maustaste auf **SQL Server Integration Services**, und klicken Sie anschließend auf **Eigenschaften**.  
  
3.  Im Dialogfeld **Eigenschaften von SQL Server Integration Services** können Sie folgende Schritte durchführen:  
  
    -   Klicken Sie auf die Registerkarte **Anmelden** , um die Anmeldeinformationen, wie z. B. den Kontonamen, anzuzeigen.  
  
    -   Klicken Sie auf die Registerkarte **Dienst** , um Informationen zum Dienst, wie z. B. den Namen des Hostcomputers, anzuzeigen und den Startmodus des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienstes anzugeben.  
  
        > [!NOTE]  
        >  Die Registerkarte **Erweitert** enthält keine Informationen zum [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst.  
  
4.  Klicken Sie auf **OK**.  
  
5.  Klicken Sie im Menü **Datei** auf **Beenden** , um das **SQL Server-Konfigurations-Manager** -Snap-In zu schließen.  
  
### <a name="to-set-properties-of-the-integration-services-service-by-using-services"></a>So legen Sie die Eigenschaften des Integration Services-Diensts mit Diensten fest  
  
1.  Wenn Sie die klassische Ansicht verwenden, klicken Sie in der **Systemsteuerung**auf **Verwaltung**. Wenn Sie die Kategorieansicht verwenden, klicken Sie auf **Leistung und Wartung** und dann auf **Verwaltung**.  
  
2.  Klicken Sie auf **Dienste**.  
  
3.  Suchen Sie im Snap-In **Dienste** in der Diensteliste **SQL Server Integration Services** , klicken Sie mit der rechten Maustaste auf **SQL Server Integration Services**, und klicken Sie anschließend auf **Eigenschaften**.  
  
4.  Im Dialogfeld **Eigenschaften von SQL Server Integration Services** können Sie folgende Schritte durchführen:  
  
    -   Klicken Sie auf die Registerkarte **Allgemein** . Um den Dienst zu aktivieren, wählen Sie den Starttyp "Manuell" oder "Automatisch" aus. Um den Dienst zu deaktivieren, wählen Sie im Feld **Starttyp** die Option "Deaktivieren" aus. Die Auswahl von "Deaktivieren" führt nicht zum Beenden des Dienstes, falls er gerade ausgeführt wird.  
  
         Wenn der Dienst bereits aktiviert ist, können Sie auf **Beenden** klicken, um den Dienst zu beenden, oder Sie können auf **Starten** klicken, um den Dienst zu starten.  
  
    -   Klicken Sie auf die Registerkarte **Anmelden** , um die Anmeldeinformationen anzuzeigen oder zu bearbeiten.  
  
    -   Klicken Sie auf die Registerkarte **Wiederherstellung** , um die Standardreaktionen des Computers bei Dienstfehlern anzuzeigen. Diese Optionen können Sie entsprechend Ihrer Umgebung anpassen.  
  
    -   Klicken Sie auf die **Abhängigkeiten** -Registerkarte, um eine Liste der abhängigen Dienste anzuzeigen. Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst weist keine Abhängigkeiten auf.  
  
5.  Klicken Sie auf **OK**.  
  
6.  Wenn als Starttyp „Manuell“ oder „Automatisch“ ausgewählt wurde, können Sie optional mit der rechten Maustaste auf **SQL Server Integration Services** klicken und anschließend auf **Starten, Beenden oder Neu starten**klicken.  
  
7.  Klicken Sie im Menü **Datei** auf **Beenden** , um das Snap-In **Dienste** zu schließen.  

## <a name="grant-permissions-to-the-service"></a>Gewähren von Berechtigungen für den Dienst
  In vorherigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hatten alle Benutzer in der Gruppe Benutzer standardmäßig Zugriff auf den Dienst [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , wenn Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installiert haben. Wenn Sie die aktuelle Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installieren, haben Benutzer keinen Zugriff auf den Dienst [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Der Dienst ist standardmäßig sicher. Nach der Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss der Administrator Zugriff auf den Dienst gewähren.  
  
### <a name="to-grant-access-to-the-integration-services-service"></a>So gewähren Sie Zugriff auf den Integration Services-Dienst  
  
1.  Führen Sie "Dcomcnfg.exe" aus. "Dcomcnfg.exe" verfügt über eine Benutzeroberfläche, über die Sie bestimmte Einstellungen in der Registrierung ändern können.  
  
2.  Erweitern Sie im Dialogfeld **Komponentendienste** den Knoten „Komponentendienste“ > „Computer“ > „Arbeitsplatz“ > „DCOM-Konfiguration“.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Microsoft SQL Server Integration Services 13.0**, und klicken Sie anschließend auf **Eigenschaften**.  
  
4.  Klicken Sie auf der Registerkarte **Sicherheit** im Abschnitt **Start- und Aktivierungsberechtigungen** auf **Bearbeiten** .  
  
5.  Fügen Sie Benutzer hinzu, weisen Sie ihnen entsprechende Berechtigungen zu, und klicken Sie dann auf OK.  
  
6.  Wiederholen Sie die Schritte 4 - 5 für Zugriffsberechtigungen.  
  
7.  Starten Sie SQL Server Management Studio neu.  
  
8.  Starten Sie den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst neu.  

## <a name="configure-the-service"></a>Konfigurieren Sie den Dienst
 
Wenn Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]installieren, erstellt und installiert der Setupprozess die Konfigurationsdatei für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst. Diese Konfigurationsdatei enthält die folgenden Einstellungen:  
  
-   Paketen wird ein Befehl zum Beenden gesendet, wenn der Dienst beendet wird.  
  
-   Die Stammordner, die für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] im Objekt-Explorer von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] angezeigt werden sollen, sind die Ordner MSDB und File System.  
  
-   Die Pakete im Dateisystem, das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst verwaltet befinden sich unter %ProgramFiles%\Microsoft SQL Server\130\DTS\Packages.  
  
 Diese Konfigurationsdatei gibt auch an, welche msdb-Datenbank die Pakete enthält, die der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst verwaltet. Standardmäßig wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst für die Verwaltung von Paketen in der msdb-Datenbank der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] konfiguriert, die zur selben Zeit wie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]installiert wird. Wenn eine Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] nicht zur selben Zeit installiert wird, wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst so konfiguriert, dass Pakete in der msdb-Datenbank der lokalen Standardinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]verwaltet werden.  
  
### <a name="default-configuration-file-example"></a>Beispiel für eine Standardkonfigurationsdatei  
 Folgendes Beispiel zeigt eine Standardkonfigurationsdatei, die die folgenden Einstellungen angibt:  
  
-   Die Ausführung von Paketen wird beim Beenden des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts beendet.  
  
-   Die Stammordner für das Speichern von Paketen in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sind die Ordner MSDB und Dateisystem.  
  
-   Der Dienst verwaltet Pakete, die in der msdb-Datenbank der lokalen Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gespeichert sind.  
  
-   Der Dienst verwaltet Pakete, die im Dateisystem im Ordner Pakete gespeichert sind.  
  
 **Beispiel einer Standardkonfigurationsdatei**  
  
```xml
\<?xml version="1.0" encoding="utf-8"?>  
\<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    \<Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>.</ServerName>  
    </Folder>  
    \<Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
### <a name="modify-the-configuration-file"></a>Ändern Sie die Konfigurationsdatei.  
 Sie können die Konfigurationsdatei ändern, um Pakete beim Beenden des Diensts weiterhin auszuführen, um zusätzliche Stammordner im Objekt-Explorer anzuzeigen oder um einen anderen Ordner oder zusätzliche Ordner im Dateisystem anzugeben, die von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwaltet werden sollen. Sie können beispielsweise zusätzliche Stammordner des Typs **SqlServerFolder**erstellen, um Pakete in den msdb-Datenbanken zusätzlicher Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)]zu verwalten.  
  
> [!NOTE]  
>  Manche Zeichen sind für Ordnernamen nicht zulässig. Die gültigen Zeichen für Ordnernamen werden durch die [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Klasse **System.IO.Path** und das Feld **GetInvalidFilenameChars** bestimmt. Das Feld **GetInvalidFilenameChars** stellt ein plattformspezifisches Array mit Zeichen bereit, das nicht in Pfadzeichenfolgenargumenten angegeben werden kann, die an Mitglieder der **Path** -Klasse übergeben werden. Die Menge der ungültigen Zeichen kann je nach Dateisystem variieren. Normalerweise zählen zu den ungültigen Zeichen das Anführungszeichen ("), das Kleiner-als-Zeichen (<) und der senkrechte Strich (|).  
  
 Um Pakete zu verwalten, die in einer benannten Instanz oder einer Remoteinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] gespeichert sind, müssen Sie die Konfigurationsdatei jedoch ändern. Wenn Sie die Konfigurationsdatei nicht aktualisieren, können Sie mit dem **Objekt-Explorer** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] keine Pakete anzeigen, die in der msdb-Datenbank auf der benannten Instanz oder der Remoteinstanz gespeichert sind. Wenn Sie versuchen, diese Pakete mit dem **Objekt-Explorer** anzuzeigen, erhalten Sie die folgende Fehlermeldung:  
  
 `Failed to retrieve data for this request. (Microsoft.SqlServer.SmoEnum)`  
  
 `The SQL Server specified in Integration Services service configuration is not present or is not available. This might occur when there is no default instance of SQL Server on the computer. For more information, see the topic "Configuring the Integration Services Service" in SQL Server 2008 Books Online.`  
  
 `Login Timeout Expired`  
  
 `An error has occurred while establishing a connection to the server. When connecting to SQL Server 2008, this failure may be caused by the fact that under the default settings SQL Server does not allow remote connections.`  
  
 `Named Pipes Provider: Could not open a connection to SQL Server [2]. (MsDtsSvr).`  
  
 Um die Konfigurationsdatei für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst zu ändern, verwenden Sie einen Text-Editor.  
  
> [!IMPORTANT]  
>  Nachdem Sie die Dienstkonfigurationsdatei geändert haben, müssen Sie den Dienst neu starten, damit Sie die aktualisierte Dienstkonfiguration verwenden können.  
  
### <a name="modified-configuration-file-example"></a>Beispiel für eine geänderte Konfigurationsdatei  
 Im folgenden Beispiel wird eine geänderte Konfigurationsdatei für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]gezeigt. Diese Datei dient für eine benannte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit dem Namen `InstanceName` auf dem Server `ServerName`.  
  
 **Beispiel einer geänderten Konfigurationsdatei für eine benannte Instanz von SQL Server**  
  
```xml
\<?xml version="1.0" encoding="utf-8"?>  
\<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    \<Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>ServerName\InstanceName</ServerName>  
    </Folder>  
    \<Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
### <a name="modify-the-configuration-file-location"></a>Ändern Sie den Speicherort der Konfigurationsdatei  
 Der Registrierungsschlüssel **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS\ServiceConfigFile** gibt den Speicherort und Namen für die Konfiguration an, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwendet wird. Der Standardwert des Registrierungsschlüssels ist **C:\Program Files\Microsoft SQL Server\130\DTS\Binn\MsDtsSrvr.ini.xml**. Sie können den Wert des Registrierungsschlüssels aktualisieren, um einen anderen Namen und Speicherort für die Konfigurationsdatei zu verwenden. Beachten Sie, dass die Versionsnummer im Pfad (120 für SQL Server [!INCLUDE[ssSQL14_md](../../includes/sssql14-md.md)], 130 für [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]usw.) variiert abhängig von der SQL Server-Version.
  
> [!CAUTION]  
>  Unsachgemäßes Bearbeiten der Registrierung kann zu schwerwiegenden Problemen führen, die ein Neuinstallieren des Betriebssystems erforderlich machen können. [!INCLUDE[msCoName](../../includes/msconame-md.md)] garantiert nicht, dass Probleme, die durch unsachgemäßes Bearbeiten der Registrierung entstehen, behoben werden können. Sichern Sie vor dem Bearbeiten der Registrierung alle wichtigen Daten. Weitere Informationen zum Sichern, Wiederherstellen und Bearbeiten der Registrierung finden Sie im [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base-Artikel [Windows-Registrierungsinformationen für Benutzer mit fortgeschrittenen Kenntnissen](http://support.microsoft.com/kb/256986).  
  
 Die Konfigurationsdatei wird beim Starten des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts geladen. Bei Änderungen am Registrierungseintrag ist es erforderlich, den Dienst neu zu starten.  

## <a name="connect-to-the-local-service"></a>Herstellen einer Verbindung mit dem lokalen Dienst
  Bevor Sie eine Verbindung mit dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst herstellen, muss der Administrator Ihnen Zugriff auf den Dienst gewähren. 
  
### <a name="to-connect-to-the-integration-services-service"></a>Verbindung mit Integration Services-Diensts  
  
1.  Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Klicken Sie im Menü **Ansicht** auf **Objekt-Explorer** .  
  
3.  Klicken Sie auf der Symbolleiste **Objekt-Explorer**auf **Verbinden**, und klicken Sie dann auf Integration Services.  
  
4.  Geben Sie im Dialogfeld **Verbindung mit Server herstellen** einen Servernamen ein. Sie können einen Punkt (.), (local) oder **localhost** zum Angeben des lokalen Servers verwenden.  
  
5.  Klicken Sie auf **Verbinden**.  

## <a name="connect-to-a-remote-ssis-server"></a>Herstellen einer Verbindung mit einem SSIS-Remoteserver
  
 Zum Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] auf einem Remoteserver über [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder eine andere Verwaltungsanwendung benötigt der Benutzer der Anwendung einen bestimmten Satz von Rechten auf dem Server.  
  
> [!IMPORTANT]
> Die verwendete Version von SQL Server Management Studio (SSMS) muss mit der SQL Server-Version kompatibel sein, unter der Integration Services ausgeführt wird, damit eine direkte Verbindung zu einer Instanz einer älteren Version von Integration Services hergestellt werden kann. Sie benötigen z.B. die für SQL Server 2016 veröffentlichte SSMS-Version, um eine Verbindung mit der Vorgängerversion von Integration Services herzustellen, die auf einer SQL Server 2016-Instanz ausgeführt wird. [Herunterladen von SQL Server Management Studio (SSMS)](/sql-docs/docs/ssms/download-sql-server-management-studio-ssms)
>
>  Zum Verwalten von Paketen auf einem Remoteserver müssen Sie keine Verbindung mit der Instanz des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts auf dem betreffenden Remoteserver herstellen. Bearbeiten Sie stattdessen die Konfigurationsdatei für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst, sodass die auf dem Remoteserver gespeicherten Pakete von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] angezeigt werden.
  
### <a name="connecting-to-integration-services-on-a-remote-server"></a>Herstellen einer Verbindung mit Integration Services auf einem Remoteserver  
  
#### <a name="to-connect-to-integration-services-on-a-remote-server"></a>So stellen Sie eine Verbindung mit Integration Services auf einem Remoteserver her  
  
1.  Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Wählen Sie im Menü **Datei**die Option **Objekt-Explorer verbinden** , um das Dialogfeld **Verbindung mit Server herstellen** anzuzeigen.  
  
3.  Wählen Sie in der Liste **Servertyp** den Eintrag **Integration Services** aus.  
  
4.  Geben Sie in das Textfeld [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] server in the **Server name** text box.  
  
    > [!NOTE]  
    >  Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst ist nicht instanzspezifisch. Sie melden sich beim Dienst mit dem Namen des Computers an, auf dem der Integration Services-Dienst ausgeführt wird.  
  
5.  Klicken Sie auf **Verbinden**.  
  
> [!NOTE]  
>  Im Dialogfeld **Nach Servern suchen** werden keine Remoteinstanzen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]angezeigt. Außerdem sind die Optionen auf der Registerkarte **Verbindungsoptionen** im Dialogfeld **Verbindung mit Server herstellen** , die durch Klicken auf die Schaltfläche **Optionen** angezeigt wird, nicht auf [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Verbindungen anwendbar.  
  
### <a name="eliminating-the-access-is-denied-error"></a>Entfernen der Fehlermeldung "Der Zugriff wurde verweigert."  
 Wenn ein Benutzer ohne ausreichende Rechte versucht, eine Verbindung mit einer Instanz von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] auf einem Remoteserver herzustellen, antwortet der Server mit der Fehlermeldung "Der Zugriff wurde verweigert". Sie können diese Fehlermeldung vermeiden, indem Sie sicherstellen, dass der Benutzer über die erforderlichen DCOM-Berechtigungen verfügt.  
  
#### <a name="to-configure-rights-for-remote-users-on-windows-server-2003-or-windows-xp"></a>So konfigurieren Sie Rechte für Remotebenutzer unter Windows Server 2003 bzw. Windows XP  
  
1.  Wenn der Benutzer kein Mitglied der lokalen Gruppe Administratoren ist, fügen Sie den Benutzer der Gruppe Distributed COM-Benutzer hinzu. Sie können dazu das MMC-Snap-In „Computerverwaltung“ verwenden, das über das Menü **Verwaltung** aufgerufen werden kann.  
  
2.  Öffnen Sie die Systemsteuerung, doppelklicken Sie auf **Verwaltung** , und doppelklicken Sie anschließend auf **Komponentendienste** , um das MMC-Snap-In „Komponentendienste“ zu starten.  
  
3.  Erweitern Sie im linken Bereich der Konsole den Knoten **Komponentendienste** . Erweitern Sie den Knoten **Computer** , erweitern Sie **Arbeitsplatz**, und klicken Sie anschließend auf den Knoten **DCOM-Konfiguration** .  
  
4.  Wählen Sie den Knoten **DCOM-Konfiguration** aus, und wählen Sie anschließend in der Liste der Anwendungen, die konfiguriert werden können, "SQL Server Integration Services 11.0" aus.  
  
5.  Klicken Sie mit der rechten Maustaste auf „SQL Server Integration Services 11.0“, und klicken Sie anschließend auf **Eigenschaften**.  
  
6.  Wählen Sie im Dialogfeld für die Eigenschaften von SQL Server Integration Services 11.0 **** die Registerkarte **Sicherheit** aus.  
  
7.  Wählen Sie unter **Start- und Aktivierungsberechtigungen**die Option **Anpassen**aus, und klicken Sie auf **Bearbeiten** , um das Dialogfeld **Startberechtigung** zu öffnen.  
  
8.  Fügen Sie im Dialogfeld **Startberechtigung** Benutzer hinzu, oder löschen Sie Benutzer, und weisen Sie die entsprechenden Berechtigungen den passenden Benutzern und Gruppen zu. Die verfügbaren Berechtigungen sind Lokaler Start, Remotestart, Lokale Aktivierung und Remoteaktivierung. Die Startrechte erteilen oder verweigern die Berechtigung zum Starten und Beenden des Diensts, während die Aktivierungsrechte die Berechtigung zum Herstellen einer Verbindung mit dem Dienst erteilen oder verweigern.  
  
9. Klicken Sie auf OK, um das Dialogfeld zu schließen.  
  
10. Wiederholen Sie die Schritte 7 und 8 unter **Zugriffsberechtigungen**, um den Benutzern und Gruppen die geeigneten Berechtigungen zuzuweisen.  
  
11. Schließen Sie das MMC-Snap-In.  
  
12. Starten Sie den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst neu.  
  
#### <a name="to-configure-rights-for-remote-users-on-windows-2000-with-the-latest-service-packs"></a>So konfigurieren Sie Rechte für Remotebenutzer unter Windows 2000 mit den neuesten Service Packs  
  
1.  Führen Sie **dcomcnfg.exe** an der Eingabeaufforderung aus.  
  
2.  Wählen Sie auf der Seite **Anwendungen** des Dialogfelds für verteilte COM-Konfigurationseigenschaften die Option **SQL Server Integration Services 11.0** aus, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Wählen Sie die Seite **Sicherheit** aus.  
  
4.  Verwenden Sie die beiden separaten Dialogfelder zum Konfigurieren der **Zugriffsberechtigungen** und der **Startberechtigungen**. Eine Unterscheidung zwischen Remote- und lokalem Zugriff ist nicht möglich. Die Zugriffsberechtigungen umfassen lokalen und Remotezugriff, die Startberechtigungen lokalen und Remotestart.  
  
5.  Schließen Sie die Dialogfelder und **dcomcnfg.exe**.  
  
6.  Starten Sie den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst neu.  
  
### <a name="connecting-by-using-a-local-account"></a>Herstellen einer Verbindung mithilfe eines lokalen Kontos  
 Wenn Sie ein lokales Windows-Konto auf einem Clientcomputer verwenden, können Sie nur dann eine Verbindung mit dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst auf einem Remotecomputer herstellen, wenn auf dem Remotecomputer ein lokales Konto mit dem gleichen Namen und Kennwort sowie ausreichenden Rechten vorhanden ist.  
  
### <a name="by-default-the-ssis-service-does-not-support-delegation"></a>Standardmäßig wird die Delegierung vom SSIS-Dienst nicht unterstützt  
Die Delegierung von Anmeldeinformationen, auch als Doppelhop bezeichnet, wird vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst standardmäßig nicht unterstützt. In diesem Szenario verwenden Sie einen Clientcomputer, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ist auf einem zweiten Computer und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem dritten Computer installiert. Zunächst übergibt [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Ihre Anmeldeinformationen erfolgreich vom Clientcomputer an den zweiten Computer, auf dem der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst ausgeführt wird. Anschließend kann der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst Ihre Anmeldeinformationen jedoch nicht vom zweiten Computer an den dritten Computer delegieren, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird.

Sie können die Delegierung von Anmeldeinformationen aktivieren, indem Sie dem SQL Server-Dienstkonto, das den Integration Services-Dienst als untergeordneten Prozess startet (ISServerExec.exe), die Berechtigung **Benutzer bei Delegierungen aller Dienste vertrauen (nur Kerberos)** erteilen. Beachten Sie, dass diese Berechtigung die Sicherheitsanforderungen Ihrer Organisation erfüllt, bevor Sie sie erteilen.

Weitere Informationen finden Sie im Blogbeitrag [Getting Cross Domain Kerberos and Delegation working with SSIS Package](https://blogs.msdn.microsoft.com/psssql/2014/06/26/getting-cross-domain-kerberos-and-delegation-working-with-ssis-package/)(Erreichen, dass Kerberos (domänenübergreifend) und Delegierung in SSIS-Paketen funktionieren).
 
## <a name="configure-the-firewall"></a>Konfigurieren der firewall
  
 Die Windows-Firewallsystem hilft nicht autorisierten Zugriff auf Computerressourcen über eine Netzwerkverbindung verhindert. Um über diese Firewall auf [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] zuzugreifen, müssen Sie die Firewall so konfigurieren, dass der Zugriff zulässig ist.  
  
> [!IMPORTANT]  
>  Zum Verwalten von Paketen auf einem Remoteserver müssen Sie keine Verbindung mit der Instanz des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts auf dem betreffenden Remoteserver herstellen. Bearbeiten Sie stattdessen die Konfigurationsdatei für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst, sodass die auf dem Remoteserver gespeicherten Pakete von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] angezeigt werden.
  
 Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst verwendet das DCOM-Protokoll. Weitere Informationen zur Funktionsweise des DCOM-Protokolls über Firewalls finden Sie im Artikel "[Using Distributed COM with Firewalls](http://go.microsoft.com/fwlink/?LinkId=12490)" in der MSDN Library.  
  
 Es gibt zahlreiche verschiedene Firewallsysteme auf dem Markt. Wenn Sie eine andere Firewall als die Windows-Firewall ausführen, finden Sie in Ihrer Firewalldokumentation für Informationen, die speziell für das System ist, die Sie verwenden.  
  
 Falls die Firewall das Filtern auf Anwendungsebene unterstützt, können Sie mithilfe der Benutzeroberfläche von Windows die für diese Firewall zulässigen Ausnahmen angeben, wie z. B. Programme und Dienste. Andernfalls müssen Sie für DCOM eine begrenzte Anzahl von TCP-Ports konfigurieren. Der zuvor bereitgestellte Link zur Microsoft-Website enthält Informationen zum Angeben der zu verwendenden TCP-Ports.  
  
 Der Integration Services-Dienst verwendet Port 135. Dies kann nicht geändert werden. Sie müssen TCP-Port 135 für den Zugriff auf den Dienstkontroll-Manager (SCM, Service Control Manager) öffnen. SCM führt u. a. folgende Tasks aus: Starten und Beenden von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensten und Übertragen von Steuerungsanforderungen an den ausgeführten Dienst.  
  
 Die Informationen im folgenden Abschnitt sind ausschließlich für die Windows-Firewall. Sie können die Windows-Firewallsystem durch Ausführen eines Befehls an der Eingabeaufforderung oder durch Festlegen von Eigenschaften im Dialogfeld Windows-Firewall konfigurieren.  
  
 Weitere Informationen zu den Standardeinstellungen der Windows-Firewall und eine Beschreibung der TCP-Ports, die sich auf Datenbankmodul, Analysis Services, Reporting Services und Integration Services auswirken, finden Sie unter [Konfigurieren der Windows-Firewall für den SQL Server-Zugriff](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
### <a name="configuring-a-windows-firewall"></a>Konfigurieren einer Windows-firewall  
 Sie können die folgenden Befehle verwenden, um TCP-Port 135 zu öffnen, MsDtsSrvr.exe der Ausnahmeliste hinzuzufügen und den Bereich zum Aufheben der Blockierung für die Firewall anzugeben.  
  
#### <a name="to-configure-a-windows-firewall-using-the-command-prompt-window"></a>So konfigurieren Sie eine Windows-Firewall mithilfe des Eingabeaufforderungsfensters  
  
1.  Führen Sie den folgenden Befehl aus:

    ```dos
    netsh firewall add portopening protocol=TCP port=135 name="RPC (TCP/135)" mode=ENABLE scope=SUBNET
    ```
  
2.  Führen Sie den folgenden Befehl aus:

    ```dos
    netsh firewall add allowedprogram program="%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.exe" name="SSIS Service" scope=SUBNET
    ```
  
    > [!NOTE]  
    >  Ersetzen Sie zum Öffnen der Firewall für alle Computer sowie für Computer im Internet scope=SUBNET durch scope=ALL.  
  
 In der folgenden schrittweisen Anleitung wird beschrieben, wie Sie mithilfe der Windows-Benutzeroberfläche TCP-Port 135 öffnen, MsDtsSrvr.exe der Ausnahmeliste hinzufügen und den Bereich zum Aufheben der Blockierung für die Firewall angeben.  
  
#### <a name="to-configure-a-firewall-using-the-windows-firewall-dialog-box"></a>Konfigurieren eine Firewall über das Dialogfeld Windows-firewall  
  
1.  Doppelklicken Sie in der Systemsteuerung auf **Windows-Firewall**.  
  
2.  Klicken Sie im Dialogfeld **Windows-Firewall** auf die Registerkarte **Ausnahmen** , und klicken Sie dann auf **Programm hinzufügen**.  
  
3.  Klicken Sie im Dialogfeld **Programm hinzufügen** auf **Durchsuchen**, navigieren Sie zum Ordner „Programme\Microsoft SQL Server\100\DTS\Binn, klicken Sie auf MsDtsSrvr.exe“, und klicken Sie anschließend auf **Öffnen**. Klicken Sie auf **OK** , um das Dialogfeld **Programm hinzufügen** zu schließen.  
  
4.  Klicken Sie auf der Registerkarte **Ausnahmen** auf **Port hinzufügen**.  
  
5.  Geben Sie im Dialogfeld **Port hinzufügen** **RPC(TCP/135)** oder einen anderen beschreibenden Namen in das Feld **Name**ein, geben Sie **135** in das Feld **Portnummer** ein, und wählen anschließend Sie **TCP**aus.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst verwendet immer Port 135. Sie können keinen anderen Port angeben.  
  
6.  Im Dialogfeld **Port hinzufügen** können Sie optional auf **Bereich ändern** klicken, um den Standardbereich zu ändern.  
  
7.  Wählen Sie im Dialogfeld **Bereich ändern** das Optionsfeld **My network (subnet only)** (Eigenes Netzwerk (nur Subnetz)) aus, oder geben Sie eine benutzerdefinierte Liste ein, und klicken Sie anschließend auf **OK**.  
  
8.  Klicken Sie auf **OK** , um das Dialogfeld **Port hinzufügen**zu schließen.  
  
9. Klicken Sie auf **OK** , um das Dialogfeld **Windows-Firewall**zu schließen.  
  
    > [!NOTE]  
    >  Um die Windows-Firewall zu konfigurieren, diese Prozedur verwendet die **Windows-Firewall** Element in der Systemsteuerung. Über die Option **Windows-Firewall** wird nur die Firewall für das Profil des aktuellen Netzwerkspeicherorts konfiguriert. Sie können auch die Windows-Firewall konfigurieren, mit der **Netsh** -Befehlszeilentool oder den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (MMC)-Snap-in mit dem Namen Windows-Firewall mit erweiterter Sicherheit. Weitere Informationen über diese Tools finden Sie unter [Konfigurieren der Windows-Firewall für den SQL Server-Zugriff](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  

