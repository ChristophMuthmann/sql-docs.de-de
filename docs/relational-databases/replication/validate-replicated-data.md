---
title: "Überprüfen von replizierten Daten | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- inline data validation [SQL Server replication]
- administering replication, validating data
- replication [SQL Server], validating data
- transactional replication, validating data
- validating data
- merge replication data validation [SQL Server replication]
- merge replication data validation [SQL Server replication], about data validation
- validating replicated data
ms.assetid: f7500a2b-61cb-41b5-816d-27609a6c58e7
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 25a6a38f4782ef72a0894cdd89006dfb1b22c315
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="validate-replicated-data"></a>Überprüfen von replizierten Daten
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Bei der Transaktions- und der Mergereplikation können Sie überprüfen, ob die Daten auf dem Abonnenten mit denen auf dem Verleger übereinstimmen. Die Überprüfung kann für bestimmte Abonnements oder für alle Abonnements für eine Veröffentlichung ausgeführt werden. Geben Sie einen der folgenden Überprüfungstypen an. Bei der nächsten Ausführung des Verteilungs-Agents oder des Merge-Agents werden die Daten dann überprüft:  
  
-   Nur Zeilenanzahl. Bei diesem Typ wird lediglich überprüft, ob die Tabelle auf dem Abonnenten dieselbe Zeilenanzahl besitzt wie die Tabelle auf dem Verleger. Der Inhalt der Zeilen wird nicht geprüft. Die Überprüfung der Zeilenanzahl bietet einen Überprüfungsansatz, der kaum Ressourcen beansprucht und Sie Probleme bei den Daten erkennen lässt.  
  
-   Zeilenanzahl und binäre Prüfsumme. Bei dieser Form der Überprüfung wird zusätzlich zum Vergleich der Zeilenanzahl auf dem Verleger und dem Abonnenten mithilfe des Prüfsummenalgorithmus eine Prüfsumme aller Daten berechnet. Ist die Zeilenanzahl fehlerhaft, wird die Berechnung der Prüfsumme nicht ausgeführt.  
  
 Bei der Mergereplikation kann außer der Übereinstimmung der Daten auf dem Abonnenten und dem Verleger auch überprüft werden, ob die Daten auf den einzelnen Abonnenten richtig partitioniert sind. Weitere Informationen finden Sie unter [Überprüfen von Partitionsinformationen für einen Mergeabonnenten](../../relational-databases/replication/validate-partition-information-for-a-merge-subscriber.md).  
  
 **So überprüfen Sie Daten**  
  
 Wenn alle Artikel in einem Abonnement überprüft werden sollen, verwenden Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], gespeicherte Prozeduren oder Replikationsverwaltungsobjekte (RMO). Weitere Informationen finden Sie unter [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md). Wenn nur bestimmte Artikel in einer Momentaufnahme- oder Transaktionsveröffentlichung überprüft werden sollen, müssen Sie gespeicherte Prozeduren verwenden.  
  
## <a name="data-validation-results"></a>Ergebnisse der Datenüberprüfung  
 Nach abgeschlossener Überprüfung protokolliert der Verteilungs-Agent bzw. der Merge-Agent Meldungen zum Erfolg bzw. Misserfolg der Überprüfung (die Replikation vermerkt nicht, bei welchen Zeilen das Ergebnis negativ war). Diese Meldungen können in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], im Replikationsmonitor und in den Replikationssystemtabellen angezeigt werden. Im oben aufgeführten Themen zur Vorgehensweise wird erläutert, wie Sie die Überprüfung ausführen und die Ergebnisse anzeigen können.  
  
 Bei negativem Überprüfungsergebnis sollten folgende Punkte bedacht werden:  
  
-   Konfigurieren Sie die Replikationswarnung **Replikation: Fehler bei der Datenüberprüfung auf dem Abonnenten** , damit Sie bei einem negativen Überprüfungsergebnis benachrichtigt werden. Weitere Informationen finden Sie unter [Konfigurieren von vordefinierten Replikationswarnungen &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md)  
  
-   Ist ein negatives Überprüfungsergebnis ein Problem für Ihre Anwendung? Falls ja, aktualisieren Sie die Daten manuell, damit sie synchronisiert sind, oder initialisieren Sie das Abonnement erneut:  
  
    -   Daten können mit dem [Hilfsprogramm "tablediff"](../../tools/tablediff-utility.md)aktualisiert werden. Weitere Informationen zum Verwenden dieses Hilfsprogramms finden Sie unter [Überprüfen replizierter Tabellen auf Unterschiede &#40;Replikationsprogrammierung&#41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
    -   Weitere Informationen zur erneuten Initialisierung finden Sie unter [Erneutes Initialisieren von Abonnements](../../relational-databases/replication/reinitialize-subscriptions.md).  
  
## <a name="considerations-for-data-validation"></a>Überlegungen zur Datenüberprüfung  
 Bedenken Sie im Zusammenhang mit dem Überprüfen von Daten Folgendes:  
  
-   Vor dem Überprüfen von Daten müssen Sie sämtliche Updateaktivitäten auf den Abonnenten beenden (die Aktivitäten auf dem Verleger müssen für die Überprüfung nicht beendet werden).  
  
-   Weil Prüfsummen und binäre Prüfsummen beim Überprüfen eines großen Datensatzes große Mengen der Prozessorressourcen benötigen, sollten Sie die Überprüfung so planen, dass sie zum Zeitpunkt der niedrigsten Aktivität auf den Servern ausgeführt wird, die für die Replikation verwendet werden.  
  
-   Die Replikation überprüft lediglich Tabellen. Ein Abgleich reiner Schemaartikel (wie z. B. gespeicherter Prozeduren) auf dem Verleger und dem Abonnenten erfolgt nicht.  
  
-   Binäre Prüfsummen können für jede veröffentlichte Tabelle verwendet werden. Die Prüfsumme kann jedoch keine Tabellen mit Spaltenfiltern bzw. logische Tabellenstrukturen überprüfen, bei denen sich die Spaltenoffsets unterscheiden (Ursache dafür sind ALTER TABLE-Anweisungen, die Spalten löschen oder hinzufügen).  
  
-   Die Überprüfung der Replikation verwendet die **checksum** -Funktion und die **binary_checksum** -Funktion. Informationen zum Verhalten finden Sie unter [CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md) und [BINARY_CHECKSUM  &#40;Transact-SQL&#41;](../../t-sql/functions/binary-checksum-transact-sql.md).  
  
-   Die Überprüfung durch binäre Prüfsummen oder Prüfsummen kann dann fälschlicherweise einen Fehler ausgeben, wenn auf dem Abonnenten andere Datentypen vorhanden sind als auf dem Verleger. Dieser Fall kann eintreten, wenn Sie eine der folgenden Aufgaben ausführen:  
  
    -   Sie legen explizit Schemaoptionen zum Zuordnen von Datentypen für frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]fest.  
  
    -   Sie legen den Veröffentlichungskompatibilitätsgrad für eine Mergeveröffentlichung auf eine frühere Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]fest, und veröffentlichte Tabellen enthalten mindestens einen Datentyp, der für diese Version zugeordnet werden muss.  
  
    -   Sie initialisieren ein Abonnement manuell und verwenden auf dem Abonnenten andere Datentypen.  
  
-   Bei der Transaktionsreplikation werden Überprüfungen mithilfe der binären Prüfsumme bzw. der Prüfsumme für transformierbare Abonnements nicht unterstützt.  
  
-   Bei Daten, die auf Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abonnenten repliziert wurden, kann keine solche Überprüfung stattfinden.  
  
## <a name="how-data-validation-works"></a>Funktionsweise der Datenüberprüfung  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] überprüft Daten, indem es auf dem Verleger die Zeilenanzahl bzw. eine Prüfsumme berechnet und dann diese Werte mit der für den Abonnenten berechneten Zeilenanzahl bzw. Prüfsumme vergleicht. Bei der Berechnung der Prüfsumme wird ein Wert für die gesamte Veröffentlichungstabelle und ein Wert für die gesamte Abonnementtabelle berechnet (die Daten in der **text**-, **ntext**- bzw. **image** -Spalte fließen nicht mit ein).  
  
 Während diese Berechnungen ausgeführt werden, werden die Tabellen, deren Zeilenanzahl bzw. Prüfsumme berechnet wird, vorübergehend für den gemeinsamen Zugriff gesperrt. Diese Berechnungen dauern aber nicht lange, sodass die Sperren meist schon innerhalb weniger Sekunden wieder aufgehoben werden.  
  
 Bei der Überprüfung anhand von binären Prüfsummen werden nicht die physischen Zeilen auf der Datenseite, sondern die einzelnen Spalten einer 32-Bit-Redundanzüberprüfung (Redundancy Check, CRC) unterzogen. Dadurch können die Spalten mit der Tabelle in einer beliebigen physischen Reihenfolge auf der Datenseite dargestellt werden, es wird aber trotzdem dieselbe CRC für die Zeile berechnet. Die Überprüfung anhand von binären Prüfsummen kann verwendet werden, wenn Zeilen- oder Spaltenfilter auf die Veröffentlichung angewendet wurden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Best Practices for Replication Administration](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  
