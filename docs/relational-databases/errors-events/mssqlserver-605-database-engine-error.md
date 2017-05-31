---
title: MSSQLSERVER_605 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 605 (Database Engine error)
ms.assetid: d8d3a22e-1ff8-48a4-891f-4c8619437e24
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9dcd61e41bb08478ed3f2cf040ffe65a02447665
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver605"></a>MSSQLSERVER_605
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|605|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|WRONGPAGE|  
|Meldungstext|Fehler beim Abrufen der logischen Seite %S_PGID in der %d-Datenbank, die nicht zur Zuordnungseinheit %I64d, sondern zu %I64d gehört.|  
  
## <a name="explanation"></a>Erklärung  
Dieser Fehler gibt im Allgemeinen eine Seiten- oder Zuordnungsbeschädigung in der angegebenen Datenbank an. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden Beschädigungen erkannt, wenn Seiten gelesen werden. Zu diesem Zweck werden entweder Seitenverknüpfungen verfolgt oder IAM (Index Allocation Map) verwendet. Alle Seiten, die einer Tabelle zugeordnet sind, müssen zu einer der Zuordnungseinheiten gehören, die der Tabelle zugeordnet sind. Wenn die im Seitenkopf enthaltene Zuordnungseinheits-ID nicht mit einer zur Tabelle gehörenden Zuordnungseinheits-ID übereinstimmt, wird diese Ausnahme ausgelöst. Die erste in der Fehlermeldung aufgeführte Zuordnungseinheits-ID entspricht der im Seitenkopf vorhandenen ID, der zweite Zuordnungseinheitswert entspricht der der Tabelle zugeordneten ID.  
  
**Datenbeschädigungsfehler**  
  
Mit dem Schweregrad 21 wird eine potenzielle Datenbeschädigung angegeben. Zu den möglichen Ursachen zählen eine beschädigte Seitenkette, eine fehlerhafte IAM und ein ungültiger Eintrag in der [sys.objects](~/relational-databases/system-catalog-views/sys-objects-transact-sql.md)-Katalogsicht für dieses Objekt. Diese Fehler werden häufig durch Hardwarefehler oder Festplatten-Gerätetreiberfehler verursacht.  
  
**Vorübergehende Fehler**  
  
Mit dem Schweregrad 12 wird ein potenzieller vorübergehender Fehler angegeben, das heißt, der Fehler tritt im Cache auf und deutet nicht auf eine Beschädigung von Daten auf dem Datenträger hin. Vorübergehende 605-Fehler können durch folgende Bedingungen verursacht werden:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird vorzeitig vom Betriebssystem benachrichtigt, dass ein E/A-Vorgang abgeschlossen wurde; die Fehlermeldung wird angezeigt, obwohl keine tatsächliche Datenbeschädigung vorliegt.  
  
Durch das Ausführen einer Abfrage mit dem Optimiererhinweis NOLOCK oder durch das Festlegen der Isolationsstufe für Transaktionen auf READ UNCOMMITTED. Wenn eine Abfrage mit NOLOCK oder READ UNCOMMITTED versucht, Daten zu lesen, die von einem anderen Benutzer verschoben oder geändert werden, tritt der Fehler 605 auf. Wenn Sie sicherstellen möchten, dass es sich um einen vorübergehenden 605-Fehler handelt, führen Sie die Abfrage später erneut aus. Weitere Informationen finden Sie in diesem KB-Artikel [235880](http://support.microsoft.com/kb/235880/en-us): „Fehlermeldung „Fehler 605“ beim Ausführen einer Abfrage mit dem NOLOCK-Optimiererhinweis oder Festlegen der Isolationsstufe für Transaktionen auf READ UNCOMMITTED in SQL Server“.  
  
Im Allgemeinen war der Fehler 605 wahrscheinlich vorübergehend, wenn der Fehler während des Datenzugriffs auftritt, nachfolgende DBCC CHECKDB-Vorgänge jedoch ohne Fehler abgeschlossen werden.  
  
## <a name="user-action"></a>Benutzeraktion  
Wenn der Fehler 605 nicht vorübergehend auftritt, ist das Problem schwerwiegend und muss behoben werden, indem folgende Aufgaben ausgeführt werden:  
  
1.  Geben Sie die Tabellen an, die den in der Meldung angegebenen Zuordnungseinheiten angehören, indem Sie folgende Abfrage ausführen. Ersetzen Sie `allocation_unit_id` durch die in der Fehlermeldung angegebenen Zuordnungseinheiten.  
  
    USE`database_name`;  
  
    GO  
  
    SELECT au.allocation_unit_id, OBJECT_NAME(p.object_id) AS table_name, fg.name AS filegroup_name,  
  
    au.type_desc AS allocation_type, au.data_pages, partition_number  
  
    FROM sys.allocation_units AS au  
  
    JOIN sys.partitions AS p ON au.container_id = p.partition_id  
  
    JOIN sys.filegroups AS fg ON fg.data_space_id = au.data_space_id  
  
    WHERE au.allocation_unit_id = `allocation_unit_id` OR au.allocation_unit_id = `allocation_unit_id`  
  
    ORDER BY au.allocation_unit_id;  
  
    GO  
  
2.  Führen Sie DBCC CHECKTABLE ohne REPAIR-Klausel für die Tabelle aus, die zur zweiten in der Fehlermeldung angegebenen Zuordnungseinheits-ID gehört.  
  
3.  Führen Sie DBCC CHECKDB ohne REPAIR-Klausel so schnell wie möglich aus, um das vollständige Ausmaß der Beschädigung in der gesamten Datenbank zu bestimmen.  
  
4.  Sehen Sie im Fehlerprotokoll nach Fehlern, die häufig in Kombination mit dem Fehler 605 auftreten, und prüfen Sie das Windows-Ereignisprotokoll auf system- bzw. hardwarebedingte Probleme. Beheben Sie alle hardwarebedingten Probleme, die in den Protokollen enthalten sind.  
  
Wenn das Problem nicht hardwarebedingt ist, führen Sie eine der folgenden Aufgaben aus:  
  
1.  Stellen Sie die Datenbank von einer bekanntermaßen fehlerfreien Sicherung wieder her. Sie können die Sicherungsfunktion der Seitenwiederherstellung verwenden, um nur die beschädigten Seiten wiederherzustellen.  
  
2.  Führen Sie DBCC CHECKDB mit der REPAIR-Klausel aus, die im DBCC CHECKDB-Vorgang empfohlen wurde, der in Schritt 2 zum Beheben der Beschädigung ausgeführt wurde. Wenn DBCC CHECKDB mit einer der REPAIR-Klauseln ausgeführt wird und das Problem nicht behebt, wenden Sie sich an Ihren primären Unterstützungsanbieter. Halten Sie die Ausgabe von DBCC CHECKDB zur Überprüfung bereit.  
  
    > [!CAUTION]  
    > Wenden Sie sich an Ihren primären Unterstützungsanbieter, bevor Sie diese Anweisung ausführen, wenn Sie nicht sicher sind, inwiefern sich die Verwendung von DBCC CHECKDB mit einer REPAIR-Klausel auf Ihre Daten auswirkt.  
  
## <a name="see-also"></a>Siehe auch  
[DBCC CHECKTABLE &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checktable-transact-sql.md)  
  

