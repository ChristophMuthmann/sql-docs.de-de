---
title: Merge-Partition-Cmdlet | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e5ca667b3172de982ea98a6d13c1fe6f810377b8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="merge-partition-cmdlet"></a>Merge-Partition-Cmdlet
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Führt die Daten von einer oder mehreren Quellpartitionen zu einer Zielpartition zusammen und löscht dann die Quellpartitionen.  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
## <a name="syntax"></a>Syntax  
 `Merge-ASDatabase [-Name] <string> [-SourcePartitions] <System.String[]> -Database <string> -Cube <string> -MeasureGroup <string> [-Server <string>] [-Credentials <PSCredential>] [<CommonParameters>]`  
  
 `Merge-ASDatabase -TargetPartition <Microsoft.AnalysisServices.Partition> [-SourcePartitions] <System.String[]> -Database <string> -Cube <string> -MeasureGroup <string> [-Server <string>] [-Credentials <PSCredential>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Das Merge-Partition-Cmdlet führt die Daten von einer oder mehreren Quellpartitionen zu einer Zielpartition zusammen und löscht dann die Quellpartitionen. Partitionen können nur zusammengeführt werden, wenn sie sämtliche der folgenden Kriterien erfüllen:  
  
-   Die Partitionen sind in der gleichen Measuregruppe.  
  
-   Die Partitionen sind auf dem gleichen Computer.  
  
-   Die Partitionen haben den gleichen (MOLAP, HOLAP und ROLAP für mehrdimensionale Datenbanken).  
  
## <a name="parameters"></a>Parameter  
  
### <a name="-name-string"></a>-Namen \<Zeichenfolge >  
 Gibt die Zielpartition an, mit der die Quellpartitionsdaten zusammengeführt werden. Die Partition muss bereits vorhanden sein.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-sourcepartition-string"></a>-SourcePartition \<Zeichenfolge >  
 Gibt die Quellpartition an, die mit der Zielpartition zusammengeführt wird. Sie können eine durch Kommas getrennte Liste der Partitionen erstellen, die Sie zusammenführen möchten. Verwenden Sie eine Variable, um die Liste zu speichern. Zum Beispiel: $Sources=”Sales_2008”, "Sales_2009”, "Sales_2010”.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|1|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-database-string"></a>-Datenbank \<Zeichenfolge >  
 Gibt die Datenbank an, zu der die Partitionen gehören.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-cube-string"></a>-Cube \<Zeichenfolge >  
 Gibt den Cube an, zu dem die Partitionen gehören.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-measuregroup-string"></a>Der MeasureGroup - \<Zeichenfolge >  
 Gibt die Measuregruppe an, zu der die Partition gehört.  
  
|||  
|-|-|  
|Erforderlich?|true|  
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
 Dieser Parameter wird für die Übergabe in einem Benutzernamen und einem Kennwort verwendet, wenn eine HTTP-Verbindung zu einer Analysis Services-Instanz verwendet wird, für die HTTP-Zugriff konfiguriert wurde. Weitere Informationen finden Sie unter [HTTP-Zugriff auf Analysis Services unter Internetinformationsdienste (IIS) konfigurieren &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md) für HTTP-Verbindungen.  
  
 Wenn dieser Parameter angegeben wird, werden der Benutzername und das Kennwort verwendet, um eine Verbindung mit der angegebenen Analysis-Server-Instanz herzustellen. Wenn keine Anmeldeinformationen angegeben sind, wird das Standard-Windows-Konto des Benutzers, der das Tool ausführt, verwendet.  
  
 Um diesen Parameter verwenden zu können, müssen Sie zuerst ein PSCredential-Objekt erstellen. Hierbei verwenden Sie Get-Credential, um den Benutzernamen und das Passwort anzugeben (z.B. `$Cred=Get-Credential “adventure-works\bobh”`). Sie können dieses Objekt anschließend an den –Credential-Parameter `(-Credential:$Cred`) übergeben.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|True (ByValue)|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-targetpartition-microsoftanalysisservicespartition"></a>-TargetPartition \<das Microsoft.AnalysisServices.Partition >  
 Gibt die Zielpartition an, mit der die Quellpartitionen zusammengeführt werden.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|true|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters>  
 Dieses Cmdlet unterstützt die gängigen Parameter: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer und -OutVariable. Weitere Informationen finden Sie unter [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|System.string|  
|Ausgaben|Keine|  
  
## <a name="example-1"></a>Beispiel 1  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups\sales orders\partitions> $Source=”Total_Orders_2001”, “Total_Orders_2002”, “Total_Orders_2003”` `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups\sales orders\partitions> Merge-Partition –Name “Total_Orders_2004” –SourcePartitions:$Source –database “AWTEST” –cube “Adventure Works” –MeasureGroup “Sales Orders”`  
  
 Dieser Befehl führt Partitionen von 2001, 2002 und 2003 mit der Partition für 2004 zusammen und löscht dann die Partitionen der vorherigen Jahre.  
  

  
