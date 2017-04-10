---
title: "New-RestoreLocations-Cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 5ca13d8c-1c5d-4f02-869c-72e0defce6d7
caps.latest.revision: 11
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 11
---
# New-RestoreLocations-Cmdlet
  Gibt Informationen an, die verwendet wurden, um eine Datenbank wiederherzustellen.  
  
## Syntax  
 `New-RestoreLocation [-File <String>] [-DataSourceId <String>] [-ConnectionString <String>] [-DataSourceType <RestoreDataSourceType>] [-Folders <RestoreFolder[]>] [-AsTemplate] [-Server <String>] [-Credential <PSCredential>] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]`  
  
 `New-RestoreLocation [-Server <String>] [-Credential <PSCredential>] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]`  
  
 Allgemeine Parameter, z. B. –Verbose, -Debug, Fehler- und Warnparameter, -Whatif und –Confirm werden in der Windows PowerShell-Referenz dokumentiert. Weitere Informationen finden Sie unter [about_CommonParameters](http://technet.microsoft.com/library/dd315352.aspx).  
  
## Description  
 Das New-RestoreLocations-Cmdlet enthält Informationen, die verwendet werden, um eine Datenbank wiederherzustellen, einschließlich der Verbindungszeichenfolge des Servers und Datenbank, der Datenquelleneigenschaften, Dateien und Ordner, die der wiederherzustellenden Datenbank zugeordnet sind.  
  
## Parameter  
  
### -Datei \<string>  
 Gibt den Namen der Sicherungsdatei an, die Sie wiederherstellen.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -DataSourceId \<string>  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -ConnectionString \<string>  
 Gibt die Verbindungszeichenfolge mit einer Analysis Services-Remoteinstanz an.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### DataSourceType - \<AS.RestoreDataSourceType>  
 Gibt an, ob die Datenquelle remote oder lokal ist, basierend auf dem Speicherort der Partition.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -Ordner \<AS.RestoreFolder>  
 Gibt Partitionsordner auf der lokalen oder Remoteinstanz an.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -AsTemplate \<SwitchParameter>  
 Gibt an, ob das Objekt im Arbeitsspeicher erstellt und zurückgegeben werden soll.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -Server \<string>  
 Gibt die Analysis Services-Instanz an, zu der das Cmdlet eine Verbindung herstellt und auf der es ausgeführt wird. Wenn kein Servername angegeben wird, wird eine Verbindung mit localhost hergestellt. Für Standardinstanzen geben Sie nur den Servernamen an. Verwenden Sie für benannte Instanzen das Format "servername\instanzenname". Verwenden Sie für HTTP-Verbindungen das Format "http[s]://server[:port]/virtualdirectory/msmdpump.dll".  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|localhost|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -Credential \<PSCredential>  
 Dieser Parameter wird für die Übergabe in einem Benutzernamen und einem Kennwort verwendet, wenn eine HTTP-Verbindung zu einer Analysis Services-Instanz verwendet wird, für die HTTP-Zugriff konfiguriert wurde. Weitere Informationen finden Sie unter [Configure HTTP Access to Analysis Services on Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure http access to analysis services on iis 8.0.md) (Konfigurieren von HTTP-Zugriff auf Analysis Services unter Internetinformationsdienste [IIS] 8.0) und [PowerShell-Skripts in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md) für HTTP-Verbindungen.  
  
 Wenn dieser Parameter angegeben wird, werden der Benutzername und das Kennwort verwendet, um eine Verbindung mit der angegebenen Analysis-Server-Instanz herzustellen. Wenn keine Anmeldeinformationen angegeben sind, wird das Standard-Windows-Konto des Benutzers, der das Tool ausführt, verwendet.  
  
 Um diesen Parameter zu verwenden, erstellen Sie zuerst mit Get-Credential ein PSCredential-Objekt, um den Benutzernamen und das Kennwort anzugeben (z.B. `$Cred=Get-Credential “adventure-works\bobh”`. Sie können dieses Objekt dann an den –Credential-Parameter `(-Credential:$Cred` weitergeben).  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|True (ByValue)|  
|Platzhalterzeichen akzeptieren?|false|  
  
## Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|InclusionThresholdSetting|  
|Ausgaben|InclusionThresholdSetting|  
  
## Beispiele  
  
## Siehe auch  
 [PowerShell-Skripterstellung in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)   
 [Verwalten von tabellarischen Modellen mit PowerShell](http://go.microsoft.com/fwlink/?linkID=227685)  
  
  