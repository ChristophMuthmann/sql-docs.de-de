---
title: PolyBase-Leitfaden | Microsoft-Dokumentation
ms.date: 5/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: get-started-article
f1_keywords:
- PolyBase
- PolyBase, guide
helpviewer_keywords:
- PolyBase
- PolyBase, overview
- "Hadoop import ×"
- Hadoop export
- Hadoop export, PolyBase overview
- Hadoop import, PolyBase overview
ms.assetid: b42b7d48-328a-4046-abe9-f73fd83212dc
caps.latest.revision: 26
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 3fc2a681f001906cf9e819084679db097bca62c7
ms.openlocfilehash: f9fe99ddd630b8444819c94111f6a363e96105f5
ms.contentlocale: de-de
ms.lasthandoff: 05/31/2017

---
# <a name="polybase-guide"></a>PolyBase-Leitfaden
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  PolyBase ist eine Technologie, die außerhalb der Datenbank über die t-Sql-Sprache Daten zugreift.  In SQL Server 2016 können Sie die zum Ausführen von Abfragen für externe Daten in Hadoop oder zum Importieren/Exportieren von Daten aus dem Azure-Blob-Speicher. Die Abfragen sind für die Übertragung der Berechnung an Hadoop optimiert. In Azure SQL Data Warehouse Sie können importieren/Daten aus Azure Blob Storage und Azure Data Lake-Speicher exportieren.
  
  
 Informationen zur Verwendung von PolyBase finden Sie unter [Erste Schritte mit PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  
 ![PolyBase logical](../../relational-databases/polybase/media/polybase-logical.png "PolyBase logical")  
  
## <a name="why-use-polybase"></a>Gründe für die Verwendung von PolyBase  
Um sinnvolle Entscheidungen treffen zu können, müssen Sie sowohl relationale Daten als auch andere, nicht in Tabellen strukturierte Daten analysieren können – insbesondere in Hadoop verarbeitete Daten. Dies ist schwer zu bewerkstelligen, sofern Sie nicht über eine Möglichkeit verfügen, Daten zwischen den verschiedenen Arten von Datenspeichern zu übertragen. PolyBase schließt diese Lücke durch Verarbeiten von Daten, die sich außerhalb von SQL Server befinden.  
  
Um einfach zu halten, ist die Installation zusätzlichen Software mit Ihrer Hadoop-Umgebung PolyBase nicht erforderlich. Beim Abfragen externer Daten wird die gleiche Syntax verwendet wie beim Abfragen einer Datenbanktabelle. All dies erfolgt transparent. PolyBase behandelt alle Details, die hinter den Kulissen und keine Kenntnisse über Hadoop wird durch den Endbenutzer erforderlich, um externe Tabellen abzufragen. 
  
 PolyBase führt Folgendes aus:  
  
-   **Abfragen von Daten in Hadoop von SQL Server oder PDW gespeichert.** Benutzer speichern Daten in kostengünstigen verteilten und skalierbaren Systemen, wie z.B. Hadoop. PolyBase vereinfacht die Abfrage der Daten mithilfe von T-SQL.  
  
-   **Abfragen von Daten in Azure Blob-Speicher gespeichert.** Ein Azure-Blobspeicher ist eine bequeme Möglichkeit, Daten zu speichern, die von Azure-Diensten verwendet werden.  PolyBase vereinfacht den Zugriff auf die Daten mithilfe von T-SQL.  
  
-   **Importieren von Daten aus Hadoop oder Azure Blob-Speicher mit Azure Data Lake-Speicher** die Geschwindigkeit des Microsoft SQL columnstore-Technologie und Funktionen nutzen, indem Sie Daten aus Hadoop oder Azure Blob-Speicher mit Azure Data Lake-Speicher in relationale Tabellen importieren. Sie benötigen keine separaten ETL-Funktionen und kein Importtool.  

-   **Exportieren von Daten in Hadoop, Azure-Blobspeicher oder Azure Data Lake Store.** Archivieren Sie Daten in Hadoop, Azure-Blobspeichern oder Azure Data Lake Store, um kostengünstigen Speicherplatz zu nutzen und Daten für einfachen Zugriff online zu halten.  
  
-   **Integrieren in BI-Tools.** Verwenden Sie PolyBase zusammen mit den Business Intelligence- und Analysis-Funktionen von Microsoft, oder verwenden Sie beliebige Drittanbietertools, die mit SQL Server kompatibel sind.  
  
## <a name="performance"></a>Leistung  
  
-   **Übertragen der Berechnung an Hadoop.**Der Abfrageoptimierer trifft eine kostenbasierte Entscheidung darüber, ob die Berechnung an Hadoop übertragen wird, um die Abfrageleistung zu verbessern.  Für diese kostenbasierte Entscheidung verwendet der Optimierer Statistiken in externen Tabellen.   Bei der Übertragung der Berechnung werden MapReduce-Aufträge erstellt und die verteilten Berechnungsressourcen von Hadoop genutzt.  
  
-   **Skalieren von Berechnungsressourcen.** Um die Abfrageleistung zu verbessern, können Sie [PolyBase-Erweiterungsgruppen](../../relational-databases/polybase/polybase-scale-out-groups.md)von SQL Server verwenden. Die ermöglicht eine parallele Datenübertragung zwischen SQL Server-Instanzen und Hadoop-Knoten und fügt Berechnungsressourcen für die Verarbeitung der externen Daten hinzu.  
  
## <a name="polybase-guide-topics"></a>PolyBase-Leitfaden – Themen  
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
  
  

