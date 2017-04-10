---
title: "Konfigurieren des Integration Services-Diensts (SSIS-Dienst) | Microsoft Docs"
ms.custom: ""
ms.date: "02/28/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server (starting with 2016)"
helpviewer_keywords: 
  - "Integration Services-Dienst, konfigurieren"
  - "Konfigurationsdateien [Integration Services]"
  - "Dienst [Integration Services], konfigurieren"
  - "Standardkonfigurationsdateien"
ms.assetid: 36d78393-a54c-44b0-8709-7f003f44c27f
caps.latest.revision: 74
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 70
---
# Konfigurieren des Integration Services-Diensts (SSIS-Dienst)
    
> [!IMPORTANT]  
>  In diesem Thema wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst beschrieben, ein Windows-Dienst zur Verwaltung von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketen. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] unterstützt den Dienst für die Abwärtskompatibilität mit früheren Versionen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]können Sie Objekte, z. B. Pakete, auf dem Integration Services-Server verwalten.  
  
 Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst erhält seine Einstellungen über eine Konfigurationsdatei. Standardmäßig lautet der Name für diese Konfigurationsdatei MsDtsSrvr.ini.xml, und die Datei befindet sich im Ordner %ProgramFiles%\Microsoft SQL Server\110\DTS\Binn.  
  
 In der Regel müssen Sie keine Änderungen an dieser Konfigurationsdatei vornehmen. Ebenso wenig müssen Sie den Standardspeicherort der Datei ändern. Sie müssen die Konfigurationsdatei jedoch ändern, wenn Ihre Pakete in einer benannten Instanz, einer Remoteinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] oder in mehreren Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)] gespeichert sind. Auch wenn Sie die Konfigurationsdatei an einen anderen Speicherort verschieben, müssen Sie den Registrierungsschlüssel ändern, der den Dateispeicherort angibt.  
  
## Inhalt der Konfigurationsdatei  
 Wenn Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installieren, erstellt und installiert der Setupprozess die Konfigurationsdatei für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst. Diese Konfigurationsdatei enthält die folgenden Einstellungen:  
  
-   Paketen wird ein Befehl zum Beenden gesendet, wenn der Dienst beendet wird.  
  
-   Die Stammordner, die für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] im Objekt-Explorer von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] angezeigt werden sollen, sind die Ordner MSDB und File System.  
  
-   Die Pakete im Dateisystem, die vom [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst verwaltet werden, befinden sich unter %ProgramFiles%\Microsoft SQL Server\110\DTS\Packages.  
  
 Diese Konfigurationsdatei gibt auch an, welche msdb-Datenbank die Pakete enthält, die der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst verwaltet. Standardmäßig wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst für die Verwaltung von Paketen in der msdb-Datenbank der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] konfiguriert, die zur selben Zeit wie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installiert wird. Wenn eine Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] nicht zur selben Zeit installiert wird, wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst so konfiguriert, dass Pakete in der msdb-Datenbank der lokalen Standardinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] verwaltet werden.  
  
### Beispiel für eine Standardkonfigurationsdatei  
 Folgendes Beispiel zeigt eine Standardkonfigurationsdatei, die die folgenden Einstellungen angibt:  
  
-   Die Ausführung von Paketen wird beim Beenden des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Diensts beendet.  
  
-   Die Stammordner für das Speichern von Paketen in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sind die Ordner MSDB und Dateisystem.  
  
-   Der Dienst verwaltet Pakete, die in der msdb-Datenbank der lokalen Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeichert sind.  
  
-   Der Dienst verwaltet Pakete, die im Dateisystem im Ordner Pakete gespeichert sind.  
  
 **Beispiel einer Standardkonfigurationsdatei**  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    <Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>.</ServerName>  
    </Folder>  
    <Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
## Änderung der Konfigurationsdatei  
 Sie können die Konfigurationsdatei ändern, um Pakete beim Beenden des Diensts weiterhin auszuführen, um zusätzliche Stammordner im Objekt-Explorer anzuzeigen oder um einen anderen Ordner oder zusätzliche Ordner im Dateisystem anzugeben, die von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwaltet werden sollen. Sie können beispielsweise zusätzliche Stammordner des Typs **SqlServerFolder** erstellen, um Pakete in den msdb-Datenbanken zusätzlicher Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)] zu verwalten.  
  
> [!NOTE]  
>  Manche Zeichen sind für Ordnernamen nicht zulässig. Die gültigen Zeichen für Ordnernamen werden durch die [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Klasse **System.IO.Path** und das Feld **GetInvalidFilenameChars** bestimmt. Das Feld **GetInvalidFilenameChars** stellt ein plattformspezifisches Array mit Zeichen bereit, das nicht in Pfadzeichenfolgenargumenten angegeben werden kann, die an Mitglieder der **Path**-Klasse übergeben werden. Die Menge der ungültigen Zeichen kann je nach Dateisystem variieren. Normalerweise zählen zu den ungültigen Zeichen das Anführungszeichen ("), das Kleiner-als-Zeichen (<) und der senkrechte Strich (|).  
  
 Um Pakete zu verwalten, die in einer benannten Instanz oder einer Remoteinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] gespeichert sind, müssen Sie die Konfigurationsdatei jedoch ändern. Wenn Sie die Konfigurationsdatei nicht aktualisieren, können Sie mit dem **Objekt-Explorer** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] keine Pakete anzeigen, die in der msdb-Datenbank auf der benannten Instanz oder der Remoteinstanz gespeichert sind. Wenn Sie versuchen, diese Pakete mit dem **Objekt-Explorer** anzuzeigen, erhalten Sie die folgende Fehlermeldung:  
  
 `Failed to retrieve data for this request. (Microsoft.SqlServer.SmoEnum)`  
  
 `The SQL Server specified in Integration Services service configuration is not present or is not available. This might occur when there is no default instance of SQL Server on the computer. For more information, see the topic "Configuring the Integration Services Service" in SQL Server 2008 Books Online.`  
  
 `Login Timeout Expired`  
  
 `An error has occurred while establishing a connection to the server. When connecting to SQL Server 2008, this failure may be caused by the fact that under the default settings SQL Server does not allow remote connections.`  
  
 `Named Pipes Provider: Could not open a connection to SQL Server [2]. (MsDtsSvr).`  
  
 Um die Konfigurationsdatei für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst zu ändern, verwenden Sie einen Text-Editor.  
  
> [!IMPORTANT]  
>  Nachdem Sie die Dienstkonfigurationsdatei geändert haben, müssen Sie den Dienst neu starten, damit Sie die aktualisierte Dienstkonfiguration verwenden können.  
  
### Beispiel für eine geänderte Konfigurationsdatei  
 Im folgenden Beispiel wird eine geänderte Konfigurationsdatei für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] gezeigt. Diese Datei dient für eine benannte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit dem Namen `InstanceName` auf dem Server `ServerName`.  
  
 **Beispiel einer geänderten Konfigurationsdatei für eine benannte Instanz von SQL Server**  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    <Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>ServerName\InstanceName</ServerName>  
    </Folder>  
    <Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
## Änderung des Speicherorts der Konfigurationsdatei  
 Der Registrierungsschlüssel HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\ServiceConfigFile gibt den Speicherort und Namen für die Konfigurationsdatei an, die vom [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst verwendet wird. Der Standardwert des Registrierungsschlüssels lautet C:\Programme\Microsoft SQL Server\110\DTS\Binn\ MsDtsSrvr.ini.xml. Sie können den Wert des Registrierungsschlüssels aktualisieren, um einen anderen Namen und Speicherort für die Konfigurationsdatei zu verwenden.  
  
> [!CAUTION]  
>  Unsachgemäßes Bearbeiten der Registrierung kann zu schwerwiegenden Problemen führen, die ein Neuinstallieren des Betriebssystems erforderlich machen können. [!INCLUDE[msCoName](../../includes/msconame-md.md)] garantiert nicht, dass Probleme, die durch unsachgemäßes Bearbeiten der Registrierung entstehen, behoben werden können. Sichern Sie vor dem Bearbeiten der Registrierung alle wichtigen Daten. Weitere Informationen zum Sichern, Wiederherstellen und Bearbeiten der Registrierung finden Sie im [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base-Artikel [Windows-Registrierungsinformationen für Benutzer mit fortgeschrittenen Kenntnissen](http://support.microsoft.com/kb/256986).  
  
 Die Konfigurationsdatei wird beim Starten des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Diensts geladen. Bei Änderungen am Registrierungseintrag ist es erforderlich, den Dienst neu zu starten.  
  
  