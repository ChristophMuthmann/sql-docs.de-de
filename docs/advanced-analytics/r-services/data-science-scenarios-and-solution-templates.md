---
title: "Szenarios f&#252;r Data Science und L&#246;sungsvorlagen | Microsoft Docs"
ms.custom: ""
ms.date: "04/18/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 49e54fa9-9b28-44ba-b256-06dad4e8dece
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# Szenarios f&#252;r Data Science und L&#246;sungsvorlagen
Vorlagen sind Beispiellösungen, die bewährte Methoden veranschaulichen und Bausteine für die schnelle Implementierung einer Lösung bereitstellen. Jede Vorlage wurde entwickelt, um ein bestimmtes Problem zu lösen und enthält Beispieldaten, R-Code (Microsoft R Server) und gespeicherte SQL-Prozeduren. Die Tasks in jeder Vorlage reichen von der Datenvorbereitung und Featureentwicklung bis hin zum Modelltraining und zur Bewertung. Der Code kann in einer R-IDE zusammen mit Berechnungen in SQL Server ausgeführt werden, oder unter Verwendung eines SQL-Clienttools, z.B. SQL Server Management Studio.  
  
Mithilfe dieser Vorlagen können Sie lernen, wie [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] funktioniert und Ihre eigene Lösung erstellen und bereitstellen, indem Sie die Vorlage so anpassen, dass Sie in Ihr Szenario passt.  
  
Anweisungen zum Download und zum Setup finden Sie unter [So verwenden Sie die Vorlagen](#bkmk_HowTo) am Ende dieses Themas.  
  
## Betrugserkennung  
[Online Fraud Detection Template (SQL Server R Services) (Online-Vorlage zur Betrugserkennung (SQL Server R Services))](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)  
  
Eines der wichtigen Aufgaben für das Onlinegeschäft ist es, betrügerische Transaktionen zu erkennen und die Transaktionen zu identifizieren, die durch gestohlene Zahlungsmittel oder Anmeldeinformationen getätigt wurden, um Verluste durch Rücklastschriften zu reduzieren. Wenn die betrügerische Transaktionen erkannt werden, ergreifen Unternehmen in der Regel Maßnahmen, um bestimmte Konten so früh wie möglich zu blockieren, um weitere Verluste zu vermeiden. In diesem Szenario erfahren Sie, wie Sie Daten von Online-Kaufvorgängen verwenden, um möglichen Betrug zu erkennen. Diese Methodik können Sie einfach auf die Betrugserkennung in anderen Domänen anwenden.  
  
In dieser Vorlage erfahren Sie, wie Sie Daten von Online-Kaufvorgängen verwenden, um möglichen Betrug zu erkennen. Die Betrugserkennung wird als binäres Klassifizierungsproblem gelöst. Die Methodik, die in dieser Vorlage verwendet wird, kann problemlos auf die Betrugserkennung in anderen Domänen angewendet werden.    
  
## Kundenabwanderung  
[Customer Churn Prediction Template (SQL Server R Services) (Online-Vorlage zur Kundenabwanderung (SQL Server R Services))](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/Introduction.md)  
  
Die Analyse und die Vorhersage von Kundenabwanderung ist für jede Branche wichtig, in der der Verlust von Kunden an Wettbewerber verwaltet und verhindert wird, z.B. im Bankwesen, in der Telekommunikation und im Einzelhandel, um ein paar zu nennen. Das Ziel der Abwanderungsanalyse ist es, zu identifizieren, welche Kunden möglicherweise abwandern und anschließend angemessene Maßnahmen einzuleiten, um diese Kunden zu behalten und weiterhin Geschäfte mit ihnen zu machen.  
  
Mit dieser Vorlage können Sie mit der Abwanderungsvorbeugung beginnen, indem Sie das Abwanderungsproblem als ein **binäres Klassifizierungsproblem** formulieren. Es werden Beispieldaten aus zwei Quellen verwendet, Kundendemografie und Kundentransaktionen, um zu klassifizieren, ob Kunden wahrscheinlich oder eher unwahrscheinlich abwandern.   
  
## Vorbeugende Wartung  
[Predictive Maintenance Template (SQL Server 2016) (Vorlage zur vorbeugenden Wartung (SQL Server 2016))](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/Introduction.md)  
  
Das Ziel der „datengesteuerten“ vorbeugenden Wartung ist die Verbesserung der Effizienz von Wartungstasks, indem in der Vergangenheit aufgetretene Fehler gesammelt werden, und diese Informationen benutzt werden, um vorherzusagen, wann oder wo bei einem Gerät möglicherweise Fehler auftreten. Die Möglichkeit die Veraltung von Geräten vorherzusagen, ist besonders wichtig für Anwendungen, die auf verteilten Daten oder Sensoren basieren, wie im Internet der Dinge (IoT) veranschaulicht wird.  
  
Diese Vorlage konzentriert sich auf die Beantwortung der Frage „Wann erzeugt ein in Betrieb genommener Computer einen Fehler?“ Die Eingabedaten stellen simulierte Sensormessungen für Flugzeugtriebwerke dar. Daten, die aus der Überwachung der aktuellen Betriebsbedingungen des Triebwerks stammen, z.B. der aktuelle Arbeitszyklus, Einstellungen, Sensormessungen usw., werden zur Erstellung von drei Typen von Vorhersagemodellen verwendet:  
  
-   **Regressionsmodelle**, um vorherzusagen, wie viel länger ein Triebwerk arbeitet, bis es ausfällt. Das Beispielmodell prognostiziert die Metrik „Remaining Useful Life“ (RUL, Verbleibende Nutzungsdauer), die auch „Time to Failure“ (TTF, Zeit bis zum Ausfall) genannt wird.  
  
-   **Klassifizierungsmodelle**, um vorherzusagen, ob ein Triebwerk womöglich ausfällt.  
  
    Das **binäre Klassifizierungsmodell** prognostiziert, ob ein Triebwerk innerhalb eines bestimmten Zeitraums (Anzahl von Tagen) ausfällt.  
  
    Das **mehrklassige Klassifikationsmodell** prognostiziert, ob ein bestimmtes Triebwerk ausfällt. Wenn es ausfällt, wird ein wahrscheinliches Zeitfenster des Ausfalls bereitgestellt. Für einen bestimmten Tag können Sie z.B. vorhersagen, ob ein Gerät an diesem bestimmten Tag womöglich ausfallen wird oder innerhalb einer Zeitspanne ab diesem bestimmten Tag.  
      
      
## Prognose des Energiebedarfs  
[Energy Demand Forecasting Template with SQL Server R Services (Vorlage zur Prognose des Energiebedarfs mit SQL Server R Services)](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast_Template_with_SQL-Server-R-Services-1)  
  
Diese Vorlage veranschaulicht, wie SQL Server-R-Services verwendet wird, um den Bedarf an Strom vorherzusagen. Die Lösung umfasst einen Bedarfs-Simulator sowie alle erforderlichen R- und T-SQL-Codes, um ein Modell zu trainieren sowie gespeicherte Prozeduren, die Sie zum Generieren und Melden von Vorhersagen verwenden können.   
  
## <a name="bkmk_HowTo"></a>So verwenden Sie die Vorlagen  
Zum Herunterladen der Dateien in den einzelnen Vorlagen können Sie GitHub-Befehle verwenden, oder Sie öffnen den Link und klicken auf **Download Zip** (Herunterladen der ZIP-Dateien), um alle Dateien auf Ihrem Computer zu speichern.  Wenn die Projektmappe heruntergeladen wurde, enthält sie in der Regel folgende Ordner:  
  
-   **Daten**: enthält die Beispieldaten für jede Anwendung.  
  
-   **R**: enthält alle Entwicklungscodes von R, die Sie für die Projektmappe benötigen. Die Projektmappe benötigt die Bibliotheken, die von Microsoft R Server bereitgestellt werden, doch sie kann in jeder beliebigen R-IDE geöffnet und bearbeitet werden. Der R-Code wurde optimiert, sodass Berechnungen „datenbankintern“ durch Festlegen des Computekontexts auf eine SQL Server-Instanz ausgeführt werden.  
  
-   **SQLR**: enthält mehrere SQL-Dateien, die Sie in einer SQL-Umgebung, z.B. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ausführen können, um die gespeicherten Prozeduren zu erstellen, die verwandte Tasks wie Datenverarbeitung, Featureentwicklung und Modellbereitstellung ausführen.  
  
    Der Ordner enthält außerdem ein PowerShell-Skript, das Sie ausführen können, um alle Skripts aufzurufen und die Ende-zu-Ende-Umgebung zu erstellen.  
  
    Denken Sie daran, das Skript an Ihre Umgebung anzupassen.  
  
  
## Siehe auch  
[SQL Server R Services-Tutorials](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
[Announcing the Templates in Azure ML (Ankündigung der Vorlagen in Azure ML)](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)  
[Ankündigung der neuen Vorlage zur vorbeugenden Wartung (in englischer Sprache)](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)  
  
  
  
