---
title: "End-to-End Data sience-Vorgehensweise für R und SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 08/22/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: edd76ae9-4125-45a8-bf42-47a85b9d9a32
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 5ff7287937e2bddd57d4b155c254bcd29bfc0d68
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="end-to-end-data-science-walkthrough-for-r-and-sql-server"></a>End-to-End Data sience-Vorgehensweise für R und SQL Server

In dieser exemplarischen Vorgehensweise entwickeln Sie eine End-to-End-Lösung für die vorhersagemodellierung basierend auf Microsoft R mit SQL Server 2016 oder SQL Server-2017.

Diese exemplarische Vorgehensweise basiert auf einem bekannten öffentlichen Dataset, dem Dataset New York City-Taxi. Sie verwenden eine Kombination von R-Code [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten und benutzerdefinierte SQL-Funktionen, die ein klassifizierungsmodell zu erstellen, der die Wahrscheinlichkeit angibt, dass der Treiber einen Hinweis für einen bestimmten Taxi Reise auftreten kann. Bereitstellung auch das R-Modell, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Verwenden von Server-Daten zum Generieren von Bewertungen, die basierend auf dem Modell.

In diesem Beispiel kann für alle Arten von realen Probleme, z. B. Vorhersagen Kundenantworten zu Marketingkampagnen oder Vorhersagen Ausgaben oder die Teilnahme an Ereignisse erweitert werden. Da das Modell aus einer gespeicherten Prozedur aufgerufen werden kann, können Sie problemlos in eine Anwendung einbetten.

Die exemplarische Vorgehensweise ist darauf ausgelegt, Entwickler R einführen [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], R wird verwendet, wenn möglich. Allerdings bedeutet dies nicht, dass R unbedingt das beste Tool für jede Aufgabe ist. In vielen Fällen stellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine bessere Leistung bereit, besonders für Aufgaben wie Datenaggregation und Featureentwicklung.  Solche Aufgaben profitieren besonders von neuen Funktionen in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], wie z.B. von speicheroptimierten Columnstore-Indizes. Wir versuchen, Stelle sei darauf hingewiesen mögliche Optimierung Erweiterungsklassen.

> [!NOTE]
> Die exemplarische Vorgehensweise wurde ursprünglich für SQL Server 2016 entwickelt und darauf getestet. Allerdings haben Screenshots und Prozeduren aktualisiert, um die neueste Version von SQL Server Management Studio verwenden, die mit SQL Server-2017 funktioniert.

## <a name="overview"></a>Übersicht

Die geschätzte Zeiten beinhalten keine Setup. Weitere Informationen finden Sie unter [Voraussetzungen für die exemplarische Vorgehensweise](../tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md).

|Themenliste|Geschätzte Zeit|
|-|------------------------------|
|[Vorbereiten der exemplarischen Vorgehensweise R](../tutorials/walkthrough-prepare-the-data.md) <br /><br />Erhalten Sie die Daten, die zum Erstellen eines Modells verwendet werden. Laden Sie ein öffentliches Dataset herunter, und laden Sie es in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank.|30 Minuten|
|[Durchsuchen der Daten mithilfe von SQL](../tutorials/walkthrough-view-and-explore-the-data.md) <br /><br />Verstehen Sie Ihre Daten mithilfe von SQL-Tools und Zusammenfassungen.|10 Minuten|
|[Zusammenfassen der Daten mithilfe von R](../tutorials/walkthrough-view-and-summarize-data-using-r.md) <br /><br />Verwenden Sie R, um die Daten untersuchen und Zusammenfassungen zu generieren.|10 Minuten|
|[Erstellen von Darstellungen, die Verwendung von R in SQL Server](../tutorials/walkthrough-create-graphs-and-plots-using-r.md) <br /><br />Erstellen von Darstellungen in lokalen und remoterechenkontexte durch das Mischen von R und SQL.|10 Minuten|
|[Erstellen Sie Data-Funktionen, die mittels R und T-SQL)](../tutorials/walkthrough-create-data-features.md) <br /><br />Entwickeln Sie Features mithilfe von benutzerdefinierten Funktionen in R und [!INCLUDE[tsql](../../includes/tsql-md.md)]. Vergleichen Sie die Leistung von R und T-SQL im Hinblick auf Featurebereitstellung. |10 Minuten|
|[Erstellen Sie ein R-Modell zu und speichern Sie sie in SQL Server](../tutorials/walkthrough-build-and-save-the-model.md) <br /><br />Trainieren und optimieren Sie ein Vorhersagemodell. Bewerten Sie die Leistung des Modells. In dieser exemplarischen Vorgehensweise wird ein Klassifizierungsmodell erstellt. Stellen Sie die Genauigkeit des Modells mithilfe von R dar.|15 Minuten|
|[Bereitstellen des R-Modells mithilfe von SQL Server](../tutorials/walkthrough-deploy-and-use-the-model.md) <br /><br />Stellen Sie das Modell in der Produktion bereit, indem Sie es in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank speichern. Rufen Sie das Modell aus einer gespeicherten Prozedur ab, um Vorhersagen zu generieren.|10 Minuten|

### <a name="intended-audience"></a>Beabsichtigte Zielgruppe

Diese exemplarische Vorgehensweise ist für R- oder SQL-Entwickler vorgesehen. Sie bietet eine Einführung in die Integration von R in Unternehmensworkflows mithilfe von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  Sie sollten mit Datenbankvorgänge, z. B. Datenbanken und Tabellen erstellen, Importieren von Daten und Ausführen von Abfragen vertraut sein.

+ Alle SQL- und R-Skripte sind enthalten.
+ Sie müssen möglicherweise Zeichenfolgen in das Ausführen von Skripts, in Ihrer Umgebung zu ändern. Hierzu können Sie mit einem beliebigen Codeeditor, z. B. [Visual Studio Code](https://code.visualstudio.com/Download).

### <a name="prerequisites"></a>Voraussetzungen

+ Sie benötigen Zugriff auf eine Instanz von SQL Server 2016 oder eine Evaluierungsversion von SQL Server-2017.
+ Auf mindestens einer Instanz des SQL Server-Computers muss [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] installiert sein.
+ Wenn Sie R-Befehle von einem Remotecomputer befindet, z. B. einen Laptop oder einem anderen Computer im Netzwerk ausführen möchten, müssen Sie die Microsoft R Open-Bibliotheken installieren. Sie können Microsoft R-Client oder Microsoft R Server installieren. Der Remotecomputer muss in der Lage, Herstellen von Verbindungen die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz.
+ Wenn Sie Client und Server auf demselben Computer platzieren möchten, achten Sie darauf, dass Sie einen separaten Satz von Microsoft R-Bibliotheken für die Verwendung beim Senden von R-Skript von einem "remote" Client installieren. Verwenden Sie die R-Bibliotheken, die installiert sind für die Verwendung von SQL Server-Instanz für diesen Zweck.

Weitere Informationen dazu, wie Sie diese Server und Client-Umgebungen einrichten, finden Sie unter [Voraussetzungen für die R und SQL Server Data sience-Vorgehensweise](../tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md).

## <a name="next-lesson"></a>Nächste Lektion

[Vorbereiten der exemplarischen Vorgehensweise R](../tutorials/walkthrough-prepare-the-data.md)
