---
title: "Lernprogramme für SQL Server-R | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 08/29/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: R
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 57ebbf72c613bd6618376482b10f5d7ef625dbc5
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="sql-server-r-tutorials"></a>SQL Server-R-Lernprogramme

Dieser Artikel enthält eine Liste der Lernprogramme und Beispiele, in denen die Verwendung von R mit SQL Server 2016 oder SQL Server-2017 veranschaulicht. Durch diese Beispiele und Demos erfahren Sie:

+ Zum Ausführen von R von T-SQL
+ Was remote und lokalen rechenkontexten sind und wie Sie R-Code mithilfe von SQL Server-Computer ausführen können
+ Gewusst wie: Umschließen von R-Code in einer gespeicherten Prozedur
+ Optimieren der R-Code für eine SQL-produktionsumgebung
+ Reale Szenarien für das Einbetten von Machine Learning in Anwendungen

Informationen zu Anforderungen und Setup finden Sie unter [Voraussetzungen](#bkmk_Prerequisites).

## <a name="bkmk_sqltutorials"></a>R-Lernprogramme

Sofern nicht anders angegeben, Lernprogramme wurden für SQL Server 2016 R Services entwickelt und werden erwartet, dass in SQL Server 2017 Machine Learning Services ohne wesentliche Änderungen zu arbeiten.

Alle Lernprogramme machen umfangreichen Gebrauch von Funktionen in die RevoScaleR-Paket für SQL Server Kontexten zu berechnen.

+ [Data Science fundierte Einblicke mit R und SQLServer](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)

  Erfahren Sie, wie die Funktionen in den Paketen "revoscaler" verwenden. Verschieben von Daten zwischen R und SQL Server und Switches remotecomputekontexten entsprechend eine bestimmte Aufgabe. Erstellen von Modellen und Darstellungen und zwischen Ihrer Entwicklungsumgebung und dem Datenbankserver verschieben.

  **Zielgruppe:** für Datenanalysten oder Entwickler, die bereits mit der R-Sprache vertraut sind, und Informationen zu den erweiterten R-Pakete und Funktionen in Microsoft R von Revolution Analytics wünschen.

  **Anforderungen:** einige grundlegende Kenntnisse zur R. Zugriff auf einen Server mit SQL Server R Services oder Machine Learning-Diensten mit r Setup-Hilfe finden Sie unter [Voraussetzungen](#bkmk_Prerequisites).

+ [In der Datenbank-R-Analyse für SQL-Entwickler](../tutorials/sqldev-in-database-r-for-sql-developers.md)

  Erstellen und bereitstellen, nur über eine vollständige R-Lösung [!INCLUDE[tsql](../../includes/tsql-md.md)] Tools.

  Konzentriert sich auf eine Lösung in die produktionsumgebung verschieben. Sie erfahren, wie Sie R-Code in einer gespeicherten Prozedur umschließen können, ein R-Modell in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank speichern können und parametrisierte Aufrufe des R-Modells für die Vorhersage durchführen können.

  **Zielgruppe:** für SQL-Entwickler, Entwickler oder SQL-Experten, die R-Lösungen unterstützen, und erfahren, wie Sie R-Modelle in SQL Server bereitstellen möchten.

  **Anforderungen:** keine R-Umgebung erforderlich ist. Alle R-Code wird bereitgestellt, und Sie können nur mit kompletten Lösung erstellen [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und vertrauten Business Intelligence und SQL-Entwicklungstools. Einige grundlegende Kenntnisse von R ist jedoch hilfreich.

  Sie benötigen Zugriff auf einen SQL Server mit der Sprache R installiert und aktiviert. Setup-Hilfe finden Sie unter [Voraussetzungen](#bkmk_Prerequisites).

+ [Schnellstart: Verwenden von R in T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)

  Dieser Schnellstart behandelt die grundlegende Syntax für die Verwendung von R in [!INCLUDE[tsql](../../includes/tsql-md.md)].

  Informationen Sie zum Aufrufen der R-Laufzeit von T-SQL, umschließen R-Funktionen in SQL-Code und führen Sie eine gespeicherte Prozedur, die Ausgabe von R und R-Modelle in einer SQL-Tabelle speichert.

  **Zielgruppe:** für Personen, die mit der Funktion nicht vertraut sind, und zum Erlernen der Grundlagen von R aus einer gespeicherten Prozedur aufgerufen werden soll.

  **Anforderungen:** keine Kenntnis von R oder SQL erforderlich. Allerdings benötigen Sie SQL Server Management Studio oder einem anderen Client, der Herstellen einer Verbindung mit einer Datenbank und T-SQL ausführen kann. Es wird empfohlen die kostenlose [MSSQL-Erweiterung für Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) , wenn Sie mit T-SQL-Abfragen vertraut sind.

  Sie benötigen auch Zugriff auf einen Server mit SQL Server R Services oder Machine Learning-Diensten mit R bereits aktiviert. Setup-Hilfe finden Sie unter [Voraussetzungen](#bkmk_Prerequisites).

+ [Lückenlose exemplarische Data Science-Vorgehensweise](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

  Zeigt die Data Science-Prozesses von Anfang bis Ende, wie Sie Daten abrufen und speichern Sie sie in SQL Server, die Daten mit R analysieren und Diagramme erstellen, an.

  Sie erfahren, wie Grafiken zwischen verschieben [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und R, und vergleichen namens Feature Engineering in T-SQL mit R-Funktionen. Schließlich erfahren Sie zum Verwenden des Vorhersagemodells in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für batchbewertung und einzeiliges bewerten.

  **Zielgruppe:** für Personen, die mit R und mit den Entwicklertools wie SQL Server Management Studio vertraut sind.

  **Anforderungen:** Sie haben Zugriff auf ein R-Entwicklungsumgebung und wissen, wie Sie R-Befehle ausführen sollten. Verwenden von PowerShell ist erforderlich, um in New York City Taxi Dataset herunterzuladen. Sie benötigen Zugriff auf einen Server mit SQL Server R Services oder Machine Learning-Diensten mit R bereits aktiviert. Setup-Hilfe finden Sie unter [Voraussetzungen](#bkmk_Prerequisites).

## <a name ="bkmk_samples"></a>Produktbeispiele

Diese Beispiele und Demos werden bereitgestellt, durch das SQL Server-Entwicklungsteam auf vielerlei Hinsicht markieren, dass Sie eingebettete Analytics in echten Anwendungen verwenden können.

+ [Erstellen eines Vorhersagemodells mittels R und SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction)

  Erfahren Sie, wie eine Ski Vermietung Business Machine learning-zukünftige Vermietung Vorhersagen verwenden kann dadurch die Business-Plan und die Mitarbeiter, zukünftige Bedarf zu decken.

+ [Ausführen von Kunden mithilfe von R und SQL Server-clustering](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/)

  Verwenden Sie Segment Kunden auf Grundlage der Umsatzdaten unüberwachtes lernen.

## <a name="bkmk_Prerequisites"></a>Voraussetzungen

Um diese Lernprogramme und Beispiele zu verwenden, müssen Sie eines der folgenden Serverprodukte installieren:

+ SQL Server 2016 R Services (Datenbankintern)
  
  Unterstützt r unbedingt Machine learning-Funktionen zu installieren und dann aktivieren externer Skripts.

+ SQL Server 2017 Machine Learning Services (Datenbankintern)
  
  Unterstützt R oder Python. Sie müssen die Machine learning-Funktion und die Sprache für die Installation auswählen und dann aktivieren externer Skripts.

Nach dem Ausführen von SQL Server-Setup, vergessen Sie nicht folgenden wichtigen Schritte aus:

+ Aktivieren Sie die externen Skript Ausführung-Funktion, indem Sie ausgeführt wird`sp_configure 'external scripts enabled', 1`
+ Neustarten des Servers
+ Stellen Sie sicher, dass der Dienst, der die externe Runtime ruft erforderlichen Berechtigungen verfügt.
+ Sicherstellen Sie, dass der SQL-Anmeldung oder die Windows-Benutzerkonto hat erforderlichen Berechtigungen zum Verbinden mit dem Server, der zum Lesen von Daten und erstellen das Beispiel erforderlichen Datenbankobjekte

Wenn Probleme auftreten, finden Sie in diesem Artikel finden Sie einige häufig auftretende Probleme: [Problembehandlung Machine Learning-Dienste](../machine-learning-troubleshooting-faq.md)
