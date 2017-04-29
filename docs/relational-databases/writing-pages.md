---
title: Schreiben von Seiten | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pages
ms.assetid: 409c8753-03c4-436d-839c-6a5879971551
caps.latest.revision: 2
author: pmasl
ms.author: pelopes
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8f8e6bff396499886a23182787d84a84e6ceaf17
ms.lasthandoff: 04/11/2017

---
# <a name="writing-pages"></a>Schreiben von Seiten
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

Die E/A-Aktivitäten von einer Instanz von [!INCLUDE[ssDE](../includes/ssde-md.md)] schließen logische und physische Schreibvorgänge ein. Ein logischer Schreibvorgang findet statt, wenn Daten auf einer Seite im Puffercache geändert werden. Ein physischer Schreibvorgang findet statt, wenn die Seite vom [Puffercache](../relational-databases/memory-management-architecture-guide.md) auf den Datenträger geschrieben wird.

Eine Seite, die im Puffercache geändert wurde, wird nicht sofort auf den Datenträger geschrieben, sondern als geändert markiert. Dies bedeutet, dass es möglich ist, dass auf einer Seite mehrere logische Schreibvorgänge ausgeführt werden, bevor sie physisch auf den Datenträger geschrieben wird. Für jeden logischen Schreibvorgang wird ein Transaktionsprotokoll-Datensatz in den Protokollcache geschrieben, der die Änderung aufzeichnet. Die Protokolldatensätze müssen auf den Datenträger geschrieben werden, bevor die zugehörige modifizierte Seite aus dem Puffercache entfernt und auf den Datenträger geschrieben wird. SQL Server verwendet eine als Write-Ahead-Protokollierung bekannte Technik, die das Schreiben einer modifizierten Seite verhindert, ehe der zugehörige Protokolldatensatz auf den Datenträger geschrieben wird. Dies ist von entscheidender Bedeutung für eine ordnungsgemäße Ausführung des Wiederherstellungs-Managers. Weitere Informationen finden Sie unter [Write-Ahead-Transaktionsprotokoll](../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md).

Die folgende Abbildung zeigt den Schreibvorgang für eine modifizierte Datenseite.

![Writing_Pages](../relational-databases/media/writing-pages.gif)

Während des Schreibvorgangs einer Seite durch den Puffer-Manager wird nach angrenzenden modifizierten Seiten gesucht, die in einen einzigen Gather-Write-Vorgang einbezogen werden können. Angrenzende Seiten haben aufeinanderfolgende Seiten-IDs und stammen von derselben Datei; sie befinden sich nicht unbedingt im Speicher nebeneinander. Die Suche wird in beide Richtungen fortgesetzt, bis eines der folgenden Ereignisse eintritt:

 * Eine nicht modifizierte Seite wurde gefunden.
 * 32 Seiten wurden gefunden.
 * Eine modifizierte ("dirty") Seite wird gefunden, deren Protokollfolgenummer (LSN, Log Sequence Number) noch nicht im Protokoll geleert wurde.
 * Eine Seite wird gefunden, für die nicht sofort ein Latchtyp zugeordnet werden kann.

Auf diese Weise kann die gesamte Gruppe der Seiten in einem einzigen Gather-Write-Vorgang auf den Datenträger geschrieben werden. 

Unmittelbar bevor eine Seite geschrieben wird, wird der Seite die in der Datenbank angegebene Seitenschutzform hinzugefügt. Wenn Schutz vor zerrissenen Seiten hinzugefügt wird, muss der Latch der Seite vom Typ „EX“ (für EXklusiv) für die E/A-Vorgänge sein. Der Grund hierfür ist, dass die Seite durch den Schutz vor zerrissenen Seiten geändert wird, sodass sie von keinem anderen Thread gelesen werden kann. Wenn ein Seitenschutz vom Typ "Prüfsumme" hinzugefügt wird oder die Datenbank keinen Seitenschutz verwendet, muss der Latch der Seite vom Typ UP (für UPdate) für die E/A-Vorgänge sein. Dieser Latch verhindert, dass die Seite während des Schreibvorgangs geändert wird, und lässt dennoch das Lesen der Seite zu. Weitere Informationen zu Seitenschutzoptionen für Datenträger-E/A-Vorgänge finden Sie unter [Pufferverwaltung](../relational-databases/memory-management-architecture-guide.md).

Für das Schreiben einer modifizierten („dirty“) Seite auf den Datenträger gibt es drei Möglichkeiten: 

* Verzögertes Schreiben   
 Das verzögerte Schreiben (lazy writing) ist ein Systemprozess, bei dem freie Puffer verfügbar gehalten werden, indem selten verwendete Seiten aus dem Puffercache entfernt werden. Modifizierte Seiten werden zuerst auf den Datenträger geschrieben. 

* Eager-Writing   
 Bei Eager-Writing handelt es sich um einen Prozess, mit dem modifizierte Datenseiten mit nicht protokollierten Vorgängen wie BULK INSERT oder SELECT INTO geschrieben werden. Dieser Prozess ermöglicht das parallele Erstellen und Schreiben neuer Seiten. Dies bedeutet, dass die aufrufende Operation nicht warten muss, bis der gesamte Vorgang abgeschlossen ist, um die Seiten auf den Datenträger zu schreiben.

* Prüfpunkt   
 Mit dem Prüfpunktprozess (checkpoint) wird der Puffercache regelmäßig auf Puffer mit Seiten aus einer angegebenen Datenbank überprüft, und alle modifizierten Seiten werden auf den Datenträger geschrieben. Durch Prüfpunkte kann bei einer späteren Wiederherstellung Zeit eingespart werden, da ein Punkt erstellt wird, an dem auf jeden Fall alle modifizierten Seiten auf den Datenträger geschrieben worden sind. Der Benutzer kann mithilfe des CHECKPOINT-Befehls eine Prüfpunktoperation anfordern. Prüfpunkte können jedoch auch automatisch durch das [!INCLUDE[ssDE](../includes/ssde-md.md)] generiert werden – auf der Grundlage des bereits verbrauchten Protokollspeicherplatzes und der seit dem letzten Prüfpunkt verstrichenen Zeit. Zusätzlich werden Prüfpunkte generiert, wenn bestimmte Aktivitäten durchgeführt werden, Beispiel: Wenn einer Datenbank eine Datendatei oder eine Protokolldatei hinzugefügt wird bzw. daraus entfernt wird oder wenn die SQL Server-Instanz beendet wird. Weitere Informationen finden Sie unter [Prüfpunkte und der aktive Teil des Protokolls](../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md).

Die oben beschriebenen Prozesse, Verzögertes Schreiben, Eager-Writing und Prüfpunkt, warten nicht, bis die E/A-Operation abgeschlossen ist. Sie verwenden immer asynchrone (oder überlappte) E/As, setzen ihre Tätigkeit fort und überprüfen die ordnungsgemäße Ausführung der E/A-Operationen zu einem späteren Zeitpunkt. Dies ermöglicht SQL Server, sowohl die Ressourcen der CPU als auch der E/As für die entsprechenden Tasks zu maximieren.

## <a name="see-also"></a>Siehe auch
[Handbuch zur Architektur von Seiten und Blöcken](../relational-databases/pages-and-extents-architecture-guide.md)   
 [Lesen von Seiten](../relational-databases/reading-pages.md)
