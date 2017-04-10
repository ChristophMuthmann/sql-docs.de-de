---
title: "Replizieren von Schema&#228;nderungen | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Replikation [SQL Server], Schemaänderungen"
  - "Schemas [SQL Server-Replikation], Replizieren von Änderungen"
ms.assetid: c09007f0-9374-4f60-956b-8a87670cd043
caps.latest.revision: 43
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 43
---
# Replizieren von Schema&#228;nderungen
  In diesem Thema wird beschrieben, wie Schemaänderungen in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]repliziert werden.  
  
 Wenn Sie in einem veröffentlichten Artikel die folgenden Schemaänderungen vornehmen, werden diese standardmäßig an [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Abonnenten weitergegeben:  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
-   **So replizieren Sie Schemaänderungen mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Die ALTER TABLE-Anweisung ... Die DROP COLUMN-Anweisung wird grundsätzlich auf alle Abonnenten repliziert, deren Abonnement die Spalten enthält, die gelöscht werden, auch wenn Sie die Replikation von Schemaänderungen deaktiviert haben.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Wenn keine schemaänderungen für eine Veröffentlichung repliziert werden soll, deaktivieren Sie die Replikation von schemaänderungen in der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### So deaktivieren Sie die Replikation von Schemaänderungen  
  
1.  Auf der **Abonnementoptionen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** Dialogfeld legen den Wert des der **Replizieren von schemaänderungen** -Eigenschaft **False**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     Wenn nur bestimmte Schemaänderungen weitergegeben werden sollen, legen Sie für die Eigenschaft vor der Schemaänderung **Wahr** und danach **Falsch** fest. Wenn umgekehrt die meisten Schemaänderungen weitergegeben werden sollen und nur eine bestimmte Änderung nicht repliziert werden soll, legen Sie für die Eigenschaft vor der entsprechenden Schemaänderung **Falsch** und anschließend wieder **Wahr** fest.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Sie können mithilfe gespeicherter Replikationsprozeduren angeben, ob diese Schemaänderungen repliziert werden sollen. Welche gespeicherte Prozedur Sie verwenden, hängt vom Typ der Veröffentlichung ab.  
  
#### So erstellen Sie eine Momentaufnahme- oder Transaktionsveröffentlichung, die keine Schemaänderungen repliziert  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addpublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), Angabe des Werts **0** für **@replicate_ddl**. Weitere Informationen finden Sie unter [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### So erstellen Sie eine Mergeveröffentlichung, die keine Schemaänderungen repliziert  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), Angabe des Werts **0** für **@replicate_ddl**. Weitere Informationen finden Sie unter [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### So deaktivieren Sie vorübergehend die Replikation von Schemaänderungen in einer Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie für eine Veröffentlichung mit Replikation von schemaänderungen, [Sp_changepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), Angabe des Werts **Replicate_ddl** für **@property** und den Wert **0** für **@value**.  
  
2.  Führen Sie den DDL-Befehl für das veröffentlichte Objekt aus.  
  
3.  (Optional) Reaktivieren Sie die Replikation von schemaänderungen durch Ausführen [Sp_changepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), Angabe des Werts **Replicate_ddl** für **@property** und einem Wert von **1** für **@value**.  
  
#### So deaktivieren Sie vorübergehend die Replikation von Schemaänderungen in einer Mergeveröffentlichung  
  
1.  Führen Sie für eine Veröffentlichung mit Replikation von schemaänderungen, [Sp_changemergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), Angabe des Werts **Replicate_ddl** für **@property** und den Wert **0** für **@value**.  
  
2.  Führen Sie den DDL-Befehl für das veröffentlichte Objekt aus.  
  
3.  (Optional) Reaktivieren Sie die Replikation von schemaänderungen durch Ausführen [Sp_changemergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), Angabe des Werts **Replicate_ddl** für **@property** und einem Wert von **1** für **@value**.  
  
## Siehe auch  
 [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  