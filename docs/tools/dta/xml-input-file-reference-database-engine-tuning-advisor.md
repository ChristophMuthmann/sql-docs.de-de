---
title: "XML-Eingabedateireferenz (Datenbankoptimierungsratgeber) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "XML"
helpviewer_keywords: 
  - "Datenbankoptimierungsratgeber [SQL Server], XML-Eingabedateien"
  - "Eingabedateireferenz [Datenbankoptimierungsratgeber]"
  - "XML-Eingabedateien [Datenbankoptimierungsratgeber]"
ms.assetid: 05e5e5f0-d6df-4336-b18e-e9bc2835a766
caps.latest.revision: 26
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 26
---
# XML-Eingabedateireferenz (Datenbankoptimierungsratgeber)
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber kann mithilfe einer XML-Eingabedatei eine Datenbank optimieren. Anhand dieser XML-Datei wird festgelegt, welche Datenbanken, Tabellen, Arbeitsauslastungsdateien oder -tabellen und Optimierungsoptionen für die Optimierungssitzung verwendet werden sollen. Außerdem können Sie mit dieser Datei eine vom Benutzer angegebene Konfiguration zum Ausführen von Was-wäre-wenn-Analysen festlegen.  
  
 In XML-Eingabedateien des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgebers befinden sich hierarchisch angeordnete XML-Elemente mit Text oder anderen Elementen, die die Einstellungen der Optimierungssitzung angeben. Die XML-Eingabedatei des [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Optimierungsratgebers muss den Standards für wohlgeformte XML-Dokumente entsprechen, d. h., dass bei allen Elementnamen die Groß-/Kleinschreibung beachtet wird. Die Groß-/Kleinschreibung der Elemente ist wie in Pascal. Das bedeutet, dass das erste Zeichen ein Großbuchstabe und der erste Buchstabe eines nachfolgenden verketteten Worts ein Großbuchstabe ist.  
  
 Alle Elementwerte müssen den XML-Benennungskonventionen entsprechen. Weitere Informationen zu diesen Konventionen finden Sie unter [XML-Textinhalt](http://go.microsoft.com/fwlink/?LinkId=7614) in der MSDN Library.  
  
 Beachten Sie, dass dies keine vollständige Referenz ist. Informationen zu allen Elementen, die Sie zum Definieren von XML-Eingabedateien verwenden können, finden Sie im XML-Schema DTASchema.xsd des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgebers.  
  
## XML-Deklaration  
  
-   [XML-Daten &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
## DTAXML-Stammelement  
  
-   [DTAXML-Element &#40;DTA&#41;](../../tools/dta/dtaxml-element-dta.md)  
  
## DTAInput-Elemente  
  
-   [DTAInput-Element &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)  
  
-   [Server-Element &#40;DTA&#41;](../../tools/dta/server-element-dta.md)  
  
-   [Workload-Element &#40;DTA&#41;](../../tools/dta/workload-element-dta.md)  
  
-   [TuningOptions-Element &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)  
  
-   [Configuration-Element &#40;DTA&#41;](../../tools/dta/configuration-element-dta.md)  
  
## Serverelemente  
  
-   [Name-Element für Server &#40;DTA&#41;](../../tools/dta/name-element-for-server-dta.md)  
  
-   [Database-Element für Server &#40;DTA&#41;](../../tools/dta/database-element-for-server-dta.md)  
  
## Arbeitsauslastungselemente  
  
-   [File-Element &#40;DTA&#41;](../../tools/dta/file-element-dta.md)  
  
-   [Database-Element zur Arbeitsauslastung &#40;DTA&#41;](../../tools/dta/database-element-for-workload-dta.md)  
  
-   [EventString-Element &#40;DTA&#41;](../../tools/dta/eventstring-element-dta.md)  
  
## Optimierungsoptionselemente  
  
-   [TuningTimeInMin-Element &#40;DTA&#41;](../../tools/dta/tuningtimeinmin-element-dta.md)  
  
-   [StorageBoundInMB-Element &#40;DTA&#41;](../../tools/dta/storageboundinmb-element-dta.md)  
  
-   [TestServer-Element &#40;DTA&#41;](../../tools/dta/testserver-element-dta.md)  
  
-   [FeatureSet-Element &#40;DTA&#41;](../../tools/dta/featureset-element-dta.md)  
  
-   [Partitioning-Element &#40;DTA&#41;](../../tools/dta/partitioning-element-dta.md)  
  
-   [DropOnlyMode-Element &#40;DTA&#41;](../../tools/dta/droponlymode-element-dta.md)  
  
-   [KeepExisting-Element &#40;DTA&#41;](../../tools/dta/keepexisting-element-dta.md)  
  
-   [OnlineIndexOperation-Element &#40;DTA&#41;](../../tools/dta/onlineindexoperation-element-dta.md)  
  
-   [DatabaseToConnect-Element &#40;DTA&#41;](../../tools/dta/databasetoconnect-element-dta.md)  
  
## Konfigurationselemente  
  
-   [Server-Element für Konfiguration &#40;DTA&#41;](../../tools/dta/server-element-for-configuration-dta.md)  
  
-   [Database-Element für Konfiguration &#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md)  
  
-   [Recommendation-Element &#40;DTA&#41;](../../tools/dta/recommendation-element-dta.md)  
  
-   [Create-Element &#40;DTA&#41;](../../tools/dta/create-element-dta.md)  
  
-   [Index-Element &#40;DTA&#41;](../../tools/dta/index-element-dta.md)  
  
-   [Name-Element für Index &#40;DTA&#41;](../../tools/dta/name-element-for-index-dta.md)  
  
-   [Column-Element für Index &#40;DTA&#41;](../../tools/dta/column-element-for-index-dta.md)  
  
-   [Name-Element für Spalte &#40;DTA&#41;](../../tools/dta/name-element-for-column-dta.md)  
  
-   [Filegroup-Element für Index &#40;DTA&#41;](../../tools/dta/filegroup-element-for-index-dta.md)  
  
## Datenbankelemente  
  
-   [Name-Element für Datenbank &#40;DTA&#41;](../../tools/dta/name-element-for-database-dta.md)  
  
-   [Schema-Element für Datenbank &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)  
  
-   [Namen-Element für Schema &#40;DTA&#41;](../../tools/dta/name-element-for-schema-dta.md)  
  
-   [Table-Element für Schema &#40;DTA&#41;](../../tools/dta/table-element-for-schema-dta.md)  
  
-   [Name-Element für Tabelle &#40;DTA&#41;](../../tools/dta/name-element-for-table-dta.md)  
  
## Siehe auch  
 [Datenbankoptimierungsratgeber](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  