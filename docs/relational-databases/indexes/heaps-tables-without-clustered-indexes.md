---
title: "Heaps (Tabellen ohne gruppierte Indizes) | Microsoft Docs"
ms.custom: ""
ms.date: "11/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-indexes"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Heaps"
ms.assetid: df5c4dfb-d372-4d0f-859a-a2d2533ee0d7
caps.latest.revision: 8
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 8
---
# Heaps (Tabellen ohne gruppierte Indizes)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Ein Heap ist eine Tabelle ohne gruppierten Index. Ein oder mehrere nicht gruppierte Indizes können für Tabellen erstellt werden, die als Heap gespeichert sind. Daten werden ohne bestimmte Reihenfolge im Heap gespeichert. Normalerweise werden Daten anfänglich in der Reihenfolge gespeichert, in der die Zeilen in die Tabelle eingefügt werden. [!INCLUDE[ssDE](../../includes/ssde-md.md)] kann die Daten jedoch im Heap verschieben, um die Zeilen effizienter zu speichern; daher kann die Reihenfolge der Daten nicht vorhergesagt werden. Um die von einem Heap zurückgegebene Zeilenreihenfolge zu garantieren, müssen Sie die **ORDER BY** -Klausel verwenden. Um die Reihenfolge zum Speichern der Zeilen anzugeben, erstellen Sie für eine Tabelle einen gruppierten Index, damit es sich bei der Tabelle nicht um einen Heap handelt.  
  
> [!NOTE]  
>  In bestimmten Fällen gibt es gute Gründe, eine Tabelle als einen Heap zu belassen, statt einen gruppierten Index zu erstellen. Die effektive Verwendung von Heaps ist jedoch Benutzern mit fortgeschrittenen Kenntnissen vorbehalten. Die meisten Tabellen sollten über einen sorgfältig ausgewählten gruppierten Index verfügen, es sei denn, es gibt gute Gründe, die Tabelle als Heap beizubehalten.  
  
## Verwendungsbereiche für Heaps  
 Wenn eine Tabelle ein Heap ist und nicht über ungruppierte Indizes verfügt, muss die ganze Tabelle überprüft werden (mit einem Tabellenscan), um eine Zeile zu finden. Dies ist durchaus denkbar, wenn es sich um eine kleine Tabelle handelt, wie z. B. eine Liste der zwölf Niederlassungen eines Unternehmens.  
  
 Wenn eine Tabelle als Heap gespeichert wird, werden einzelne Zeilen durch einen Zeilenbezeichner (RID, Row Identifier) gekennzeichnet, der aus der Dateinummer, der Datenseitennummer und einem Slot auf der Seite besteht. Die Zeilen-ID ist eine kleine und effiziente Struktur. In einigen Fällen verwenden Datenarchitekten Heaps, wenn immer über nicht gruppierte Indizes auf Daten zugegriffen wird und die RID kleiner als ein Schlüssel des gruppierten Indexes ist.  
  
## Keine Verwendungsbereiche für Heaps  
 Verwenden Sie keinen Heap, wenn die Daten häufig in einer sortierten Reihenfolge zurückgegeben werden. Mit einem gruppierten Index für die Sortierspalte kann der Sortiervorgang vermieden werden.  
  
 Verwenden Sie keinen Heap, wenn die Daten häufig zusammen gruppiert werden. Daten müssen vor dem Gruppieren sortiert werden, und ein gruppierter Index für die Sortierspalte kann den Sortiervorgang vermeiden.  
  
 Verwenden Sie keinen Heap, wenn häufig Datenbereiche aus der Tabelle abgefragt werden.  Mit einem gruppierten Index für die Bereichsspalte kann der Sortiervorgang für den gesamten Heap vermieden werden.  
  
 Verwenden Sie keinen Heap, wenn keine nicht gruppierten Indizes vorhanden sind und die Tabelle sehr groß ist. In einem Heap müssen alle Zeilen des Heaps gelesen werden, um eine Zeile zu finden.  
  
## Verwalten von Heaps  
 Erstellen Sie zum Anlegen eines Heaps eine Tabelle ohne gruppierten Index. Alternativ dazu können Sie den gruppierten Index löschen, wenn die Tabelle bereits über einen gruppierten Index verfügt, damit die Tabelle wieder ein Heap ist.  
  
 Erstellen Sie zum Löschen eines Heaps auf dem Heap einen gruppierten Index.  
  
 Um einen Heap neu zu erstellen, damit nicht verwendeter Speicherplatz wieder genutzt werden kann, erstellen Sie auf dem Heap einen gruppierten Index und löschen den gruppierten Index dann wieder.  
  
> [!WARNING]  
>  Das Erstellen oder Löschen von gruppierten Indizes erfordert, dass die gesamte Tabelle neue geschrieben werden muss. Wenn die Tabelle über nicht gruppierte Indizes verfügt, müssen alle nicht gruppierten Indizes immer dann neu erstellt werden, wenn der gruppierte Index geändert wird. Aus diesem Grund kann es sehr lange dauern, von einem Heap zu einem gruppierten Index zu wechseln und umgekehrt, sowie viel Festplattenspeicher zum Neuordnen der Daten in tempdb erfordern.  

## Heapstrukturen


Ein Heap ist eine Tabelle ohne gruppierten Index. Heaps haben eine Zeile in [sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md), mit `index_id = 0` für jede vom Heap verwendete Partition. Standardmäßig verfügt ein Heap über eine einzelne Partition. Wenn ein Heap über mehrere Partitionen verfügt, hat jede Partition eine Heapstruktur, in der die Daten für die jeweilige Partition enthalten sind. Wenn ein Heap z. B. über vier Partitionen verfügt, gibt es vier Heapstrukturen – jeweils eine in jeder Partition.

Je nach den im Heap enthaltenen Datentypen weist jede Heapstruktur eine oder mehrere Zuordnungseinheiten auf, um die Daten für eine bestimmte Partition zu speichern und zu verwalten. Zumindest verfügt jeder Heap über eine `IN_ROW_DATA`-Zuordnungseinheit pro Partition. Der Heap hat außerdem eine `LOB_DATA`-Zuordnungseinheit pro Partition, wenn diese LOB-Spalten (Large OBject) enthält. Außerdem ist eine `ROW_OVERFLOW_DATA`-Zuordnungseinheit pro Partition vorhanden, wenn der Index Spalten variabler Länge aufweist, die die Zeilengrößenbegrenzung von 8.060 Byte übersteigen.

Die Spalte `first_iam_page` in der Systemsicht `sys.system_internals_allocation_units` verweist auf die erste IAM-Seite in der Kette der IAM-Seiten, die den Speicherplatz auf dem Heap in einer bestimmten Partition verwalten. SQL Server verwendet die IAM-Seiten, um sich durch den Heap zu bewegen. Die Datenseiten und die Zeilen innerhalb eines Heaps weisen keine bestimmte Reihenfolge auf und sind nicht verknüpft. Die einzige logische Verbindung zwischen den Datenseiten sind die Informationen, die auf den IAM-Seiten aufgezeichnet sind.

> [!IMPORTANT]  
> Die Systemsicht `sys.system_internals_allocation_units` ist nur für die interne Verwendung durch Microsoft SQL Server reserviert. Zukünftige Kompatibilität wird nicht sichergestellt.
 
Tabellenscans oder serielle Lesevorgänge in einem Heap können durchgeführt werden, indem die IAM-Seiten gescannt werden, um auf diese Weise die Blöcke zu ermitteln, die Seiten des Heaps enthalten. Da die IAM die Blöcke in derselben Reihenfolge darstellt, in der sie in der Datendatei vorliegen, werden serielle Heapscans immer sequenziell durch jede Datei ausgeführt. Das Verwenden der IAM-Seiten zum Festlegen der Scanfolge bedeutet weiterhin, dass Zeilen aus dem Heap nicht notwendigerweise in der Reihenfolge zurückgegeben werden, in der sie eingefügt wurden.

Die folgende Abbildung zeigt, wie das SQL Server-Datenbankmodul die IAM-Seiten zum Abrufen von Datenzeilen in einem Heap mit einer einzelnen Partition verwendet. 

![iam_heap](../../relational-databases/indexes/media/iam-heap.gif)

  
## Verwandte Inhalte  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
 [Beschreibung von gruppierten und nicht gruppierten Indizes](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)  
  
  