---
title: "Erste Schritte mit Microsoft R Server (eigenst&#228;ndig) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "r-server"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 52347d0d-ce60-4bb8-98d2-6163e87716b0
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 16
---
# Erste Schritte mit Microsoft R Server (eigenst&#228;ndig)
  Mit Microsoft R Server (eigenständig) können Sie die beliebte Open Source-R-Sprache in Ihrem Unternehmen einführen, um leistungsfähige Analyselösungen und die Integration mit anderen Unternehmensanwendungen zu ermöglichen.  
  
## Was ist Microsoft R Server?  
 Microsoft R Server (eigenständig) enthält die von Revolution Analytics entwickelten erweiterten R-Pakete und unterstützt Verbindungen mit unterschiedlichen Datenquellen wie Hadoop oder Teradata. Durch die Installation des eigenständigen Servers können Sie eine Serverumgebung zur Ausführung komplexer, skalierbarer R-Aufträge erstellen.  
  
## Vorteile der Verwendung von Microsoft R-Server (eigenständig)  
 R ist die weltweit leistungsstärkste Programmiersprache für statistische Berechnungen, maschinelles Lernen und Grafiken und wird von einer stark wachsenden globalen Community von Benutzern, Entwicklern und Mitwirkenden unterstützt. Bisher führte die Verwendung von R in einer Unternehmensumgebung zu einigen Herausforderungen, besonders wenn das Datenvolumen anstieg oder wenn Sie Lösungen in Produktionsumgebungen bereitstellen mussten. Microsoft R Server löst das Problem der Bereitstellung und Operationalisierung von R-Code.  
  
 Microsoft R-Server kann auf jedem Windows-Computer installiert werden und umfasst alle R-Pakete und Konnektivitätstools remote Compute-Kontext zu aktivieren und skalierbare, parallelisierbar-Lösungen unterstützen.  
  
 Microsoft-R-Server (eigenständig) unterstützt diese Szenarien:  
  
-   **Verwenden eines zentralen Servers zum Operationalisieren von R-Lösungen**  
  
     Der eigenständige Server bietet Ihnen eine verbesserte R-Leistung, die sich nicht auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verlässt. Komplexe oder ressourcenintensiven Berechnungen können auf dem Server, sondern auf einem Laptop oder Entwicklung ausgeführt werden, die Ressourcen möglicherweise eingeschränkt.  
  
     Sie können Aufträge auch zentralisieren, z. B. ggf. für ein Vorhersagemodell in der Produktion bewerten, oder verwenden Sie zeichnet den R-Server als eine einzige Anlaufstelle für R Vorhersagen, die im Bericht verwendet. 
     
     Außerdem wird empfohlen, dass Sie R-Server (eigenständig) auf dem SQL Server-Computer installieren, wenn Sie häufig R im Kontext von SQL Server ausführen müssen.
  
-   **Aktivieren einer leistungsfähigeren Datensuche und Vorhersagemodellierung**  
  
     Der Datenanalyst kann jede Clientarbeitsstation und beliebige R-Entwicklungstools verwenden, um R-Lösungen zu erstellen. Wenn für die Lösung die RevoScaleR-Paket-APIs verwendet werden, können Berechnungen auf dem Server ausgeführt werden, der in der Regel über eine sehr viel größere Leistung und mehr Arbeitsspeicher verfügt. Daher können Ihre Lösungen mit viel größeren Datasets arbeiten und Berechnungen mit mehreren Threads, Kernen und Prozessen nutzen.  
  
## Wie erhalte ich diese?  
 Die Installationsanweisungen finden Sie unter [Create a Standalone R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md). Alle Komponenten können installiert werden, mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup.  
  
## Zusätzliche R-Tools installieren  
 Wenn Sie eine bevorzugte R Entwicklungsumgebung haben, sind viele Optionen. Weitere Informationen finden Sie unter [einrichten oder Konfigurieren von R-Tools](../../advanced-analytics/r-services/setup-or-configure-r-tools.md). 
 
 Für eine Verbindung mit Microsoft-R-Server mit SQL Server-R-Services von einer Data Science-Arbeitsstation, empfehlen wir die kostenlosen [Microsoft R Client](http://aka.ms/rclient/download) (download).  
  
## R-Skript ausführen, auf Microsoft R-Server (eigenständig)  
 Nachdem Sie die Server-Komponenten einrichten und Ihrer bevorzugten R IDE installiert haben, können Sie mit der Entwicklung der Projektmappe mithilfe des Pakets RevoScaleR beginnen. Mit diesen APIs können Sie R-Befehle für die Ausführung an einen Remoteserver senden.  
  
-   [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started): zunächst untersuchen diese Sammlung von verteilbaren analytischen Funktionen, die hohen Leistung bereitstellen und Skalieren auf R-Lösungen. Enthält parallelisierbar Versionen von vielen der beliebtesten r Pakete wie k-Means-clustering, Entscheidungsstrukturen und entscheidungswälder und Tools für die Bearbeitung von Daten zu modellieren. HPC können auch um Ihre eigenen parallelen Algorithmus zu erstellen.  
    
-   [DeployR](https://msdn.microsoft.com/microsoft-r/deployr-about): Dieses optionale Framework bietet die Tools für R-Programmierern, Java, JavaScript oder .net verwenden, um die Ausgabe eines Pakets von Drittanbietern R-Analyse zu integrieren.  

Sie können mit Daten in einer Vielzahl von Formaten, einschließlich SAS, SPSS, Hadoop und Text-Dateien arbeiten. Sie können Daten zu analysieren oder Ihre Daten effizient in Ihrer lokalen R-Entwicklungsumgebung, die mit dem Dateiformat .xdf verschieben.  
  
Zum Einstieg in R-Server finden Sie unter diesem Handbuch in der MSDN Library: [R Server – Erste Schritte](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started)  
  
 Informationen zum Verwenden der ScaleR-Pakete finden Sie unter [ein R-Lernprogramm in 25 Funktionen](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started#an-r-tutorial-in-25-functions-or-so)  
  
## Siehe auch  
 [Erste Schritte mit SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  