---
title: "&#220;bersicht &#252;ber die Architektur (SQL Server R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6c4a4f66-ea3e-4a73-acf2-6c8aeafc94b0
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 9
---
# &#220;bersicht &#252;ber die Architektur (SQL Server R Services)
Dieser Abschnitt enthält eine Übersicht über die Architektur von [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], einschließlich Sicherheit, neue Komponenten im SQL Server-Datenbankmodul und Support R-Komponenten und Interoperabilität von open-Source-R-Skripts in SQL Server ausgeführt wird.


## Ziele


Die Architektur des [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] die open-Source-R-Sprache unterstützt. Aktueller Benutzer von R sollte ihre R-Code Portieren und mit geringfügigen Änderungen in T-SQL ausführen können.

SQL Server-R-Services bietet jedoch auch Innovationen, die engere Integration für die Sprache R, um schneller Datendurchsatz und Verarbeitung zu ermöglichen und Hindernisse für die Entwicklung von R-Lösungen für Unternehmen zu senken und höhere Leistung bieten. Diese Innovationen umfassen open-Source und proprietären Komponenten von Microsoft entwickelt wurde.


Die Hauptziele der Integration mit SQL Server sind, verbesserte Leistung und Skalierbarkeit für R, geben Sie während der sicheren Verwaltung der Daten. Zu diesem Ziel bietet SQL Server-R-Services eine mit mehreren Prozesse Infrastruktur, die integrierte Windows-Authentifizierung und SQL-Anmeldungen kennwortbasierte unterstützt. 

+ [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] bietet eine Basis-Verteilung von R, zusammen mit den Paketen ScaleR und R Aufgaben parallel ausführen.
+ Neue Komponenten in SQL Server bieten einen sicheren, hochleistungsfähigen Rahmen zum Ausführen von externen Skripts.
+ R-Tasks außerhalb des SQL Server-Prozesses, um Sicherheit und bessere Verwaltung bereitzustellen.
+ [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] verwaltet die Sicherheit aller R-Prozesse. 

Zum Optimieren von vorhandenen R-Code und diese Verbesserungen nutzen, werden die Themen in diesem Abschnitt die neue Architektur im Detail beschrieben. Kenntnisse wie Analyse und Verarbeitung von Daten erfolgt durch [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], treffen Sie entsprechende Optionen zum Erfassen von Daten, wie effizient verarbeiten von Funktionen ausgeführt und Ergebnisse zu nutzen.
 

## In diesem Abschnitt
+ [R-Interoperabilität](../../advanced-analytics/r-services/r-interoperability-in-sql-server-r-services.md)
+ [Neue Komponenten in SQLServer für R-Dienste](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)
+ [Sicherheitsübersicht](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md)

## Siehe auch
[R Services-Lernprogramme](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)
