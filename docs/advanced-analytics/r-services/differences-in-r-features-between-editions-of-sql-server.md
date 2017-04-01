---
title: "R-Funktionen Unterschiede zwischen SQLServer-Editionen | Microsoft Docs"
ms.custom: ""
ms.date: "01/19/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8b33a3e2-04d3-4bad-9335-9568ae09db0b
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# R-Funktionen Unterschiede zwischen SQLServer-Editionen
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] steht in den folgenden Editionen von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
-   **Enterprise Edition**  
    
     Umfasst sowohl R-Dienste, für die Analyse der in der Datenbank in SQL Server 2016 sowie R Server (eigenständig) unter Windows, die Verbindung mit einer Vielzahl von Datenbanken und Daten für die Analyse zur angemessenen verwendet werden können, aber die in der Datenbank nicht ausgeführt. Umfasst auch **DeployR**, die R-Skripts und Modelle als Webdienst bereitstellen verwendet werden können.  

     Keine Einschränkungen. Optimierte Leistung und Skalierbarkeit durch die Parallelisierung und streaming. Suopprts Analyse von großen Datasets, die nicht in den verfügbaren Arbeitsspeicher, mithilfe der **ScaleR** Funktionen.  
  
     In der Datenbank-Analysen in SQL Server unterstützt die Ressourcenkontrolle des externen Skripts Serverressourcenverwendung anpassen.  
  
-   **Developer Edition**  

    Dieselben Funktionen wie Enterprise Edition; Developer Edition kann jedoch nicht in produktionsumgebungen verwendet werden.  

  
  
-   **Standard Edition**  
  
     Verfügt über alle Funktionen der Analyse, die in der Datenbank mit Ausnahme der flexiblen Ressourcenkontrolle mit Enterprise Edition enthalten. Leistung und Skalierung wird auch begrenzt: die Daten, die verarbeitet werden können, wurde im Arbeitsspeicher des Servers an und Verarbeitung an einen einzelnen Compute-Thread beschränkt ist, auch bei Verwendung der **ScaleR** Funktionen.
  
-   **Express-Editionen**  
  
     Nur Express Edition with Advanced Services stellt R-Dienste. Die leistungseinschränkungen ähneln Standard Edition.  
  
 Weitere Informationen zu anderen Produktfeatures finden Sie unter [von den Editionen von SQL Server 2016 unterstützte Funktionen](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  

> [!NOTE]
>
> + Microsoft R Open ist in allen Editionen enthalten.
> + Microsoft-R-Client können mit allen Editionen arbeiten.
  
## Enterprise Edition  
 Leistung von R-Lösungen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sollten im Allgemeinen besser als alle herkömmlichen R-Implementierung, erhalten dieselbe Hardware, da R Verwendung von Serverressourcen ausgeführt werden kann, und manchmal mit mehreren Prozessen, die mit verteilten die **ScaleR** Funktionen.  
  
 Benutzer können auch erwarten erhebliche Unterschiede in der Leistung und Skalierbarkeit für die gleichen R-Funktionen im Vs Enterprise Edition ausgeführt. Standard Edition. Gründe Unterstützung für parallele Verarbeitung, streaming und erhöhte Threads für die Verarbeitung von R-Worker verfügbar.  
  
 Leistung selbst bei identischer Hardware kann jedoch von vielen Faktoren außerhalb der R-Code, einschließlich konkurrierende Belastung der Serverressourcen, der Typ der Abfrageplan, der erstellt wird, Schema geändert wird, beeinflusst werden Statistiken aktualisieren oder erstellen Sie einen neuen Abfrageplan und Fragmentierung müssen. Es ist möglich, dass eine gespeicherte Prozedur mit R-Code in wenigen Sekunden unter einer Arbeitslast ausgeführt, aber nehmen, wenn Minuten andere Dienste ausgeführt.  Aus diesem Grund wird empfohlen, dass Sie mehrere Aspekte der serverleistung, einschließlich Netzwerke für remote Compute-Kontexte quantifizieren R Leistung überwachen.  

Zudem wird empfohlen, dass Sie konfigurieren [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md) (verfügbar in der Enterprise Edition) die Art und Weise anpassen, die R-Aufträge sind oder unter starker Serverarbeitslasten behandelt. Sie können Klassifizierungsfunktionen Geben Sie die Quelle des Auftrags, R und bestimmte Arbeitslasten zu priorisieren, die Menge des Arbeitsspeichers von SQL-Abfragen definieren und steuern die Anzahl der parallelen Prozessen pro Arbeitslast verwendet.  
  
## Developer Edition  
 Developer Edition bietet die Leistung, die Enterprise Edition. Verwenden der Developer Edition wird jedoch nicht für produktionsumgebungen unterstützt.  
  
  
## Standard Edition  
 Auch Standard Edition bieten einige Leistungsvorteil, im Vergleich zu standard R-Pakete, die gleiche Hardwarekonfiguration angegeben.  
  
 Standard Edition unterstützt jedoch nicht die Ressourcenkontrolle. Verwenden die Ressourcenkontrolle ist die beste Methode zum Anpassen von Serverressourcen für die Unterstützung von unterschiedlichen R-Workloads wie Modell trainieren und bewerten.  
  
 Standard Edition bietet auch nur eine eingeschränkte Leistung und Skalierbarkeit im Vergleich zu Enterprise und Developer Edition. Insbesondere alle die **ScaleR** Funktionen und Pakete sind in der Standard Edition enthalten, aber der Dienst, der gestartet und R-Skripts verwaltet ist beschränkt die Anzahl der Prozesse, die sie verwenden kann. Darüber hinaus müssen vom Skript verarbeitet Daten in den Arbeitsspeicher passen.  
  
  
## Express Edition with Advanced Services  
 Express Edition unterliegt denselben Einschränkungen wie Standard Edition.  
  
## Siehe auch  
 [Von den SQL Server 2016-Editionen unterstützte Funktionen](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
  
  