---
title: "SQL Server, SQL-Statistik-Objekt | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQLServer:SQL-Statistik"
  - "SQL-Statistik-Objekt"
ms.assetid: da7dbb4b-f632-45a0-b1ab-c35cc2695c86
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# SQL Server, SQL-Statistik-Objekt
  Das **SQLServer:SQL-Statistik** -Objekt in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt Indikatoren bereit, mit denen Sie die Kompilierung und die Art der Anforderungen, die an eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gesendet werden, überwachen können. Das Überwachen der Anzahl der Kompilierungen und Neukompilierungen von Abfragen sowie der Anzahl der Batches, die eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erhalten hat, gibt Ihnen einen Hinweis auf die Verarbeitungsgeschwindigkeit von Benutzerabfragen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sowie auf die Effektivität, mit der der Abfrageoptimierer die Abfragen verarbeitet.  
  
 Das Kompilieren ist ein wesentlicher Bestandteil der Verarbeitungszeit einer Abfrage. Um Kompilierungskosten zu sparen, speichert [!INCLUDE[ssDE](../../includes/ssde-md.md)] den kompilierten Abfrageplan in einem Abfragecache. Das Ziel des Caches liegt darin, die Kompilierung durch Speichern der kompilierten Abfragen zur späteren Wiederverwendung zu reduzieren, wodurch vermieden wird, dass die Abfragen bei einer späteren Ausführung erneut kompiliert werden müssen. Jede eindeutige Abfrage muss jedoch mindestens einmal kompiliert werden. Das Neukompilieren von Abfragen kann durch die folgenden Faktoren ausgelöst werden:  
  
-   Schemaänderungen, einschließlich Basisschemaänderungen, wie etwa das Hinzufügen von Spalten oder Indizes zu einer Tabelle, oder Statistikschemaänderungen, wie das Einfügen oder Löschen einer großen Anzahl von Zeilen aus einer Tabelle.  
  
-   Umgebungsänderungen (SET-Anweisungen). Änderungen an Sitzungseinstellungen, wie z. B. ANSI_PADDING oder ANSI_NULLS, können dazu führen, dass eine Abfrage neu kompiliert wird.  
  
 Weitere Informationen zur einfachen und erzwungenen Parametrisierung finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
 Es folgen die Leistungsindikatoren für das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **-Objekt von** .  
  
|SQL-Statistik-Leistungsindikatoren von SQL Server|Beschreibung|  
|----------------------------------------|-----------------|  
|**Versuche für automatische Parametrisierung/Sekunde**|Anzahl der Versuche für automatische Parametrisierung pro Sekunde. Die Gesamtanzahl sollte die Summe der fehlgeschlagenen, gesicherten und ungesicherten automatischen Parametrisierungen sein. Eine automatische Parametrisierung tritt dann ein, wenn eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versucht, eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anforderung zu parametrisieren, indem bestimmte Literale durch Parameter ersetzt werden, damit der sich ergebende zwischengespeicherte Ausführungsplan für mehrere ähnliche Anforderungen wiederverwendet werden kann. Beachten Sie, dass in höheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Auto-Parametrisierungen auch als einfache Parametrisierungen bezeichnet werden. Dieser Leistungsindikator schließt keine erzwungenen Parametrisierungen ein.|  
|**Batchanforderungen/Sekunde**|Anzahl der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Befehlsbatches, die pro Sekunde empfangen wurden. Diese Statistik ist von allen Einschränkungen (wie z. B. E/A, Anzahl der Benutzer, Cachegröße, Komplexität der Anforderungen usw.) betroffen. Eine hohe Anzahl der Batchanforderungen bedeutet einen guten Durchsatz.|  
|**Fehler bei Auto-Parametrisierungen/Sekunde**|Anzahl der fehlgeschlagenen automatischen Parametrisierungen pro Sekunde. Dieser Wert sollte niedrig sein. Beachten Sie, dass in höheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Auto-Parametrisierungen auch als einfache Parametrisierungen bezeichnet werden.|  
|**Erzwungene Parametrisierungen/Sekunde**|Anzahl der pro Sekunde erfolgreichen erzwungenen Parametrisierungen.|  
|**Planausführungen mit Planhinweisliste/Sek.**|Die Anzahl der Planausführungen pro Sekunde, bei denen der Abfrageplan mithilfe einer Planhinweisliste erzeugt wurde.|  
|**Planausführungen ohne Planhinweisliste/Sek.**|Die Anzahl der Planausführungen pro Sekunde, bei denen die Planhinweisliste bei der Erzeugung des Plans ignoriert wurde. Die Planhinweisliste wurde übergangen, und der Ausführungsplan wurde über eine normale Kompilierung erzeugt.|  
|**Sichere Auto-Parametrisierungen/Sekunde**|Anzahl der sicheren automatischen Parametrisierungen pro Sekunde. Sicher bezieht sich darauf, dass ein zwischengespeicherter Ausführungsplan von unterschiedlichen, ähnlich lautenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen gemeinsam verwendet werden kann. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unternimmt eine Vielzahl von Versuchen für die automatische Parametrisierung, wovon einige sich als sicher erweisen und bei anderen Fehler auftreten. Beachten Sie, dass in höheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Auto-Parametrisierungen auch als einfache Parametrisierungen bezeichnet werden. Dieser Leistungsindikator schließt keine erzwungenen Parametrisierungen ein.|  
|**SQL-Warnungsrate**|Anzahl der Warnungen pro Sekunde. Eine Warnung ist eine Anforderung des Clients, die aktuell ausgeführte Anforderung zu beenden.|  
|**SQL-Kompilierungen/Sekunde**|Anzahl der SQL-Kompilierungen pro Sekunde. Gibt an, wie oft der Pfad für den Kompilierungscode eingegeben wurde. Dies schließt Kompilierungen ein, die durch Neukompilierungen auf Anweisungsebene in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verursacht wurden. Wenn die Benutzeraktivität von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stabil ist, erreicht dieser Wert einen gleich bleibenden Status.|  
|**Erneute SQL-Kompilierungen/Sekunde**|Anzahl der erneuten Anweisungskompilierungen pro Sekunde. Zählt, wie oft erneute Kompilierungen von Anweisungen ausgelöst werden. Im Allgemeinen liegt es in Ihrem Interesse, dass der Wert der Neukompilierungen niedrig ist.|  
|**Unsichere Auto-Parametrisierungen/Sekunde**|Anzahl der unsicheren automatischen Parametrisierungen pro Sekunde. Beispielsweise weist die Abfrage Eigenschaften auf, die verhindern, dass der zwischengespeicherte Plan wiederverwendet wird. Diese werden als unsafe gekennzeichnet. Die Anzahl der erzwungenen Parametrisierungen wird von diesem Leistungsindikator nicht gezählt.|  
  
## Siehe auch  
 [SQL Server, Plancache-Objekt](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)   
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  