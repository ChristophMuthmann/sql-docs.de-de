---
title: Hash Warning-Ereignisklasse | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Hash Warning event class
ms.assetid: cb93c620-4be9-4362-8bf0-af3f2048bdaf
caps.latest.revision: 39
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 322018e04193b8cabd7354719b85f230b11b2d26
ms.lasthandoff: 04/11/2017

---
# <a name="hash-warning-event-class"></a>Hash Warning-Ereignisklasse
  Mit der Hash Warning-Ereignisklasse können Sie überwachen, ob während eines Hashvorgangs eine Hashrekursion oder eine Beendigung des Hashings (Hashabbruch) aufgetreten ist.  
  
 Die Hashrekursion tritt auf, wenn die Eingabe für den verfügbaren Arbeitsspeicher zu groß ist und deshalb auf mehrere Partitionen verteilt wird, die separat verarbeitet werden. Sollten diese Partitionen für den Arbeitsspeicher immer noch zu groß sein, werden sie in Unterpartitionen aufgeteilt, die dann ebenfalls separat verarbeitet werden. Dieser Vorgang wird so lange fortgesetzt, bis jede Partition in den verfügbaren Arbeitsspeicher passt oder die maximale Rekursionsebene erreicht ist (die in der IntegerData-Datenspalte angezeigt wird).  
  
 Ein Hashabbruch tritt auf, wenn ein Hashvorgang die maximale Rekursionsebene erreicht hat und ein alternativer Plan verwendet wird, um die restlichen Partitionsdaten zu verarbeiten. Ein Hashabbruch tritt gewöhnlich aufgrund von verfälschten Daten auf.  
  
 Durch die Hashrekursion und den Hashabbruch wird die Leistung auf dem Server beeinträchtigt. Führen Sie eine der folgenden Aktionen aus, um Hashrekursionen und Hashabbrüche zu eliminieren oder deren Häufigkeit zu reduzieren:  
  
-   Stellen Sie sicher, dass in den Spalten, die verknüpft oder gruppiert werden, Statistiken vorhanden sind.  
  
-   Falls in den Spalten Statistiken vorhanden sind, aktualisieren Sie diese.  
  
-   Verwenden Sie einen anderen Jointyp. Verwenden Sie beispielsweise ggf. einen MERGE- bzw. LOOP-Join.  
  
-   Erhöhen Sie den verfügbaren Arbeitsspeicher auf dem Computer. Eine Hashrekursion oder ein Hashabbruch tritt auf, wenn nicht ausreichend Arbeitsspeicher zum Verarbeiten von Abfragen vorhanden ist und ein Überlauf auf den Datenträger notwendig ist.  
  
 Das Erstellen oder Aktualisieren der Statistiken in der an dem Join beteiligten Spalte ist die effizienteste Methode, um die Anzahl von Hashrekursionen oder Hashabbrüchen zu reduzieren.  
  
> [!NOTE]  
>  Die Begriffe *schrittweiser Hashjoin* und *rekursiver Hashjoin* werden ebenfalls zur Beschreibung eines Hashabbruchs verwendet.  
  
> [!IMPORTANT]  
>  Sie sollten auch eine Showplan-Ereignisklasse in der Ablaufverfolgung sammeln, um zu bestimmen, an welcher Stelle das Hash Warning-Ereignis auftritt, wenn der Abfrageoptimierer einen Ausführungsplan generiert. Abgesehen von den Ereignisklassen Showplan Text und Showplan Text (Unencoded), die keine Knoten-ID zurückgeben, können Sie jede der Showplan-Ereignisklassen auswählen. Knoten-IDs in Showplans identifizieren jeden Vorgang, den der Abfrageoptimierer beim Generieren eines Abfrageausführungsplans ausführt. Diese Vorgänge werden als *Operatoren*bezeichnet. Jeder Operator in einem Showplan verfügt über eine Knoten-ID. Die ObjectID-Spalte für Hash Warning-Ereignisse entspricht der Knoten-ID in Showplans, sodass Sie den Operator bzw. den Vorgang ermitteln können, der den Fehler verursacht.  
  
## <a name="hash-warning-event-class-data-columns"></a>Datenspalten der Hash Warning-Ereignisklasse  
  
|Datenspaltenname|Datentyp|Beschreibung|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den von der Anwendung übergebenen Werten und nicht mit dem angezeigten Programmnamen aufgefüllt.|10|ja|  
|ClientProcessID|**int**|Die ID, die der Hostcomputer dem Prozess zuweist, in dem die Clientanwendung ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Client eine Clientprozess-ID bereitstellt.|9|ja|  
|DatabaseID|**int**|Die ID der Datenbank, die durch die USE *database* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *database* -Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die ServerName-Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|DatabaseName|**nvarchar**|Name der Datenbank, in der die Benutzeranweisung ausgeführt wird.|35|ja|  
|EventClass|**int**|Ereignistyp = 55.|27|Nein|  
|EventSequence|**int**|Sequenz eines bestimmten Ereignisses innerhalb der Anforderung.|51|Nein|  
|EventSubClass|**int**|Der Typ der Ereignisunterklasse.<br /><br /> 0 = Rekursion<br /><br /> 1 = Abbruch|21|ja|  
|GroupID|**int**|ID der Arbeitsauslastungsgruppe, in der das SQL-Ablaufverfolgungsereignis ausgelöst wird.|66|ja|  
|HostName|**nvarchar**|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname vom Client bereitgestellt wird. Der Hostname kann mithilfe der HOST_NAME-Funktion bestimmt werden.|8|Ja|  
|IntegerData|**int**|Rekursionsebene (nur Hashrekursion)|25|Ja|  
|IsSystem|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, 0 = Benutzer.|60|ja|  
|LoginName|**nvarchar**|Anmeldename des Benutzers (Entweder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sicherheitsanmeldung oder Windows-Anmeldeinformationen im Format *\<DOMAIN>\\<username\>*).|11|ja|  
|LoginSid|**image**|Sicherheits-ID (SID) des angemeldeten Benutzers. Diese Informationen finden Sie in der sys.server_principals-Katalogsicht. Die SID ist für jede Anmeldung beim Server eindeutig.|41|ja|  
|NTDomainName|**nvarchar**|Windows-Domäne, zu der der Benutzer gehört.|7|ja|  
|NTUserName|**nvarchar**|Windows-Benutzername.|6|ja|  
|ObjectID|**int**|Die Knoten-ID des Stammes vom an der Neupartition beteiligten Hashteam. Entspricht der Knoten-ID in Showplans.|22|ja|  
|RequestID|**int**|Die ID der Anforderung, die die Anweisung enthält.|49|ja|  
|ServerName|**nvarchar**|Name der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , für die eine Ablaufverfolgung ausgeführt wird.|26||  
|SessionLoginName|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie beispielsweise mithilfe von Login1 eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und eine Anweisung als Login2 ausführen, zeigt SessionLoginName den Wert Login1 an und LoginName den Wert Login2. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|ja|  
|SPID|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|StartTime|**datetime**|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|Ja|  
|TransactionID|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|ja|  
|XactSequence|**bigint**|Das Token, das die aktuelle Transaktion beschreibt.|50|ja|  
  
## <a name="see-also"></a>Siehe auch  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
