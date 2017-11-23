---
title: Tempdb-Datenbank (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5840033d-2dc6-4576-8a5f-067e2a58b170
caps.latest.revision: "22"
ms.workload: not set
ms.openlocfilehash: 94cd8614f5098a1f065dbfe19f0ec024c42f9179
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="tempdb-database"></a>tempdb-Datenbank
**Tempdb** ist eine SQL Server PDW-Systemdatenbank, in der lokale temporäre Tabellen für die Benutzerdatenbanken gespeichert. Temporäre Tabellen werden häufig verwendet, um die abfrageleistung zu verbessern. Sie können beispielsweise eine temporäre Tabelle verwenden, um ein Skript zu modularisieren und berechnete Daten wiederverwenden.  
  
Weitere Informationen zu den Systemdatenbanken, finden Sie unter [Systemdatenbanken](system-databases.md).  
  
## <a name="Basics"></a>Hauptbegriffe und-Konzepte  
*lokale temporäre Tabelle*  
Ein *lokale temporäre Tabelle* verwendet das Präfix # vor dem Namen der Tabelle und eine temporäre Tabelle, die von einer Sitzung des lokalen Benutzers erstellt wird. Jede Sitzung kann nur die Daten in lokale temporäre Tabellen für eigene Sitzung zugreifen.  
  
Jede Sitzung kann die Metadaten für lokale temporäre Tabellen in allen Sitzungen anzeigen. Beispielsweise können alle Sitzungen Anzeigen der Metadaten für lokale temporäre Tabellen mit der `SELECT * FROM tempdb.sys.tables` Abfrage.  
  
Globale temporäre Tabelle  
*Globale temporäre Tabellen*, unterstützte in SQL Server mit der ## Syntax werden in dieser Version von SQL Server PDW nicht unterstützt.  
  
pdwtempdb  
**Pdwtempdb** ist die Datenbank, in der lokale temporäre Tabellen gespeichert.  
  
PDW temporäre Tabellen nicht mit dem SQL Server implementiert**Tempdb** Datenbank. Stattdessen speichert PDW sie in einer Datenbank mit dem Namen Pdwtempdb. Diese Datenbank auf jedem Compute-Knoten vorhanden ist und über die PDW-Schnittstellen an den Benutzer nicht sichtbar ist. In der Verwaltungskonsole, auf der Seite "Speicher" sehen Sie diese machte für in einer PDW-Systemdatenbank aufgerufen **Tempdb Sql**.  
  
tempdb  
**Tempdb** ist die SQL Server-Tempdb-Datenbank. Die minimale Protokollierung verwendet. SQL Server verwendet Tempdb auf den Serverknoten zum Speichern von temporärer Tabellen, die beim Ausführen von SQL Server-Vorgängen benötigt.  
  
SQL Server PDW löscht die Tabellen aus **Tempdb** wenn:  
  
-   Die DROP TABLE-Anweisung wird ausgeführt.  
  
-   Eine Sitzung wird getrennt. Für die Sitzung nur temporäre Tabellen werden gelöscht.  
  
-   Das Gerät wird heruntergefahren.  
  
-   Der Knoten "Zugriffssteuerung" wurde ein Clusterfailover ausgeführt.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
SQL Server PDW führt die gleichen Vorgänge für temporäre Tabellen und dauerhaften Tabellen, sofern nicht explizit anders. Z. B. ist die Daten in dauerhaften Tabellen, wie lokale temporäre Tabellen verteilt oder über den Compute-Knoten repliziert.  
  
## <a name="LimitationsRestrictions"></a>Einschränkungen  
Einschränkungen für die SQL Server-PDW**Tempdb** Datenbank. Sie *kann nicht:*  
  
-   Erstellen eine globale temporäre Tabelle, die mit beginnt ##.  
  
-   Führen Sie eine Sicherung oder Wiederherstellung des **Tempdb**.  
  
-   Ändern von Berechtigungen für **Tempdb** mit der **GRANT**, **DENY**, oder **widerrufen** Anweisungen.  
  
-   Führen Sie **DBCC SHRINKLOG** für **Tempdb**Tempdb.  
  
-   Ausführen von DDL-Vorgänge auf **Tempdb**. Es gibt einige Ausnahmen. Weitere Informationen finden Sie unter der folgenden Liste der Einschränkungen für lokale temporäre Tabellen.  
  
Einschränkungen für lokale temporäre Tabellen. Sie *kann nicht:*  
  
-   Umbenennen einer temporären Tabelle  
  
-   Erstellen von Partitionen, Sichten oder nicht gruppierte Indizes für eine temporäre Tabelle. **ALTER INDEX** können verwendet werden, um einen gruppierten Index für eine Tabelle erstellt, die mit einem neu erstellen.  
  
-   Ändern von Berechtigungen für temporäre Tabellen mit der GRANT, DENY oder oder REVOKE-Anweisungen.  
  
-   Führen Sie Datenbank-Konsolenbefehle auf temporäre Tabellen.  
  
-   Verwenden Sie denselben Namen für mindestens zwei temporäre Tabellen innerhalb desselben Batches. Wenn mehr als eine lokale temporäre Tabelle innerhalb eines Batches verwendet wird, muss jede einen eindeutigen Namen haben. Wenn mehrere Sitzungen sind die gleichen Batch ausgeführt und die gleiche lokale temporäre Tabelle erstellen, fügt SQL Server PDW intern ein numerisches Suffix an den Namen lokaler temporärer Tabellen einen eindeutigen Namen für jede lokale temporäre Tabelle zu verwalten.  
  
> [!NOTE]  
> Sie *können* erstellen und Aktualisieren von Statistiken für eine temporäre Tabelle. **ALTER INDEX** können verwendet werden, um einen gruppierten Index neu erstellen.  
  
## <a name="permissions"></a>Berechtigungen  
Jeder Benutzer ist berechtigt, temporäre Objekte in tempdb zu erstellen. Benutzer haben nur Zugriff auf ihre eigenen Objekte, es sei denn, ihnen wurden zusätzliche Berechtigungen zugewiesen. Die CONNECT-Berechtigung für tempdb kann widerrufen werden, um Benutzer daran zu hindern, die tempdb-Datenbank zu verwenden. Von diesem Schritt wird jedoch abgeraten, da einige Routinevorgänge auf die Verwendung von tempdb angewiesen sind.  
  
## <a name="RelatedTasks"></a>Verwandte Aufgaben  
  
|Aufgaben|Description|  
|---------|---------------|  
|Erstellen Sie eine Tabelle in **Tempdb**.|Sie können eine temporäre Tabelle für Benutzer mit der CREATE TABLE und CREATE TABLE AS SELECT-Anweisungen erstellen. Weitere Informationen finden Sie unter [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md) und [CREATE TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md).|  
|Anzeigen einer Liste vorhandener Tabellen in **Tempdb**.|`SELECT * FROM tempdb.sys.tables;`|  
|Anzeigen einer Liste vorhandener Spalten im **Tempdb**.|`SELECT * FROM tempdb.sys.columns;`|  
|Anzeigen einer Liste von vorhandenen Objekten im **Tempdb**.|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
