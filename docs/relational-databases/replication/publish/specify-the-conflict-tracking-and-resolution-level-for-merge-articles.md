---
title: "Angeben der Konfliktnachverfolgungs- und -lösungsebene für Mergeartikel | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], levels
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 81e9ecb6-1d31-4a78-b32a-96f7f4d67077
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 36e500ce1044dcbaff1146c29459c31e3f425cde
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="specify-the-conflict-tracking-and-resolution-level-for-merge-articles"></a>Angeben der Konfliktnachverfolgungs- und -lösungsebene für Mergeartikel
  In diesem Thema wird beschrieben, wie die Konfliktnachverfolgung und die Auflösungsebene für Mergeartikel in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]angegeben werden.  
  
 Wenn ein Abonnement für eine Mergeveröffentlichung synchronisiert wird, prüft die Replikation auf Konflikte, die sich ergeben, wenn der Verleger und der Abonnent die gleichen Daten ändern. Sie können angeben, ob Konflikte auf Zeilenebene erkannt werden, wobei jede Änderung in der Zeile als Konflikt eingestuft wird, oder auf Spaltenebene, wobei nur die Änderungen in derselben Spalte und derselben Zeile als Konflikte eingestuft werden. Die Konfliktlösung für Artikel wird auf Zeilenebene ausgeführt. Weitere Informationen zur Konflikterkennung und -lösung bei logischen Datensätzen finden Sie unter [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
-   **So geben Sie die Konfliktnachverfolgungs- und -lösungsebene für Mergeartikel an mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn Sie die Nachverfolgungsebene nach dem Initialisieren von Abonnements ändern, müssen diese Abonnements erneut initialisiert werden. Weitere Informationen über die Auswirkungen von Eigenschaftsänderungen finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
-   Bei der Nachverfolgung auf Zeilen- oder Spaltenebene erfolgt die Konfliktlösung immer auf Zeilenebene: die gewinnende Zeile überschreibt die verlierende Zeile. Bei der Mergereplikation können Sie auch angeben, dass Konflikte auf der Ebene logischer Datensätze nachverfolgt und gelöst werden. Diese Optionen sind in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]jedoch nicht verfügbar. Informationen zum Festlegen dieser Optionen über gespeicherte Replikationsprozeduren finden Sie unter [Define a Logical Record Relationship Between Merge Table Articles](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Geben Sie die Nachverfolgung auf Zeilen- oder Spaltenebene für Mergeartikel im Dialogfeld **Artikeleigenschaften** auf der Registerkarte **Eigenschaften** an. Dieses Dialogfeld ist im Assistenten für neue Veröffentlichung und im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** verfügbar. Weitere Informationen zum Verwenden des Assistenten sowie Zugriff auf das Dialogfeld finden Sie unter [Erstellen einer Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-row--or-column-level-tracking"></a>So geben Sie die Nachverfolgung auf Zeilen- oder Spaltenebene an  
  
1.  Wählen Sie auf der Seite **Artikel** des Assistenten für neue Veröffentlichung bzw. des Dialogfelds **Veröffentlichungseigenschaften - \<Veröffentlichung>** eine Tabelle aus.  
  
2.  Klicken Sie auf **Artikeleigenschaften**und anschließend auf **Eigenschaften des hervorgehobenen Tabellenartikels festlegen** bzw. **Eigenschaften aller Tabellenartikel festlegen**.  
  
3.  Wählen Sie im Dialogfeld **Artikeleigenschaften \<Article>** auf der Registerkarte **Eigenschaften** einen der folgenden Werte für die Eigenschaft **Nachverfolgungsebene** aus: **Nachverfolgung auf Zeilenebene** oder **Nachverfolgung auf Spaltenebene**.  
  
4.  Wenn Sie sich im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** befinden, klicken Sie auf **OK**, um eine Speicherung vorzunehmen und das Dialogfeld zu schließen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-specify-conflict-tracking-options-for-a-new-merge-article"></a>So geben Sie Konfliktverfolgungsoptionen für einen neuen Mergeartikel an  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) aus, und geben Sie einen der folgenden Werte für **@column_tracking**an:  
  
    -   **true** &ndash; Nachverfolgung auf Spaltenebene für den Artikel verwenden.  
  
    -   **false** &ndash; Nachverfolgung auf Zeilenebene verwenden (Standard).  
  
#### <a name="to-change-conflict-tracking-options-for-a-merge-article"></a>So ändern Sie die Konfliktverfolgungsoptionen für einen Mergeartikel  
  
1.  Um die Konfliktverfolgungsoptionen für einen Mergeartikel zu bestimmen, führen Sie [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)aus. Achten Sie auf den Wert der **column_tracking** -Option im Resultset für den Artikel. Der Wert **1** bedeutet, dass die Nachverfolgung auf Spaltenebene verwendet wird, und der Wert **0** bedeutet, dass die Nachverfolgung auf Zeilenebene verwendet wird.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)aus. Geben Sie den Wert **column_tracking** für **@property** und einen der folgenden Werte für **@value**an:  
  
    -   **true** &ndash; Nachverfolgung auf Spaltenebene für den Artikel verwenden.  
  
    -   **false** &ndash; Nachverfolgung auf Zeilenebene verwenden (Standard).  
  
     Geben Sie den Wert **1** sowohl für **@force_invalidate_snapshot** und **@force_reinit_subscription**angegeben werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Ermitteln und Lösen von Konflikten in logischen Datensätzen](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)   
 [Definieren einer logische Datensatzbeziehung zwischen Mergetabellenartikeln](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [Erkennen und Beseitigen von Konflikten bei der Mergereplikation](../../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)  
  
  
