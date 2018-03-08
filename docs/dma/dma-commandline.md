---
title: "Führen Sie von der Befehlszeile (SQL Server Data Migration Assistant) | Microsoft Docs"
ms.custom: 
ms.date: 09/01/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: sql-dma
ms.tgt_pltfrm: 
ms.topic: article
keywords: 
helpviewer_keywords: Data Migration Assistant, Command Line
ms.assetid: 
caps.latest.revision: 
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6147d01802a363082baf27d6b909e2c98f9afef2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>Führen Sie Daten Migrations-Assistenten aus, über die Befehlszeile
In Version 2.1 und höher, wenn Sie Daten Migration Assistant, installieren sie installieren außerdem dmacmd.exe in *"% ProgramFiles%"\\Microsoft Data Migration Assistant\\*. Verwenden Sie dmacmd.exe zur Bewertung Ihrer Datenbanken in einem unbeaufsichtigten Modus, und geben Sie das Ergebnis in JSON oder CSV-Datei. Dies ist besonders nützlich, wenn mehrere Datenbanken oder große Datenbanken zu bewerten. 

> [!NOTE]
> Dmacmd.exe unterstützt nur Bewertungen ausgeführt. Migrationen werden zu diesem Zeitpunkt nicht unterstützt.


## <a name="command-line-arguments"></a>Befehlszeilenargumente

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```


|Argument  |Description  | Erforderlich (J/N)
|---------|---------|---------------|
| `/help or /?`     | Zum Verwenden von dmacmd.exe-Hilfetext        | N
|`/AssessmentName`     |   Name des Projekts assessment   | J
|`/AssessmentDatabases`     | Durch Leerzeichen getrennte Liste von Verbindungszeichenfolgen. Der Datenbankname (Ursprünglicher Katalog) ist Groß-/Kleinschreibung beachtet. | J
|`/AssessmentTargetPlatform`     | Die Zielplattform für die Bewertung, unterstützte Werte: SqlServer2012, SqlServer2014, SqlServer2016 und AzureSqlDatabaseV12. Standardmäßig wird SqlServer2016   | N
|`/AssessmentEvaluateFeatureParity`  | Führen Sie die Parität Funktionsregeln  | N
|`/AssessmentEvaluateCompatibilityIssues`     | Führen Sie Kompatibilitätsregeln  | J <br> (AssessmentEvaluateCompatibilityIssues oder AssessmentEvaluateRecommendations ist erforderlich.)
|`/AssessmentEvaluateRecommendations`     | Führen Sie die Funktion Empfehlungen        | J <br> (AssessmentEvaluateCompatibilityIssues oder AssessmentEvaluateRecommendationsis erforderlich)
|`/AssessmentOverwriteResult`     | Überschreiben Sie die Ergebnisdatei    | N
|`/AssessmentResultJson`     | Vollständiger Pfad in die JSON-Ergebnisdatei     | J <br> (AssessmentResultJson oder AssessmentResultCsv ist erforderlich)
|`/AssessmentResultCsv`    | Vollständiger Pfad in der CSV-Ergebnisdatei   | J <br>(AssessmentResultJson oder AssessmentResultCsv ist erforderlich)




## <a name="examples"></a>Beispiele

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Mithilfe der Windows-Authentifizierung und Ausführung Kompatibilitätsregeln einzelnen Datenbank-Bewertung**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***Integrated Security=true*"**
***/AssessmentEvaluateCompatibilityIssues*** /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```



**Mithilfe von SQL Server-Authentifizierung und Ausführung Feature Empfehlung einzelnen Datenbank-Bewertung**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***User Id=myUsername;Password=myPassword;***"
***/AssessmentEvaluateRecommendations*** /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```


**Single-Datenbank-Bewertung für SQL Server 2012-Zielplattform und Ergebnisse zu JSON und CSV-Datei speichern**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
***/AssessmentTargetPlatform="SqlServer2012"***
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
***/AssessmentResultJson***="C:\\temp\\Results\\AssessmentReport.json"
***/AssessmentResultCsv***="C:\\temp\\Results\\AssessmentReport.csv"
```


**Bewertung der einzelnen Datenbank Zielplattform SQL Azure-Datenbank Ergebnisse in JSON und CSV-Datei speichern**

```
DmaCmd.exe /AssessmentName="TestAssessment" 
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="AzureSqlDatabaseV12"
/AssessmentEvaluateCompatibilityIssues /AssessmentEvaluateFeatureParity
/AssessmentOverwriteResult 
/AssessmentResultCsv="C:\\temp\\AssessmentReport.csv" 
/AssessmentResultJson="C:\\temp\\AssessmentReport.json"
```


**Bewertung von mehreren Datenbanken**

```
DmaCmd.exe /AssessmentName="TestAssessment"
***/AssessmentDatabases="Server=SQLServerInstanceName1;Initial
Catalog=DatabaseName1;Integrated Security=true"
"Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated
Security=true" "Server=SQLServerInstanceName2;Initial
Catalog=DatabaseName3;Integrated Security=true"***
/AssessmentTargetPlatform="SqlServer2016"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
/AssessmentResultJson="C:\\Results\\test2016.json"
```



## <a name="see-also"></a>Siehe auch

[Herunterladen von Daten Migrations-Assistent](https://www.microsoft.com/download/details.aspx?id=53595)
