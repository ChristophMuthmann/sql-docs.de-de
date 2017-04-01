---
title: "Data Quality-Projekte (DQS) | Microsoft Docs"
ms.custom: ""
ms.date: "10/01/2012"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a43fc9c0-19b6-414a-8661-4c7c55e0c03e
caps.latest.revision: 16
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 16
---
# Data Quality-Projekte (DQS)
  Ein Data Quality-Projekt in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) ist eine Wissensdatenbank zu verwenden, um die Qualität der Quelldaten durch Ausführen *DatenBereinigung* und *Datenabgleich* Aktivitäten und anschließend die resultierenden Daten einer SQL Server-Datenbank oder eine CSV-Datei exportieren. Sie können ein Data Quality-Projekt als Bereinigungsprojekt oder Abgleichsprojekt erstellen, um jeweilige Aktivitäten auszuführen. Bereinigung und Abgleichsprojekte können mit der gleichen Wissensdatenbank ausgeführt werden, da Wissen für Datenbereinigung und das Abgleichen in die gleiche Wissensdatenbank integriert werden können.  
  
 Ein Data Quality-Projekt hat die folgenden Vorteile:  
  
-   Data Quality-Projekte ermöglichen es Ihnen, die Quelldaten mithilfe von Wissen in einer DQS-Wissensdatenbank zu bereinigen.  
  
-   Sie können Datenabgleiche für Ihre Quelldaten durchführen, indem Sie die Abgleichsrichtlinie in einer Wissensdatenbank verwenden.  
  
-   Stellt einen Assistenten bereit, um Sie durch die Bereinigungs- und Abgleichsaktivitäten zu führen und exportiert die Daten gemäß Ihrer Auswahl in eine SQL Server-Datenbank oder eine CSV-Datei. Der Data Steward kann das Data Quality-Projekt verwenden, um die computergestützten/interaktiven Schritte zum Bereinigen und Abgleichen von Daten auszuführen.  
  
##  <a name="Cleansing"></a> Data Quality-Projekt: Bereinigungsaktivität  
 Data Quality-Projekte ermöglichen es Ihnen, die Quelldaten basierend auf einer Wissensdatenbank zu bereinigen. Die Datenbereinigungsaktivität in DQS ist ein zwei Schritte umfassender Prozess:  
  
1.  Ein *computergestützten* datenbereinigungsprozess, der Quelldaten mit den Informationen in der Wissensdatenbank analysiert und Änderungen vorschlägt. Die verarbeiteten Daten werden von DQS kategorisiert (vorgeschlagen, neu, ungültig und richtig) und werden dem Benutzer zur weiteren Verarbeitung angezeigt.  
  
2.  Ein *interaktive* Bereinigung Prozess, mit dem Data Steward genehmigen, ablehnen oder ändern Sie die Daten, die von der computergestützten datenbereinigungsprozess vorgeschlagen.  
  
 Ausführliche Informationen zur Bereinigungsaktivität in einem Data Quality-Projekt finden Sie unter [Data Cleansing](../data-quality-services/data-cleansing.md).  
  
##  <a name="Matching"></a> Data Quality-Projekt: Abgleichsaktivität  
 Ein Data Quality-Abgleichsprojekt ermöglicht es Ihnen, Abgleichsaktivitäten auf Grundlage der Abgleichsrichtlinie in einer Wissensdatenbank auszuführen, um Datenduplizierung durch das Identifizieren exakter und ungefährer Treffer zu verhindern und dadurch das Entfernen doppelter Daten zu ermöglichen. Es wird empfohlen, dass Sie die Daten bereinigen, bevor Sie entsprechende Abgleiche ausführen. Gehen Sie folgendermaßen vor:  
  
1.  Erstellen Sie ein Data Quality-Projekt, wählen Sie die **Bereinigungsaktivität** aus, schließen Sie die Datenbereinigungsaktivität für die Quelldaten ab, und exportieren Sie sie dann in eine Tabelle in einer SQL Server-Datenbank.  
  
2.  Erstellen Sie ein weiteres Data Quality-Projekt mithilfe einer Wissensdatenbank, die eine Abgleichsrichtlinie enthält, wählen Sie die **Abgleichsaktivität** aus, und wählen Sie dann auf der Seite **Struktur** die Datenbank und die Tabelle aus, in die Sie die gereinigten Daten in Schritt 1 exportiert haben.  
  
3.  Schließen Sie die Abgleichsaktivität für die bereinigten Daten ab.  
  
 Ausführliche Informationen zur Abgleichsaktivität in einem Data Quality-Projekt finden Sie unter [Data Matching](../data-quality-services/data-matching.md).  
  
##  <a name="ProfilingNotification"></a> Datenprofilerstellung und Benachrichtigungen  
 Beim Ausführen der Bereinigungs- und Abgleichsaktivitäten in einem Data Quality-Projekt werden Ihnen Statistiken und Informationen über die von DQS verarbeiteten Daten in Echtzeit angezeigt. Mithilfe der Datenprofilerstellung können Sie die Effektivität der Bereinigungs- und Abgleichsprozesse bewerten und potenziell bestimmen, inwiefern die Datenbereinigung oder der -abgleich dabei behilflich waren, die Datenqualität zu verbessern. DQS-profilerstellung stellt zwei Data Quality-Dimensionen bereit: *Vollständigkeit* (das Ausmaß, zu dem Daten vorhanden sind) und *Genauigkeit* (das Ausmaß, in dem Daten für den beabsichtigten Zweck verwendet werden können). Außerdem werden auf Grundlage der Datenprofilinformationen dem Benutzer Benachrichtigungen zu den Aktionen angezeigt, die ausgeführt werden können, um die Datenbereinigungs- und Datenabgleichsvorgänge zu verbessern. Weitere Informationen zur Datenprofilerstellung und zu Benachrichtigungen finden Sie unter [Data Profiling and Notifications in DQS](../data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
## Verwandte Aufgaben  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Beschreibt, wie ein Data Quality-Projekt erstellt wird.|[Erstellen eines Data Quality-Projekts](../data-quality-services/create-a-data-quality-project.md)|  
|Beschreibt das Öffnen, nicht entsperren, umbenennen und Löschen eines Data Quality-Projekts.|[Öffnen, nicht entsperren, umbenennen und Löschen eines Data Quality-Projekts](https://msdn.microsoft.com/library/hh510417.aspx)|  
|Beschreibt, wie ein Integration Services-Projekt in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]geöffnet wird.|[Öffnen von Integration Services-Projekten im Data Quality-Client](../data-quality-services/open-integration-services-projects-in-data-quality-client.md)|  
  
## Siehe auch  
 [DQS-Wissensdatenbanken und -Domänen](../data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  