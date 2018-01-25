---
title: "Data Science-Szenarien und Lösungsvorlagen | Microsoft Docs"
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
ms.assetid: 49e54fa9-9b28-44ba-b256-06dad4e8dece
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 3c180282735da59d8d3dfa039e70d0eea5ebd7e5
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="data-science-scenarios-and-solution-templates"></a>Data Science-Szenarien und -Projektmappenvorlagen

Vorlagen sind Beispiellösungen, die bewährte Methoden veranschaulichen und Bausteine für die schnelle Implementierung einer Lösung bereitstellen. Jede Vorlage dient zur Lösung eines bestimmten Problems, für einen bestimmten vertikal oder Branche. Die Tasks in jeder Vorlage reichen von der Datenvorbereitung und Featureentwicklung bis hin zum Modelltraining und zur Bewertung. Diese Vorlagen verwenden, um zu erfahren, wie [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] funktioniert. Anschließend können Sie anpassen, die Vorlage, um Ihr eigenes Szenario anpassen und erstellen Sie eine benutzerdefinierte Lösung. 

Jede Lösung enthält Beispieldaten, R-Code oder Python-Code sowie SQL gespeicherten Prozeduren aus, falls zutreffend. Der Code kann in Ihrer bevorzugten Entwicklungsumgebung R oder Python mit Berechnungen, die im SQL Server durchgeführt wird, ausgeführt werden. In einigen Fällen können Sie Code direkt mit T-SQL und alle SQL-Clienttool, wie z. B. SQL Server Management Studio ausführen.

> [!TIP]
> 
> Die meisten der Vorlagen gibt es mehrere Versionen unterstützen sowohl lokal und cloud-Plattformen für maschinelles lernen. Z. B. können Sie erstellen Sie die Projektmappe, die nur SQL Server verwenden, oder Sie können die Lösung in Microsoft R Server oder in Azure Machine Learning erstellen.

+ Weitere Informationen und Updates finden Sie unter dieser Ankündigung: [interessante neue Vorlagen in Azure ML](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

+ Download und installationsanweisungen finden Sie unter [wie mithilfe der Vorlagen](#bkmk_HowTo).

## <a name="fraud-detection"></a>Betrugserkennung

[Online-Betrug Erkennung Vorlage (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)

**Was:** die Fähigkeit, betrügerische Transaktionen zu erkennen ist wichtig für Onlineunternehmen. Um Chargeback-Verluste zu verringern, müssen Unternehmen Transaktionen, die mit gestohlenen Zahlungsweise oder Anmeldeinformationen vorgenommen wurden, schnell zu identifizieren. Wenn die betrügerische Transaktionen erkannt werden, ergreifen Unternehmen in der Regel Maßnahmen, um bestimmte Konten so früh wie möglich zu blockieren, um weitere Verluste zu vermeiden. In diesem Szenario erfahren Sie, wie Sie Daten aus Transaktionen, online-Kauf um wahrscheinlich Betrug zu identifizieren.

**Vorgehensweise:** Fraud Detection ist als ein binäres klassifikationsproblem gelöst. Die Methodik, die in dieser Vorlage verwendet wird, kann problemlos auf die Betrugserkennung in anderen Domänen angewendet werden.


## <a name="campaign-optimization"></a>Optimierung der Kampagne

[Vorhersagen, wie und wann Leads kontaktieren](https://microsoft.github.io/r-server-campaign-optimization/)

**Was:** diese Lösung verwendet Versicherungsbranche Daten basierend auf demografischen Daten, die Verlaufsdaten Antwortdaten und produktspezifische Details Leads vorherzusagen.  Empfehlungen werden auch generiert, um anzugeben, die beste Kanal und Zeit für Ansatz Benutzer zum Kaufverhalten beeinflussen.

**Vorgehensweise:** die Projektmappe erstellt, und mehrere Modelle verglichen. Die Lösung zeigt auch automatisierte Datenintegration und die Vorbereitung der Daten mithilfe von gespeicherten Prozeduren. Parallele Beispiele werden für SQL Server in-Datenbank, in Azure HDInsight Spark bereitgestellt. 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>Gesundheitswesen: Dauer der Krankenhaus Vorhersagen 

[Dauer der Krankenhäusern Vorhersagen](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**Was:** genau Vorhersagen, welche Patienten langfristigen Krankenhausaufenthalt möglicherweise ist ein wichtiger Teil von Sorgfalt und Planung. Administratoren müssen in der Lage, um zu bestimmen, welche Funktionen mehr Ressourcen benötigen, und Betreuer sicherstellen möchten, dass diese den Bedürfnissen von Patienten können.

**Vorgehensweise:** dieser Lösung verwendet die Data Science Virtual Machine und eine Instanz von SQL Server mit Machine Learning aktiviert. Darüber hinaus eine Reihe von Power BI-Berichten, die Sie für die Interaktion mit einem bereitgestellten Modell verwenden können.

## <a name="customer-churn"></a>Änderungsumfang von Kunden

[Kunden Änderungsumfang Vorhersage Vorlage (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/Introduction.md)

**Was:** analysieren und Vorhersagen von Kunden codeänderung ist wichtig, in allen Branchen, bei der Verlust von Kunden an die Konkurrenz verwaltet und verhindert werden muss: Bankgeschäfte, Telekommunikation und Einzelhandel, um nur einige zu nennen. Das Ziel der Abwanderungsanalyse ist es, zu identifizieren, welche Kunden möglicherweise abwandern und anschließend angemessene Maßnahmen einzuleiten, um diese Kunden zu behalten und weiterhin Geschäfte mit ihnen zu machen.

**Vorgehensweise:** dieser Vorlage formuliert, die codeänderung Problem als ein **binäre Klassifizierung** Problem. Es werden Beispieldaten aus zwei Quellen verwendet, Kundendemografie und Kundentransaktionen, um zu klassifizieren, ob Kunden wahrscheinlich oder eher unwahrscheinlich abwandern.
  
## <a name="predictive-maintenance"></a>Vorbeugende Wartung

[Vorbeugende Wartung-Vorlage (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/Introduction.md)

**Was:** vorbeugende Wartung zielt darauf ab, die Effizienz von Wartungstasks erhöhen, indem Sie ältere Fehler erfassen und diese Informationen verwenden, um vorherzusagen, wann oder wo ein Gerät kann nicht ausgeführt. Die Möglichkeit, das veralten von Gerät zu prognostizieren ist besonders nützlich für Anwendungen, die verteilte Daten oder Sensoren benötigen. Diese Methode kann auch zum Überwachen oder Vorhersagen Fehler in IoT (Internet of Things) Geräte angewendet werden.

Finden Sie unter dieser Ankündigung für Weitere Informationen: [Vorlage für die vorbeugende Wartung](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

**Vorgehensweise:** diese Lösung konzentriert sich auf die Beantwortung der Frage "Bei ein Computer in Betrieb befindlichen fehl?" Die Eingabedaten stellen simulierte Sensormessungen für Flugzeugtriebwerke dar. Von der Überwachung des Moduls aktuellen Vorgang Bedingungen erfüllt, wie die aktuelle Arbeit Zyklus, Einstellungen und Sensor Messungen, abgerufene Daten werden verwendet, um die drei Arten von Vorhersagemodellen erstellen:

-   **Regressionsmodelle**, um vorherzusagen, wie viel länger ein Triebwerk arbeitet, bis es ausfällt. Das Beispielmodell vorhersagt, die Metrik "Verbleibende Lebensdauer" (RUL), auch als "Zeit auf Fehler" (TTF) bezeichnet wird.
  
-   **Klassifizierungsmodelle**, um vorherzusagen, ob ein Triebwerk womöglich ausfällt.
  
    Die **binäres klassifizierungsmodell** vorhersagt, wenn ein Modul innerhalb eines bestimmten Zeitraums aufgetretenen fehl.

    Die **multiklassenklassifizierung Modell** vorhersagt, ob ein bestimmtes Modul möglicherweise fehlschlägt, und ein Zeitfenster ein wahrscheinlich der Fehler aufgetreten bietet. Für einen bestimmten Tag können Sie z.B. vorhersagen, ob ein Gerät an diesem bestimmten Tag womöglich ausfallen wird oder innerhalb einer Zeitspanne ab diesem bestimmten Tag.

## <a name="energy-demand-forecasting"></a>Energie Demand forecasting

[Energie Demand forecasting Vorlage mit SQL Server R Services](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**Was:**: Demand forecasting ist ein wichtiges Problem in verschiedenen Domänen einschließlich Energie, Verkaufs- und Dienste. Genaue Anforderung Prognose helfen dem Unternehmen, die eine bessere Planung, ressourcenzuweisung, Produktion durchführen und andere wichtige geschäftsentscheidungen. In den Energiesektor ist die Anforderung Prognose für Senkung der Speicherkosten Energie und Ausgleichen von Angebot und Nachfrage entscheidend.

**Vorgehensweise:** dieser Vorlage verwendet SQL Server R Services, um bei Bedarf für Elektrizität vorherzusagen. Das Modell für die Vorhersage verwendet wird, einer zufälligen Gesamtstruktur Regressionsmodell basierend auf **RxDForest**, eine hohe Leistung Algorithmus für maschinelles lernen in Microsoft R Server enthalten. Die Lösung umfasst einen Bedarfs-Simulator sowie alle erforderlichen R- und T-SQL-Codes, um ein Modell zu trainieren sowie gespeicherte Prozeduren, die Sie zum Generieren und Melden von Vorhersagen verwenden können. 


## <a name="bkmk_HowTo"></a>Gewusst wie: Verwenden Sie die Vorlagen

Zum Herunterladen der Dateien in den einzelnen Vorlagen können Sie GitHub-Befehle verwenden, oder Sie öffnen den Link und klicken auf **Download Zip** (Herunterladen der ZIP-Dateien), um alle Dateien auf Ihrem Computer zu speichern.  Wenn die Projektmappe heruntergeladen wurde, enthält sie in der Regel folgende Ordner:
  
-   **Daten**: enthält die Beispieldaten für jede Anwendung.
  
-   **R**: enthält alle Entwicklungscodes von R, die Sie für die Projektmappe benötigen. Die Projektmappe benötigt die Bibliotheken, die von Microsoft R Server bereitgestellt werden, doch sie kann in jeder beliebigen R-IDE geöffnet und bearbeitet werden. Der R-Code wurde optimiert, sodass Berechnungen „datenbankintern“ durch Festlegen des Computekontexts auf eine SQL Server-Instanz ausgeführt werden.
  
-   **SQLR**: enthält mehrere SQL-Dateien, die Sie in einer SQL-Umgebung, z.B. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , ausführen können, um die gespeicherten Prozeduren zu erstellen, die verwandte Tasks wie Datenverarbeitung, Featureentwicklung und Modellbereitstellung ausführen.
  
    Der Ordner enthält außerdem ein PowerShell-Skript, das Sie ausführen können, um alle Skripts aufzurufen und die Ende-zu-Ende-Umgebung zu erstellen. Denken Sie daran, das Skript an Ihre Umgebung anzupassen.

## <a name="next-steps"></a>Nächste Schritte

+ [SQL Server Machine Learning-Lernprogramme](machine-learning-services-tutorials.md)




