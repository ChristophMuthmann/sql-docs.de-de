---
title: Erstellen von BI-Workflows mit R | Microsoft Docs
ms.custom: SQL2016_New_Updated
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 34c3b1c2-97db-4cea-b287-c7f4fe4ecc1b
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 177242eadd1883e4f6c9de0893dc805c4312c36f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="creating-bi-workflows-with-r"></a>Erstellen von BI-Workflows mit R

Eine relationale Datenbank ist eine hochgradig optimierte Technologie für die Bereitstellung von skalierbaren Lösungen für die Transaktionsverarbeitung sowie zur Speicherung und Abfrage von Daten.

Im Gegensatz dazu haben bisher R-Lösungen in der Regel verlassen zum Importieren von Daten aus verschiedenen Quellen, oft im CSV-Format, zum Ausführen von weiteren Durchsuchen von Daten und Modellierung. Solche Methoden sind nicht nur ineffizient, sondern auch unsicher.

Dieses Thema beschreibt einige Integrationsszenarien für R und SQL Server, der zu vermeiden, häufige Fehlerquellen und Sicherheitsrisiken, die auftreten können, wenn Sie außerhalb der Datenbank Machine Learning-Lösungen entwickelt werden.

Außerdem wird beschrieben, wie Business Intelligence-Anwendungen, vor allem Integration Services und Reportng-Services, R-Code interagieren können, und Nutzen von Daten oder Grafiken, die von r generierte-Beispiele

Gilt für: SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Dienste

## <a name="bring-compute-power-to-the-data"></a>Schalten Sie die Rechenleistung an den Daten

Ein Schlüssel Entwurfsziel der Integration von Machine Learning in SQL Server wurde um Analysen in der Nähe der Daten zu bringen. Dies bietet mehrere Vorteile:

+ Datensicherheit. Kombinieren von R näher an die Quelle der Daten vermeidet Aufwand oder unsichere datenverschiebungen.

+ Geschwindigkeit. Datenbanken sind für setbasierte Vorgänge optimiert. Aktuelle Innovationen in Datenbanken wie z. B. in-Memory-Tabellen stellen Zusammenfassungen und Aggregationen der Daten extrem und eine perfekte Ergänzung zu Data Science sind.

+ Einfache Bereitstellung und Integration. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ist der zentrale Punkt von Vorgängen für andere Verwaltungsaufgaben für Daten und Anwendungen. Mithilfe von Daten, die in der Datenbank oder reporting Warehouse befindet, stellen Sie sicher, dass die Daten von Machine learning-Lösungen, konsistente und auf dem neuesten Stand sind. 

+ Effizienz über Cloud und lokal. Anstatt die Daten in R zu verarbeiten, können Sie Datenpipelines des Unternehmens nutzen, darunter [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] und Azure Data Factory. Das Berichten von Ergebnissen oder Analysen ist über Power BI oder [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]einfach.

Durch die Verwendung der richtigen Kombination von SQL und R für verschiedene Datenverarbeitungstasks und analytische Tasks, können Datenanalysten und Entwickler produktiver sein.

## <a name="use-integration-services-for-data-transformation-and-automation"></a>Mithilfe von Integration Services für Data Transformation und Automatisierung

Data Science-Workflows sind hoch iterativ und umfassen eine Menge Transformation von Daten, einschließlich Skalierung, Aggregationen, die Berechnung der Wahrscheinlichkeiten, sowie das Umbenennen und Zusammenführen von Attributen. Obwohl Datenanalysten daran gewöhnt sind, viele dieser Aufgaben in R, Python oder einer anderen Sprache zu erledigen, erfordert das Ausführen solcher Workflows mit Unternehmensdaten nahtlose Integration mit ETL-Tools und -Prozessen.

Da [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] es Ihnen ermöglicht, komplexe Vorgänge in R über Transact-SQL und gespeicherte Prozeduren auszuführen, können Sie R-spezifische Aufgaben mit vorhandenen ETL-Prozessen ohne erneute Entwicklung integrieren. Stattdessen als eine Kette von arbeitsspeicherintensive Vorgänge in R auszuführen, Vorbereitung der Daten kann optimiert werden mit den effizientesten Tools, einschließlich [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] und [!INCLUDE[tsql](../../includes/tsql-md.md)]. 

Hier sind einige Ideass für wie Ihre Daten, die Verarbeitung einer Dmodeling automatisiert werden können pipelines mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ Verwendung [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Aufgaben zum Erstellen von Features erforderlichen Daten in der SQL-Datenbank
+ Verwenden von bedingter Verzweigung, um Computekontext für R-Aufträge zu wechseln
+ Führen Sie R-Aufträge, die ihre eigenen Daten in der Datenbank zu generieren und Freigeben von Daten für Anwendungen
+ Bei Verwendung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], laden Sie R-Skript in einer Textvariablen gespeichert, und führen Sie es in SQL Server

### <a name="examples"></a>Beispiele

[Operationalize your machine learning project using SQL Server 2016 SSIS and R Services (Operationalisieren Ihres Machine Learning-Projekts mithilfe von SQL Server 2016 Integration Services (SSIS) und R Services)](https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/)  

In diesem Blogbeitrag veranschaulicht die grundlegenden Techniken zum Bearbeiten der R-Code mithilfe von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]: 

+ Verwenden den Task SQL ausführen zum Generieren von Daten und speichern ihn in R aufrufen[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

+ Verwenden einer gespeicherten Prozedur zum Trainieren eines R-Modells und Speichern in der Datenbank

+ Ausführen der Bewertung auf dem Modell mit dem Skripttask und dem Task „SQL ausführen“

##  <a name="bkmk_ssrs"></a>Verwenden von Reporting Services für die Visualisierung

Obwohl R Diagramme und interessante Visualisierungen erstellen kann, ist es nicht gut mit externen Datenquellen integriert, was bedeutet, dass jedes Diagramm oder jeder Graph einzeln erstellt werden muss. Gemeinsame Nutzung kann auch schwierig sein.

Mithilfe von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] können Sie komplexe Vorgänge in R über gespeicherte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozeduren ausführen, die problemlos von einer Vielzahl von Tools für Unternehmensberichte, einschließlich [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] und Power BI, genutzt werden können.

+ Visualisieren von Grafikobjekten, die über ein R-Skript mit [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]zurückgegeben werden
+ Verwenden der Tabelle in Power BI

### <a name="examples"></a>Beispiele

[R Graphics Device for Microsoft Reporting Services (SSRS) (R-Grafikgerät für Microsoft Reporting Services (SSRS))](https://rgraphicsdevice.codeplex.com/)

Dieses CodePlex-Projekt enthält den Code, mit dem Sie ein benutzerdefiniertes Berichtselement erstellen können, das die Grafikausgabe von R als Bild zur Verwendung in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Berichten rendert.  Mit dem benutzerdefinierten Berichtselement können Sie folgende Aktionen ausführen:

+ Veröffentlichen von Diagrammen und mit dem R-Grafikgerät erstellten Plots an [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Dashboards

+ Übergeben von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Parametern an R-Plots

> [!NOTE]
> Für dieses Beispiel muss der Code, der die R-Grafikgerät für Reporting Services unterstützt sowohl auf dem Reporting Services-Server als auch in Visual Studio installiert sein. Manuelle Kompilierung und Konfiguration sind ebenfalls erforderlich.
