---
title: "Exemplarische Data Science Ende-zu-Ende-Vorgehensweise | Microsoft Docs"
ms.custom: ""
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
ms.assetid: edd76ae9-4125-45a8-bf42-47a85b9d9a32
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# Exemplarische Data Science Ende-zu-Ende-Vorgehensweise
In dieser exemplarischen Vorgehensweise werde eine Ende-zu-Ende-Lösung für die Vorhersagemodellierung mithilfe von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]entwickeln.  
  
Diese exemplarische Vorgehensweise basiert auf einem bekannten öffentlichen Dataset, dem Dataset New York City-Taxi. Sie werden eine Kombination aus R-Code, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten und benutzerdefinierten SQL-Funktionen verwenden, um ein Klassifikationsmodell zu erstellen, das die Wahrscheinlichkeit angibt, dass der Fahrer ein Trinkgeld für eine bestimmte Taxifahrt erhält. Sie stellen außerdem Ihr R-Modell für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereit und verwenden Serverdaten, um Bewertungen basierend auf dem Modell zu erstellen.  
  
Dieses Beispiel kann einfach auf alle möglichen realen Probleme übertragen werden, wie die Vorhersage von Reaktionen von Kunden auf Verkaufsaktionen oder die Vorhersage des Betrags, den Besucher bei Veranstaltungen ausgeben. Da das Modell aus einer gespeicherten Prozedur aufgerufen werden kann, können Sie es auch einfach in eine Anwendung einbetten.  
  
**Zielgruppe**  
  
Diese exemplarische Vorgehensweise ist für R-Entwickler vorgesehen. Sie sollten sich mit den grundlegenden Datenbankvorgängen auskennen, z.B. mit dem Erstellen von Datenbanken und Tabellen, dem Importieren von Daten in Tabellen und der Abfrage der Tabellen mithilfe von [!INCLUDE[tsql](../../includes/tsql-md.md)].  Sie erhalten die SQL- und R-Skripts zum Ausführen.  
  
Wenn Sie noch nicht mit R vertraut sind, jedoch mit Datenbanken, hält dieses Tutorial eine Einweisung bereit, wie R in Unternehmensworkflows mithilfe von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]integriert werden kann. Es ist keine R-Codierung erforderlich. Alle Skripts werden bereitgestellt. Zum Ausführen der Befehle ist es nicht nötig, dass Sie eine Art R-IDE installiert haben.  
  
**Voraussetzungen**  
  
Zum Ausführen dieses Tutorials benötigen Sie Zugriff auf eine Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , auf der [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] installiert ist. Bereiten Sie für Ihre lokale Umgebung eine Data Science-Arbeitsstation vor, der eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz herstellen kann, und installieren Sie anschließend die erforderlichen R-Bibliotheken.  
  
Weitere Informationen finden Sie unter [Voraussetzungen für die exemplarischen Vorgehensweisen für Data Science &#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/prerequisites-for-data-science-walkthroughs-sql-server-r-services.md).  
  
## <a name="overview"></a>Übersicht  
Diese exemplarische Vorgehensweise veranschaulicht eine typische Ende-zu-Ende-Lösung für die erweiterte Analyse. Sie müssen die Lektionen der Reihenfolge nach ausführen.  
  
||Für den Abschluss voraussichtlich benötigte Zeit|  
|-|------------------------------|  
|[Lektion 1: Vorbereiten der Daten &#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)<br /><br />Der analytische Prozess beginnt mit dem Abrufen von Daten, die zum Erstellen eines Modells benötigt werden. Laden Sie ein öffentliches Dataset herunter, und speichern Sie es in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank.|30 Minuten|  
|[Lektion 2: Anzeigen und Durchsuchen der Daten &#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)<br /><br />Ein Datenanalyst verbringt viel Zeit damit, die Daten zu erforschen und sie für die Modellierung vorzubereiten, neue Funktionen zu erstellen oder die Daten nach Bedarf zu transformieren.  Sie werden SQL und R verwenden, um die Daten zu erforschen und Zusammenfassungen zu generieren.|20 Minuten|  
|[Lektion 3: Erstellen der Datenfunktionen &#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)<br /><br />Sie werden neue Datenfunktionen mithilfe von benutzerdefinierten Funktionen in R und [!INCLUDE[tsql](../../includes/tsql-md.md)]erstellen.|10 Minuten|  
|[Lektion 4: Erstellen und Speichern des Modells&#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)<br /><br />Wenn die Daten bereit sind, trainiert und optimiert der Datenanalyst das Modell, bewertet dessen Leistung und testet verschiedene Parameter. In dieser exemplarischen Vorgehensweise werden Sie ein Klassifizierungsmodell erstellen und Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwenden, um Vorhersagen zu generieren. Sie werden auch die Genauigkeit des Modells grafisch mithilfe von R darstellen.|15 Minuten|  
|[Lektion 5: Bereitstellen und Verwenden des Modells &#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/lesson-5-deploy-and-use-the-model-data-science-end-to-end-walkthrough.md)<br /><br />Schließlich werden Sie das Modell für den Produktivbetrieb bereitstellen, indem Sie das Modell in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank speichern und es aus einer gespeicherten Prozedur aufrufen, um Vorhersagen zu generieren.|10 Minuten|  
  
## <a name="notes"></a>Hinweise  
Die exemplarische Vorgehensweise ist darauf ausgelegt, R-Entwicklern eine Einführung in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]zu geben, da so viele Aktionen wie möglich mithilfe von R durchgeführt werden. Das bedeutet nicht, das R unbedingt das beste Tool für jede Aufgabe ist. In vielen Fällen stellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine bessere Leistung bereit, besonders für Aufgaben wie Datenaggregation und Featureentwicklung. Solche Aufgaben profitieren besonders von neuen Funktionen in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], wie z.B. von speicheroptimierten Columnstore-Indizes.  
  
## <a name="next-step"></a>Nächster Schritt  
[Lektion 1: Vorbereiten der Daten &#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
