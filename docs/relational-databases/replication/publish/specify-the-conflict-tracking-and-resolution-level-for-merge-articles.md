---
title: "Angeben der Konfliktnachverfolgungs- und -l&#246;sungsebene f&#252;r Mergeartikel | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Konfliktlösung bei der Mergereplikation [SQL Server-Replikation], Ebenen"
  - "Artikel [SQL Server-Replikation], Konfliktlösung"
  - "Konfliktlösung [SQL Server-Replikation], Mergereplikation "
ms.assetid: 81e9ecb6-1d31-4a78-b32a-96f7f4d67077
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# Angeben der Konfliktnachverfolgungs- und -l&#246;sungsebene f&#252;r Mergeartikel
  In diesem Thema wird beschrieben, wie die Konfliktnachverfolgung und die Auflösungsebene für Mergeartikel in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]angegeben werden.  
  
 Wenn ein Abonnement für eine Mergeveröffentlichung synchronisiert wird, prüft die Replikation auf Konflikte, die sich ergeben, wenn der Verleger und der Abonnent die gleichen Daten ändern. Sie können angeben, ob Konflikte auf Zeilenebene erkannt werden, wobei jede Änderung in der Zeile als Konflikt eingestuft wird, oder auf Spaltenebene, wobei nur die Änderungen in derselben Spalte und derselben Zeile als Konflikte eingestuft werden. Die Konfliktlösung für Artikel wird auf Zeilenebene ausgeführt. Weitere Informationen zur Konflikterkennung und -lösung bei logischen Datensätzen finden Sie unter [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/detecting-and-resolving-conflicts-in-logical-records.md).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
-   **So geben Sie die Konfliktnachverfolgungs- und -lösungsebene für Mergeartikel an mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn Sie die Nachverfolgungsebene nach dem Initialisieren von Abonnements ändern, müssen diese Abonnements erneut initialisiert werden. Weitere Informationen zu den Auswirkungen von eigenschaftenänderungen finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
-   Bei der Nachverfolgung auf Zeilen- oder Spaltenebene erfolgt die Konfliktlösung immer auf Zeilenebene: die gewinnende Zeile überschreibt die verlierende Zeile. Bei der Mergereplikation können Sie auch angeben, dass Konflikte auf der Ebene logischer Datensätze nachverfolgt und gelöst werden. Diese Optionen sind in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]jedoch nicht verfügbar. Informationen zum Festlegen dieser Optionen über gespeicherte Replikationsprozeduren finden Sie unter [Define a Logical Record Relationship Between Merge Table Articles](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Geben Sie die Überwachung für Mergeartikel mit Zeilen- oder Spaltenebene der **Eigenschaften** Registerkarte der **Artikeleigenschaften** Dialogfeld, das im Assistenten für neue Veröffentlichung verfügbar ist und die **Veröffentlichungseigenschaften - \< Veröffentlichung>** im Dialogfeld. Weitere Informationen zum Verwenden des Assistenten sowie Zugriff auf das Dialogfeld finden Sie unter [Erstellen Sie eine Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### So geben Sie die Nachverfolgung auf Zeilen- oder Spaltenebene an  
  
1.  Auf der **Artikel** Seite des Assistenten für neue Veröffentlichung oder **Veröffentlichungseigenschaften - \< Veröffentlichung>** Dialogfeld Wählen Sie eine Tabelle aus.  
  
2.  Klicken Sie auf **Artikeleigenschaften**und anschließend auf **Eigenschaften des hervorgehobenen Tabellenartikels festlegen** bzw. **Eigenschaften aller Tabellenartikel festlegen**.  
  
3.  Auf der **Eigenschaften** Registerkarte der **Artikeleigenschaften \< Artikel>** Wählen Sie im Dialogfeld einen der folgenden für Werte die **Nachverfolgungsebene** Eigenschaft: **auf Zeilenebene** oder **auf Spaltenebene**.  
  
4.  Wenn Sie haben die **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld klicken Sie auf **OK** zum Speichern und schließen das Dialogfeld.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So geben Sie Konfliktverfolgungsoptionen für einen neuen Mergeartikel an  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) und geben Sie einen der folgenden Werte für **@column_tracking**:  
  
    -   **true** -auf Spaltenebene für den Artikel verwenden.  
  
    -   **false** -Verwendung Zeilenebene, was der Standardeinstellung entspricht.  
  
#### So ändern Sie die Konfliktverfolgungsoptionen für einen Mergeartikel  
  
1.  Um die konfliktverfolgungsoptionen für einen Mergeartikel zu bestimmen, führen [Sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Beachten Sie den Wert der **Column_tracking** Option im Resultset für den Artikel. Der Wert **1** bedeutet, dass auf Spaltenebene verwendet wird, und der Wert **0** bedeutet, dass auf Zeilenebene verwendet wird.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Geben Sie den Wert **Column_tracking** für **@property** und einen der folgenden Werte für **@value**:  
  
    -   **true** -auf Spaltenebene für den Artikel verwenden.  
  
    -   **false** -Verwendung Zeilenebene, was der Standardeinstellung entspricht.  
  
     Geben Sie den Wert **1** für beide **@force_invalidate_snapshot** und **@force_reinit_subscription**.  
  
## Siehe auch  
 [Erweiterte Konflikterkennung und -lösung bei der Mergereplikation](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Ermitteln und Lösen von Konflikten in logischen Datensätzen](../../../relational-databases/replication/merge/detecting-and-resolving-conflicts-in-logical-records.md)   
 [Definieren einer logische Datensatzbeziehung zwischen Mergetabellenartikeln](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [Erkennen und Beseitigen von Konflikten bei der Mergereplikation](../../../relational-databases/replication/merge/detect-and-resolve-merge-replication-conflicts.md)  
  
  