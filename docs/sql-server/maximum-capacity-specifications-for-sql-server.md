---
title: "Spezifikationen der maximalen Kapazität für SQL Server | Microsoft-Dokumentation"
ms.date: 03/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- objects [SQL Server]
- number capacity specifications [SQL Server]
- size [SQL Server], capacity specifications
- number of objects
- capacity specifications [SQL Server]
- maximum capacity specifications [SQL Server]
- size [SQL Server]
- replication capacity specifications [SQL Server]
- objects [SQL Server], capacity specifications
- Database Engine [SQL Server], capacity specifications
ms.assetid: 13e95046-0e76-4604-b561-d1a74dd824d7
caps.latest.revision: 88
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: d4dc2ff665ff191fb75dd99103a222542262d4c4
ms.openlocfilehash: b03d9514e39fad101a305784b6852e012e3e4aad
ms.contentlocale: de-de
ms.lasthandoff: 05/12/2017

---
# <a name="maximum-capacity-specifications-for-sql-server"></a>Spezifikationen der maximalen Kapazität für SQL Server

 > Inhalt im Zusammenhang mit früheren Versionen von SQL Server, finden Sie unter [Maximum Capacity Specifications for SQL Server](https://msdn.microsoft.com/en-US/library/ms143432(SQL.120).aspx).

  Die folgenden Tabellen geben die maximale Größe und Anzahl verschiedener in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Komponenten definierter Objekte an. Um zur Tabelle für eine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Technologie zu navigieren, klicken Sie auf den zugehörigen Link:  
  
 [SQL Server-Datenbankmodul-Objekte](#Engine)  
  
 [SQL Server-Hilfsprogrammobjekte](#Utility)  
  
 [SQL Server-Datenebenenanwendungs-Objekte](#DAC)  
  
 [SQL Server-Replikationsobjekte](#Replication)  
  
##  <a name="Engine"></a> [!INCLUDE[ssDE](../includes/ssde-md.md)] Objekte  
 Die maximale Größe und Anzahl verschiedener Objekte, die in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Datenbanken definiert sind oder auf die in [!INCLUDE[tsql](../includes/tsql-md.md)] -Anweisungen verwiesen wird.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] Objekt (object)||Maximale Größe/Anzahl – [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 Bit)|Zusätzliche Informationen|  
|---------------------------------------------------------|-|------------------------------------------------------------------|----------------------------|  
|Batchgröße||65.536 * Netzwerkpaketgröße|Die Netzwerk-Paketgröße entspricht der Größe der TDS-Pakete (Tabular Data Stream), die für die Kommunikation zwischen Anwendungen und relationalem [!INCLUDE[ssDE](../includes/ssde-md.md)]verwendet werden. Die Standardpaketgröße beträgt 4 KB und wird durch die Konfigurationsoption Netzwerkpaketgröße gesteuert.|  
|Bytes pro Spalte mit kurzen Zeichenfolgen||8.000||  
|Bytes pro GROUP BY, ORDER BY||8.060||  
|Bytes pro Indexschlüssel||900 Bytes für einen gruppierten Index. 1.700 Bytes für einen nicht gruppierten Index.|Die maximale Anzahl von Bytes in einem Schlüssel für einen gruppierten Index darf in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]den Wert 900 nicht überschreiten. Bei einem Schlüssel für einen nicht gruppierten Index liegt der Höchstwert bei 1700 Byte.<br /><br /> Sie können einen Schlüssel mithilfe von Spalten mit variabler Länge definieren, deren maximale Größe in der Summe oberhalb des Grenzwerts liegen. Die Gesamtgröße der in diesen Spalten enthaltenen Daten darf den Grenzwert jedoch nie überschreiten.<br /><br /> In einem nicht gruppierten Index können Sie zusätzliche Nichtschlüsselspalten einschließen. Sie zählen nicht bei der Berechnung der maximalen Schlüsselgröße. Die Nichtschlüsselspalten können die Leistung einer Abfragen verbessern.|  
|Bytes pro Indexschlüssel für speicheroptimierte Tabellen||2500 Bytes für einen nicht gruppierten Index. Für einen Hashindex gilt keine Beschränkung, vorausgesetzt dass alle Indexschlüssel in Zeilen passen.|Ein nicht gruppierter Index darf bei speicheroptimierten Tabellen keine Schlüsselspalten enthalten, deren maximale deklarierte Größe 2500 Bytes überschreiten. Dabei ist es unerheblich, ob die tatsächlich in den Spalten vorhandenen Daten kürzer sind als die maximale deklarierte Größe.<br /><br /> Für einen Hashindexschlüssel gibt es keinen festen Grenzwert für die Größe.<br /><br /> Für Indizes von speicheroptimierten Tabellen ist das Konzept der eingeschlossenen Spalten hinfällig, da alle Indizes grundsätzlich alle Spalten abdecken.<br /><br /> Obwohl die Zeilenlänge bei speicheroptimierten Tabellen 8060 Bytes beträgt, können einige Spalten mit variabler Länge physisch außerhalb dieser 8060 Bytes gespeichert werden. Allerdings müssen die maximale deklarierte Größe aller Schlüsselspalten für alle Indizes einer Tabelle sowie alle zusätzlichen Spalten mit fester Länge in der Tabelle in die 8060 Bytes passen.|  
|Bytes pro Fremdschlüssel||900||  
|Bytes pro Primärschlüssel||900||  
|Bytes pro Zeile||8.060|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] unterstützt die Zeilenüberlaufspeicherung, sodass Spalten variabler Länge aus der Zeile verschoben werden können. Für Spalten variabler Länge, die aus der Zeile verschoben wurden, wird im Hauptdatensatz nur ein 24-Byte-Stamm gespeichert. Aus diesem Grund ist das tatsächlich gültige Zeilenlimit höher als in früheren Versionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Weitere Informationen finden Sie unter "Zeilenüberlauf bei Daten über 8 KB" in der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Onlinedokumentation.|  
|Bytes pro Zeile in speicheroptimierten Tabellen||8.060|Ab [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] unterstützen speicheroptimierte Tabellen das Speichern außerhalb von Zeilen. Spalten mit variabler Länge werden aus der Zeile verschoben, wenn die maximale Größe aller Spalten in der Tabelle 8060 Bytes überschreitet. Diese Entscheidung fällt bei der Kompilierung. Für Spalten, die außerhalb der Zeile gespeichert wurden, wird in der Zeile nur eine 8-Byte-Referenz gespeichert. Weitere Informationen finden Sie unter [Tabellen- und Zeilengröße in speicheroptimierten Tabellen](../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md).|  
|Bytes im Quelltext einer gespeicherten Prozedur||Kleiner als Batchgröße oder 250 MB||  
|Bytes pro **varchar(max)**-, **varbinary(max)**-, **xml**-, **text**-, oder **image** -Spalte||2^31-1||  
|Zeichen pro **ntext** - oder **nvarchar(max)** -Spalte||2^30-1||  
|Gruppierte Indizes pro Tabelle||1||  
|Spalten in GROUP BY, ORDER BY||Begrenzung nur durch die Anzahl von Bytes||  
|Spalten oder Ausdrücke in einer GROUP BY WITH CUBE- oder WITH ROLLUP-Anweisung||10||  
|Spalten pro Indexschlüssel||32|Wenn die Tabelle einen oder mehrere XML-Indizes enthält, ist der Gruppierungsschlüssel der Benutzertabelle auf 31 Spalten beschränkt, da die XML-Spalte dem Gruppierungsschlüssel des primären XML-Index hinzugefügt wird. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]können Sie Nichtschlüsselspalten in den nicht gruppierten Index aufnehmen, um die Beschränkung auf maximal 32 Schlüsselspalten zu vermeiden. Weitere Informationen finden Sie unter [Create Indexes with Included Columns](../relational-databases/indexes/create-indexes-with-included-columns.md).|  
|Spalten pro Fremdschlüssel||32||  
|Spalten pro Primärschlüssel||32||  
|Spalten pro Tabelle (keine breite Tabelle)||1.024||  
|Spalten pro breiter Tabelle||30.000||  
|Spalten pro SELECT-Anweisung||4.096||  
|Spalten pro INSERT-Anweisung||4096||  
|Verbindungen pro Client||Höchstwert konfigurierter Verbindungen||  
|Datenbankgröße||524.272 Terabytes||  
|Datenbanken pro Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]||32.767||  
|Dateigruppen pro Datenbank||32.767||  
|Dateigruppen pro Datenbank für speicheroptimierte Daten||1||  
|Dateien pro Datenbank||32.767||  
|Dateigröße (Daten)||16 Terabytes||  
|Dateigröße (Protokoll)||2 Terabytes||  
|Datendateien für speicheroptimierte Daten pro Datenbank||4.096||  
|Änderungsdatei pro Datendatei für speicheroptimierte Daten||1||  
|Verweise auf Fremdschlüsseltabellen pro Tabelle||Ausgehend = 253. Eingehend = 10.000.|Einschränkungen finden Sie unter [Create Foreign Key Relationships](../relational-databases/tables/create-foreign-key-relationships.md).|  
|Bezeichnerlänge (in Zeichen)||128||  
|Instanzen pro Computer||50 Instanzen auf einem eigenständigen Server.<br /><br /> 25 Instanzen auf einem Failovercluster, wenn Sie für die Clusterinstallation einen freigegebenen Clusterdatenträger als Speicheroption verwenden. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] unterstützt 50 Instanzen auf einem Failovercluster, wenn Sie für die Clusterinstallation SMB-Dateifreigaben als Speicheroption verwenden.||  
|Indizes pro speicheroptimierter Tabelle||8||  
|Länge einer Zeichenfolge, die SQL-Anweisungen enthält (Batchgröße)||65.536 * Netzwerkpaketgröße|Die Netzwerk-Paketgröße entspricht der Größe der TDS-Pakete (Tabular Data Stream), die für die Kommunikation zwischen Anwendungen und relationalem [!INCLUDE[ssDE](../includes/ssde-md.md)]verwendet werden. Die Standardpaketgröße beträgt 4 KB und wird durch die Konfigurationsoption Netzwerkpaketgröße gesteuert.|  
|Sperren pro Verbindung||Maximale Anzahl Sperren pro Server||  
|Sperren pro Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]||Begrenzung nur durch Arbeitsspeicher|Dieser Wert dient der statischen Sperrenzuordnung. Dynamische Sperren sind nur durch den Arbeitsspeicher beschränkt.|  
|Schachtelungsebenen gespeicherter Prozeduren||32|Wenn eine gespeicherte Prozedur auf mehr als 64 Datenbanken zugreift oder sich mehr als 2 Datenbanken überlappen, wird eine Fehlermeldung angezeigt.|  
|Geschachtelte Unterabfragen||32||  
|Schachtelungsebenen für Trigger||32||  
|Nicht gruppierte Indizes pro Tabelle||999||  
|Anzahl der unterschiedlichen Ausdrücke in der GROUP BY-Klausel bei Vorhandensein eines der folgenden Ausdrücke: CUBE, ROLLUP, GROUPING SETS, WITH CUBE, WITH ROLLUP||32||  
|Anzahl der Gruppierungssätze, die von Operatoren in der GROUP BY-Klausel generiert wurden||4.096||  
|Parameter pro gespeicherter Prozedur||2.100||  
|Parameter pro benutzerdefinierter Funktion||2.100||  
|REFERENCES pro Tabelle||253||  
|Zeilen pro Tabelle||Begrenzung durch verfügbaren Speicherplatz||  
|Tabellen pro Datenbank||Begrenzung durch die Anzahl der Objekte in einer Datenbank|Zu den Datenbankobjekten zählen Tabellen, Sichten, gespeicherte Prozeduren, benutzerdefinierte Funktionen, Trigger, Regeln, Standardwerte und Einschränkungen. Die Summe aller Objekte in einer Datenbank kann 2.147.483.647 nicht übersteigen.|  
|Partitionen pro partitionierter Tabelle oder partitioniertem Index||15.000||  
|Statistiken für nicht indizierte Spalten||30.000|| 
|Tabellen pro SELECT-Anweisung||Begrenzung nur durch verfügbare Ressourcen||  
|Trigger pro Tabelle||Begrenzung durch die Anzahl der Objekte in einer Datenbank|Zu den Datenbankobjekten zählen Tabellen, Sichten, gespeicherte Prozeduren, benutzerdefinierte Funktionen, Trigger, Regeln, Standardwerte und Einschränkungen. Die Summe aller Objekte in einer Datenbank kann 2.147.483.647 nicht übersteigen.|  
|Spalten pro UPDATE-Anweisung (breite Tabellen)||4096||  
|Benutzerverbindungen||32.767||  
|XML-Indizes||249||  
  
##  <a name="Utility"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Hilfsprogrammobjekte  
 Die maximale Größe und Anzahl verschiedener, im [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Hilfsprogramm getesteter Objekte.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Hilfsprogrammobjekt||Maximale Größe/Anzahl – [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 Bit)|  
|----------------------------------------------|-|------------------------------------------------------------------|  
|Computer (physische Computer oder virtuelle Computer) pro [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Hilfsprogramm||100|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanzen pro Computer||5|  
|Gesamtzahl von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanzen pro [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Hilfsprogramm||200*|  
|Benutzerdatenbanken pro [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz, einschließlich Datenebenenanwendungen||50|  
|Gesamtzahl von Benutzerdatenbanken pro [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Hilfsprogramm||1.000|  
|Dateigruppen pro Datenbank||1|  
|Datendateien pro Dateigruppe||1|  
|Protokolldateien pro Datenbank||1|  
|Volumes pro Computer||3|  
  
 * Die maximale Anzahl verwalteter [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanzen, die vom [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Hilfsprogramm unterstützt werden, ist von der Hardwarekonfiguration des Servers abhängig. Informationen zu ersten Schritten finden Sie unter [Funktionen und Tasks im SQL Server-Hilfsprogramm](https://msdn.microsoft.com/library/ee210548.aspx). [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Ein Steuerungspunkt für das Hilfsprogramm ist nicht in jeder Edition von [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]verfügbar. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](https://msdn.microsoft.com/library/cc645993.aspx).  
  
##  <a name="DAC"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Datenebenenanwendungs-Objekte  
 Die maximale Größe und Anzahl verschiedener in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Datenebenenanwendungen (DAC) getesteter Objekte.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] DAC-Objekt||Maximale Größe/Anzahl – [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 Bit)|  
|------------------------------------------|-|------------------------------------------------------------------|  
|Datenbanken pro DAC||1|  
|Objekte pro DAC*||Durch die Anzahl der Objekte in einer Datenbank oder durch den verfügbaren Speicher beschränkt.|  
  
 * Die maximalen Werte gelten für folgende Objekttypen: Benutzer, Tabellen, Sichten, gespeicherte Prozeduren, benutzerdefinierte Funktionen, Datentypen und Tabellentypen sowie Datenbankrollen und Schemas.  
  
##  <a name="Replication"></a> Replikationsobjekte  
 Die maximale Größe und Anzahl verschiedener in der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Replikation definierter Objekte.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Replikationsobjekt||Maximale Größe/Anzahl SQL Server (64-Bit)|  
|--------------------------------------------------|-|---------------------------------------------------|  
|Artikel (Mergeveröffentlichung)||256|  
|Artikel (Momentaufnahmen- oder Transaktionsveröffentlichung)||32.767|  
|Spalten in einer Tabelle* (Mergeveröffentlichung)||246|  
|Spalten in einer Tabelle** ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Momentaufnahmen- oder -Transaktionsveröffentlichung)||1.000|  
|Spalten in einer Tabelle** (Oracle-Momentaufnahmen- oder -Transaktionsveröffentlichung)||995|  
|Bytes für eine in einem Zeilenfilter verwendete Spalte (Mergeveröffentlichung)||1.024|  
|Bytes für eine in einem Zeilenfilter verwendete Spalte (Momentaufnahmen- oder Transaktionsveröffentlichung)||8.000|  
  
 * Falls die Zeilennachverfolgung zur Konflikterkennung verwendet wird (Standardeinstellung), kann die Basistabelle maximal 1.024 Spalten enthalten. Die Spalten müssen jedoch im Artikel gefiltert werden, sodass maximal 246 Spalten veröffentlicht werden. Wenn Spaltennachverfolgung verwendet wird, kann die Basistabelle maximal 246 Spalten enthalten.  
  
 ** Die Basistabelle kann die maximal zulässige Anzahl von Spalten in der Veröffentlichungsdatenbank (1.024 für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]) enthalten. Die Spalten müssen aber aus dem Artikel herausgefiltert werden, wenn sie das für den Veröffentlichungstyp angegebene Maximum überschreiten.  
  
## <a name="see-also"></a>Siehe auch  
 [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [Überprüfen der Parameter für die Systemkonfigurationsprüfung](../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)   
 [Funktionen und Tasks im SQL Server-Hilfsprogramm](../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  

