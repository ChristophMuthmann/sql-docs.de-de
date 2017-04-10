---
title: "Einschr&#228;nkungen (Stretch-Datenbank) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/14/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.service: "sql-server-stretch-database"
ms.suite: ""
ms.technology: 
  - "dbe-stretch"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Stretch-Datenbank, Einschränkungen"
  - "Stretch-Datenbank, blockierende Probleme"
  - "Einschränkungen (Stretch-Datenbank)"
  - "Blockierende Probleme (Stretch-Datenbank)"
ms.assetid: 2b1fbec1-7859-44fc-8417-724fc57a59c0
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Einschr&#228;nkungen (Stretch-Datenbank)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Erfahren Sie mehr zu Einschränkungen für Stretch-aktivierten Tabellen und zu Einschränkungen, die derzeit verhindern, Stretch für eine Tabelle zu aktivieren.  
  
##  <a name="Caveats"></a> Einschränkungen für Stretch-aktivierte Tabellen  
  
Die folgenden Einschränkungen für Stretch-aktivierte Tabellen sind zu beachten.  
  
### Einschränkungen  
-   Für UNIQUE-Einschränkungen und PRIMARY KEY-Einschränkungen wird in der Azure-Tabelle,die die migrierten Daten enthält, keine Eindeutigkeit erzwungen.  
  
### DML-Vorgänge  
-   Sie können Zeilen, die für die Migration geeignet sind, mit der UPDATE- oder DELETE-Anweisung in einer Stretch-aktivierten Tabelle oder einer Sicht, die Stretch-aktivierte Tabellen enthält, aktualisieren oder löschen.  
  
-   In eine Stretch-aktivierte Tabelle auf einem Verbindungsserver können Zeilen nicht mit INSERT eingefügt werden.  
  
### Indizes  
-   Für eine Sicht, die Stretch-aktivierte Tabellen enthält, kann kein Index erstellt werden.  
  
-   Filter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Indizes werden nicht an die Remotetabelle weitergegeben.  
  
##  <a name="Limitations"></a> Einschränkungen, die derzeit die Aktivierung von Stretch für eine Tabelle verhindern  
   
 Die folgenden Elemente verhindern derzeit die Aktivierung von Stretch für eine Tabelle.  
  
 ### Tabelleneigenschaften  
-   Tabellen, die mehr als 1.023 Spalten oder mehr als 998 Indizes enthalten  
  
-   FileTables, die FILESTREAM-Daten enthalten  
  
-   Tabellen, die repliziert sind oder die Änderungsnachverfolgung oder Change Data Capture aktiv verwenden  
  
-   Speicheroptimierte Tabellen  
  
 ### Datentypen  
 -   text, ntext und image  
  
-   timestamp  
  
-   sql_variant  
  
-   XML  
  
-   CLR-Datentypen, einschließlich „geometry“, „geography“, „hierarchyid“ sowie benutzerdefinierte CLR-Typen  
  
 ### Spaltentypen  
 -   COLUMN_SET  
  
-   Berechnete Spalten  
  
### Einschränkungen  
-   Default- und CHECK-Einschränkungen  
  
-   FOREIGN KEY-Einschränkungen, die auf die Tabelle verweisen. In einer Über-/Unterordnungsbeziehung (z.B. Order und Order_Detail) können Sie Stretch für die untergeordnete Tabelle (Order-Detail) aktivieren, jedoch nicht für die übergeordnete Tabelle (Order).  
  
### Indizes  
-   Volltextindizes  
  
-   XML-Indizes  
  
-   Räumlichkeitsindizes  
  
-   Indizierte Sichten, die auf die Tabelle verweisen  
  
## Siehe auch  
 [Identifizieren von Datenbanken und Tabellen für Stretch-Datenbank durch Ausführen des Ratgebers für Stretch-Datenbank](../../sql-server/stretch-database/stretch database databases and tables - stretch database advisor.md)   
 [Aktivieren von Stretch-Datenbank für eine Datenbank](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Aktivieren von Stretch-Datenbank für eine Tabelle](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  