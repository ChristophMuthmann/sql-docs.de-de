---
title: "SQLServer R Services Optimieren der Leistung | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cf6f3b7d-f9f9-4e45-b0d1-07850b53e0c5
caps.latest.revision: 20
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 19
---
# SQLServer R Services Optimieren der Leistung
[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] bietet eine Plattform für die Entwicklung von intelligenten Clientanwendungen, die neue Einblicke. Der Datenanalyse können die Leistungsfähigkeit der R-Sprache zu trainieren und Erstellen von Modellen, die in gespeicherte Daten [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Nachdem das Modell für die Produktion bereit ist, kann einem Datenanalysten Datenbankadministratoren und SQL-Entwickler zum Bereitstellen ihrer Lösung in der Produktion verwenden. Die Informationen in diesem Abschnitt erfahren Sie hohe Ebene für das Optimieren der Leistung sowohl beim Erstellen und Trainieren von Modellen und beim Bereitstellen von Modellen für die Produktion.

Die Informationen in diesem Dokument wird davon ausgegangen, dass Sie mit vertraut sind [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] Konzepte und Terminologie. Allgemeine Informationen zu R Services finden Sie unter [SQL Serverdienste R](../../advanced-analytics/r-services/sql-server-r-services.md).

> [!NOTE]
> Ein Großteil der Informationen in diesem Abschnitt allgemeine Anleitung zum Konfigurieren von zwar [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], einige Informationen sind spezifisch für analytische Funktionen RevoScaleR.

## In diesem Abschnitt

* [SQL Server-Konfiguration](../../advanced-analytics/r-services/sql-server-configuration-r-services.md): Dieses Dokument enthält Hinweise zum Konfigurieren der Hardware, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] installiert ist. Es ist besonders nützlich für __Datenbankadministratoren__.

* [R und Datenoptimierung](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md): Dieses Dokument bietet einen Leitfaden zur Verwendung von R-Skripts mit R-Dienste. Es ist besonders nützlich für __Datenanalysten__.

* [Leistung-Fallstudie](../../advanced-analytics/r-services/performance-case-study-r-services.md): Dieses Dokument enthält Daten für Tests und R-Skripts, die zum Testen der Auswirkungen der Anweisungen in den vorherigen Dokumenten verwendet werden können.

## Verweise

Im folgenden sind Links zu Informationen, die bei der Entwicklung dieses Dokuments verwendet.

* [Gewusst wie: Bestimmen der geeigneten Auslagerungsdateigröße für 64-Bit-Versionen von Windows](https://support.microsoft.com/kb/2860880)

* [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md)

* [Aktivieren der Komprimierung für eine Tabelle oder einen Index](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

* [Deaktivieren der Komprimierung für eine Tabelle oder einen Index](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

* [DISKSPD Speicher Load Generator/Leistung Test-tool](https://github.com/microsoft/diskspd)

* [FSUtil-Dienstprogramm-Referenz](https://technet.microsoft.com/library/cc753059.aspx)

* [Neuorganisieren und Neuerstellen von Indizes](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

* [R Services](../../advanced-analytics/r-services/r-services.md)

* [Optimieren von Leistungsoptionen für RxDForest und rxDTree](https://support.microsoft.com/kb/3104235)

* [Überwachen und Optimieren der Leistung](../../relational-databases/performance/monitor-and-tune-for-performance.md)

* [RevoScaleR-Benutzerhandbuch](https://packages.revolutionanalytics.com/doc/7.0.0/win/RevoScaleR_Users_Guide.pdf)

* [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)

## Siehe auch

 
 [SQL Server-Konfiguration für R-Dienste](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [Fallstudie zur Leistung](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 
 [R und Datenoptimierung](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)