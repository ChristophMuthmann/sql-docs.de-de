---
title: Restore-ASDatabase-Cmdlet | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 8ab7a2d0-679c-40e6-b9b9-042184b2dfc9
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ae57bdc2a1f385e06248ab9486b7ef5fc07f7932
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="restore-asdatabase-cmdlet"></a>Restore-ASDatabase-Cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Stellt eine mehrdimensionale oder tabellarische Datenbanksicherungsdatei (.abf) in einer Analysis Services-Instanz wieder her.  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
## <a name="syntax"></a>Syntax  
 `Restore-ASDatabase [-RestoreFile] <string> [-Name] <string> [-AllowOverwrite <SwitchParameter>] Locations <Microsoft.AnalysisServices.RestoreLocation[]>] [-Security <Microsoft.AnalysisServices.RestoreSecurity>] [-Password <System.SecureString>] [-StorageLocation <System.string>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Ermöglicht einem Analysis Services-Systemadministrator, eine mehrdimensionale oder tabellarische Datenbank aus einer Sicherungsdatei (.abf) in einer lokalen oder Remoteserverinstanz wiederherzustellen. Wenn die Datei, die Sie wiederherstellen, verschlüsselt war, können Sie das Kennwort, das zum Verschlüsseln der Datei verwendet wurde, mit "-FilePassword" angeben.  
  
 Dieses Cmdlet unterstützt den –Credential-Parameter, der verwendet werden kann, wenn Sie die Analysis Services-Instanz für HTTP-Zugriff konfigurierten. Der –Credential-Parameter verwendet ein PSCredential-Objekt, das eine Windows-Benutzeridentität bereitstellt. Beim Herstellen einer Verbindung mit Analysis Services nimmt wird die Identität dieses Benutzers dann von IIS angenommen. Die Identität muss über Systemadministratorberechtigungen für die Analysis Services-Instanz verfügen, um eine Datei wiederherstellen zu können.  
  
## <a name="parameters"></a>Parameter  
  
### <a name="-restorefile-string"></a>RestoreFile - \<Zeichenfolge >  
 Gibt den Pfad und den Namen der wiederherzustellenden Datei an. Wenn Sie nur den Dateinamen ohne Pfad angeben, wird vom Standardsicherungsspeicherort ausgegangen.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-name-string"></a>-Namen \<Zeichenfolge >  
 Gibt die Analysis Services-Datenbank an, die wiederhergestellt werden soll.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|1|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-allowoverwrite-switchparameter"></a>AllowOverwrite - \<Switch-Parameter >  
 Überschreibt eine Datenbank, die den gleichen Namen und Speicherort verwendet.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-locations-microsoftanalysisservicesrestorelocation"></a>-Standorte \<Microsoft.AnalysisServices.RestoreLocation [] >  
 Gibt den Remotestandort der Partitionen an, die wiederhergestellt werden sollen.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-security-microsoftanalysisservicesrestoresecurity"></a>-Sicherheit \<Microsoft.AnalysisServices.RestoreSecurity >  
 Stellt die für den Wiederherstellungsvorgang verwendeten Sicherheitseinstellungen dar. Gültige Werte sind CopyAll, SkipMembership, IgnoreSecurity. CopyAll stellt Rollen und Mitgliedschaft wieder her. SkipMembership erstellt nur die Rolle neu. IgnoreSecurity stellt die Datenbank ohne Rollen wieder her.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-password-securestring"></a>-Kennwort \<SecureString >  
 Gibt ein Kennwort an, das verwendet werden soll, um eine verschlüsselte Sicherungsdatei wiederherzustellen. Sie müssen das Kennwort, das bei der ursprünglichen Verschlüsselung der Datei verwendet wurde, angeben.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-storagelocation-string"></a>StorageLocation - \<Zeichenfolge >  
 Gibt den Datenbankspeicherort an. Dies ist der Speicherort der Datenbankdateien im Dateisystem. Legen Sie diesen Parameter fest, wenn Sie nicht den Standardspeicherort verwenden (den Sicherungsordner der Zielinstanz).  
  
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
  
### <a name="commonparameters"></a>\<Allgemeine Parameter >  
 Dieses Cmdlet unterstützt die gängigen Parameter: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer und -OutVariable. Weitere Informationen finden Sie unter [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|System.string<br /><br /> Sie können Zeichenfolgenwerte an das Cmdlet weitergeben.|  
|Ausgaben|Keine.|  
  
## <a name="example-1"></a>Beispiel 1  
  
```  
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase awtest.abf testawrestoredb –security:CopyAll  
```  
  
 Dieser Befehl stellt eine Analysis Services-Sicherungsdatei ("awtest.abf") im lokalen Sicherungsordner der Standardinstanz in einer lokalen Analysis Services wieder her. Der Datenbankname muss nicht vorhanden sein; in diesem Fall wird der Datenbankname als Teil des Wiederherstellungsvorgangs angegeben. Wenn Sie "-Security:CopyAll" hinzufügen, werden Rollen und Rollenmitgliedschaften aus der Sicherungsdatenbank in der neu wiederhergestellten Datenbank aufgefüllt.  
  
## <a name="example-2"></a>Beispiel 2  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default > $pwd = read-host –AsSecureString –Prompt “Password”   
PS SQLSERVER:\SQLAS\Localhost\default > $pwd -is [System.IDisposable]   
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase –restorefile testdb.abf –name AWTEST2 –password:$pwd  
PS SQLSERVER:\SQLAS\Localhost\default >$pwd.Dispose()  
PS SQLSERVER:\SQLAS\Localhost\default >Remove-Variable –Name pwd  
```  
  
 Linie 1 und 2 werden verwendet, um das Kennwort aufzufordern, das verwendet wurde, die Datei zu verschlüsseln.  
  
 Linie 3 stellt eine verschlüsselte Analysis Services-Sicherungsdatei (testdb.abf) von einem Remotesicherungsordner auf einer Analysis Services-Standardinstanz wieder her.  
  
 Mit Linie 4 und 5 wird das Kennwort entfernt.  
  
## <a name="example-3-remote-scenario"></a>Beispiel 3 (Remoteszenario)  
 Dieses Beispiel veranschaulicht, wie eine lokale Sicherungsdatei aus einer Dateifreigabe in einer Remoteinstanz von Analysis Services wiederhergestellt wird. In diesem Beispiel wird eine Sicherungsdatei als Datenbank namens **internetsales** in einer Standardinstanz von Analysis Services auf einem Computer namens **ssas-aw-srv01**wiederhergestellt.  
  
 Die Sicherungsdatei befindet sich auf einer Netzwerkfreigabe mit öffentlichem Lesezugriff. Die Remoteinstanz von Analysis Services benötigt eine Leseberechtigung für die Datei. Der Speicherort der Datei muss sich auf einer Netzwerkfreigabe (keine Laufwerke) befinden.  
  
 Beachten Sie, dass dieses Beispiel nicht vom SQLAS-Anbieter abhängig ist. Sie können das Cmdlet als eigenständigen Befehl ausführen.  
  
```  
PS SQLSERVER:\> restore-asdatabase -restorefile "\\FileServer01\DBFiles\InternetSalesTabular.abf" -name "internetsales  
" -server "SSAS-AW-SRV01"  
```  
  
## <a name="example-4"></a>Beispiel 4  
  
```  
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase –restorefile “\\myremoteserver\backups\testdb.abf” –name Contoso_Retail –server myremoteserver –storagelocation “\\myremoteserver\restoreDBFiles”  
```  
  
 Dieser Befehl stellt eine verschlüsselte Analysis Services-Sicherungsdatei (testdb.abf) in einem Remotesicherungsordner auf einer Remote-Analysis Services Standardinstanz wieder her. Der –StorageLocations-Parameter wird verwendet, um die Datenbankdateien an einem nicht standardmäßigen Speicherort einzufügen, in diesem Fall eine freigegebene Datei mit dem Namen "restoreDBfiles".  
  
