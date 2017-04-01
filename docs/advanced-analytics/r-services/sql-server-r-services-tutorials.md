---
title: "SQL Server R Services-Tutorials | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 5ccc75f6-6703-47d9-b879-9a740569b45e
caps.latest.revision: 31
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 27
---
# SQL Server R Services-Tutorials
In diesen Tutorials erfahren Sie mehr über [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] und die unterstützten Data Science-Szenarios, einschließlich:

+ dem Entwickeln von Modellen in R und deren Bereitstellung in SQL Server
+ dem Operationalisieren von R-Code mithilfe der Bereitstellung einer R-Lösung, die von einem Datenanalysten entwickelt wurde, auf einem Server oder einer anderen Produktionsumgebung.
+ dem Verschieben von Daten zwischen R und SQL Server
+ dem Verwenden von lokalen Computekontexten und Remotecomputekontexten
  

## <a name="a-namebkmkend-to-endadeveloping-an-end-to-end-advanced-analytics-solution"></a><a name="bkmk_end-to-end"></a>Entwickeln einer lückenlosen Advanced Analytics-Lösung  

[Lückenlose exemplarische Data Science-Vorgehensweise](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md) 

Erleben Sie den Data Science-Prozess lückenlos, von der Datenerfassung und -analyse bis hin zur Bewertung. Erfahren Sie, wie Sie Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwenden und Ihr Modell durch das Speichern in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] operationalisieren.  
Sie importieren das New York City Taxi-Dataset mithilfe von PowerShell in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und untersuchen die Daten mit R. 

Sie erstellen anschließend ein Vorhersagemodell und stellen das R-Modell zur Bewertung im Bath- und Einzelvorhersagemodus in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereit. 

  
Dieses Tutorial richtet sich an Personen, die sowohl mit R als auch mit Entwicklertools wie PowerShell und SQL Server Management Studio vertraut sind. Sie sollten über Zugang zu einer R-Entwicklungsumgebung verfügen und mit R-Befehlen vertraut sein. 
  
## <a name="a-namebkmkdatascienceadata-science-deep-dive"></a><a name="bkmk_dataScience"></a>Tieferer Einblick in Data Science  

[Erste Schritte mit RevoScaleR und SQL Server](http://go.microsoft.com/fwlink/?LinkID=691640&clcid=0x809)  

Diese exemplarische Vorgehensweise ist ein guter Ausgangspunkt für Datenanalysten oder Entwickler, die bereits mit der Sprache R vertraut sind und etwas über die erweiterten R-Pakete und -Funktionen in Microsoft R von Revolution Analytics lernen möchten. 

Sie erfahren, wie die Funktionen in den ScaleR-Paketen zum Verschieben von Daten zwischen R und SQL und zum Wechseln von Computekontexten entsprechend einer bestimmten Aufgabe verwendet werden. Sie erstellen verschiedene Modelle und Diagramme und verschieben diese zwischen Ihrer Entwicklungsumgebung und SQL Server.  
  
Dieses Tutorial richtet sich an Personen, die R bereits verwenden und mehr darüber erfahren möchten, wie RevoScaleR und SQL Server die Arbeit in R erleichtern können.

## <a name="in-database-advanced-analytics-for-the-sql-developer"></a>Datenbankinterne Advanced Analytics für SQL-Entwickler  
  
[Datenbankinterne Advanced Analytics für SQL-Entwickler &#40;Tutorial&#41;](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)

Erstellen Sie eine vollständige Lösung für erweiterte Analysen mithilfe von [!INCLUDE[tsql](../../includes/tsql-md.md)], und stellen Sie diese bereit. Dieses Beispiel konzentriert sich darauf, wie die Open Source-Sprache R in das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbankmodul integriert werden kann. Sie erfahren, wie Sie R-Code in einer gespeicherten Prozedur umschließen können, ein R-Modell in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank speichern können und parametrisierte Aufrufe des R-Modells für die Vorhersage durchführen können. 
  
Dieses Tutorial richtet sich an SQL-Entwickler, Anwendungsentwickler oder SQL-DBAs, die R-Lösungen unterstützen und erfahren möchten, wie R-Modelle in SQL Server bereitgestellt werden.  Eine R-Umgebung ist nicht erforderlich. Der gesamte R-Code wird bereitgestellt, und Sie können die vollständige Lösung ausschließlich mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und der üblichen Business Intelligence- und SQL-Entwicklungstools erstellen.   

## <a name="use-r-services-in-an-application"></a>Verwenden von R Services in einer Anwendung

[Build an intelligent app with SQL Server and R](https://www.microsoft.com/sql-server/developer-get-started/r) (Erstellen einer intelligenten App mit SQL Server und R)

In diesem Tutorial erfahren Sie, wie ein Skiverleih Machine Learning einsetzen könnte, um zukünftige Verleihe vorherzusagen. Dies hilft dem Geschäft und den Mitarbeitern, der zukünftigen Nachfrage zu begegnen.


## <a name="using-r-code-in-t-sql"></a>Verwenden von R-Code in T-SQL  

[Verwenden von R-Code in Transact-SQL &#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)  

Dies ist eine Reihe kurzer, eigenständiger Beispiele, die die grundlegende Syntax zum Verwenden von R in [!INCLUDE[tsql](../../includes/tsql-md.md)] veranschaulichen. 

Sie erfahren, wie Sie die R-Laufzeit in SQL aufrufen, lernen die Hauptunterschiede bei Datentypen zwischen R und SQL kennen, umschließen R-Funktionen in SQL-Code und führen eine gespeicherte Prozedur aus, die die R-Ausgabe in einer SQL-Tabelle speichert.
  
Dieses Tutorial richtet sich an Personen, die keinerlei Vorkenntnisse mit R-Diensten mitbringen und die Grundlagen des Aufrufens von R mithilfe von T-SQL erfahren möchten. Erfahrung mit R ist nicht erforderlich. Sie sollten jedoch wissen, wie Sie SQL Server Management Studio oder ein anderes Tool verwenden, das eine Verbindung zu einer Datenbank herstellen, und einfache T-SQL-Abfragen ausführen kann.

  
## <a name="a-namebkmkprerequisitesaprerequisites"></a><a name="bkmk_Prerequisites"></a>Voraussetzungen
  
Um eines der folgenden Tutorials auszuführen, müssen Sie **R Services (datenbankintern)** herunterladen und installieren, wie unter [Einrichten von SQL Server R Services (In-Database)](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md) beschrieben.

Nach dem Ausführen des SQL Server-Setups, dürfen Sie nicht diese zusätzlichen Schritte vergessen:
+ Aktivieren von R Services durch Ausführen von *sp_configure*
+ Neustarten des Servers
+ Sicherstellen, dass der Dienst, der die R-Laufzeit aufruft, über die erforderlichen Berechtigungen verfügt
+ Sicherstellen, dass die SQL-Anmeldung oder das Windows-Benutzerkonto, das Sie für Ihren R-Code verwenden, über die erforderlichen Berechtigungen für die Verbindungsherstellung mit dem Server und dessen Datenbanken verfügt

Wenn Schwierigkeiten auftreten, finden Sie in diesem Artikel einige der häufigsten Probleme: [Häufig gestellte Fragen zu Upgrade und Installation (SQL Server R Services)](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md).

Wenn Sie noch keine bevorzugte R-Entwicklungsumgebung haben, können Sie für den Einstieg eines dieser Tools installieren:

+ [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-get-started)
+ [R-Tools für Visual Studio](https://www.visualstudio.com/vs/rtvs/)

Beachten Sie, dass die R-Standardbibliotheken für diese Tutorials nicht ausreichen. Sowohl Ihre R-Entwicklungsumgebung als auch der SQL Server-Computer, auf dem R ausgeführt wird, müssen über ScaleR-Pakete von Microsoft verfügen. Weitere Informationen zu den in Microsoft R enthaltenen Funktionen und Funktionalitäten finden Sie unter [Microsoft R Products (Microsoft R-Produkte)](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started#compare-prods).

## <a name="additional-resources"></a>Zusätzliche Ressourcen

Wenn Sie diese Tutorials abgeschlossen haben, verwenden Sie die folgenden Links, um erweiterte Szenarios und Beispiele anzuzeigen.
  
### <a name="end-to-end-solution-templates-for-key-machine-learning-tasks"></a>Ende-zu-Ende-Lösungsvorlagen für die wichtigsten Machine Learning-Tasks  

[Machine Learning Templates with SQL Server 2016 R Services (Vorlagen für das maschinelle Lernen mit SQL Server 2016 R Services)](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/)  

Das Microsoft Machine Learning-Team hat anpassbare Vorlagen bereitgestellt, die Ihnen beim Schnelleinstieg in eine Lösung für diese entscheidenden Tasks im Bereich maschinelles Lernen weiterhelfen:  
* Betrugserkennung  
* Vorhersage der Kundenabwanderung  
* Vorbeugende Wartung  
  
Es werden der vollständige T-SQL- und R-Code bereitgestellt sowie Anweisungen, wie ein Modell für die Bewertung mithilfe von gespeicherten SQL Server-Prozeduren trainiert und bereitgestellt wird. 

### <a name="sample-data-and-sample-scripts"></a>Beispieldaten und Beispielskripts  
Produktbeispiele für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] sind im Microsoft Download Center verfügbar. Um nur die Beispiele für [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] abzurufen, wählen Sie die ZIP-Datei aus, und öffnen Sie den Ordner **Advanced Analytics**.  Einige der Anweisungen gelten für frühere Versionen, es gibt aber eine Demo zum Versicherungsbetrug auf Grundlage des Benfordschen Gesetzes und eine einfache Exemplarische Vorgehensweise zu einem Vorhersagemodell für ein sehr kleines Dataset (Iris-Dataset), das für Demos nützlich sein kann.
  
[SQL Server 2016 Produktbeispiele](https://www.microsoft.com/en-us/download/details.aspx?id=49502)  
### <a name="learn-more-about-r"></a>Weitere Informationen zu R  
Um mehr über R im Allgemeinen zu erfahren, sehen Sie sich eine der vielen hervorragenden Ressourcen an, die [auf der Seite für Microsoft R Server](http://revolutionanalytics.com/r-language-resources)aufgeführt sind.  
  
Weitere zusätzliche Informationen über die R-Pakete, die in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]bereitgestellt werden, finden Sie auf der  [Seite von für Microsoft R Server](http://go.microsoft.com/fwlink/?LinkId=691541).  
  
Der folgende Blogbeitrag umfasst sowohl den Beispielcode als auch eine Beschreibung des Verwendungsprozesses der R-Pakete und -Funktionen, die von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] zum Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]bereitgestellt werden: [Using R inside SQL Server](http://blog.revolutionanalytics.com/2015/10/previewing-using-revolution-r-enterprise-inside-sql-server.html)(Verwenden von R in SQL Server).  
  
## <a name="see-also"></a>Siehe auch  
[Erste Schritte mit SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
[SQL Server R Services: Features und Aufgaben](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)  
  
