---
title: Backup-ASDatabase-Cmdlet | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 03d58a82-021c-4e13-b265-c084f42a8bb2
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1a4daeaf04fc9fe9c41064fe047110037c6d34e1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="backup-asdatabase-cmdlet"></a>Backup-ASDatabase-Cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Sichern Sie eine mehrdimensionale oder tabellarische Analysis Services-Datenbank in einer Analysis Services-Sicherungsdatei (.abf).  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
## <a name="syntax"></a>Syntax  
 `Backup-ASDatabase [-BackupFile] <string> [-Name] <string> [-AllowOverwrite <SwitchParameter>] [-BackupRemotePartitions <SwitchParameter>] [-ApplyCompression <SwitchParameter>] [-FilePassword <SecureString>] [-Locations <Microsoft.AnalysisServices.BackupLocation[]>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
 `Backup-ASDatabase –Database <Microsoft.AnalysisServices.Database> [-AllowOverwrite <SwitchParameter>] [-BackupRemotePartitions <SwitchParameter>] [-ApplyCompression <SwitchParameter>] [-FilePassword <SecureString>] [-Locations <Microsoft.AnalysisServices.BackupLocation[]>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Ermöglicht es einem Analysis Services-Systemadministrator, eine mehrdimensionale oder tabellarische Datenbank in einer Sicherungsdatei zu sichern. Wenn Sie keinen Speicherort angeben, wird der Standardsicherungsspeicherort verwendet, der während des Setups angegeben wurde.  
  
 Gesicherte Dateien können verschlüsselt werden. Verwenden Sie "–FilePassword", um die Datei zu verschlüsseln. Wenn Sie die Datei später wiederherstellen, müssen Sie dasselbe Kennwort angeben, das Sie zum Verschlüsseln angegeben haben.  
  
 Dieses Cmdlet unterstützt den –Credential-Parameter, der verwendet werden kann, wenn Sie die Analysis Services-Instanz für HTTP-Zugriff konfigurierten. Der –Credential-Parameter verwendet ein PSCredential-Objekt, das eine Windows-Benutzeridentität bereitstellt. Beim Herstellen einer Verbindung mit Analysis Services nimmt wird die Identität dieses Benutzers dann von IIS angenommen. Die Identität muss über Systemadministratorberechtigungen für die Analysis Services-Instanz verfügen, um eine Sicherung erstellen zu können.  
  
## <a name="parameters"></a>Parameter  
  
### <a name="-backupfile-string"></a>BackupFile - \<Zeichenfolge >  
 Gibt den Pfad und den Namen der Sicherungsdatei an. Wenn Sie nur einen Dateinamen ohne Pfad angeben, wird der Standardsicherungsspeicherort verwendet. Dieser Parameter wird nur mit dem -Name-Parameter verwendet.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-name-string"></a>-Namen \<Zeichenfolge >  
 Gibt die Analysis Services-Datenbank an, die gesichert werden soll. Sie können eine Datenbank entweder mit dem -Database-Parameter oder mit dem -Name-Parameter angeben, wenn Sie im Namen als Zeichenfolge übergeben möchten.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|1|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-allowoverwrite-switchparameter"></a>AllowOverwrite - \<Switch-Parameter >  
 Überschreibt eine Sicherungsdatei mit dem gleichen Namen.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-backupremotepartitions-switchparameter"></a>BackupRemotePartitions - \<Switch-Parameter >  
 Gibt an, ob Remotepartitionen in der Sicherung enthalten sind.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-applycompressionswitchparameter"></a>ApplyCompression -\<Switch-Parameter >  
 Gibt an, ob die Sicherungsdatei komprimiert wird.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-filepassword-securestring"></a>– FilePassword \<SecureString >  
 Gibt ein Kennwort an, das für die Verschlüsselung der Sicherungsdatei verwendet werden soll.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-locations-microsoftanalysisservicesbackuplocation"></a>-Standorte \<Microsoft.AnalysisServices.BackupLocation [] >  
 Gibt die Position an, an der die Sicherungsdatei gespeichert wird.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-server-string"></a>-Server \<Zeichenfolge >  
 Gibt die Analysis Services-Instanz an, zu der das Cmdlet eine Verbindung herstellt und auf der es ausgeführt wird. Wenn kein Servername angegeben wird, wird eine Verbindung mit localhost hergestellt. Für Standardinstanzen geben Sie nur den Servernamen an. Verwenden Sie für benannte Instanzen das Format "servername\instanzenname". Verwenden Sie für HTTP-Verbindungen das Format "http[s]://server[:port]/virtualdirectory/msmdpump.dll".  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|localhost|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-credential-pscredential"></a>-Credential \<"PSCredential" >  
 Gibt ein PSCredential-Objekt an, das einen Windows-Benutzernamen und ein -Kennwort angegeben werden. Geben Sie diesen Parameter nur an, wenn die Analysis Services-Instanz mit der Standardauthentifizierung für HTTP-Zugriff konfiguriert wird. Für systemeigene Verbindungen, die integrierte Sicherheit verwenden, wird dieser Parameter ignoriert.  
  
 Wenn dieser Parameter vorhanden ist, werden die Anmeldeinformationen, die es bereitstellt, an die Verbindungszeichenfolge angefügt. Beim Herstellen einer Verbindung mit Analysis Services wird die Identität dieses Benutzers dann von IIS angenommen. Wenn keine Anmeldeinformationen angegeben sind, wird das Windows-Standardkonto des Benutzers, der das Tool ausführt, verwendet.  
  
 Um diesen Parameter verwenden zu können, müssen Sie zuerst ein PSCredential-Objekt erstellen. Hierbei verwenden Sie Get-Credential, um den Benutzernamen und das Passwort anzugeben (z.B. `$Cred=Get-Credential “adventure-works\admin”`). Sie können dieses Objekt anschließend an den –Credential-Parameter `(-Credential:$Cred`) übergeben.  
  
Weitere Informationen zum HTTP-Zugriff finden Sie unter [Konfigurieren von HTTP-Zugriff auf Analysis Services unter Internetinformationsdienste &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|True (ByValue)|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-database-microsoftanalysisservicesdatabase"></a>-Datenbank \<Microsoft.AnalysisServices.Database [] >  
 Gibt ein Analysis Services-Datenbankobjekt an, das gesichert werden soll. Sie können eine Datenbank mithilfe entweder mit dem -Database-Parameter oder mit dem –Name-Parameter angeben. Verwenden Sie –Database, wenn Sie über die Pipeline den Datenbanknamen weitergeben möchten.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|true|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="commonparameters"></a>\<Allgemeine Parameter >  
 Dieses Cmdlet unterstützt die gängigen Parameter: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer und -OutVariable. Weitere Informationen finden Sie unter [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|Microsoft.AnalysisServices.Database<br /><br /> Sie können mehrere Datenbanken übergeben, die Sie sichern möchten, z. B. alle Datenbanken einer bestimmten Instanz.|  
|Ausgaben|Keine.|  
  
## <a name="example-1"></a>Beispiel 1  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default >backup-asdatabase awdb-20110930.abf “Adventure Works” -AllowOverwrite -ApplyCompression  
```  
  
 Dieser Befehl sichert die Adventure Works-Datenbank in einer ABF-Datei am Standardsicherungsspeicherort. Wenn eine Datei des gleichen Namens am Speicherort vorhanden ist, wird sie überschrieben.  
  
## <a name="example-2"></a>Beispiel 2  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default >$AWDB = get-item “databases\Adventure Works”   
PS SQLSERVER:\SQLAS\Localhost\default >Backup-asdatabase –database:$AWDB –AllowOverwrite  
```  
  
 Dieser Befehl verwendet –Database statt -Backupfile und -Name. Verwenden Sie den –Database-Parameter, wenn Sie den Datenbanknamen an das Cmdlet weitergeben möchten.  
  
## <a name="example-3"></a>Beispiel 3  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default\databases >dir * | backup-asdatabase  
```  
  
 Dieser Befehl sichert alle Datenbanken auf dem lokalen Server.  
  
## <a name="example-4"></a>Beispiel 4  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default > $pwd = read-host –AsSecureString –Prompt “Password”   
PS SQLSERVER:\SQLAS\Localhost\default > $pwd -is [System.IDisposable]   
PS SQLSERVER:\SQLAS\Localhost\default > backup-asdatabase –backupfile test.abf –name contoso_retail –filepassword:$pwd server myremoteserver  
PS SQLSERVER:\SQLAS\Localhost\default >$pwd.Dispose()  
PS SQLSERVER:\SQLAS\Localhost\default >Remove-Variable –Name pwd  
```  
  
 Linie 1 und 2 werden verwendet, um ein Kennwort aufzufordern, das dazu dient, die Datei zu verschlüsseln.  
  
 Linie 3 sichert die Beispieldatenbank "Contoso_Retail" auf einem Remote-Analysis Services-Server in einer Analysis Services-Sicherungsdatei mit dem Namen "test.abf", die sich auch auf dem Remoteserver befindet. Die Datei wird im Standardsicherungsordner der Standardinstanz gespeichert.  
  
 Mit Linie 4 und 5 wird das Kennwort entfernt.  
  
  
  

