---
title: "Showplan Text (Ereignisklasse) | Microsoft Docs"
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
  - "Showplan Text-Ereignisklasse"
ms.assetid: f36c73b2-a1d1-4513-9594-78818f3fcb0d
caps.latest.revision: 37
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 37
---
# Showplan Text (Ereignisklasse)
  Die Showplan Text-Ereignisklasse tritt auf, wenn [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine SQL-Anweisung ausführt. Bei den eingeschlossenen Informationen handelt es sich um eine Teilmenge der Informationen, die in den Ereignisklassen „Showplan All“, „Showplan XML Statistics Profile“ oder „Showplan XML“ verfügbar sind.  
  
 Wenn die Showplan Text-Ereignisklasse in eine Ablaufverfolgung aufgenommen wird, beeinträchtigt der Verarbeitungsaufwand die Leistung erheblich. Um diesen zu minimieren, sollten Sie die Verwendung dieser Ereignisklasse auf Ablaufverfolgungen beschränken, die bestimmte Probleme für kurze Zeiträume überwachen. Showplan Text verursacht weniger Verarbeitungsaufwand als andere Showplan-Ereignisklassen.  
  
 Wenn die Showplan Text-Ereignisklasse in eine Ablaufverfolgung aufgenommen wird, muss die BinaryData-Datenspalte ausgewählt sein. Ist dies nicht der Fall, werden Informationen zu dieser Ereignisklasse nicht in der Ablaufverfolgung angezeigt.  
  
## Datenspalten der Showplan Text-Ereignisklasse  
  
|Datenspaltenname|Datentyp|Beschreibung|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|10|Ja|  
|BinaryData|**image**|Geschätzte Kosten des Showplan-Texts.|2|Nein|  
|ClientProcessID|**int**|Die ID, die der Hostcomputer dem Prozess zuweist, in dem die Clientanwendung ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn die Clientprozess-ID durch den Client bereitgestellt wird.|9|ja|  
|DatabaseID|**int**|Die ID der Datenbank, die durch die USE *database* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *database* -Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die ServerName-Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|Ja|  
|DatabaseName|**nvarchar**|Name der Datenbank, in der die Benutzeranweisung ausgeführt wird.|35|Ja|  
|Ereignisklasse|**int**|Ereignistyp = 96.|27|Nein|  
|EventSequence|**int**|Sequenz eines bestimmten Ereignisses innerhalb der Anforderung.|51|Nein|  
|HostName|**nvarchar**|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname durch den Client bereitgestellt wird. Der Hostname kann mithilfe der HOST_NAME-Funktion bestimmt werden.|8|Ja|  
|Ganzzahlige Daten|**integer**|Geschätzte Anzahl der zurückgegebenen Zeilen.|25|ja|  
|IsSystem|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, 0 = Benutzer.|60|ja|  
|LineNumber|**int**|Zeigt die Nummer der Zeile an, die den Fehler enthält|5|ja|  
|LoginSID|**Bitmap**|Sicherheits-ID (SID) des angemeldeten Benutzers. Diese Informationen finden Sie in der sys.server_principals-Katalogsicht. Die SID ist für jede Anmeldung beim Server eindeutig.|41|Nein|  
|LoginName|**nvarchar**|Der Anmeldename des Benutzers ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sicherheitsanmeldung oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmeldeinformationen im Format DOMAIN\username).|11|ja|  
|NestLevel|**int**|Ganze Zahl, die die von @@NESTLEVEL zurückgegebenen Daten darstellt.|29|ja|  
|NTDomainName|**nvarchar**|Windows-Domäne, zu der der Benutzer gehört.|7|ja|  
|ObjectID|**int**|Vom System zugewiesene ID des Objekts.|22|ja|  
|ObjectName|**nvarchar**|Name des Objekts, auf das verwiesen wird|34|Ja|  
|ObjectType|**int**|Der Wert, der den Typ des am Ereignis beteiligten Objekts darstellt. Dieser Wert entspricht der type-Spalte in sys.objects. Weitere Werte finden Sie unter [ObjectType (Spalte für Ablaufverfolgungsereignisse)](../../relational-databases/event-classes/objecttype-trace-event-column.md).|28|ja|  
|RequestID|**int**|Die Anforderungs-ID, von der die Volltextabfrage initiiert wurde.|49|Ja|  
|ServerName|**nvarchar**|Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, für die eine Ablaufverfolgung ausgeführt wird.|26|Nein|  
|SessionLoginName|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie beispielsweise mithilfe von Login1 eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und eine Anweisung als Login2 ausführen, zeigt SessionLoginName den Wert Login1 an und LoginName den Wert Login2. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]- als auch den Windows-Anmeldenamen an.|64|Ja|  
|SPID|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|StartTime|**datetime**|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|Ja|  
|TransactionID|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|Ja|  
|XactSequence|**bigint**|Token zur Beschreibung der aktuellen Transaktion.|50|ja|  
  
## Siehe auch  
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Referenz zu logischen und physischen Showplanoperatoren](../../relational-databases/showplan-logical-and-physical-operators-reference.md)   
 [Showplan All (Ereignisklasse)](../../relational-databases/event-classes/showplan-all-event-class.md)   
 [Showplan XML Statistics Profile-Ereignisklasse](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md)   
 [Showplan XML (Ereignisklasse)](../../relational-databases/event-classes/showplan-xml-event-class.md)  
  
  