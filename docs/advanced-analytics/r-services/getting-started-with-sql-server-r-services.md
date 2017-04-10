---
title: "Erste Schritte mit SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/07/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 5b28a663-effe-41f6-9bda-eda95f0c6943
caps.latest.revision: 34
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 32
---
# Erste Schritte mit SQL Server R Services
 Ein typischer Workflow für das Erstellen einer erweiterten Analyselösung beginnt mit der Datenauswertung und der Vorhersagemodellierung, während der Datenanalyst R-Skripts und -Modelle entwickelt, die für die aktuelle Aufgabe nützlich sind. Wenn die Skripts und Modelle bereitstehen, können sie in der Produktion bereitgestellt und in vorhandene oder neue Anwendungen integriert werden.   
  
SQL Server R Services soll Sie bei diesen Data Science-Aufgaben unterstützen. Sie können weiterhin mit Ihren bevorzugten R- oder SQL-Tools arbeiten und die Analyse dabei auf Milliarden von Datensätzen ausweiten, ohne zusätzliche Hardware zu installieren und die Leistung steigern zu müssen. So vermeiden Sie das unnötige Verschieben von Daten. Sie können Ihren R-Code nun in der Produktionsumgebung verwenden, ohne ihn in einer anderen Sprache neu schreiben zu müssen. So wird auch die Verwendung von R für möglicherweise schwer mit SQL implementierbare statistische Berechnungen erleichtert. Gleichzeitig können Sie die umfassenden SQL Server-Funktionen wie z.B. das In-Memory-Datenbankmodul und Columnstore-Indizes nutzen, um maximale Leistung zu erzielen.  
  
Die folgenden Abschnitte stellen eine grobe Übersicht über einige übliche analytische Workflows und ihre Aktivierung mit SQL Server R Services bereit.  

> [!TIP] Mit diesem Tutorial gelingt Ihnen der schnelle Einstieg. Sie erfahren, wie sich ein Skiverleih maschinelles Lernen bei der Vorhersage von zukünftigen Verleihen und der Mitarbeiterplanung zunutze machen kann, um die Nachfrage zu decken.
> 
> [Build an intelligent app with SQL Server and R](https://www.microsoft.com/sql-server/developer-get-started/r) (Erstellen einer intelligenten App mit SQL Server und R)


  
-   **Entwickeln**  
  
     Datenanalysten verwenden R in der Regel auf ihren Arbeitsstationen zum Untersuchen von Daten und zum Generieren von Vorhersagemodellen mithilfe einer R-IDE ihrer Wahl. Der Datenanalyst durchläuft Tests und Optimierungen, bis ein geeignetes Vorhersagemodell erreicht ist. 
     
     [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]-Clientkomponenten stellen für Datenanalysten sämtliche Tools bereit, die zum Experimentieren und Entwickeln erforderlich sind. Zu diesen Tools zählen die R-Laufzeitversion, die mathematische Kernelbibliothek von Intel zur Leistungssteigerung von R-Standardfunktionen sowie eine Reihe von erweiterten R-Paketen, die das Ausführen von R-Code in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützen.  
  
     Datenanalysten können eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und dem Client die Daten wie gewohnt zur lokalen Analyse vorlegen. Die Verwendung der **ScaleR**-APIs zum Verlagern von Berechnungen mittels Push auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Computer, um kostenintensive und unsichere Datenbewegungen zu vermeiden, ist jedoch die bessere Lösung.  
  
     Zur Entwicklung von R-Lösungen können die Datenanalysten eine beliebige Windows-basierte IDE verwenden, die R unterstützt, einschließlich [R-Tools für Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx) oder RStudio.  
 
    ![rsql_keyscenario2](../../advanced-analytics/r-services/media/rsql-keyscenario2.PNG) 
 
     Weitere Informationen zu diesem Szenario finden Sie unter [Datensuche und Vorhersagemodellierung mit R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md).  

  
-   **Optimieren**  
  
     Bei der Analyse großer Datasets mit R treten bei den Datenanalysten häufig Leistungs- und Skalierungsprobleme auf, da die Implementierung des allgemeinen Laufzeitmoduls nur einen einzelnen Thread verwendet und nur die Datasets unterstützt, die auf dem lokalen Computer in den verfügbaren Arbeitsspeicher passen. Datenanalysten können erweiterte **ScaleR**-APIs verwenden, die als Teil von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] bereitgestellt werden, um höhere Leistungen zu erzielen und mit größeren Datenmengen arbeiten zu können. Das **RevoScaleR**-Paket enthält z.B. die Implementierung einiger der beliebtesten R-Funktionen, die umgestaltet wurden, um Parallelität und Skalierung bereitzustellen. Das Paket enthält auch Funktionen, die die Leistung und Skalierung weiter erhöhen, indem Berechnungen mittels Push auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Computer übertragen werden, der in der Regel über wesentlich mehr Arbeitsspeicher und Rechenleistung verfügt.  
  
     Weitere Informationen zu diesem Szenario finden Sie unter [Datensuche und Vorhersagemodellierung mit R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md).  
  
-   **Bereitstellen**  
  
     Nachdem das R-Skript oder das Modell für die Produktionsumgebung bereit ist, kann ein Datenbankentwickler den Code oder das Modell in gespeicherte Prozeduren einbetten und den gespeicherten Code über eine Anwendung aufrufen. Das Speichern und Ausführen von R über [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bietet viele Vorteile: Sie können die komfortable [!INCLUDE[tsql](../../includes/tsql-md.md)]-Benutzeroberfläche verwenden. Außerdem erfolgen sämtliche Berechnungen in der Datenbank, wodurch unnötige Datenbewegungen vermieden werden. Sie können [!INCLUDE[tsql](../../includes/tsql-md.md)] verwenden, um die Bewertungen in der Produktion anhand eines Vorhersagemodells zu generieren oder um von R generierte Darstellungen zurückzugeben und diese in einer Anwendung wie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] darzustellen.  
  
     Zur weiteren Optimierung des R-Codes, der in gespeicherten Systemprozeduren eingebettet ist, wird die Verwendung von [ScaleR](https://msdn.microsoft.com/microsoft-r/rserver/rserver-scaler-getting-started)-Paket-APIs empfohlen, die sich für die Verarbeitung größerer Datasets eignen. Diese Pakete unterstützen die In-Database-Ausführung für Berechnungen mit mehreren Threads, Kernen und Prozessen.  
  
     Wenn Sie R-Code für die Produktion bereitstellen müssen, bietet [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] das Beste aus den Bereichen R und SQL. Sie können R für statistische Berechnungen verwenden, die mit SQL schwierig zu implementieren sind, und gleichzeitig die Leistungsfähigkeit von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nutzen, um die maximale Leistung mithilfe von Funktionen wie dem In-Memory-Datenbankmodul und Columnstore-Indizes zu erzielen.  
  
    ![rsql_keyscenario1](../../advanced-analytics/r-services/media/rsql-keyscenario1.PNG)  
  
     Weitere Informationen finden Sie unter [Operationalisieren Ihres R-Codes](../../advanced-analytics/r-services/operationalizing-your-r-code.md).  
 
 > [!TIP] In diesem Buch erfahren Sie, wie Sie SQL Server in Data Science integrieren. Es ist als kostenloser Download in der Microsoft Virtual Academy verfügbar: [Data Science with Microsoft SQL Server 2016 (Data Science mit Microsoft SQL Server 2016)](https://mva.microsoft.com/ebooks/)

-   **Verwalten und Überwachen**  
  
     [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] verwendet eine neue Erweiterbarkeitsarchitektur, die das Datenbankmodul sichert und R-Sitzungen isoliert. Außerdem haben Sie die Kontrolle über Benutzer, die R-Skripts ausführen können, und können angeben, auf welche Datenbanken der R-Code zugreifen darf. Sie können den Umfang der Ressourcen steuern, die der R-Laufzeit zugeordnet werden, um zu verhindern, dass umfangreiche Berechnungen die Gesamtleistung des Servers gefährden.  
  
     Wenn R-Aufträge in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt werden, können Sie auch die von Analysten verwendeten Daten steuern und überwachen oder Aufträge planen und Workflows erstellen, die R-Skripts enthalten, wie es auch mit anderen gespeicherten Prozeduren möglich wäre.  
  
     Weitere Informationen finden Sie unter [Verwalten und Überwachen von R-Lösungen](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md).  
  
  
-   **Integrieren**  
  
     Sie müssen Ihr IT-Budget nicht mehr für Unternehmenstools aufwenden, damit diese mit einer externen R-Laufzeitumgebung arbeiten können. Sie können in der vertrauten [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]-Umgebung arbeiten und integrierte Workflows und Berichtslösungen mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] entwickeln.  
  
     Weitere Informationen finden Sie unter [Erstellen von Workflows, die R in SQL Server verwenden](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md).  
  
  
## <a name="how-do-i-get-it"></a>Wie erhalte ich diese?  
   
  
+   **Installieren Sie [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC2 oder höher, und aktivieren Sie R-Services (datenbankintern).**  
  
    [Einrichten von SQL Server R Services &#40;In-Database&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  
-   **Richten Sie eine Clientarbeitsstation ein.**  
  
     [Einrichten eines Data Science-Clients](../../advanced-analytics/r-services/set-up-a-data-science-client.md)  
   
> [!TIP]   
>   
> Möchten Sie einen Server für R-Aufträge mit einem anderen Betriebssystem als SQL Server erstellen? Versuchen Sie es mit [Microsoft R Server](https://msdn.microsoft.com/library/mt674874.aspx).  
  
## <a name="how-to-run-r-code-using-sql-server-r-services"></a>So führen Sie R-Code mithilfe von SQL Server-R-Services aus  
 Nach der Installation können Sie R-Code unter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausführen, indem Sie R in der gespeicherten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur einbetten oder Ad-hoc-R-Skripts schreiben, die mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Daten arbeiten.  
  
-   Erfahren Sie, wie Sie R aus einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung aufrufen und die Ergebnisse in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] zurückgeben.  
  
     [Verwenden von R-Code in Transact-SQL](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)  
  
-   Erfahren Sie Grundlegendes zum vollständigen Flow zum Erstellen einer erweiterten Analyselösung und deren Bereitstellung mit SQL Server R Services:  
  
     [Lückenlose exemplarische Data Science-Vorgehensweise](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)  
  
-   Erfahren Sie, wie Sie das RevoScaleR-Paket für skalierbare und leistungsstarke Analysen verwenden und wie Sie R-Berechnungen mithilfe von Push auf den SQL Server-Computer übertragen:  
  
     [Tieferer Einblick in Data Science: Verwenden der RevoScaleR-Pakete](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
-   Betten Sie funktionierende R-Skripts in gespeicherte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozeduren ein, damit Sie Modelle für Vorhersagen aufrufen, Modelle erneut trainieren oder Vorhersagen aus Anwendungen abrufen können:  
  
     [Datenbankinterne Advanced Analytics für SQL-Entwickler](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
  
-   Verwenden Sie [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und verwandte Business Intelligence-Tools im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Stapel, um maschinelles Lernen zu automatisieren. Die Vorbereitung der Daten und Berichterstellung können mithilfe von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]automatisiert werden. Zeigen Sie grafische Darstellungen in R zusammen mit anderen Berichten mithilfe von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] oder Power View an.  
  
+ Weitere Beispiele, darunter Lösungsvorlagen und R-Beispielcode, finden Sie unter:  
   [SQL Server R Services Tutorials](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [Erste Schritte mit Microsoft R Server &#40;eigenständig&#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  