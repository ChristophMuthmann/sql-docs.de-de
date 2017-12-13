---
title: Cmdlet "Invoke-ProcessTable" | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 865e6d06-b99a-41f3-9d6f-c3c97b529b23
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 01d14a3ee7db466f184cb99fbb271520ab448244
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="invoke-processtable-cmdlet"></a>Invoke-ProcessTable-Cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Führt die **Prozess** -Vorgang für eine **Tabelle** mit einem bestimmten **RefreshType**.  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
## <a name="syntax"></a>Syntax  
 `Invoke-ProcessTable [-DatabaseName] <string> [-TableName] <string> [-RefreshType] <RefreshType> {Full |     ClearValues | Calculate | DataOnly | Automatic | Add | Defragment} [-Server <string>] [-Credential <pscredential>     [-WhatIf] [-Confirm]  [<CommonParameters>]`  
  
 `Invoke-ProcessTable -RefreshType <RefreshType> {Full | ClearValues | Calculate | DataOnly | Automatic | Add |     Defragment} -Table <Table> [-Server <string>] [-Credential <pscredential>] [-WhatIf] [-Confirm]     [<CommonParameters>]`  
  
## <a name="parameters"></a>Parameter  
  
### <a name="-tablename-string"></a>-TableName \<Zeichenfolge >  
 Der Name der Tabelle, der die zu verarbeitende Partition angehört.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-databasename-string"></a>DatabaseName - \<Zeichenfolge >  
 Gibt die Datenbank an, zu der die Tabelle gehört.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-servermicrosoftanalysissevicesserver"></a>-Server\<Microsoft.AnalysisSevices.Server >  
 Gibt optional die Serverinstanz an, mit der eine Verbindung hergestellt werden soll, wenn Sie nicht das **SQLAS** -Anbieterverzeichnis für den Kontext verwenden.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-refreshtype-microsoftanalysisservicesrefreshtype"></a>-RefreshType \<Microsoft.AnalysisServices.RefreshType >  
 Gibt den Prozesstyp für eine tabellarische Datenbank an.  Gültige Werte sind „Full“, „ClearValues“, „Calculate“, „DataOnly“, „Automatic“, „Add“ und „Defragment“. Beschreibungen und einen Leitfaden finden Sie unter [Verarbeiten von Datenbank, Tabelle oder Partition &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md).  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|1|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-credential"></a>-Credential  
 Wenn dieser Parameter angegeben wird, werden der übergebene Benutzername bzw. das übergebene Kennwort verwendet, um eine Verbindung mit der Analysis Services-Instanz herzustellen. Wenn keine Anmeldeinformationen angegeben sind, wird das Windows-Standardkonto des Benutzers verwendet, der das Skript ausführt.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-whatif"></a>-Whatif  
 Verwenden Sie diesen Parameter, um Informationen über die Auswirkungen des Vorgangs zu erhalten, bevor er ausgeführt wird.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-confirm"></a>-Confirm  
 Verwenden Sie diesen Parameter, um den Vorgang interaktiv mit "Ja" oder "Nein" zu bestätigen, bevor er ausgeführt wird.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?||  
|Standardwert||  
|Pipelineeingabe akzeptieren?||  
|Platzhalterzeichen akzeptieren?|false|  
  
## <a name="example-1"></a>Beispiel 1  
 `PS SQLSERVER:\SQLAS\MachineName\Instance\Databases\DB1\> Invoke-ProcessTable -TableName "myTable" -Database "DB1"  -RefreshType "Full"`  
  
 Dieser Befehl wird bis in die Identität der zu verarbeitenden Tabelle weitergereicht.  
  
## <a name="example-2"></a>Beispiel 2  
 `PS SQLSERVER:\SQLAS\MachineName\Instance\Databases\DB1\> Invoke-ProcessTable -TableName "myTable" -Database "DB1"  -RefreshType [Microsoft.AnalysisServices.Tabular.RefreshType]::Full`  
  
 Dieser Befehl verarbeitet eine tabellarische Metadatentabelle mit einem **enum** -Aktualisierungstyp.  
  
  
