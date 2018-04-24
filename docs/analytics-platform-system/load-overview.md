---
title: Laden von Daten in Parallel Data Warehouse | Microsoft Docs
description: Laden oder Einfügen von Daten in SQL Server Parallel Data Warehouse (PDW) mit Integration Services, Bcp (Hilfsprogramm), Dwloader oder die SQL-INSERT-Anweisung.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3fed89686683616164132cf0322e3709eab78f32
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="loading-data-into-parallel-data-warehouse"></a>Laden von Daten in Parallel Data Warehouse
Laden oder Einfügen von Daten in SQL Server Parallel Data Warehouse (PDW) mit Integration Services, [Bcp (Hilfsprogramm)](../tools/bcp-utility.md), **Dwloader** Command-Line-Ladeprogramm oder die SQL-INSERT-Anweisung.  

## <a name="loading-environment"></a>Laden die Umgebung  
Um Daten zu laden, benötigen Sie eine oder mehrere beim Laden von Servern. Können Sie eigene vorhandene ETL oder auf anderen Servern, oder Sie können neue Server erwerben. Weitere Informationen finden Sie unter [erwerben und Konfigurieren eines Servers geladen](acquire-and-configure-loading-server.md). Diese Anweisungen beinhalten eine [laden Server Kapazität Planungsarbeitsblatt](loading-server-capacity-planning-worksheet.md) helfen Ihnen beim Planen der richtigen Lösung für das Laden.  
  
## <a name="load-with-dwloader"></a>Laden Sie mit dwloader  
Mithilfe der [Dwloader Command-Line-Ladeprogramm](dwloader.md) ist die schnellste Möglichkeit zum Laden von Daten in PDW.  
  
![Prozess des Ladens](media/loading-process.png "Prozess des Ladens")  
  
Dwloader lädt Daten direkt an den Compute-Knoten, ohne die Daten über den Knoten "Zugriffssteuerung" übergeben. Zum Laden der Daten kommuniziert mit dem Steuerungsknoten zum Abrufen der Kontaktinformationen für die Serverknoten zuerst Dwloader. Dwloader richtet einen Kommunikationskanal mit jeder Serverknoten, und sendet dann 256KB-Segmenten der Daten für die Serverknoten in einer Weise Round-Robin-Prinzip.  
  
Auf jedem Knoten Compute Daten Bewegung Service (DMS) empfängt und verarbeitet die Datenabschnitte. Verarbeitung der Daten enthält jede Zeile in systemeigenen SQL Server-Format zu konvertieren und Errechnen des Hashs Verteilung, um die Compute-Knoten zu bestimmen, zu dem jede Zeile gehört.  
  
Nach der Verarbeitung der Zeilen verwendet DMS eine zufälligen Verschiebung, die um jede Zeile in den richtigen Compute-Knoten und die Instanz von SQL Server zu übertragen. Wie SQL Server die Zeilen empfängt, als batches werden gemäß der **– b** batchgrößenparameter setzen Dwloader und Bulk lädt dann den Batch.  

## <a name="load-with-prepared-statements"></a>Laden Sie mit vorbereiteten Anweisungen

Vorbereitete Anweisungen können Sie um Daten in verteilten und replizierte Tabellen zu laden. Wenn die Eingabedaten nicht den Zieldatentyp übereinstimmt, wird eine implizite Konvertierung durchgeführt. Die impliziten Konvertierungen von vorbereiteten Anweisungen PDW unterstützt sind eine Teilmenge von Konvertierungen, die von SQL Server unterstützt. D. h. nur eine Teilmenge der Konvertierungen werden unterstützt, aber die unterstützten Konvertierungen entsprechen implizite Konvertierungen von SQL Server. Unabhängig davon, ob die Zieltabelle geladen werden als verteilte oder aus der replizierten Tabelle definiert ist werden implizite Konvertierungen angewendet (falls erforderlich) für alle Spalten, die in der Zieltabelle vorhanden sind. 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Task|Description|  
|--------|---------------|  
|Erstellen der staging-Datenbank.|[Erstellen der Stagingdatenbank](staging-database.md)|  
|Laden Sie mit Integrationsservices.|[Laden mit Integration Services](load-with-ssis.md)|  
|Verstehen Sie typkonvertierungen für Dwloader.|[Regeln für das Konvertieren von Datentypen für dwloader](dwloader-data-type-conversion-rules.md)|  
|Laden Sie Daten mit Dwloader.|[Dwloader Command-Line-Ladeprogramm](dwloader.md)|  
|Verstehen Sie typkonvertierungen für das Einfügen.|[Laden von Daten mit SSIS](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
