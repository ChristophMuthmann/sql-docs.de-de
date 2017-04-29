---
title: "SORT_IN_TEMPDB-Option für Indizes | Microsoft-Dokumentation"
ms.custom: 
ms.date: 04/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SORT_IN_TEMPDB option
- disk space [SQL Server], indexes
- space [SQL Server], indexes
- tempdb database [SQL Server], indexes
- indexes [SQL Server], tempdb database
- index creation [SQL Server], tempdb database
ms.assetid: 754a003f-fe51-4d10-975a-f6b8c04ebd35
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1fa7ac1cb00252f855ba71b39fbccbe901365b00
ms.lasthandoff: 04/11/2017

---
# <a name="sortintempdb-option-for-indexes"></a>SORT_IN_TEMPDB-Option für Indizes
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Wenn Sie einen Index erstellen oder neu erstellen, indem Sie die SORT_IN_TEMPDB-Option auf ON setzen, wird [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] angewiesen, zum Speichern der Zwischenergebnisse der Sortierung für die Erstellung eines Indexes **tempdb** zu verwenden. Obwohl durch diese Option die Menge an Speicherplatz erhöht wird, die zur Indexerstellung verwendet wird, kann dadurch die Zeit verringert werden, die zum Erstellen eines Indexes erforderlich ist, wenn **tempdb** auf einer anderen Gruppe von Datenträgern gespeichert ist als die Benutzerdatenbank. Weitere Informationen zu **tempdb**finden Sie unter [Configure the index create memory Server Configuration Option](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md).  
  
## <a name="phases-of-index-building"></a>Phasen der Indexerstellung  
 Wenn [!INCLUDE[ssDE](../../includes/ssde-md.md)] einen Index erstellt, werden die folgenden Phasen durchlaufen:  
  
-   Zunächst scannt [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Datenseiten, um Schlüsselwerte abzurufen, und erstellt eine Indexzeile auf Blattebene für jede Datenzeile. Wenn die internen Puffer der Sortierung mit Indexeinträgen auf Blattebene aufgefüllt wurden, werden die Einträge sortiert und als Zwischensortierlauf auf den Datenträger geschrieben. Dann setzt [!INCLUDE[ssDE](../../includes/ssde-md.md)] den Scanvorgang der Datenseiten fort, bis die Puffer der Sortierung erneut aufgefüllt sind. Dieses Muster des Scannens mehrerer Datenseiten, gefolgt vom Sortieren und Schreiben eines Sortierlaufs, wird so lange fortgesetzt, bis alle Zeilen der Basistabelle verarbeitet worden sind.  
  
     Bei einem gruppierten Index handelt es sich bei den Blattzeilen des Indexes um die Datenzeilen der Tabelle, sodass die Zwischensortierläufe alle Datenzeilen enthalten. In einem nicht gruppierten Index können die Blattzeilen Nichtschlüsselspalten enthalten, daher sind sie jedoch in der Regel kleiner als bei einem gruppierten Index. Ein nicht gruppierter Sortierlauf kann jedoch umfangreich sein, wenn die Indexschlüssel groß sind oder wenn mehrere Nichtschlüsselspalten in den Index einbezogen sind. Weitere Informationen zum Einbeziehen von Nichtschlüsselspalten finden Sie unter [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] führt die sortierten Läufe der Indexzeilen auf Blattebene in einem einzelnen, sortierten Strom zusammen. Die Komponente von [!INCLUDE[ssDE](../../includes/ssde-md.md)] für das Zusammenführen der Sortierung beginnt mit der ersten Seite jedes Sortierlaufs, sucht nach dem niedrigsten Schlüssel in allen Seiten und gibt die Blattzeile an die Indexerstellungskomponente weiter. Danach wird der nächste niedrigste Schlüssel verarbeitet, dann der darauf folgende usw. Wenn die letzte Indexzeile auf Blattebene aus einer Sortierlaufseite extrahiert wurde, wechselt der Prozess zur nächsten Seite dieses Sortierlaufs. Wenn alle Seiten in einem Sortierlaufblock verarbeitet worden sind, wird der Block freigegeben. Bei der Übergabe jeder Blattindexzeile an die Indexerstellungskomponente wird diese Zeile in einer Blattindexseite im Puffer eingeschlossen. In jede Blattseite wird geschrieben, wenn sie aufgefüllt wird. Während des Beschreibens von Blattseiten erstellt [!INCLUDE[ssDE](../../includes/ssde-md.md)] außerdem die oberen Ebenen des Indexes. In jede Indexseite einer oberen Ebene wird geschrieben, wenn sie aufgefüllt wird.  
  
## <a name="sortintempdb-option"></a>SORT_IN_TEMPDB-Option  
 Wenn die SORT_IN_TEMPDB-Option auf OFF gesetzt ist (Standardeinstellung), werden die Sortierläufe in der Zieldateigruppe gespeichert. Während der ersten Phase der Indexerstellung werden durch die sich abwechselnden Lesevorgänge in den Basistabellenseiten und den Schreibvorgängen der Sortierläufe die Schreib-/Leseköpfe des Datenträgers von einem Bereich des Datenträgers in einen anderen Bereich verschoben. Die Köpfe befinden sich in dem Bereich der Datenseiten, während die Datenseiten gescannt werden. Sie werden in einen Bereich mit freiem Speicherplatz verschoben, wenn die Sortierpuffer aufgefüllt werden und der aktuelle Sortierlauf auf den Datenträger geschrieben werden muss. Anschließend werden sie wieder in den Bereich der Datenseiten verschoben, wenn der Seitenscanvorgang in der Tabelle fortgesetzt wird. Das Verschieben der Schreib-/Leseköpfe nimmt in der zweiten Phase zu. Zu dieser Zeit wechselt der Sortierprozess in der Regel die Lesevorgänge in jedem Sortierlaufbereich. Sowohl die Sortierläufe als auch die neuen Indexseiten werden in der Zieldateigruppe erstellt. Dies bedeutet, dass zur gleichen Zeit, wenn das [!INCLUDE[ssDE](../../includes/ssde-md.md)] Lesevorgänge auf die Sortierläufe verteilt, ein regelmäßiges Springen zu den Indexblöcken erforderlich ist, um neue Indexseiten zu schreiben, während sie aufgefüllt werden.  
  
 Falls die Option SORT_IN_TEMPDB auf ON festgelegt ist und **tempdb** auf einer anderen Datenträgergruppe als der Zieldateigruppe gespeichert ist, finden die Lesevorgänge der Datenseiten während der ersten Phase auf einem anderen Datenträger statt als die Schreibvorgänge in den Bereich der Sortierarbeit in **tempdb**. Dies bedeutet, dass die Lesevorgänge der Datenschlüssel auf dem Datenträger eher seriell auf dem Datenträger verlaufen und dass die Schreibvorgänge auf dem Datenträger mit **tempdb** ebenfalls seriell sind, genauso wie die Schreibvorgänge zum Erstellen des endgültigen Indexes. Auch wenn andere Benutzer die Datenbank verwenden und auf unterschiedliche Datenträgeradressen zugreifen, ist die Gesamtstruktur der Lese- und Schreibvorgänge viel effizienter, wenn die Option SORT_IN_TEMPDB angegeben ist.  
  
 Mithilfe der Option SORT_IN_TEMPDB stehen die Indexblöcke möglicherweise näher zusammen, besonders wenn der CREATE INDEX-Vorgang nicht parallel ausgeführt wird. Die Blöcke im Bereich der Sortierarbeit werden im Hinblick auf ihren Speicherort in der Datenbank eher nach dem Zufallsprinzip freigegeben. Wenn die Bereiche der Sortierarbeit in der Zieldateigruppe enthalten sind, können sie bei der Freigabe der Blöcke der Sortierarbeit durch Anforderungen von Blöcken reserviert werden, in denen die Indexstruktur während ihrer Erstellung gespeichert werden soll. Dabei können die Speicherorte der Indexblöcke bis zu einem gewissen Grad zufällig ausgewählt werden. Wenn die Sortierblöcke separat in **tempdb**gespeichert werden, steht die Abfolge, in der sie freigegeben werden, in keinem Zusammenhang mit dem Speicherort der Indexblöcke. Wenn darüber hinaus die Zwischensortierläufe in **tempdb** anstelle der Zieldateigruppe gespeichert werden, steht mehr Speicherplatz in der Zieldateigruppe zur Verfügung, Dadurch werden die Möglichkeiten verbessert, dass die Indexblöcke zusammenhängend sind.  
  
 Die Option SORT_IN_TEMPDB wirkt sich nur auf die aktuelle Anweisung aus. Ob der Index in **tempdb**sortiert wurde, wird nicht in Metadaten aufgezeichnet. Wenn Sie z. B. einen nicht gruppierten Index mithilfe der Option SORT_IN_TEMPDB und später einen gruppierten Index ohne Angabe dieser Option erstellen, verwendet [!INCLUDE[ssDE](../../includes/ssde-md.md)] diese Option nicht, wenn es den nicht gruppierten Index neu erstellt.  
  
> [!NOTE]  
>  Wenn kein Sortiervorgang erforderlich ist oder die Sortierung im Arbeitsspeicher erfolgen kann, wird die Option SORT_IN_TEMPDB ignoriert.  
  
## <a name="disk-space-requirements"></a>Anforderungen an den Datenträgerspeicher  
 Wenn Sie die Option SORT_IN_TEMPDB auf ON setzen, muss in **tempdb** genügend freier Speicherplatz zum Speichern der Zwischensortierläufe zur Verfügung stehen, und es muss in der Zieldateigruppe genügend Speicherplatz verfügbar sein, damit der neue Index gespeichert werden kann. Die CREATE INDEX-Anweisung erzeugt einen Fehler, wenn nicht genügend freier Speicherplatz zur Verfügung steht und es eine Ursache dafür gibt, dass die Datenbanken keine automatische Vergrößerung durchführen können, um mehr Speicherplatz zu reservieren (wenn z. B. kein Datenträgerspeicher verfügbar ist oder die automatische Vergrößerung ausgeschaltet ist).  
  
 Falls SORT_IN_TEMPDB auf OFF gesetzt ist, muss der verfügbare Speicherplatz in der Zieldateigruppe ungefähr der Größe des endgültigen Indexes entsprechen. Während der ersten Phase werden die Sortierläufe erstellt, sie benötigen ungefähr gleich viel Speicherplatz wie der endgültige Index. Während der zweiten Phase wird jeder Block mit Sortierläufen freigegeben, nachdem er verarbeitet worden ist. Die Blöcke mit Sortierläufen werden demnach ungefähr genauso häufig freigegeben, wie Blöcke zum Speichern der Seiten des endgültigen Indexes reserviert werden, sodass die gesamten Speicherplatzanforderungen nicht bedeutend über der Größe des endgültigen Indexes liegen. Als Nebeneffekt hiervon tendiert [!INCLUDE[ssDE](../../includes/ssde-md.md)] dazu, die Blöcke mit Sortierläufen sehr schnell nach ihrer Freigabe wieder zu verwenden, wenn die Menge an verfügbarem Speicherplatz ungefähr der Größe des endgültigen Indexes entspricht. Da die Blöcke mit Sortierläufen eher nach dem Zufallsprinzip freigegeben werden, wird dadurch die Kontinuität der Indexblöcke in dieser Szenario verringert. Wenn SORT_IN_TEMPDB auf OFF gesetzt ist, wird die Kontinuität der Indexblöcke verbessert, wenn ausreichend freier Speicherplatz in der Zieldateigruppe verfügbar ist, sodass für die Indexblöcke ein zusammenhängender Pool anstatt der Blöcke, deren Zuordnung soeben aufgehoben wurde, mit Sortierläufen zugeordnet werden können.  
  
 Wenn Sie einen nicht gruppierten Index erstellen, muss die folgende Menge an Speicherplatz zur Verfügung stehen:  
  
-   Falls SORT_IN_TEMPDB auf ON gesetzt ist, muss in **tempdb** ausreichend freier Speicherplatz zur Verfügung stehen, um die Sortierläufe zu speichern, und es muss ausreichend freier Speicherplatz in der Zieldateigruppe vorhanden sein, um die endgültige Indexstruktur zu speichern. Die Sortierläufe enthalten die Blattzeilen des Indexes.  
  
-   Falls SORT_IN_TEMPDB auf OFF gesetzt ist, muss genügend freier Speicherplatz für das Speichern der endgültigen Indexstruktur in der Zieldateigruppe verfügbar sein. Die Kontinuität der Indexblöcke kann verbessert werden, wenn mehr freier Speicherplatz zur Verfügung steht.  
  
 Wenn Sie einen gruppierten Index für eine Tabelle erstellen, die über keine nicht gruppierten Indizes verfügen, muss die folgende Menge an Speicherplatz zur Verfügung stehen:  
  
-   Wenn SORT_IN_TEMPDB auf ON gesetzt ist, muss in **tempdb** ausreichend freier Speicherplatz zur Verfügung stehen, um die Sortierläufe zu speichern. Diese schließen die Datenzeilen der Tabelle ein. Es muss ausreichend freier Speicherplatz in der Zieldateigruppe vorhanden sein, um die endgültige Indexstruktur zu speichern. Dies schließt die Datenzeilen der Tabelle und des B-Baumes des Indexes ein. Sie müssen evtl. die Schätzung für Faktoren wie eine große Schlüsselgröße oder ein Füllfaktor mit einem niedrigen Wert entsprechend anpassen.  
  
-   Falls SORT_IN_TEMPDB auf OFF gesetzt ist, muss genügend freier Speicherplatz für das Speichern der endgültigen Tabelle in der Zieldateigruppe verfügbar sein. Dies schließt die Indexstruktur ein. Die Kontinuität der Tabelle und Indexblöcke kann verbessert werden, wenn mehr freier Speicherplatz zur Verfügung steht.  
  
 Wenn Sie einen gruppierten Index für eine Tabelle erstellen, die über nicht gruppierten Indizes verfügen, muss die folgende Menge an Speicherplatz zur Verfügung stehen:  
  
-   Falls SORT_IN_TEMPDB auf ON gesetzt ist, muss in **tempdb** ausreichend freier Speicherplatz zur Verfügung stehen, um die Auflistung von Sortierläufen für den größten Index (üblicherweise der gruppierte Index) zu speichern, und es muss ausreichend freier Speicherplatz in der Zieldateigruppe vorhanden sein, um die endgültigen Strukturen aller Indizes zu speichern. Das schließt den gruppierten Index ein, der die Datenzeilen der Tabelle enthält.  
  
-   Falls SORT_IN_TEMPDB auf OFF gesetzt ist, muss genügend freier Speicherplatz für das Speichern der endgültigen Tabelle in der Zieldateigruppe verfügbar sein. Das schließt die Strukturen aller Indizes ein. Die Kontinuität der Tabelle und Indexblöcke kann verbessert werden, wenn mehr freier Speicherplatz zur Verfügung steht.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
 [Neuorganisieren und Neuerstellen von Indizes](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
 [Configure the index create memory Server Configuration Option](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md)  
  
 [Speicherplatzanforderungen für Index-DDL-Vorgänge](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
  

