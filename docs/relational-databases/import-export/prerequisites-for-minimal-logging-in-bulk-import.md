---
title: "Voraussetzungen f&#252;r die minimale Protokollierung beim Massenimport | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-bulk-import-export"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Minimale Protokollierung [SQL Server]"
  - "Protokolliertes Massenkopieren [SQL Server]"
  - "Protokolle [SQL Server], minimale Protokollierung"
  - "Minimal protokollierte Vorgänge [SQL Server]"
  - "Massenimport [SQL Server], minimale Protokollierung"
ms.assetid: bd1dac6b-6ef8-4735-ad4e-67bb42dc4f66
caps.latest.revision: 48
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 47
---
# Voraussetzungen f&#252;r die minimale Protokollierung beim Massenimport
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Für eine Datenbank, bei der das vollständige Wiederherstellungsmodell verwendet wird, werden alle beim Massenimport ausgeführten Vorgänge für das Einfügen von Zeilen vollständig im Transaktionsprotokoll protokolliert. Bei umfangreichen Datenimporten kann das Transaktionsprotokoll schnell aufgefüllt werden, wenn das vollständige Wiederherstellungsmodell verwendet wird. Im Gegensatz dazu reduziert die minimale Protokollierung von Massenimportvorgängen beim einfachen Wiederherstellungsmodell oder beim massenprotokollierten Wiederherstellungsmodell die Gefahr eines Überlaufs des Protokollspeichers durch einen Massenimportvorgang. Darüber hinaus ist die minimale Protokollierung effizienter als die vollständige Protokollierung.  
  
> [!NOTE]  
>  Das massenprotokollierte Wiederherstellungsmodell wurde entwickelt, um das vollständige Wiederherstellungsmodell während umfangreicher Massenvorgänge vorübergehend zu ersetzen.  
  
## Tabellenanforderungen für die minimale Protokollierung bei Massenimportvorgängen  
 Für die minimale Protokollierung muss die Zieltabelle die folgenden Bedingungen erfüllen:  
  
-   Die Tabelle wird nicht repliziert.  
  
-   Eine Tabellensperre ist angegeben (mit TABLOCK). Für die Tabelle mit gruppiertem Columnstore-Index ist TABLOCK für eine minimale Protokollierung nicht erforderlich.  Darüber hinaus wird nur die Datenlast in komprimierte Zeilengruppen minimal protokolliert, was eine Batchgröße von 102400 oder höher erfordert.  
  
    > [!NOTE]  
    >  Obwohl Dateneinfügungen bei einem minimal protokollierten Massenimportvorgang nicht im Transaktionsprotokoll protokolliert werden, protokolliert das [!INCLUDE[ssDE](../../includes/ssde-md.md)] dennoch Blockzuordnungen, wenn der Tabelle ein neuer Block zugeordnet wird.  
  
-   Die Tabelle ist keine speicheroptimierte Tabelle.  
  
 Ob die minimale Protokollierung für eine Tabelle möglich ist, hängt auch davon ab, ob die Tabelle indiziert ist und, falls dies der Fall ist, ob die Tabelle leer ist:  
  
-   Wenn die Tabelle keine Indizes besitzt, werden die Datenseiten minimal protokolliert.  
  
-   Falls die Tabelle keinen gruppierten Index, aber mindestens einen nicht gruppierten Index aufweist, werden die Datenseiten immer minimal protokolliert. Wie Indexseiten protokolliert werden, hängt jedoch davon ab, ob die Tabelle leer ist:  
  
    -   Falls die Tabelle leer ist, werden Indexseiten minimal protokolliert.  
  
    -   Falls die Tabelle nicht leer ist, werden Indexseiten vollständig protokolliert.  
  
        > [!NOTE]  
        >  Wenn Sie mit einer leeren Tabelle beginnen und die Daten in mehreren Batches massenimportieren, werden für den ersten Batch sowohl Index- als auch Datenseiten minimal protokolliert. Ab dem zweiten Batch jedoch werden nur Datenseiten minimal protokolliert.  
  
-   Falls die Tabelle einen gruppierten Index aufweist und leer ist, werden Daten- und Indexseiten minimal protokolliert. Wenn dagegen eine Tabelle einen auf BTree basierenden gruppierten Index aufweist und nicht leer ist, werden Daten- und Indexseiten unabhängig vom Wiederherstellungsmodell vollständig protokolliert. Bei Tabellen mit gruppiertem Columnstore-Index wird die Datenlast in die komprimierte Zeilengruppe bei Batchgröße > = 102400 immer minimal protokolliert – unabhängig davon, ob die Tabelle leer ist.  
  
    > [!NOTE]  
    >  Wenn Sie mit einer leeren Rowstore-Tabelle beginnen und die Daten in Batches massenimportieren, werden für den ersten Batch sowohl Index- als auch Datenseiten minimal protokolliert. Ab dem zweiten Batch werden jedoch nur Datenseiten massenprotokolliert.  
  
> [!NOTE]  
>  Wenn die Transaktionsreplikation aktiviert ist, werden BULK INSERT-Vorgänge auch unter dem massenprotokollierten Wiederherstellungsmodell vollständig protokolliert.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Anzeigen oder Ändern des Wiederherstellungsmodells einer Datenbank &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  
 ![Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird](../../analysis-services/instances/media/uparrow16x16.png "Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird") [&#91;Nach oben&#93;](#Top)  
  
## Siehe auch  
 [Wiederherstellungsmodelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [bcp (Hilfsprogramm)](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Tabellenhinweise &#40;Transact-SQL&#41;](../Topic/Table%20Hints%20\(Transact-SQL\).md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)  
  
  