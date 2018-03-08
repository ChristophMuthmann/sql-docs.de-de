---
title: Load
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Laden oder Einfügen von Daten in SQL Server Parallel Data Warehouse (PDW) mit Integration Services, Bcp (Hilfsprogramm), Dwloader oder die SQL-INSERT-Anweisung."
ms.date: 10/20/2016
ms.topic: article
ms.assetid: c7292108-4a48-409e-b0f4-e4ba84dce26f
caps.latest.revision: "22"
ms.openlocfilehash: be5ea7c2b939b58c7dfd826965f1568431cb1bff
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="load-sql-server-pdw"></a>Load (SQLServer PDW)
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
  
## <a name="related-tasks"></a>Related Tasks  
  
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
