---
title: "Einführung in tabellarischen Objektmodell (TOM) in Analysis Services AMO | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 57a4a934-ecd0-4365-8147-d36899d86751
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 2f9e5d07831070ad69ccf23a3975fbdc19fa4c83
ms.contentlocale: de-de
ms.lasthandoff: 09/21/2017

---
# <a name="introduction-to-the-tabular-object-model-tom-in-analysis-services-amo"></a>Einführung in die im tabellarischen Objektmodell (TOM) in Analysis Services AMO

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Im tabellarischen Objektmodell (TOM) ist eine Erweiterung von der Clientbibliothek des Analysis Services Management Object (AMO) erstellt zur Unterstützung von Programmierszenarien für tabellarische Modelle mit Kompatibilitätsgrad 1200 oder höher erstellt. Wie bei AMO, bietet TOM eine programmgesteuerte Möglichkeit zum Verarbeiten von Verwaltungsfunktionen wie das Erstellen von Modellen, importieren und Aktualisieren von Daten und Zuweisen von Rollen und Berechtigungen.  
  
TOM macht native tabellarischen Metadaten, wie z. B. **Modell**, **Tabellen**, **Spalten**, und **Beziehungen** Objekte.  Ein allgemeinen Überblick über das Modell Objektstruktur unten veranschaulicht, wie die Komponententeile miteinander verknüpft sind.  
  
 Da TOM eine Erweiterung von AMO ist, werden alle Klassen, die neue tabellarische Objekte, die in SQL Server 2016 eingeführt darstellt in eine neue Microsoft.AnalysisServices.Tabular.dll-Assembly implementiert. Allgemeine Klassen von AMO wurden auf "Microsoft.AnalysisServices.Core" Assembly verschoben. Der Code müssen beide Assemblys verweisen.
Finden Sie unter [installieren, verteilen und verweisen auf die tabellarischen Objektmodell &#40; Microsoft.AnalysisServices.Tabular &#41; ](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md) für Details.  
  
 Derzeit ist die API über .NET Framework nur für verwalteten Code verfügbar. Überprüfen Sie die vollständige Liste der Optionen, einschließlich Skripts und Abfragen sprachunterstützung-Programmierung finden Sie unter [tabellarische Programmiermodell für die Kompatibilität auf 1200](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md).  
  
## <a name="tabular-object-model-hierarchy"></a>Tabellarische Objektmodellhierarchie  
 Aus Sicht der logischen alle tabellarische Objekte bilden eine Struktur, die der Stamm ist eine **Modell**, descended aus der Datenbank. **Server** und **Datenbank** gelten nicht als "tabellarisch", da diese Objekte ebenfalls eine mehrdimensionale Datenbank, die auf einem Server im mehrdimensionalen Modus oder ein tabellarisches Modell mit einem niedrigeren Kompatibilitätsgrad unter gehostet darstellen können Ebene verwendet, die nicht tabellarische Metadaten für Objektdefinitionen. 
  
 Mit Ausnahme von **AttributeHierarchy**, **KPI**, und **LinguisticMetadata**, jedes untergeordnete Objekt kann Mitglied einer Sammlung sein. Z. B. die **Modell** Objekt enthält eine Auflistung von **Tabelle** Objekte (über die **Tabellen** Eigenschaft), mit jedem **Tabelle** Objekt enthält eine Auflistung von **Spalte** Objekte und So weiter.  
  
 Der niedrigsten Ebene Nachfolger eines übergeordneten Objekts in dieser Hierarchie ist eine **Anmerkung** -Objekt, das verwendet werden kann, optional das Schema erweitern, solange Sie den Code, um seine Handhabung bereitstellen.  
  
 ![Objekt-Hierarchiediagramm](../../analysis-services/tabular-model-programming-compatibility-level-1200/media/ssastomobjectmodeldiagram.png "Objekt Hierarchiediagramm")  
  
## <a name="tom-and-other-related-technologies"></a>PETER und andere verwandten Technologien

Die AMO-Infrastruktur mit diesem für mehrdimensionale und tabellarische Datenbanken mit Kompatibilitätsgraden unter 1200 auch ausgelegten TOM basieren.

Dies wirkt sich einige praktische.
Erste daran, bei der Verwaltung von Objekten, die in tabellarischen Metadaten nicht angegeben werden (z. B. eine **Server** oder **Datenbank**), müssen Sie die Teile des vorhandenen AMO-Stapels zu nutzen, die diese Objekte beschreiben. Wird Sie zusammen mit dem legacy-API das Konzept der Haupt- und Nebenversionsnummern-Objekten, die eine präzise Beschreibung des Objektstatus als ermittelt den Server oder bei Veröffentlichung auf dem Server gespeichert bereitstellen. Die MajorObject-Klasse finden Sie unter "Microsoft.AnalysisServices"-Namespace stellt Methoden für **aktualisieren** und **Update**. Nebenobjekte sind nur aktualisieren oder über das Hauptobjekt gespeichert, die sie enthält.

Im Gegensatz dazu bei der Verwaltung von Objekten, die Teil der tabellarischen Metadaten sind (z. B. **Modell** oder **Tabelle**), Sie nutzen einen vollständig neuen tabellarischen Stapel. In diesem Stapel Updates sind differenzierte, d. h. alle Metadatenobjekt (abgeleitet wurde. die **MetadataObject** Klasse finden Sie unter der Microsoft.AnalysisServices.Tabular-Namespace) einzeln auf dem Server gespeichert werden. In der Regel würden Sie ermitteln, die gesamte **Modell**, nehmen dann Änderungen einzelne Metadatenobjekte darunter (z. B. **Tabelle** oder **Spalte**), rufen Sie anschließend ** Model.SaveChanges()** -Methode (die differenzierte Ebene von Ihnen vorgenommenen Änderungen versteht), senden Befehle an den Server nur die Objekte zu aktualisieren, die sich geändert.

### <a name="tom-and-xmla"></a>PETER und XMLA

Bei der Übertragung verwendet TOM das XMLA-Protokoll aus, für die Kommunikation mit dem Analysis Services-Server und zum Verwalten von Objekten. Wenn Sie nicht tabellarische Objekte zu verwalten, die PETER verwendet [ASSL](/sql-docs/docs/analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla), die Analysis Services Scripting Language-Erweiterung des XMLA. Wenn Sie tabellarische Objekte zu verwalten, verwendet dem tabellarische SSAS-Protokoll bei TOM auch die eine Erweiterung der XMLA. Finden Sie unter [MS-SSAS-T-SQL Server Analysis Services-Tabellendatenbank protokolldokumentation](https://msdn.microsoft.com/library/mt719260.aspx) für Weitere Informationen.

### <a name="tom-and-json"></a>PETER und JSON

Tabellarische Metadaten, die als JSON-Dokumente strukturiert ist, verfügt über eine neue Befehl und Objekt Modell definitionssyntax über die Tabular Model Scripting Language [TMSL](/sql-docs/docs/analysis-services/tabular-model-scripting-language-tmsl-reference). Die verwendete Skriptsprache verwendet JSON für den Text der Anforderungen und Antworten.

Obwohl dieselben Objekte verfügbar, TMSL und TOM machen (**Tabelle**, **Spalte**usw.) und die gleichen Vorgänge (**erstellen**, **löschen**, ** Aktualisieren Sie**), TOM TMSL nicht bei der Übertragung (er verwendet das tabellarische MS-SSAS-Protokoll stattdessen, wie bereits erwähnt) verwendet.

Als Benutzer können Sie auswählen, ob zum Verwalten von tabellarischer Datenbanken über die Bibliothek TOM aus dem C#-Programm oder die PowerShell-Skript oder TMSL-Skript über PowerShell, SQL Server Management Studio (SSMS) oder einem SQL Server-Agent-Auftrag ausgeführt.

Die Entscheidung zum Verwenden eines dieser Zuordnungsverfahren wird auf die Einzelheiten der Erfordernissen sinken. Die TOM-Bibliothek bietet umfangreichere Funktionen, die im Vergleich zu TMSL. Insbesondere während TMSL nur groben Vorgänge auf der Datenbank, Tabelle, Partitions- oder Rolle-Ebene bietet, kann TOM Vorgänge viel feiner differenziert. Zum Generieren oder Modelle programmgesteuert aktualisieren, benötigen Sie das Ausmaß der API in der Bibliothek TOM.
  
## <a name="see-also"></a>Siehe auch  
 [Programmierung von tabellarischen Modellen für den Kompatibilitätsgrad 1200](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)   
 [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
[Analysis Services PowerShell](../../analysis-services/powershell/analysis-services-powershell-reference.md)
  
