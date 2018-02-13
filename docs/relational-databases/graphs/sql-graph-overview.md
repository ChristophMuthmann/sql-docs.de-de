---
title: Diagramm, die Verarbeitung mit SQL Server und Azure SQL-Datenbank | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: graphs
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, overview
ms.assetid: 
caps.latest.revision: 
author: shkale-msft
ms.author: shkale;barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: 77a50d48ee5c6d5baa8b05b327146e74b5eff815
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>Diagramm, die Verarbeitung mit SQL Server und Azure SQL-Datenbank
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bietet Graph Funktionen zur Modellierung von m: n-Beziehungen. Die Graph-Beziehungen sind in integriert [!INCLUDE[tsql-md](../../includes/tsql-md.md)] und empfangen Sie die Vorteile der Verwendung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als grundlegende Datenbankmanagementsystem.


## <a name="what-is-a-graph-database"></a>Was ist eine Graph-Datenbank?  
Eine Graph-Datenbank ist eine Auflistung von Knoten (oder Scheitelpunkte) und Ränder (oder Beziehungen). Ein Knoten eine Entität (z. B. eine Person oder Organisation) und eine Kante darstellt eine Beziehung zwischen zwei Knoten, die es (z. B. Nachrichtengrenzen oder Freunde) eine Verbindung herstellt. Knoten und Kanten möglicherweise ihnen zugeordnete Eigenschaften. Hier sind einige Funktionen, die eine Datenbank Graph eindeutig zu machen:  
-   Ränder oder Beziehungen sind erstklassige Entitäten in einer Datenbank Graph und können Attribute oder Eigenschaften zugeordnet werden. 
-   Eine einzelne Kante kann mehrere Knoten in einer Datenbank Graph flexibel verbinden.
-   Sie können Mustervergleich und Navigation der Multi-Hop-Abfragen problemlos Ausdrücken.
-   Sie können transitiver und polymorphe Abfragen problemlos Ausdrücken.

## <a name="when-to-use-a-graph-database"></a>Wenn eine Graph-Datenbank verwenden

Es ist kein, eine Graph-Datenbank erreichen kann, die nicht mithilfe einer relationalen Datenbank erreicht werden können. Allerdings kann eine Datenbank Graph express bestimmte Art von Abfragen erleichtern. Darüber hinaus können mit bestimmten Optimierungen, bestimmte Abfragen eine bessere Leistung. Ihre Entscheidung, einen anderen auswählen kann auf folgenden Faktoren basieren:  
-   Die Anwendung verfügt über hierarchische Daten. HierarchyID-Datentyp kann verwendet werden, um Hierarchien zu implementieren, aber es gelten einige Einschränkungen. Beispielsweise können dabei nicht mehrere übergeordnete Elemente für einen Knoten zu speichern.
-   Die Anwendung verfügt über komplexe viele-zu-viele-Beziehungen; Wenn sich Anwendung weiterentwickelt, werden neue Beziehungen hinzugefügt.
-   Sie müssen miteinander verbundener Daten und Beziehungen zu analysieren.

## <a name="graph-features-introduced-in-includesssqlv14includessssqlv14-mdmd"></a>Graph-Funktionen in [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 
Wir beginnen, Hinzufügen von Graph-Erweiterungen zu SQL Server, um das Speichern von und Abfragen von Graph-Daten zu vereinfachen. Folgende Funktionen sind in der ersten Version eingeführt. 


### <a name="create-graph-objects"></a>Graph-Objekte erstellen
[!INCLUDE[tsql-md](../../includes/tsql-md.md)] Benutzern das Erstellen von Knoten oder Edge Tabellen ermöglicht. Knoten und Kanten haben Eigenschaften, die ihnen zugeordnet sind. Seit Knoten und Kanten werden als Tabellen gespeichert, alle Vorgänge, die auf relationalen Tabellen unterstützt werden, werden für Knoten oder Edge-Tabelle unterstützt. Beispiel:  

```   
CREATE TABLE Person (ID INTEGER PRIMARY KEY, Name VARCHAR(100), Age INT) AS NODE;
CREATE TABLE friends (StartDate date) AS EDGE;
```   

![Person Freunde Tabellen](../../relational-databases/graphs/media/person-friends-tables.png "Person-Knoten und Freunde edge-Tabellen")  
Knoten und Kanten werden als Tabellen gespeichert.  

### <a name="query-language-extensions"></a>Abfrage-spracherweiterungen  
Neue `MATCH` Klausel wurde eingeführt, um einen Musterabgleich und Multi-Hop-Navigation durch das Diagramm zu unterstützen. Die `MATCH` Funktion verwendet die Syntax lautet: ASCII-Grafiken für den Mustervergleich. Beispiel:  

```   
-- Find friends of John
SELECT Person2.Name 
FROM Person Person1, Friends, Person Person2
WHERE MATCH(Person1-(Friends)->Person2)
AND Person1.Name = 'John';
```   
 
### <a name="fully-integrated-in-includessnoversionincludesssnoversion-mdmd-engine"></a>Vollständig integrierte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Modul 
Graph-Erweiterungen sind vollständig integriert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Modul. Wir verwenden die gleichen Speichermodul, Metadaten, Abfrageprozessor usw. zum Speichern und Abfragen von Daten im Diagramm anzeigen. Dadurch kann Benutzer ihre Graph und relationale Daten in einer einzelnen Abfrage abzufragen. Benutzer können auch aus der Kombination von Graph-Funktionen mit anderen profitieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Technologien wie Columnstore, hohe Verfügbarkeit, R-Services, usw. SQL-Graph-Datenbank unterstützt auch alle Sicherheits- und Compliance Funktionen zur Verfügung, mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
 
### <a name="tooling-and-ecosystem"></a>Tools und das Ökosystem  
Der Benutzer profitiert von vorhandenen Tools und das Ökosystem, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bietet. Tools wie Sichern und wiederherstellen, importieren und exportieren, BCP nur Arbeit ausgegeben. Andere Tools oder Dienste wie SSIS, SSRS oder PowerBI funktionieren bei Diagramm Tabellen, nur die Möglichkeit, die sie mit relationalen Tabellen arbeiten.
 
 ## <a name="next-steps"></a>Nächste Schritte  
Lesen der [SQL-Datenbank Graph - Architektur](./sql-graph-architecture.md)
   

