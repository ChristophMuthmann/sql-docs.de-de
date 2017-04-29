---
title: DML-Trigger | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- triggers [SQL Server], about triggers
- DML triggers, about DML triggers
- triggers [SQL Server]
ms.assetid: 298eafca-e01f-4707-8c29-c75546fcd6b0
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 49e88050bea0405d8801a5b53faafcb644a6b62d
ms.lasthandoff: 04/11/2017

---
# <a name="dml-triggers"></a>DML-Trigger
  Bei DML-Triggern handelt es sich um einen bestimmten Typ einer gespeicherten Prozedur, die automatisch wirksam wird, sobald ein DML-Ereignis (Data Manipulation Language, Datenbearbeitungssprache) ausgeführt wird, das sich auf die im Trigger definierte Tabelle oder Sicht auswirkt. DML-Ereignisse schließen die Anweisungen INSERT, UPDATE oder DELETE ein. DML-Trigger können zum Erzwingen von Geschäftsregeln und Datenintegrität, Abfragen anderer Tabellen und Einschließen komplexer [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen verwendet werden. Der Trigger und die auslösende Anweisung werden wie eine einzige Transaktion behandelt, für die aus dem Trigger heraus ein Rollback ausgeführt werden kann. Tritt ein schwerer Fehler auf (z B. bei unzureichendem Speicherplatz), wird für die gesamte Transaktion automatisch ein Rollback ausgeführt.  
  
## <a name="dml-trigger-benefits"></a>Vorteile von DML-Triggern  
 DML-Trigger ähneln Einschränkungen insofern, als sie die Entitätsintegrität oder Domänenintegrität erzwingen können. Im Allgemeinen sollte die Entitätsintegrität immer auf der untersten Ebene durch Indizes erzwungen werden, die Teil von PRIMARY KEY- und UNIQUE-Einschränkungen sind oder unabhängig von Einschränkungen erstellt wurden. Die Domänenintegrität sollte durch CHECK-Einschränkungen und referenzielle Integrität (RI) sollte durch FOREIGN KEY-Einschränkungen erzwungen werden. DML-Trigger sind dann am sinnvollsten, wenn die von Einschränkungen unterstützten Funktionen nicht die Funktionalitätsanforderungen der Anwendung erfüllen.  
  
 Die folgende Liste vergleicht DML-Trigger mit Einschränkungen und gibt an, wenn DML-Trigger Vorteile aufweisen.  
  
-   DML-Trigger können Änderungen über verknüpfte Tabellen in der Datenbank kaskadierend weitergeben. Diese Änderungen können jedoch mithilfe von kaskadierenden Einschränkungen der referenziellen Integrität effizienter ausgeführt werden. FOREIGN KEY-Einschränkungen können einen Spaltenwert nur anhand eines exakt übereinstimmenden Wertes in einer anderen Spalte überprüfen, außer die REFERENCES-Klausel definiert eine überlappende referenzielle Aktion.  
  
-   Sie können vor böswilligen oder falschen INSERT-, UPDATE- und DELETE-Operationen schützen und andere Einschränkungen erzwingen, die komplexer als die mit CHECK-Einschränkungen definierten sind.  
  
     Im Gegensatz zu CHECK-Einschränkungen können DML-Trigger auf Spalten in anderen Tabellen verweisen. So kann ein Trigger beispielsweise eine SELECT-Anweisung aus einer anderen Tabelle verwenden, um die eingefügten oder aktualisierten Daten zu vergleichen und weitere Aktionen auszuführen, wie z. B. Ändern der Daten oder Anzeigen einer benutzerdefinierten Fehlermeldung.  
  
-   Sie können den Status einer Tabelle vor und nach einer Datenänderung auswerten und, basierend auf den festgestellten Unterschieden, bestimmte Aktionen ausführen.  
  
-   Mehrere DML-Trigger desselben Typs (INSERT, UPDATE oder DELETE) für eine Tabelle ermöglichen es, dass als Reaktion auf dieselbe Änderungsanweisung unterschiedliche Aktionen durchgeführt werden.  
  
-   Einschränkungen können Fehlerinformationen nur mithilfe von standardisierten Systemfehlermeldungen weitergeben. Wenn die Anwendung benutzerdefinierte Meldungen erfordert und eine komplexere Fehlerbehandlung benötigt oder diese von Vorteil wären, müssen Sie einen Trigger verwenden.  
  
-   DML-Trigger können Änderungen nicht zulassen oder einen Rollback für Änderungen ausführen, die die referenzielle Integrität verletzen, und auf diese Weise den Versuch der Datenänderung abbrechen. Ein entsprechender Trigger kann wirksam werden, wenn Sie einen Fremdschlüssel ändern und der neue Wert nicht mit dem Primärschlüssel übereinstimmt. Zu diesem Zweck werden jedoch normalerweise FOREIGN KEY-Einschränkungen verwendet.  
  
-   Wenn für die Triggertabelle Einschränkungen vorhanden sind, werden sie nach der Ausführung des INSTEAD OF-Triggers, jedoch vor der Ausführung des AFTER-Triggers überprüft. Falls eine Verletzung der Einschränkungen vorliegt, wird für die Aktionen des INSTEAD OF-Triggers ein Rollback ausgeführt. Der AFTER-Trigger wird nicht ausgeführt.  
  
## <a name="types-of-dml-triggers"></a>DML-Triggertypen  
 AFTER-Trigger  
 AFTER-Trigger werden nach der INSERT-, UPDATE-, MERGE- oder DELETE-Anweisung ausgeführt. AFTER-Trigger werden niemals ausgeführt, wenn eine Einschränkungsverletzung auftritt; diese Trigger können somit nicht für Verarbeitungen verwendet werden, die Einschränkungsverletzungen verhindern. Bei jeder in der MERGE-Anweisung angegebenen INSERT-, UPDATE- oder ENTF-Aktion, wird für jeden DML-Vorgang der entsprechende Trigger ausgelöst.  
  
 INSTEAD OF-Trigger  
 INSTEAD OF-Trigger überschreiben die Standardaktionen der auslösenden Anweisung. Sie können daher zum Ausführen einer Fehler- oder Wertüberprüfung für eine oder mehrere Spalten sowie zum Ausführen zusätzlicher Aktionen vor dem Einfügen, Aktualisieren oder Löschen der Zeile bzw. Zeilen verwendet werden. Nehmen Sie z. B. an, der aktualisierte Wert in einer Spalte für Stundenlöhne in einer Gehaltstabelle überschreitet einen bestimmten Wert. Für diesen Fall kann ein Trigger definiert werden, der entweder eine Fehlermeldung erstellt und ein Rollback für die Transaktion ausführt oder einen neuen Datensatz in einen Überwachungspfad einfügt, bevor der Datensatz in die Gehaltstabelle eingefügt wird. Der wichtigste Vorteil von INSTEAD OF-Triggern ist, dass sie das Aktualisieren von Sichten ermöglichen, die normalerweise nicht aktualisiert werden könnten. Eine Sicht, die sich aus mehreren Basistabellen zusammensetzt, muss beispielsweise einen INSTEAD OF-Trigger verwenden, um INSERT-, UPDATE- und DELETE-Vorgänge zu unterstützen, die auf Daten in mehreren Tabellen verweisen. Ein weiterer Vorteil von INSTEAD OF-Triggern ist die Möglichkeit, Logik zu codieren, die Teile eines Batches zurückweist, während andere Teile zugelassen werden.  
  
 In der folgenden Tabelle werden die Funktionen von AFTER- und INSTEAD OF-Triggern verglichen.  
  
|Funktion|AFTER-Trigger|INSTEAD OF-Trigger|  
|--------------|-------------------|------------------------|  
|Anwendbarkeit|Tabellen|Tabellen und Sichten|  
|Anzahl pro Tabelle oder Sicht|Mehrere Trigger pro auslösende Aktion (INSERT, UPDATE oder DELETE)|Ein Trigger pro auslösende Aktion (INSERT, UPDATE oder DELETE)|  
|Kaskadierende Verweise|Keine Einschränkungen|INSTEAD OF UPDATE- und DELETE-Trigger sind nicht für Tabellen zulässig, die Ziel von kaskadierenden Einschränkungen für die referenzielle Integrität sind.|  
|Ausführung|Nachher:<br /><br /> Einschränkungsverarbeitung<br /><br /> Deklarativen referenziellen Aktionen<br /><br /> Erstellung der**inserted** - und **deleted** -Tabellen<br /><br /> Der auslösenden Aktion|Vorher: Einschränkungsverarbeitung<br /><br /> Anstelle: Der auslösenden Aktion<br /><br /> Nach: Erstellung der  **inserted** - und **deleted** -Tabellen|  
|Ausführungsreihenfolge|Der zuerst und zuletzt auszuführende Trigger kann angegeben werden.|Nicht zutreffend|  
|**varchar(max)**-, **nvarchar(max)**-, und **varbinary(max)** -Spaltenverweise in **eingefügten** und **gelöschten** Tabellen|Zulässig|Zulässig|  
|Verweise auf**text**, **ntext**- und **image** -Spalten in **inserted** - und **deleted** -Tabellen|Nicht zulässig|Zulässig|  
  
 CLR-Trigger  
 Ein CLR-Trigger kann ein AFTER- oder ein INSTEAD OF-Trigger sein. Bei einem CLR-Trigger kann es sich auch um einen DDL-Trigger handeln. Anstatt eine gespeicherte [!INCLUDE[tsql](../../includes/tsql-md.md)] -Prozedur auszuführen, führt ein CLR-Trigger eine oder mehrere Methoden aus, die in verwaltetem Code geschrieben wurden und Elemente einer Assembly sind, die in .NET Framework erstellt und in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hochgeladen werden.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Task|Thema|  
|----------|-----------|  
|Beschreibt, wie ein DML-Trigger erstellt wird.|[Erstellen von DML-Triggern](../../relational-databases/triggers/create-dml-triggers.md)|  
|Beschreibt, wie ein CLR-Trigger erstellt wird.|[Erstellen von CLR-Triggern](../../relational-databases/triggers/create-clr-triggers.md)|  
|Beschreibt, wie ein DML-Trigger zum Verarbeiten von einzeiligen und mehrzeiligen Datenänderungen erstellt wird.|[Erstellen von DML-Triggern für die Verarbeitung mehrerer Datenzeilen](../../relational-databases/triggers/create-dml-triggers-to-handle-multiple-rows-of-data.md)|  
|Beschreibt, wie Trigger geschachtelt werden.|[Erstellen von geschachtelten Triggern](../../relational-databases/triggers/create-nested-triggers.md)|  
|Beschreibt, wie die Reihenfolge der Auslösung von AFTER-Triggern angegeben wird.|[Angeben des ersten und des letzten Triggers](../../relational-databases/triggers/specify-first-and-last-triggers.md)|  
|Beschreibt, wie die speziellen INSERT- und DELETE-Tabellen im Triggercode verwendet werden.|[Verwenden der Tabellen inserted und deleted](../../relational-databases/triggers/use-the-inserted-and-deleted-tables.md)|  
|Beschreibt, wie ein DML-Trigger geändert oder umbenannt wird.|[Ändern oder Umbenennen von DML-Triggern](../../relational-databases/triggers/modify-or-rename-dml-triggers.md)|  
|Beschreibt, wie Informationen zu DML-Triggern angezeigt werden.|[Abrufen von Informationen zu DML-Triggern](../../relational-databases/triggers/get-information-about-dml-triggers.md)|  
|Beschreibt, wie DML-Trigger gelöscht oder deaktiviert werden.|[Löschen oder Deaktivieren von DML-Triggern](../../relational-databases/triggers/delete-or-disable-dml-triggers.md)|  
|Beschreibt, wie Triggersicherheit verwaltet wird.|[Verwalten der Triggersicherheit](../../relational-databases/triggers/manage-trigger-security.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [Triggerfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/trigger-functions-transact-sql.md)  
  
  
