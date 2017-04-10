---
title: "Anhalten und Fortsetzen der Datenbankspiegelung (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Sitzungen [SQL Server], Datenbankspiegelung"
  - "Fortsetzen der Datenbankspiegelung"
  - "Datenbankspiegelung [SQL Server], anhalten"
  - "Datenbankspiegelung [SQL Server], fortsetzen"
  - "Anhalten der Datenbankspiegelung"
ms.assetid: c67802c6-ee8c-4cbd-a6d4-f7b80413a4ab
caps.latest.revision: 32
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 32
---
# Anhalten und Fortsetzen der Datenbankspiegelung (SQL Server)
  Der Datenbankbesitzer kann eine Datenbank-Spiegelungssitzung jederzeit anhalten und später fortsetzen. Durch Anhalten bleibt der Sitzungsstatus erhalten, während die Spiegelung unterbrochen wird. Bei Engpässen ist das Anhalten möglicherweise nützlich, um die Leistung auf dem Prinzipalserver zu verbessern.  
  
 Wenn eine Sitzung angehalten wird, bleibt die Prinzipaldatenbank weiterhin verfügbar. Durch das Anhalten wird der Status der Spiegelungssitzung auf SUSPENDED festgelegt, und die Spiegeldatenbank hält nicht mehr Schritt mit der Prinzipaldatenbank. Dadurch wird die Prinzipaldatenbank fehleranfällig ausgeführt.  
  
 Es empfiehlt sich, eine angehaltene Sitzung rasch fortzusetzen, weil das Transaktionsprotokoll nicht gekürzt werden kann, während eine Datenbank-Spiegelungssitzung angehalten ist. Wenn die Datenbank-Spiegelungssitzung zu lange angehalten wird, kann es somit sein, dass das Transaktionsprotokoll vollständig aufgefüllt wird und die Datenbank nicht mehr verfügbar ist. Eine Erläuterung dazu finden Sie unter "Auswirkung des Anhaltens und Fortsetzens auf die Protokollkürzung" weiter unten in diesem Thema.  
  
> [!IMPORTANT]  
>  Nach einem erzwungenen Dienst, wenn der ursprüngliche Prinzipalserver die Verbindung wiederherstellt, wird die Spiegelung angehalten. Das Fortsetzen der Spiegelung in dieser Situation könnte auf dem ursprünglichen Prinzipalserver zu Datenverlust führen. Weitere Informationen zum Verwalten des potenziellen Datenverlusts finden Sie unter [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).  
  
 **In diesem Thema:**  
  
-   [Auswirkung des Anhaltens und Fortsetzens auf die Protokollkürzung](#EffectOnLogTrunc)  
  
-   [Vermeiden eines vollen Transaktionsprotokolls](#AvoidFullLog)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
##  <a name="EffectOnLogTrunc"></a> Auswirkung des Anhaltens und Fortsetzens auf die Protokollkürzung  
 Wenn ein automatischer Prüfpunkt für eine Datenbank ausgeführt wird, wird normalerweise das zugehörige Transaktionsprotokoll nach der nächsten Protokollsicherung auf diesen Prüfpunkt gekürzt. Während eine Datenbank-Spiegelungssitzung angehalten ist, bleiben alle aktuellen Protokolldatensätze aktiv, weil der Prinzipalserver darauf wartet, sie an den Spiegelserver zu senden. Die ungesendeten Protokolldatensätze sammeln sich im Transaktionsprotokoll der Prinzipaldatenbank an, bis die Sitzung fortgesetzt wird und der Prinzipalserver die Protokolldatensätze an den Spiegelserver gesendet hat.  
  
 Wenn die Sitzung fortgesetzt wird, beginnt der Prinzipalserver sofort damit, die akkumulierten Protokolldatensätze an den Spiegelserver zu senden. Nachdem der Spiegelserver bestätigt hat, dass der dem ältesten automatischen Prüfpunkt entsprechende Protokolldatensatz in die Warteschlange gestellt wurde, kürzt der Prinzipalserver das Protokoll der Prinzipaldatenbank auf diesen Prüfpunkt. Der Spiegelserver kürzt die Wiederholungswarteschlange auf denselben Protokolldatensatz. Da dieser Prozess für jeden sukzessiven Prüfpunkt wiederholt wird, wird das Protokoll schrittweise, von Prüfpunkt zu Prüfpunkt, gekürzt.  
  
> [!NOTE]  
>  Weitere Informationen zu Prüfpunkten und der Protokollkürzung finden Sie unter [Datenbankprüfpunkte &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
##  <a name="AvoidFullLog"></a> Vermeiden eines vollen Transaktionsprotokolls  
 Wenn das Protokoll voll ist (weil die maximale Größe erreicht wurde oder weil für die Serverinstanz der Speicherplatz nicht ausreicht), kann die Datenbank keine Updates mehr ausführen. Es gibt zwei Möglichkeiten, um dieses Problem zu vermeiden:  
  
-   Setzen Sie die Datenbank-Spiegelungssitzung fort, bevor das Protokoll voll ist, oder fügen Sie mehr Protokollspeicher hinzu. Durch das Fortsetzen der Datenbankspiegelung kann der Prinzipalserver das angesammelte aktive Protokoll an den Spiegelserver senden, und die Spiegeldatenbank erhält den Status SYNCHRONIZING. Der Spiegelserver kann dann das Protokoll auf den Datenträger schreiben und damit beginnen, es zu wiederholen.  
  
-   Beenden Sie die Datenbank-Spiegelungssitzung durch Entfernen der Spiegelung.  
  
     Im Gegensatz zum Anhalten einer Sitzung werden beim Entfernen der Spiegelung alle Informationen zur Spiegelungssitzung gelöscht. Jede Partnerserverinstanz behält eine eigene Kopie der Datenbank. Wenn die frühere Spiegelkopie wiederhergestellt wird, weicht sie von der früheren Prinzipalkopie ab und liegt um die Zeitspanne zurück, die seit dem Anhalten der Sitzung vergangen ist. Weitere Informationen finden Sie unter [Entfernen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So halten Sie eine Datenbankspiegelung an bzw. setzen sie fort**  
  
-   [Anhalten oder Fortsetzen einer Datenbank-Spiegelungssitzung &#40;SQL Server&#41;](../../database-engine/database-mirroring/pause-or-resume-a-database-mirroring-session-sql-server.md)  
  
 **So beenden Sie die Datenbankspiegelung**  
  
-   [Entfernen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/remove-database-mirroring-sql-server.md)  
  
## Siehe auch  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Entfernen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)  
  
  