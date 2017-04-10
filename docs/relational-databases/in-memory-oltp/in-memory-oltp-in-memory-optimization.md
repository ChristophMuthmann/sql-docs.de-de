---
title: "In-Memory OLTP (Arbeitsspeicheroptimierung) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "In-Memory OLTP"
  - "Speicheroptimierte Tabellen"
ms.assetid: e1d03d74-2572-4a55-afd6-7edf0bc28bdb
caps.latest.revision: 106
author: "MightyPen"
ms.author: "genemi"
manager: "jhubbard"
caps.handback.revision: 105
---
# In-Memory OLTP (Arbeitsspeicheroptimierung)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] kann die Leistung beim Verarbeiten von Transaktionen, Erfassen und Laden von Daten sowie in vorübergehenden Datenszenarien erheblich verbessern.  Informationen zum grundlegenden Code und Wissen, den bzw. das Sie für einen schnellen Test Ihrer eigenen speicheroptimierten Tabelle und nativ kompilierten gespeicherten Prozedur benötigen, finden Sie unter
 -  [Schnellstart 1: In-Memory-OLTP-Technologien für höhere Transact-SQL-Leistung](../../relational-databases/in-memory-oltp/quick-start-1-in-memory-oltp-technologies-for-faster-transact-sql-performance.md).  
 
Ein 17-minütiges Video, in dem In-Memory-OLTP erläutert wird und Leistungsvorteile veranschaulicht werden:

-  [In-Memory-OLTP in SQL Server 2016](https://www.youtube.com/watch?v=l5l5eophmK4).

Herunterladen der Demo der Leistung für In-Memory-OLTP, die in dem Video verwendet wird: 

- [In-Memory OLTP Performance Demo v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)

Eine detailliertere Übersicht über In-Memory-OLTP und die Szenarien, in denen die Technologie Leistungsvorteile bringt, finden Sie unter:

- [Übersicht und Verwendungsszenarien](../../relational-databases/in-memory-oltp/overview-and-usage-scenarios.md)
 
 Beachten Sie, dass [!INCLUDE[hek_2](../../includes/hek-2-md.md)] die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Technologie zur Verbesserung der Leistung der Transaktionsverarbeitung ist. Zur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Technologie, die die Leistung von Berichts- und Analyseabfragen verbessert, siehe [Beschreibung von Columnstore-Indizes](../Topic/Columnstore%20Indexes%20Guide.md).
  
 Mehrere Verbesserungen wurden an In-Memory-OLTP sowohl in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] als auch in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] vorgenommen. Die Transact-SQL-Oberfläche wurde verbessert, um das Migrieren von Datenbanken zu vereinfachen. Unterstützung für die Ausführung von ALTER-Vorgängen für speicheroptimierte Tabellen und systemintern kompilierte gespeicherte Prozeduren wurde hinzugefügt, um Anwendungen einfacher zu verwalten. Informationen zu den neuen Funktionen in [!INCLUDE[hek_2](../../includes/hek-2-md.md)] finden Sie unter [Neuigkeiten im Datenbankmodul](../Topic/What's%20New%20in%20Database%20Engine.md).  
  
> [!NOTE]  
>  **Probieren Sie es aus**  
>   
>  In-Memory-OLTP ist in Azure SQL-Datenbanken im Tarif „Premium“ verfügbar. Zum Einstieg in In-Memory-OLTP sowie Columnstore in Azure SQL-Datenbank finden Sie Informationen unter [Optimieren der Leistung mithilfe von In-Memory-Technologien in SQL-Datenbank](https://azure.microsoft.com/documentation/articles/sql-database-in-memory/).  
  

## <a name="in-this-section"></a>In diesem Abschnitt  
 Dieser Abschnitt enthält die folgenden Themen:  
  
|Thema|Description|  
|-----------|-----------------|  
|[Schnellstart 1: In-Memory-OLTP-Technologien für höhere Transact-SQL-Leistung](../../relational-databases/in-memory-oltp/quick-start-1-in-memory-oltp-technologies-for-faster-transact-sql-performance.md)|Tauchen Sie direkt in In-Memory-OLTP ein.|
|[Übersicht und Verwendungsszenarien](../../relational-databases/in-memory-oltp/overview-and-usage-scenarios.md)|Übersicht über die Aufgaben von In-Memory-OLTP und die Szenarien, die hinsichtlich Leistung davon profitieren.|
|[Anforderungen für die Verwendung speicheroptimierter Tabellen](../../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)|Erläutert Hardware- und Softwareanforderungen und Richtlinien zum Verwenden von speicheroptimierten Tabellen.|  
|[Codebeispiele für In-Memory OLTP](../../relational-databases/in-memory-oltp/in-memory-oltp-code-samples.md)|Enthält Codebeispiele, die das Erstellen und Verwenden einer speicheroptimierten Tabelle veranschaulichen.|  
|[Speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)|Bietet eine Einführung in speicheroptimierte Tabellen.|  
|[Speicheroptimierte Tabellenvariablen](../Topic/Memory-Optimized%20Table%20Variables.md)|Ein Codebeispiel, das veranschaulicht, wie eine speicheroptimierte Tabellenvariable anstelle einer herkömmlichen Tabellenvariable verwendet wird, um die Verwendung von tempdb zu reduzieren.|  
|[Indizes für speicheroptimierte Tabellen](../Topic/Indexes%20on%20Memory-Optimized%20Tables.md)|Bietet eine Einführung in speicheroptimierte Indizes.|  
|[Nativ kompilierte gespeicherte Prozeduren](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)|Führt systemintern kompilierte gespeicherte Prozeduren ein.|  
|[Verwalten des Arbeitsspeichers für In-Memory-OLTP](../Topic/Managing%20Memory%20for%20In-Memory%20OLTP.md)|Erläutert die Funktionsweise und Verwaltung der Speicherverwendung im System.|  
|[Erstellen und Verwalten von Speicher für speicheroptimierte Objekte](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)|Erläutert Daten- und Änderungsdateien, die Informationen zu Transaktionen in speicheroptimierten Tabellen speichern.|  
|[Sichern und Wiederherstellen speicheroptimierter Tabellen](../Topic/Backup,%20Restore,%20and%20Recovery%20of%20Memory-Optimized%20Tables.md)|Erläutert die Sicherung und Wiederherstellung von speicheroptimierten Tabellen.|  
|[Transact-SQL-Unterstützung für In-Memory-OLTP](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)|Erläutert die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Unterstützung für [!INCLUDE[hek_2](../../includes/hek-2-md.md)].|  
|[Unterstützung für Hochverfügbarkeit für In-Memory-OLTP-Datenbanken](../../relational-databases/in-memory-oltp/high-availability-support-for-in-memory-oltp-databases.md)|Erläutert Verfügbarkeitsgruppen und Failoverclustering in [!INCLUDE[hek_2](../../includes/hek-2-md.md)].|  
|[SQL Server-Unterstützung für In-Memory-OLTP](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)|Listet neue und aktualisierte Syntax und Funktionen auf, die speicheroptimierte Tabellen unterstützen.|  
|[Migrieren zu In-Memory-OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)|Erläutert, wie datenträgerbasierte Tabellen zu speicheroptimierten Tabellen migriert werden.|  
  
 Weitere Informationen zu [!INCLUDE[hek_2](../../includes/hek-2-md.md)] finden Sie unter:  

- [Video, in dem In-Memory-OLTP erläutert wird und Leistungsvorteile veranschaulicht werden](https://www.youtube.com/watch?v=l5l5eophmK4).

- [In-Memory OLTP Performance Demo v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)

-   [SQL Server In-Memory-OLTP: Internes technisches Whitepaper](https://msdn.microsoft.com/library/mt764316.aspx)  

-   [Vergleich zwischen SQL Server In-Memory-OLTP und Columnstore-Funktion](http://download.microsoft.com/download/D/0/0/D0075580-6D72-403D-8B4D-C3BD88D58CE4/SQL_Server_2016_In_Memory_OLTP_and_Columnstore_Comparison_White_Paper.pdf)

-   Neuigkeiten bei In-Memory OLTP in SQL Server 2016 – [Teil 1](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/11/12/in-memory-oltp-whats-new-in-sql2016-ctp3/) und [Teil 2](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/25/whats-new-for-in-memory-oltp-in-sql-server-2016-since-ctp3/)
  
-   [In-Memory-OLTP – Allgemeine Arbeitsauslastungsmuster und Überlegungen zur Migration](http://msdn.microsoft.com/library/dn673538.aspx)  
  
-   [In-Memory-OLTP-Blog](http://go.microsoft.com/fwlink/?LinkId=311696)  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankfunktionen](../../relational-databases/database-features.md)  
  
  