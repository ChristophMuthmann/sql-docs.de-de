---
title: "ADOMD.NET-Clientfunktionalität | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- functionality [ADOMD.NET]
- ADOMD.NET, functionality
ms.assetid: 0f5e16a1-dc2d-4c87-8551-985921bf069b
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4573834d025c7afb066c4e363c476e8fb18c4ab7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="adomdnet-client-functionality"></a>ADOMD.NET-Clientfunktionalität
  Wie andere [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework-Datenanbieter auch dient ADOMD.NET als Verbindung zwischen einer Anwendung und einer Datenquelle. Im Gegensatz zu anderen .NET Framework-Datenanbietern arbeitet ADOMD.NET jedoch mit analytischen Daten. Um das leisten zu können, unterstützt ADOMD.NET eine Funktionalität, die sich von der anderer .NET Framework-Datenanbieter erheblich unterscheidet. ADOMD.NET ermöglicht nicht nur das Abrufen von Daten, sondern auch das Abrufen von Metadaten und Änderungen an der Struktur des analytischen Datenspeichers:  
  
 **Abrufen von Metadaten**  
 Anwendungen können mehr über die Daten "lernen", die durch Metadatenabruf aus der Datenquelle abgerufen werden können, wobei entweder Schemarowsets oder das Objektmodell verwendet werden. Informationen, wie zum Beispiel die jeweils verfügbaren Key Performance Indicator (KPI)-Arten, die Dimensionen in einem Cube, und die von den Miningmodellen benötigten Parameter, können alle ermittelt werden. Metadaten sind am wichtigsten für *dynamische* Anwendungen, die Benutzereingaben zur Ermittlung des Typs, Tiefe und Umfang der Daten abgerufen werden müssen. Beispiele: Query Analyzer, Microsoft Excel und andere Abfragetools. Metadaten sind weniger wichtig *statische* Anwendungen, die einen vordefinierten Satz von Aktionen ausführen.  
  
 Weitere Informationen: [Abrufen von Metadaten aus einer analytischen Datenquelle](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md).  
  
 **Abrufen von Daten**  
 Datenabruf ist das eigentliche Abrufen der in der Datenquelle gespeicherten Informationen. Datenabruf ist die primäre Funktion "statischer" Anwendungen, die die Struktur die Datenquelle kennen. Datenabruf ist auch das Endergebnis "dynamischer" Anwendungen. Der Wert des KPI zu einer bestimmten Tageszeit, die Anzahl der in den letzten Stunden je Geschäft verkauften Fahrräder und die Faktoren, welche die Jahresleistung der Mitarbeiter beeinflussen, sind allesamt Beispiele für Daten, die abgerufen werden können. Das Abrufen von Daten ist für jede Abfrageanwendung von entscheidender Bedeutung.  
  
 Weitere Informationen: [Abrufen von Daten aus einer analytischen Datenquelle](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md).  
  
 **Ändern die Struktur des analytischen Daten**  
 ADOMD.NET kann auch verwendet werden, um die Struktur des analytischen Datenspeichers zu ändern. Dies erfolgt zwar in der Regel durch das Analysis Management Objects (AMO)-Objektmodell, doch können Sie auch ADOMD.NET verwenden, um Analysis Services Scripting Language (ASSL)-Befehle zum Erstellen, Ändern oder Löschen von Objekten auf dem Server zu senden.  
  
 Weitere Informationen: [ausführen Befehle für eine analytische Datenquelle](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md), [Entwickeln mit Analysis Management Objects &#40; AMO &#41; ](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md), [Analysis Services Scripting Language &#40; ASSL XMLA &#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)  
  
 Das Abrufen von Metadaten, das Abrufen von Daten und das Ändern der Datenstruktur erfolgt jeweils an einem bestimmten Punkt im Workflow einer typischen ADOMD.NET-Anwendung.  
  
## <a name="typical-process-flow"></a>Typischer Verarbeitungsablauf  
 Beim Arbeiten mit einer analytischen Datenbank folgen herkömmliche ADOMD.NET-Anwendungen normalerweise demselben Workflow:  
  
1.  Zuerst wird mit dem <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekt eine Verbindung zur Datenbank hergestellt. Wenn Sie die Verbindung öffnen, macht das <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekt Metadaten über den Server verfügbar, zu dem Sie eine Verbindung hergestellt haben. In einer dynamischen Anwendung wird ein Teil dieser Informationen meist dem Benutzer angezeigt, damit er eine Auswahl treffen kann, z. B. welcher Cube abgefragt werden soll. Die bei diesem Schritt erstellte Verbindung kann mehrmals von der Anwendung wiederverwendet werden, was den Verwaltungsaufwand verringert.  
  
     Weitere Informationen: [Establishing Connections in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)  
  
2.  Sobald eine Verbindung hergestellt ist, würde eine dynamische Anwendung den Server abfragen, um genauere Metadaten zu erhalten. Bei einer statischen Anwendung weiß der Programmierer vorher, welche Objekte die Anwendung abfragen wird. Somit müssen diese Metadaten nicht abgerufen werden. Abgerufene Metadaten können von der Anwendung und dem Benutzer für den nächsten Schritt verwendet werden.  
  
     Weitere Informationen: [Abrufen von Metadaten aus einer analytischen Datenquelle](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
3.  Die Anwendung führt dann einen Befehl für den Server aus. Dieser Befehl kann zum Zweck haben, zusätzliche Metadaten abzurufen, Daten abzurufen oder die Datenbankstruktur zu verändern. Für jeden dieser Tasks könnte die Anwendung eine zuvor festgelegte Abfrage verwenden oder mithilfe neu abgerufener Metadaten weitere Abfragen erstellen.  
  
     Weitere Informationen: [Abrufen von Metadaten aus einer analytischen Datenquelle](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md), [Abrufen von Daten aus einer analytischen Datenquelle](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md), [ausführen Befehle für eine analytische Datenquelle](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md)  
  
4.  Nachdem der Befehl an den Server gesendet wurde, beginnt die Rückgabe der Metadaten oder Daten vom Server an den Client. Diese Informationen kann angezeigt werden, mithilfe einer <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> -Objekt, ein <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> -Objekt, oder ein **System.XmlReader** Objekt.  
  
 Zur Veranschaulichung dieses herkömmlichen Workflows enthält das folgende Beispiel eine Methode, die eine Verbindung mit der Datenbank öffnet, einen Befehl für einen bekannten Cube ausführt und die Ergebnisse in ein Cellset abruft. Das Cellset gibt dann eine tabstoppgetrennte Zeichenfolge zurück, die Spaltenheader, Zeilenheader und Zellendaten enthält.  
  
 [!code-cs[Adomd.NetClient#ReturnCommandUsingCellSet](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/adomd-net-client-functio_1.cs)]  
  
## <a name="see-also"></a>Siehe auch  
 [ADOMD.NET-Clientprogrammierung](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  
