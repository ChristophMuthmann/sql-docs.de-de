---
title: Datensuche und Vorhersagemodellierung mit R | Microsoft-Dokumentation
ms.custom: SQL2016_New_Updated
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bf6de7e2-f394-4b8a-a4b7-0b8dadf25426
caps.latest.revision: "20"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 79f82cbf4cba40a4c4fd2b2683ce3c16913ef315
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="data-exploration-and-predictive-modeling-with-r"></a>Datensuche und Vorhersagemodellierung mit R

In diesem Thema wird beschrieben, Verbesserungen an den Data Science-Prozess, die durch die Integration mit SQL Server möglich sind.

Gilt für: SQL Server 2016-R-Services, SQL Server 2017 Machines Learnign-Diensten

## <a name="the-data-science-process"></a>Die Data Science-Prozess

Datenanalysten verwenden R häufig zum Durchsuchen von Daten und Erstellen von Vorhersagemodellen. Dies ist normalerweise ein iterativer Prozess durch Ausprobieren, bis ein geeignetes Vorhersagemodell erreicht wird. Als erfahrener Datenanalyst können Sie eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank herstellen und die Daten mithilfe des RODBC-Pakets auf die lokale Arbeitsstation abrufen. Dort können Sie die Daten untersuchen und mithilfe von R-Standardpaketen ein Vorhersagemodell erstellen.

Dieser Ansatz hat jedoch viele Nachteile dieser Hae beeinträchtigt die breitere Übernahme von R im Unternehmen. 

+ Verschieben von Daten kann langsam, ineffizient oder unsicher sein.
+ R weist Einschränkungen für Leistung und Skalierung

Diese Nachteile werden deutlicher, wenn Sie große Datenmengen verschieben und analysieren müssen, oder Datasets verwenden, die nicht in den auf dem Computer verfügbaren Arbeitsspeicher passen.

Die neuen, skalierbaren Pakete und R-Funktionen, die in enthaltenen [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] können Sie viele dieser Herausforderung zu umgehen. 

## <a name="whats-different-about-revoscaler"></a>Was hat sich zu "revoscaler"?

Das **RevoScaleR** -Paket enthält die Implementierung einiger der beliebtesten R-Funktionen, die umgestaltet wurden, um die Parallelität und Skalierung bereitzustellen. Weitere Informationen finden Sie unter [verteiltes rechnen mit "revoscaler"](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing).

Das RevoScaleR-Paket bietet auch Unterstützung zum Ändern des *Ausführungskontexts*. Dies bedeutet, dass für eine gesamte Lösung oder für eine einzelne Funktion, die Sie angeben können, die Berechnungen mithilfe der Ressourcen des Computers ausgeführt werden sollen, der die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz hostet, und nicht auf der lokalen Arbeitsstation. Dies hat mehrere Vorteile: Sie vermeiden unnötige Datenbewegungen und Sie können auf dem Server ergiebigere Berechnungsressourcen nutzen.

## <a name="r-environment-and-packages"></a>R-Umgebung und -Pakete

Der in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] unterstützte R-Umgebung besteht aus einem Laufzeitmodul, der Open Source-Sprache und einem grafischen Modul, das von mehreren Paketen unterstützt und erweitert wird. Die Sprache ermöglicht eine Vielzahl von Erweiterungen, die mithilfe der Pakete implementiert werden.  

### <a name="using-other-r-packages"></a>Mithilfe von anderen R-Pakete

Zusätzlich zu Microsoft Machine Learning enthaltenen proprietären R-Bibliotheken, können Sie fast alle R-Pakete in der Projektmappe, einschließlich:

+ Allgemeine R-Pakete aus öffentlichen Repositorys. Sie finden die beliebtesten Open Source-R-Pakete in öffentlichen Repositorys wie CRAN, wo über 6.000 Pakete gehostet werden, die von Datenanalysten verwendet werden können.
  
  Für die Windows-Plattform werden R-Pakete als ZIP-Dateien bereitgestellt, die unter der GPL-Lizenz heruntergeladen und installiert werden können.  
  
  Weitere Informationen zum Installieren der Pakete von Drittanbietern für die Verwendung mit [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]finden Sie unter [Install Additional R Packages on SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
  
+ Zusätzliche von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]bereitgestellte Pakete und Bibliotheken.   
  
     Das **RevoScaleR**-Paket enthält leistungsstarke Big Data-Analysen, verbesserte Versionen von Funktionen, die allgemeine Data Science-Aufgaben unterstützen, optimierte Lernmodule für Naive Bayes, lineare Regression, Zeitreihenmodelle, neuronale Netzwerke und erweiterte mathematische Bibliotheken.  
  
     Mit dem **RevoPemaR** -Paket können Sie eigene parallele, externe Speicheralgorithmen in R entwickeln.  
  
     Weitere Informationen zu diesen Paketen und deren Verwendung finden Sie unter [Neuigkeiten "revoscaler"](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) und [erste Schritte mit RevoPemaR](https://msdn.microsoft.com/microsoft-r/pemar-getting-started). 

+ **MicrosoftML** enthält eine Auflistung von hochgradig optimierten Machine Learning-Algorithmen und Transformieren von Daten aus dem Microsoft Data Science-Team. Viele der Algorithmen werden auch in Azure Machine Learning verwendet werden. Weitere Informationen finden Sie unter [mithilfe des Pakets MicrosoftML](../../advanced-analytics/using-the-microsoftml-package.md).

### <a name="r-development-tools"></a>R-Entwicklungstools

Wenn Sie Ihre R-Lösung zu entwickeln, achten Sie darauf, dass Sie Microsoft R-Client heruntergeladen werden. Dieser freie Download umfasst die Bibliotheken, die zur Unterstützung von remote rechenkontexte und skalierbare Alorithms erforderlich sind:

+ **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]:** Eine Verteilung des R-Laufzeitmoduls und einer Reihe von Paketen, z.B. die mathematische Kernelbibliothek von Intel, die die Leistung von R-Standardfunktionen steigern.  
  
+ **RevoScaleR:** Ein R-Paket, mit dem Sie Berechnungen auf eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verlagern können. [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]neuen skalierbaren Pakete und R-Funktionen verwenden. Es enthält auch einen Satz von allgemeinen R-Funktionen, die neu gestaltet wurden, um eine bessere Leistung und Skalierbarkeit zu bieten. Sie können diese verbesserten Funktionen am Präfix **rx** erkennen. Darüber hinaus sind verbesserte Datenanbieter für eine Vielzahl von Quellen enthalten; diese Funktionen haben das Präfix **Rx**.

Können Sie Windows-basierten Codeeditor, die R, z. B. unterstützt [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] oder RStudio. Der Download von [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] umfasst zudem allgemeine Befehlszeilentools für R, z.B. „RGui.exe.“

## <a name="use-new-data-sources-and-compute-contexts"></a>Verwenden neuer Datenquellen und Computekontexten

Wenn die RevoScaleR-Paket für die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], suchen Sie für diese Funktionen, die in Ihrem R-Code verwenden:

+ **RxSqlServerData** ist eine im „RevoScaleR“-Paket bereitgestellte Funktion zur Unterstützung der verbesserten Datenkonnektivität mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]neuen skalierbaren Pakete und R-Funktionen verwenden.
  
     Sie können diese Funktion im R-Code verwenden, um die *Datenquelle*zu definieren. Das Datenquellenobjekt gibt den Server und die Tabellen an, auf dem bzw. in denen sich die Daten befinden. Zudem verwaltet es das Lesen der Daten aus sowie das Schreiben der Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
-   Das **RxInSqlServer** -Funktion kann der *Computekontext*neuen skalierbaren Pakete und R-Funktionen verwenden.  Sie können mit anderen Worten angeben, wo der R-Code ausgeführt werden soll: auf der lokalen Arbeitsstation oder auf dem Computer, der die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz hostet.  Weitere Informationen finden Sie unter [RevoScaleR-Funktionen](https://msdn.microsoft.com/microsoft-r/scaler/scaler).
  
     Wenn Sie Computekontext festlegen, wirkt sich das nur auf Berechnungen aus, die einen Remoteausführungskontext unterstützen, d.h. vom RevoScaleR-Paket bereitgestellte R-Vorgänge und verwandte Funktionen. Üblicherweise können R-Lösungen, die auf standardmäßigen CRAN-Paketen basieren, nicht im Remotecomputekontext ausgeführt werden. Sie können allerdings auf dem [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Computer ausgeführt werden, wenn sie mit T-SQL gestartet werden. Sie können aber mithilfe der `rxExec`-Funktion einzelne R-Funktionen aufrufen, und sie remote in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ausführen.

Beispiele zum Erstellen und Arbeiten mit Datenquellen und Ausführungskontexten finden Sie in diesen Lernprogrammen:

+ [Tieferer Einblick in Data Science](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)  
+  [-Datenanalyse mithilfe von Microsoft R](https://msdn.microsoft.com/en-us/microsoft-r/data-analysis-in-microsoft-r)

## <a name="deploy-r-code-to-production"></a>Bereitstellen Sie R-Code für die Produktion.

Ein wichtiger Teil der Data Science ist die Bereitstellung Ihrer Analysen für andere Benutzer oder die Verwendung von Vorhersagemodellen zur Optimierung von Geschäftsergebnissen oder -prozessen. In [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]gestaltet sich der Wechsel zur Produktion einfach, wenn Ihr R-Skript oder das Modell fertig ist.

Weitere Informationen zum Verschieben Ihres Codes zur Ausführung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]finden Sie unter [Operationalizing Your R Code](../../advanced-analytics/r/operationalizing-your-r-code.md)neuen skalierbaren Pakete und R-Funktionen verwenden.

Normalerweise beginnt der Bereitstellungsprozess mit dem Bereinigen Ihres Skripts, um den für die Produktion nicht erforderlichen Code zu entfernen. Während des Verschiebens Berechnungen näher auf die Daten können Sie nach Möglichkeiten suchen, effizienter verschieben, zusammenfassen oder präsentieren von Daten als das alles in R.  Es wird empfohlen, dass der Data Scientist wenden Sie sich an ein Datenbankentwickler über Methoden zur Verbesserung der Leistung, insbesondere dann, wenn die Lösung verwendet die DatenBereinigung oder das Feature Engineering-Team, die möglicherweise effektiver in SQL. Möglicherweise sind Änderungen an ETL-Prozessen erforderlich, um sicherzustellen, dass Workflows zum Erstellen oder Bewerten eines Modells erfolgreich ausgeführt werden und eingegebene Daten im richtigen Format vorliegen.

## <a name="see-also"></a>Siehe auch

[Comparison of Base R and ScaleR Functions (Grundlegende R- und ScaleR-Funktionen im Vergleich)](https://msdn.microsoft.com/microsoft-r/scaler/compare-base-r-scaler-functions)

[ScaleR Functions for Working with SQL Server (ScaleR-Funktionen für das Arbeiten mit SQL Server)](../../advanced-analytics/r/scaler-functions-for-working-with-sql-server-data.md)
