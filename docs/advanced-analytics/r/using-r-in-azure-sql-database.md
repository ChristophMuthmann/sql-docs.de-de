---
title: Verwendung von R in Azure SQL-Datenbank | Microsoft Docs
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e3c781449a8f7a1b236508cd21b8c00ff175774f
ms.openlocfilehash: 619921bbf00801fd5930a1c1b110e69a9fd05a81
ms.contentlocale: de-de
ms.lasthandoff: 09/30/2017

---
# <a name="using-r-in-azure-sql-database"></a>Verwendung von R in Azure SQL-Datenbank

Ab Oktober 2017 unterstützt Azure SQL-Datenbank die Ausführung von R-Code in der Datenbank mithilfe von gespeicherten Prozeduren, ähnlich wie R Services in SQL Server 2016.

Dieser Artikel bietet einen Überblick über die Funktion und beschreibt bekannte Einschränkungen.

> [!NOTE]
> Diese Version wird eine anfängliche Preview-Version und dient zum Testen und nur durchsuchen. Über eine Produktionsversion werden einige Zeit in 2018 veröffentlicht werden. Die genaue Veröffentlichungsdatum und den Build werden auf Feedback der Benutzer zu basieren. Daher empfehlen wir Ihnen, versuchen die Funktion, und lassen Sie uns wissen, welche Funktionen wichtig sind. 
> 
> Informationen zum Zeitplan Version finden Sie unter der [SQL Server-Blog](https://blogs.technet.microsoft.com/dataplatforminsider/) oder [Microsoft R Server-Blog](https://blogs.msdn.microsoft.com/rserver/).

## <a name="features"></a>Funktionen

Die Preview-Version bietet die folgenden Funktionen:

+ Rufen Sie R, die mithilfe von gespeicherten Prozeduren für die einfache Bereitstellung von Machine learning-Lösungen
+ Abrufen von Bewertungen aus dem Modell, die mit jeder Anwendung, die mit Ihrer Clouddatenbank herstellen können
+ Bewertung der PREDICT-Funktion, zur schnellen Bewertung ohne Verwendung von R-Laufzeitmoduls mit systemeigenen unterstützt

Informationen über Einschränkungen, die spezifisch für die Preview-Version finden Sie unter [Einschränkungen und bekannte Probleme](#bkmk_restrictions).

### <a name="components"></a>Components

Die Gesamtarchitektur gleicht der SQL Server-Computer-R-Services.

**Sicherheit**

+ Der SQL Server-Launchpad vertrauenswürdige verwaltet die Ausführung von R-Aufträgen und steuert die Lebensdauer von Prozessen. 

**R-Pakete**

+ Die Preview-Version umfasst Microsoft R Open 3.3.3 und Microsoft R Server, Version 9.2. Die ["revoscaler"-Paket](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) vorinstalliert ist.

+ Einige R-Pakete entfernten oder so geändert, dass um in der Azure-Umgebung zu verkleinern. Beispielsweise **Mrsdeploy** ist nicht in Azure SQL-Datenbank enthalten.

**Leistung**

+ Unterstützt das Trainieren und Bewerten von jedes Modell, in dem Daten können in den Arbeitsspeicher passen.  Die Menge des verfügbaren Speichers hängt von der Edition der Datenbank ab. 
+ Trivial Parallelität wird unterstützt, mit der @parallel = 1 Argument als auch für die Ausführung von R-Skripten streaming 
+ In der Vorschau, die auf ein einzelnes pro Datenbank gleichzeitig ausgeführten R-Skript beschränkt werden.

**Sprachen**

Die Roadmap für künftige Version umfasst Unterstützung für zusätzliche Pakete und Python.

## <a name="restrictions"></a>Einschränkungen

Dieser Abschnitt enthält einige zusätzlichen Einschränkungen, die für die Preview-Version gelten.

### <a name="upgrading-r-components-and-adding-packages-not-supported"></a>Aktualisieren von R-Komponenten und Hinzufügen von Paketen, die nicht unterstützt.

Azure SQL-Datenbank ist ein verwalteter Dienst, und Kunden sind nicht dazu gedacht, Upgrades für die R-Komponenten zu verwalten. Verwenden Sie die verfügbaren installierten Pakete, für die Preview-Version.

Upgrades für R und anderen Machine learning-Komponenten werden veröffentlicht, sobald sie verfügbar sind.

### <a name="availability"></a>Verfügbarkeit

Die Möglichkeit zum Ausführen von R und anderen Machine learning-Skripts in Azure SQL-Datenbank ist eine Vorschaufunktion in West Mitte-NORD Region nur. Erweiterung auf andere Regionen, z. B. Westeuropa, ist für spätere Versionen geplant.

Ausführen von R in Azure SQL-Datenbank erfordert ausreichend Speicherplatz und Arbeitsspeicher. Derzeit werden die folgenden Datenbank-Dienstebenen und Leistungsstufen unterstützt:

+ Premium-Dienstebene: P1, P2, P4, P6, P11, P15 
+ Premium-Dienst von RS-Ebene: PRS1 PRS2, PRS4, PRS6 
+ Elastischen Premium-Pools: 125 eDTUs oder höher 
+ Premium RS elastischen Pool: 125 eDTUs oder höher 

### <a name="resource-management"></a>Ressourcenverwaltung

Diese Version unterstützt nicht die Möglichkeit zum Anpassen der R-Installation oder die Verwendung von R-Skripts zu überwachen.

Angenommen, Sie Ausführung von R-Skripts nur auf bestimmte Datenbanken ist nicht möglich.

Die DMV-dm_db_resource_stats, verwendet, um die Überwachung der Verwendung von CPU- und Arbeitsspeicherressourcen von R-Skripts ist nicht in der Preview-Version verfügbar.

### <a name="other-limitations"></a>Weitere Einschränkungen

Die folgende Funktionalität wird nicht unterstützt: 

+ Das MicrosoftML-Paket ist nicht verfügbar.
+ Paket-Verwaltungsfunktionen wie z. B. externe Bibliothek erstellen, werden nicht unterstützt.
+ Die Azure SQL-Datenbank kann nicht als remote computekontext verwenden werden, beim Ausführen von Skripts in einem R-Client. R-Skripts müssen mithilfe der gespeicherten Prozedur Sp_execute_external_script ausgeführt werden. Andere rechenkontexte können keine Skripts, die von der gespeicherten Prozedur aufgerufen.
+ Aufrufen von Rx-Funktionen, die parallele Ausführung erfordern, kann nicht ausgeführt werden.
+ Loopback-Verbindungen von R-Skript mit SQL Server werden nicht unterstützt. Sie können nicht mit anderen Worten, externe Aufrufe in Ihrem R-Skript eine andere ODBC-Datenquelle verwenden.

## <a name="get-started"></a>Erste Schritte

Diese Ankündigung aus der SQL Server-Entwicklungsteam enthält kurze Beispiele, in denen Sie in Ihrem eigenen Azure SQL-Datenbanken zum Experimentieren mit R-Modelle erstellen und das Generieren von Vorhersagen ausführen können.

+ [Schulen und Ergebnis-Modellen in Azure SQL-Datenbank](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/09/25/announcing-preview-of-machine-learning-services-with-r-support-in-azure-sql-database/)

