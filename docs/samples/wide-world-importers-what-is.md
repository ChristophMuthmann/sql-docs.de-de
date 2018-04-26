---
title: Wide World Importers - Beispieldatenbank für SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: samples
ms.technology:
- samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
caps.latest.revision: 3
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: 01ba6c673078f7c79690e14e4102e5c431a6271a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="wide-world-importers-sample-databases-for-microsoft-sql"></a>Wide World Importers-Beispieldatenbanken für Microsoft SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Dies ist eine Übersicht über das fiktive Unternehmen Wide World Importers und die Workflows, die in die "wideworldimporters"-Beispieldatenbanken für SQL Server und Azure SQL-Datenbank behoben werden.  

Wide World Importers (Schlachtfeld) ist eine Großhandel Neuheit waren Importer-Tool und die Verteiler im San Francisco Bay-Bereich ausgeführt.

Als ein Großhändler sind Schlachtfeld des Kunden meist Unternehmen, die an Personen zu verkaufen. Schlachtfeld verkauft Retail-Kunden in den Vereinigten Staaten Specialty speichert, Supermärkten, einschließlich Geschäfte, Sport-Attraktion Cafés und einige Personen berechnen. Schlachtfeld verkauft auch an andere Großhändler über ein Netzwerk von Agents, die die Produkte im Auftrag des Schlachtfeld höher stufen. Während alle Schlachtfeld des Kunden in den Vereinigten Staaten derzeit basieren, ist das Unternehmen beabsichtigten push für die Erweiterung in anderen Ländern.

Schlachtfeld kauft Waren vom Lieferanten einschließlich Neuheit Toy Hersteller und andere Neuheit Großhändler. Sie vordefinierte Waren in ihrer Warehouse Schlachtfeld und Anordnen von Lieferanten Bedarf kundenbestellungen zu erfüllen. Sie auch große Mengen an Materialien Verpacken erwerben und verkaufen diese in kleinere Mengen zur Vereinfachung für den Kunden.

Erst kürzlich Schlachtfeld, um eine Vielzahl von genießbare Novelties z. B. Chilli Pralinen verkaufen.  Das Unternehmen zuvor keine gekühlt Elemente behandeln. Jetzt müssen um Essen Behandlung von Anforderungen zu erfüllen, sie überwachen, die Temperatur in ihre Kühler Platz und alle ihre LKWs denen Kühler Abschnitte.

## <a name="workflow-for-warehouse-stock-items"></a>Workflow für das Warehouse stock-Elemente

Die typische Ablauf für das Lager und Verteilung wie Elemente lautet folgendermaßen:
- Schlachtfeld Bestellungen erstellt und die Aufträge an den Lieferanten sendet.
- Lieferanten senden, die Elemente, Schlachtfeld Empfangs und diese in ihrer Warehouse auf Lager hat.
- Kunden Bestellartikel aus Schlachtfeld
- Schlachtfeld füllt die kundenbestellung mit vordefinierten Elemente in das Warehouse und die zusätzliche Aktie nicht ausreichend Stock verfügen, von den Lieferanten angeordnet.
- Einige Kunden sollten keine Elemente warten, die nicht auf Lager sind. Wenn sie z. B. fünf verschiedene bestellen vordefinierte Elemente und vier zur Verfügung stehen, die vier Elemente und der Rückstand der verbleibenden Element empfangen werden soll. Das Element würde sie weiter unten in einer separaten Lieferung gesendet werden.
- Schlachtfeld Rechnungen Kunden für die vordefinierten Elemente in der Regel durch konvertieren die Reihenfolge, in eine Rechnung.
- Kunden können Elemente sortieren, die nicht auf Lager sind. Diese Elemente sind rückständigen.
- Schlachtfeld bietet vordefinierte Elemente über ihre eigenen Lieferwagen oder über andere Kurieren oder Freight-Methoden.
- Kunden Zahlen Rechnungen, Schlachtfeld.
- In regelmäßigen Abständen, zahlt Schlachtfeld Lieferanten für Elemente, die auf Bestellungen waren. Dies ist häufig einige Zeit nach dem Empfang der Wareneigentümers.

## <a name="data-warehouse-and-analysis-workflow"></a>Data Warehouse und Analysis-workflow

Während das Team bei Schlachtfeld mit, dass der SQL Server Reporting Services Berichte für operative aus der Datenbank "wideworldimporters" generiert, müssen sie auch Analytics für ihre Daten durchführen und müssen strategische Berichte generieren. Das Team haben ein Modell für die Dimensionsdaten in einer Datenbank WideWorldImportersDW erstellt. Diese Datenbank wird durch ein Integration Services-Paket aufgefüllt.

SQL Server Analysis Services wird verwendet, um analytische Datenmodelle aus den Daten im Modell Dimensionsdaten zu erstellen. SQL Server Reporting Services wird verwendet, um strategische Berichte direkt aus dem Modell Dimensionsdaten und aus dem analytischen Modell zu erstellen. Power BI wird verwendet, um Dashboards aus der gleichen Daten zu erstellen. Die Dashboards werden verwendet, auf Websites und auf Telefonen und Tablets. *Hinweis: Diese Datenmodelle und Berichte sind noch nicht verfügbar*

## <a name="additional-workflows"></a>Zusätzliche workflows

Hierbei handelt es sich um zusätzliche Workflows.
- Schlachtfeld Probleme Gutschriften, wenn ein Kunde empfängt nicht die funktionierende aus irgendeinem Grund ist, oder wenn die Waren fehlerhaft sind. Diese werden als negative Rechnungen behandelt.
- Schlachtfeld zählt in regelmäßigen Abständen der Lagerbestand von vordefinierten Elementen, stellen Sie sicher, dass die vordefinierten Mengen als verfügbar angezeigt, auf ihrem System richtig sind. (Die auf diese Weise wird eine Stocktake bezeichnet).
- Kalte Platz Temperaturen. Ablaufenden waren, werden in Kühlräume gespeichert. Temperatursensor Daten aus diesen Räume ist in der Datenbank für die Überwachung und Analyse aufgenommen.
- Standort des Fahrzeugs nachverfolgen. Fahrzeuge, die für Schlachtfeld waren transport enthalten, Sensoren, die den Speicherort zu verfolgen. Dieser Speicherort wird in der Datenbank für die Überwachung und weitere Analysen wieder aufgenommen.

## <a name="fiscal-year"></a>Geschäftsjahr

Das Unternehmen arbeitet mit einem Geschäftsjahr, das am 1. November startet.

## <a name="terms-of-use"></a>Nutzungsbedingungen

Die Lizenz für die Beispieldatenbank und den Beispielcode wird hier beschrieben: [license.txt](https://github.com/Microsoft/sql-server-samples/blob/master/license.txt)

Die Beispieldatenbank enthält öffentliche Daten, die aus der kriminalstatistik und natürliche EarthData geladen wurde. Die Nutzungsbedingungen sind hier: [http://www.naturalearthdata.com/about/terms-of-use/](http://www.naturalearthdata.com/about/terms-of-use/)
