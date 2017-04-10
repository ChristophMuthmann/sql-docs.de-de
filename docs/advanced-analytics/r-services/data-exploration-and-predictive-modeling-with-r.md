---
title: "Datensuche und Vorhersagemodellierung mit R | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bf6de7e2-f394-4b8a-a4b7-0b8dadf25426
caps.latest.revision: 20
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 19
---
# Datensuche und Vorhersagemodellierung mit R
  Datenanalysten verwenden R häufig zum Durchsuchen von Daten und Erstellen von Vorhersagemodellen. Dies ist normalerweise ein iterativer Prozess durch Ausprobieren, bis ein geeignetes Vorhersagemodell erreicht wird. Als eine erfahrene Datenanalysten, Sie möglicherweise eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank und die Daten auf der lokalen Arbeitsstation mithilfe des Pakets RODBC abzurufen, untersuchen Sie Ihre Daten und ein Vorhersagemodell mithilfe von standard-R-Pakete erstellen.  
  
 Dieser Ansatz hat jedoch Nachteile. Das Verschieben von Daten kann sich als langsam, ineffizient oder unsicher erweisen und auch R weist Einschränkungen hinsichtlich Leistung und Skalierung auf. Diese Nachteile werden deutlicher, wenn Sie große Datenmengen verschieben und analysieren müssen, oder Datasets verwenden, die nicht in den auf dem Computer verfügbaren Arbeitsspeicher passen.  
  
 Sie können diese Probleme umgehen, indem Sie mit den neuen skalierbare Paketen und R-Funktionen enthalten [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Die **RevoScaleR** Paket enthält die Implementierung einiger der beliebtesten R-Funktionen, die überarbeitet, Parallelität und Skalierung bereitzustellen. Das RevoScaleR-Paket bietet auch Unterstützung zum Ändern des *Ausführungskontext*. Dies bedeutet, dass für eine gesamte Projektmappe oder nur eine Funktion, Sie angeben können, dass Berechnungen ausgeführt werden soll, mithilfe der Ressourcen des Computers, der hostet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz, anstatt der lokalen Arbeitsstation. Dies hat mehrere Vorteile: Sie vermeiden unnötige Datenbewegungen und Sie können auf dem Server ergiebigere Berechnungsressourcen nutzen.  
  
 Dieser Abschnitt enthält Anweisungen für die Datenanalysten zur Verwendung von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] und zum Ausführen von Aufgaben zum Entwickeln und Testen von R-Lösungen.  
  
##  <a name="bkmk_RDevTools"></a> R-Entwicklungstools  
 Microsoft R-Client bietet die Datenanalysten eine vollständige Umgebung zum Entwickeln und Testen von Vorhersagemodellen. R-Client enthält:  
  
-  **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]:** Eine Verteilung der R-Runtime und einen Satz von Paketen, wie z. B. die Intel Kernel Mathematikbibliothek, die die Leistung von R-Standardfunktionen steigern.  
  
-   **RevoScaleR:** ein R-Paket, mit dem Sie push Berechnungen mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]. Darüber hinaus eine Reihe von allgemeinen R-Funktionen, die neu gestaltet wurde, um bessere Leistung und Skalierbarkeit bereitzustellen. Sie können diese verbesserten Funktionen von identifizieren die **Rx** Präfix. Darüber hinaus erweiterte Datenanbieter für eine Vielzahl von Quellen; Diese Funktionen sind mit dem Präfix **Rx**.  
  
-   **Auswahl der Entwicklungstools frei:** können Sie alle Windows-basierten Code-Editor, die unterstützt R, z. B. [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] oder RStudio. Der Download von [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] enthält außerdem allgemeine Befehlszeilentools für R, z. B. RGui.exe.  
  
##  <a name="bkmk_packages"></a> R-Umgebung und -Pakete  
 Der R-Umgebung unterstützt [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] besteht aus einer Laufzeit, die open-Source-Sprache und ein grafisch Modul unterstützt und erweitert, indem mehrere Pakete. Die Sprache ermöglicht eine Vielzahl von Erweiterungen, die mithilfe der Pakete implementiert werden.  
  
 Es stehen mehrere Informationsquellen zusätzliche R-Pakete, die Sie verwenden können [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] :  
  
  
-   Allgemeine R-Pakete aus öffentlichen Repositorys. Sie finden die beliebtesten Open Source-R-Pakete in öffentlichen Repositorys wie CRAN, wo über 6.000 Pakete gehostet werden, die von Datenanalysten verwendet werden können.  
  
     Zusätzliche Pakete sind zur Unterstützung von Vorhersageanalysen in speziellen Domänen verfügbar, z. B. Finanzen, Genomik usw.  
  
     Für die Windows-Plattform und können R-Pakete als Zip-Dateien bereitgestellt werden und heruntergeladen und installiert unter der GPL-Lizenz.  
  
     Weitere Informationen zum Installieren von Drittanbieter-Pakete für die Verwendung mit [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], finden Sie unter [Installieren Sie zusätzliche R-Pakete auf SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
-   Zusätzliche Pakete und Bibliotheken [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].   
  
     Die **RevoScaleR** Paket enthält big Data-Analyse für hohe Leistung, verbesserte Versionen von Funktionen, die allgemeine Data Science-Aufgaben, optimierte lernmodule für Naive Bayes, lineare Regression, zeitreihenmodelle, neuronale Netzwerke und erweiterte mathematische Bibliotheken unterstützen.  
  
     Die **RevoPemaR** Paket können Sie bei der Entwicklung eigener parallele, externe Speicher Algorithmen in r  
  
     Weitere Informationen zu diesen Paketen und deren Verwendung finden Sie unter [Durchsuchen von Daten und Modellierung von Predictive & #40; Lernprogramm: SQL Serverdienste R & #41;](../../advanced-analytics/r-services/sql-server-r-services.md).  
  
## Verwenden von Datenquellen und Computekontexten  
 Wenn das RevoScaleR-Paket für die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], es gibt einige wichtigen neue Funktionen in Ihren R-Code verwenden:  
  
-   [RxSqlServerData](RxSqlServerData.md) ist eine Funktion, die im Paket RevoScaleR zur Unterstützung der verbesserten Konnektivität mit bereitgestellten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Sie können diese Funktion in Ihren R-Code verwenden, definieren die *Datenquelle*. Das Datenquellenobjekt gibt den Server und die Tabellen, wo die Daten und verwaltet die Aufgabe für das Lesen von Daten aus und Schreiben von Daten auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Die [RxInSqlServer](rxInSqlServer.md) -Funktion kann verwendet werden, an die *Kontext compute*.  Das heißt, können Sie angeben, in denen der R-Code ausgeführt werden soll: auf der lokalen Arbeitsstation oder auf dem Computer, der hostet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz.  
  
     Wenn Sie den Compute-Kontext festlegen, wirkt sich dies nur Berechnungen, die remote Ausführungskontext, R-Vorgänge von der RevoScaleR-Paket bereitgestellt und verwandten Funktionen zu unterstützen. In der Regel können nicht R-Lösungen, die basierend auf standardmäßigen CRAN Pakete in einem Kontext remote Compute ausgeführt, obwohl sie ausgeführt werden können, auf die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Computer, wenn von T-SQL gestartet. Sie können jedoch die `rxExec` -Funktion einzelne R-Funktionen aufrufen, und führen Sie sie Remote in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  
  
 Beispiele für das Erstellen und Arbeiten mit Datenquellen und Ausführungskontexte finden Sie in diesen Lernprogrammen:
 
 + [Data Science Deep Dive](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
 +  [RevoScaleR SQL Server – Erste Schritte](https://msdn.microsoft.com/microsoft-r/rserver/rserver-scaler-sql-server-getting-started).  
  
## Bereitstellen von R-Code für die Produktion  
 Ein wichtiger Teil der Data Science ist die Bereitstellung Ihrer Analysen für andere Benutzer oder die Verwendung von Vorhersagemodellen zur Optimierung von Geschäftsergebnissen oder -prozessen. In [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], es ist einfach, zur Produktion wechseln, wenn Ihre R-Skript oder das Modell bereit ist.  
  
 Weitere Informationen, wie Sie den Code für die Ausführung im verschieben können [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], finden Sie unter [R-Code betrieblichen](../../advanced-analytics/r-services/operationalizing-your-r-code.md).  
  
 Normalerweise beginnt der Bereitstellungsprozess mit dem Bereinigen Ihres Skripts, um den für die Produktion nicht erforderlichen Code zu entfernen. während des Verschiebens Berechnungen näher auf die Daten möglicherweise Möglichkeiten, effizienter verschieben, zusammenfassen oder präsentieren von Daten als das alles in R.  
  
 Es wird empfohlen, dass die Datenanalysten finden Sie in einem Datenbank-Entwickler über Methoden zur Verbesserung der Leistung, insbesondere dann, wenn die Lösung kann die DatenBereinigung oder Verarbeiten von Funktionen, die in SQL effektiver sein. Änderungen an ETL-Prozesse können erforderlich sein, um Stellen Sie sicher, dass Workflows zum Erstellen bzw. einem Bewertungsmodell fehlschlagen nicht und Eingabedaten im richtigen Format verfügbar ist.  
  
##  <a name="bkmk_SQLInR"></a> In diesem Abschnitt  

[Vergleich der ScaleR und CRAN R-Funktionen](Summary%20of%20rx%20Functions.md)

[ScaleR Funktionen zum Arbeiten mit SQLServer](../../advanced-analytics/r-services/scaler-functions-for-working-with-sql-server-data.md)
   
## Siehe auch  

 
 [SQL Server R Services – Features und Aufgaben](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)   
 
 [Operationalisieren Ihres R-Codes](../../advanced-analytics/r-services/operationalizing-your-r-code.md)  
  
  