---
title: Analysis Services-Lernprogrammszenario | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 2f5b1a42-b814-4d7d-b603-5383d9ac66b9
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c93a6456ba3d77c93449c05897baeca9527eeb5c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="analysis-services-tutorial-scenario"></a>Analysis Services-Lernprogrammszenario
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]
Dieses Lernprogramm basiert auf [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)], einem fiktiven Unternehmen. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]ist ein großes, multinationales Herstellungsunternehmen, das produziert und vertreibt Fahrräder aus Metallene und Verbundwerkstoffen für kommerzielle Märkte in Nordamerika, Europa und Asien. Die Zentrale von [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] befindet sich in Bothell, Washington (USA), wo das Unternehmen 500 Arbeiter beschäftigt. Zusätzlich beschäftigt [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] eine Reihe von regionalen Verkaufsteams für die gesamte Marktbasis.  
  
In den vergangenen Jahren hat [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] die kleine Fabrik Importadores Neptuno erworben, die sich in Mexiko befindet. Importadores Neptuno stellt einige wichtige Unterkomponenten für die [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] -Produktlinie her. Diese Unterkomponenten werden für die Produktendmontage in Bothell angeliefert. Im Jahr 2005 wurde Importadores Neptuno alleiniger Hersteller und Vertreiber der Tourenrad-Produktgruppe.  
  
Nach einem erfolgreichen Geschäftsjahr möchte [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] seinen Marktanteil erweitern, indem die Werbung auf die Hauptkunden konzentriert wird, die Produktverfügbarkeit durch eine externe Website erweitert wird, und die Kosten verkaufter Fahrräder durch eine Produktionskostensenkung reduziert werden.  
  
## <a name="current-analysis-environment"></a>Aktuelle Analyseumgebung  
Die Vertriebs- und Marketingteams sowie die oberen Managementebenen benötigen Datenanalysen. Um sie darin zu unterstützen, ruft die Firma derzeit Transaktionsdaten aus der [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] -Datenbank ab, und ruft außerdem nicht transaktionsbezogene Daten, z. B. Sollvorgaben für den Verkauf, aus Kalkulationstabellen ab. Diese Informationen werden anschließend im relationalen Data Warehouse **AdventureWorksDW2012** konsolidiert. Das relationale Data Warehouse stellt allerdings die folgenden Herausforderungen:  
  
-   Berichte sind statisch. Es gibt für die Benutzer keine Möglichkeit, die Daten in den Bericht interaktiv zu durchsuchen, um detailliertere Informationen zu erhalten, wie das beispielsweise bei einer [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel-Pivot-Tabelle möglich ist. Obwohl der vorhandene Satz vordefinierter Berichte für viele Benutzer ausreichend ist, benötigen fortgeschrittene Benutzer direkten Abfragezugriff auf die Datenbank für interaktive Abfragen und spezielle Berichte. Wegen der Komplexität der **AdventureWorksDW2012** -Datenbank ist allerdings das Erlernen der Erstellung effektiver Abfragen für solche Benutzer zu zeitaufwändig.  
  
-   Die Abfrageleistung variiert sehr stark. Einige Abfragen führen beispielsweise in wenigen Sekunden zu Ergebnissen, während andere mehrere Minuten benötigen.  
  
-   Aggregattabellen sind schwierig zu verwalten. Um die Abfrageantwortzeiten zu verbessern, hat das Data Warehouse-Team der Firma [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] mehrere Aggregattabellen in der **AdventureWorksDW2012** -Datenbank erstellt. So wurde beispielsweise eine Tabelle erstellt, die die monatlichen Verkäufe zusammenfasst. Während diese Aggregattabellen die Abfrageleistung stark verbessern, ist allerdings die Infrastruktur, die mit der Zeit zum Warten der Tabelle erstellt wurde, unsolide und fehleranfällig.  
  
-   Die komplexe Berechnungslogik ist tief in Berichtsdefinitionen verborgen und nur schwer für mehrere Berichte gemeinsam zu verwenden. Weil die Geschäftslogik separat für jeden Bericht generiert wird, unterscheiden sich die Zusammenfassungsinformationen manchmal von Bericht zu Bericht. Deshalb hat das Management nur beschränktes Vertrauen in die Data Warehouse-Berichte.  
  
-   Benutzer in verschiedenen Geschäftseinheiten sind an unterschiedlichen Sichten der Daten interessiert. Jede Gruppe wird durch Datenelemente abgelenkt und verwirrt, die für sie unwichtig sind.  
  
-   Die Berechnungslogik stellt eine besondere Herausforderung für Benutzer dar, die spezielle Berichte benötigen. Weil solche Benutzer die Berechnungslogik separat für jeden Bericht definieren müssen, gibt es keine zentralisierte Kontrolle darüber, wie sie definiert wird. Einige Benutzer wissen beispielsweise, dass sie einfache statistische Techniken wie den gleitenden Durchschnitt verwenden sollten. Sie wissen allerdings nicht, wie solche Berechnungen konstruiert werden, also verwenden sie sie nicht.  
  
-   Es ist schwierig, zusammengehörige Informationssätze zu kombinieren. Spezielle Abfragen, die zwei Sätze verwandter Informationen wie Verkäufe und Sollvorgaben für den Verkauf miteinander kombinieren, sind für Geschäftsbenutzer schwierig zu konstruieren. Durch solche Abfragen wurde die Datenbank überlastet. Das Unternehmen verlangt deshalb von den Benutzern, dass sie themenübergreifende Datenabfragen beim Data Warehouse-Team anfordern. Als Folge davon wurden nur wenige vordefinierter Berichte definiert, die Daten aus mehreren Themenbereichen kombinieren. Außerdem weigern sich Benutzer, diese Berichte zu ändern, weil sie so komplex sind.  
  
-   Die Berichte sind in erster Linie auf Geschäftsinformationen in den USA zugeschnitten. Benutzer in Niederlassungen außerhalb der USA sind mit diesem Schwerpunkt ausgesprochen unzufrieden. Sie möchten Berichte in verschiedenen Währungen und verschiedenen Sprachen anzeigen können.  
  
-   Informationen sind schwer zu überwachen. Die Buchhaltungsabteilung verwendet derzeit die **AdventureWorksDW2012** -Datenbank nur als Quelle für Massendatenabfragen. Sie lädt dann die Daten in einzelne Kalkulationstabellen herunter und wendet beträchtliche Zeit für die Vorbereitung der Daten und die Bearbeitung der Kalkulationstabellen auf. Die Unternehmensfinanzberichte sind deshalb schwer zu erstellen, zu überwachen und über das gesamte Unternehmen hinweg zu verwalten.  
  
## <a name="the-solution"></a>Die Lösung  
Das Data Warehouse-Team hat kürzlich eine Entwurfsüberprüfung des aktuellen Analysesystems durchgeführt. Zu der Überprüfung gehörte eine Analyse zum Aufdecken von Lücken, die durch aktuelle Probleme oder zukünftigen Anforderungen entstehen können. Das Data Warehouse-Team hat ermittelt, dass die **AdventureWorksDW2012** -Datenbank eine durchdachte, dimensionsbasierte Datenbank mit konformen Dimensionen und Ersatzschlüsseln ist. Konforme Dimensionen ermöglichen die Verwendung einer Dimension in mehreren Datamarts, beispielsweise einer Zeit- oder Produktdimension. Ersatzschlüssel sind künstliche Schlüssel, die Dimensions- und Faktentabellen verknüpfen, die verwendet werden, um Eindeutigkeit sicherzustellen und die Leistung zu verbessern. Das Data Warehouse-Team hat außerdem ermittelt, dass derzeit keine wesentlichen Probleme beim Laden und Verwalten der Basistabellen in der **AdventureWorksDW2012** -Datenbank vorliegen. Das Team hat sich deshalb entschieden, [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] zum Erreichen der folgenden Ziele einzusetzen:  
  
-   Vereinheitlichung des Datenzugriffs durch eine gemeinsame Metadatenebene für die Analyse und Berichterstellung.  
  
-   Vereinfachung der Benutzersichten von Daten, und damit Beschleunigung der Entwicklung interaktiver und vordefinierter Abfragen sowie vordefinierter Berichte.  
  
-   Ordnungsgemäße Konstruktion von Abfragen, die Daten aus mehreren Themenbereichen kombinieren.  
  
-   Verwalten von Aggregaten.  
  
-   Speichern und Wiederverwenden komplexer Berechnungen.  
  
-   Anpassungen für Geschäftsbenutzer außerhalb der USA anhand der örtlichen Gegebenheiten.  
  
Die Lektionen im Analysis Services-Lernprogramm bieten eine Anleitung zum Erstellen einer Cubedatenbank, die all diese Zielsetzungen erfüllt. Um mit der Erstellung zu beginnen, gehen Sie zur ersten Lektion über: [Lesson 1: Create a New Tabular Model Project](../analysis-services/lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="see-also"></a>Siehe auch  
[Mehrdimensionale Modellierung & #40; Adventure Works-Lernprogramm & #41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)  
  
  
  
