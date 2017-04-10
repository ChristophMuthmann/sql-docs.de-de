---
title: "Invoke-ProcessTable-Cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 865e6d06-b99a-41f3-9d6f-c3c97b529b23
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Invoke-ProcessTable-Cmdlet
  Wendet den Vorgang **Verarbeiten** mit einem bestimmten **RefreshType** auf eine **Tabelle** an.  
  
 Dieses Cmdlet gilt nur für tabellarische Modelle auf der SQL Server 2016-Kompatibilitätsebene 1200.  
  
## Syntax  
 `Invoke-ProcessTable [-DatabaseName] <string> [-TableName] <string> [-RefreshType] <RefreshType> {Full |     ClearValues | Calculate | DataOnly | Automatic | Add | Defragment} [-Server <string>] [-Credential <pscredential>     [-WhatIf] [-Confirm]  [<CommonParameters>]`  
  
 `Invoke-ProcessTable -RefreshType <RefreshType> {Full | ClearValues | Calculate | DataOnly | Automatic | Add |     Defragment} -Table <Table> [-Server <string>] [-Credential <pscredential>] [-WhatIf] [-Confirm]     [<CommonParameters>]`  
  
## Parameter  
  
### -TableName \<string>  
 Der Name der Tabelle, der die zu verarbeitende Partition angehört.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -DatabaseName \<string>  
 Gibt die Datenbank an, zu der die Tabelle gehört.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -Server\<Microsoft.AnalysisSevices.Server>  
 Gibt optional die Serverinstanz an, mit der eine Verbindung hergestellt werden soll, wenn Sie nicht das **SQLAS** -Anbieterverzeichnis für den Kontext verwenden.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -RefreshType \<Microsoft.AnalysisServices.RefreshType>  
 Gibt den Prozesstyp für eine tabellarische Datenbank mit dem Kompatibilitätsgrad 1200 an.  Gültige Werte sind „Full“, „ClearValues“, „Calculate“, „DataOnly“, „Automatic“, „Add“ und „Defragment“. Beschreibungen und Anleitungen finden Sie unter [Verarbeiten von Datenbank, Tabelle oder Partition &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md).  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|1|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -Credential  
 Wenn dieser Parameter angegeben wird, werden der übergebene Benutzername bzw. das übergebene Kennwort verwendet, um eine Verbindung mit der Analysis Services-Instanz herzustellen. Wenn keine Anmeldeinformationen angegeben sind, wird das Windows-Standardkonto des Benutzers verwendet, der das Skript ausführt.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -Whatif  
 Verwenden Sie diesen Parameter, um Informationen über die Auswirkungen des Vorgangs zu erhalten, bevor er ausgeführt wird.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -Confirm  
 Verwenden Sie diesen Parameter, um den Vorgang interaktiv mit "Ja" oder "Nein" zu bestätigen, bevor er ausgeführt wird.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?||  
|Standardwert||  
|Pipelineeingabe akzeptieren?||  
|Platzhalterzeichen akzeptieren?|false|  
  
## Beispiel 1  
 `PS SQLSERVER:\SQLAS\MachineName\Instance\Databases\DB1\> Invoke-ProcessTable -TableName "myTable" -Database "DB1"  -RefreshType "Full"`  
  
 Dieser Befehl wird bis in die Identität der zu verarbeitenden Tabelle weitergereicht.  
  
## Beispiel 2  
 `PS SQLSERVER:\SQLAS\MachineName\Instance\Databases\DB1\> Invoke-ProcessTable -TableName "myTable" -Database "DB1"  -RefreshType [Microsoft.AnalysisServices.Tabular.RefreshType]::Full`  
  
 Dieser Befehl verarbeitet eine tabellarische Metadatentabelle mit einem **enum**-Aktualisierungstyp.  
  
## Siehe auch  
 [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  