---
title: "PolyBase-Leitfaden | Microsoft Docs"
ms.date: "12/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-polybase"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
f1_keywords: 
  - "PolyBase"
  - "PolyBase, guide"
helpviewer_keywords: 
  - "PolyBase"
  - "PolyBase, Übersicht"
  - "Hadoop-Import ×"
  - "Hadoop-Export"
  - "Hadoop-Export, PolyBase-Übersicht"
  - "Hadoop-Import, PolyBase-Übersicht"
ms.assetid: b42b7d48-328a-4046-abe9-f73fd83212dc
caps.latest.revision: 26
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 24
---
# PolyBase-Leitfaden
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  PolyBase ist eine Technologie, die auf relationale und nicht relationale Daten zugreift und diese Daten kombiniert – alles innerhalb von SQL Server.   Mit dieser Technologie können Sie Abfragen für externe Daten in Hadoop oder Azure-Blobspeichern ausführen.   Die Abfragen sind für die Übertragung der Berechnung an Hadoop optimiert.  
  
 Sie können ganz einfach durch Verwendung von Transact-SQL-Anweisungen (T-SQL) Daten zwischen relationalen Tabellen in SQL Server und nicht relationalen Datenspeichern in Hadoop oder Azure-Blobspeichern importieren und exportieren. Sie können die externen Daten auch aus einer T-SQL-Abfrage heraus abfragen und mit relationalen Daten verknüpfen.  
  
 Informationen zur Verwendung von PolyBase finden Sie unter [Erste Schritte mit PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  
 ![PolyBase logical](../../relational-databases/polybase/media/polybase-logical.png "PolyBase logical")  
  
## Gründe für die Verwendung von PolyBase  
 Um sinnvolle Entscheidungen treffen zu können, müssen Geschäftsentscheidungsträger sowohl relationale Daten als auch andere, nicht in Tabellen strukturierte Daten analysieren können – insbesondere in Hadoop und anderen NoSQL-Technologien verarbeitete Daten. Dies ist schwer zu bewerkstelligen, sofern Sie nicht über eine Möglichkeit verfügen, Daten zwischen den verschiedenen Arten von Datenspeichern zu übertragen. PolyBase schließt diese Lücke durch Verarbeiten von Daten, die sich außerhalb von SQL Server befinden.  
  
 Einfach ausgedrückt: Mit PolyBase müssen Sie keine zusätzliche Software in Ihrer Hadoop- oder Azure-Umgebung installieren.         Beim Abfragen externer Daten wird die gleiche Syntax verwendet wie beim Abfragen einer Datenbanktabelle. All dies erfolgt transparent. PolyBase kümmert sich hinter den Kulissen um alle Details, und für einen erfolgreichen Einsatz von PolyBase sind keinerlei Kenntnisse zu Hadoop oder Azure erforderlich.  
  
 PolyBase führt Folgendes aus:  
  
-   **Abfragen von in Hadoop gespeicherten Daten.** Benutzer speichern Daten in kostengünstigen verteilten und skalierbaren Systemen, wie z.B. Hadoop. PolyBase vereinfacht die Abfrage der Daten mithilfe von T-SQL.  
  
-   **Abfragen von in Azure-Blobspeichern gespeicherten Daten.** Ein Azure-Blobspeicher ist eine bequeme Möglichkeit, Daten zu speichern, die von Azure-Diensten verwendet werden.  PolyBase vereinfacht den Zugriff auf die Daten mithilfe von T-SQL.  
  
-   **Importieren von Daten aus Hadoop oder Azure-Blobspeichern.** Profitieren Sie von der Geschwindigkeit der Columnstore-Technologie und den Analysefunktionen von Microsoft SQL, indem Sie Daten aus Hadoop oder Azure-Blobspeichern in relationale Tabellen importieren. Sie benötigen keine separaten ETL-Funktionen und kein Importtool.  
  
-   **Exportieren von Daten in Hadoop oder Azure-Blobspeicher.** Archivieren Sie Daten in Hadoop oder Azure-Blobspeicher, um kostengünstigen Speicherplatz zu nutzen und Daten für einfachen Zugriff online zu halten.  
  
-   **Integrieren in BI-Tools.** Verwenden Sie PolyBase zusammen mit den Business Intelligence- und Analysis-Funktionen von Microsoft, oder verwenden Sie beliebige Drittanbietertools, die mit SQL Server kompatibel sind.  
  
## Leistung  
  
-   **Übertragen der Berechnung an Hadoop.** Der Abfrageoptimierer trifft eine kostenbasierte Entscheidung darüber, ob die Berechnung an Hadoop übertragen wird, um die Abfrageleistung zu verbessern.  Für diese kostenbasierte Entscheidung verwendet der Optimierer Statistiken in externen Tabellen.   Bei der Übertragung der Berechnung werden MapReduce-Aufträge erstellt und die verteilten Berechnungsressourcen von Hadoop genutzt.  
  
-   **Skalieren von Berechnungsressourcen.** Um die Abfrageleistung zu verbessern, können Sie [PolyBase-Erweiterungsgruppen](../../relational-databases/polybase/polybase-scale-out-groups.md) von SQL Server verwenden. Die ermöglicht eine parallele Datenübertragung zwischen SQL Server-Instanzen und Hadoop-Knoten und fügt Berechnungsressourcen für die Verarbeitung der externen Daten hinzu.  
  
## PolyBase-Leitfaden – Themen  
 Dieser Leitfaden enthält Themen, die Sie bei der effizienten und effektiven Verwendung von PolyBase unterstützen.  
  
|||  
|-|-|  
|**Thema**|**Beschreibung**|  
|[Erste Schritte mit PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)|Grundlegende Schritte zum Installieren und Konfigurieren von PolyBase. Dieses Thema zeigt Ihnen, wie Sie externe Objekte erstellen, die auf Daten in Hadoop oder Azure-Blobspeichern zeigen, und enthält Abfragebeispiele.|  
|[Zusammenfassung der PolyBase-Funktionen mit Versionsangabe](../../relational-databases/polybase/polybase-versioned-feature-summary.md)|Beschreibt die PolyBase-Funktionen, die in SQL Server, SQL-Datenbank und SQL Data Warehouse unterstützt werden.|  
|[PolyBase-Erweiterungsgruppen](../../relational-databases/polybase/polybase-scale-out-groups.md)|Horizontales Skalieren der Parallelität zwischen SQL Server und Hadoop durch Verwenden von SQL-Server-Erweiterungsgruppen.|  
|[PolyBase-Installation](../../relational-databases/polybase/polybase-installation.md)|Referenz und Schritte zur Installation von PolyBase mit dem Installations-Assistenten oder über ein Befehlszeilentool.|  
|[PolyBase-Konfiguration](../../relational-databases/polybase/polybase-configuration.md)|Konfigurieren der SQL Server-Einstellungen für PolyBase.  Beispiel: Konfigurieren von Berechnungsweitergabe und Kerberos-Sicherheit.|  
|[PolyBase T-SQL-Objekte](../../relational-databases/polybase/polybase-t-sql-objects.md)|Erstellen der T-SQL-Objekte, die PolyBase verwendet, um externe Daten zu definieren und darauf zuzugreifen.|  
|[PolyBase-Abfragen](../../relational-databases/polybase/polybase-queries.md)|Verwenden von T-SQL-Anweisungen zum Abfragen, Importieren oder Exportieren externer Daten.|  
|[Problembehandlung in PolyBase](../../relational-databases/polybase/polybase-troubleshooting.md)|Techniken zum Verwalten von PolyBase-Abfragen. Verwenden von dynamischen Verwaltungssichten (Dynamic Management Views, DMVs) zum Überwachen von PolyBase-Abfragen sowie Informationen zum Lesen eines PolyBase-Abfrageplans, um Leistungsengpässe zu ermitteln.|  
  
  