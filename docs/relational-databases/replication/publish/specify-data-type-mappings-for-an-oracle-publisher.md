---
title: "Angeben von Datentypzuordnungen f&#252;r einen Oracle-Verleger | Microsoft Docs"
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
  - "Veröffentlichungen mit Oracle [SQL Server-Replikation], Datentypzuordnung"
  - "Datentypen [SQL Server-Replikation], Veröffentlichungen mit Oracle"
  - "Zuordnen von Datentypen [SQL Server-Replikation]"
ms.assetid: f172d631-3b8c-4912-bd0f-568366cd9870
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Angeben von Datentypzuordnungen f&#252;r einen Oracle-Verleger
  In diesem Thema wird beschrieben, wie Datentypzuordnungen für einen Oracle-Verleger in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]angegeben werden. Obwohl eine Gruppe von Standard-Datentypzuordnungen für Oracle-Verleger bereitgestellt wird, ist es möglicherweise erforderlich, für eine bestimmte Veröffentlichung andere Zuordnungen anzugeben.  
  
 **In diesem Thema**  
  
-   **So geben Sie Datentypzuordnungen für einen Oracle-Verleger an mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Geben Sie datentypzuordnungen für die **Zuordnung** Registerkarte der **Artikeleigenschaften - \< Artikel>** (Dialogfeld). Erfolgt die **Artikel** Seite des Assistenten für neue Veröffentlichung und die **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zum Verwenden des Assistenten sowie Zugriff auf das Dialogfeld finden Sie unter [Erstellen einer Veröffentlichung aus einer Oracle-Datenbank](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md) und [anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### So geben Sie eine Datentypzuordnung an  
  
1.  Auf der **Artikel** Seite des Assistenten für neue Veröffentlichung oder **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld Wählen Sie eine Tabelle, und klicken Sie dann auf **Artikeleigenschaften**.  
  
2.  Klicken Sie auf die Option **Eigenschaften des hervorgehobenen Tabelle-Artikels festlegen**.  
  
3.  Auf der **Zuordnung von** auf der Registerkarte der **Artikeleigenschaften - \< Artikel>** Klicken Sie im Dialogfeld select Zuordnungen aus den **Abonnentendatentyp** Spalte:  
  
    -   Bei bestimmten Datentypen gibt es nur eine mögliche Zuordnung. In diesem Fall ist die Spalte im Eigenschaftenraster schreibgeschützt.  
  
    -   Für einige Typen sind mehrere Typen zur Auswahl vorhanden. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] empfiehlt die Verwendung der Standardzuordnung, sofern die Anwendung keine andere Zuordnung erfordert. Weitere Informationen finden Sie unter [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Sie können benutzerdefinierte Datentypzuordnungen programmgesteuert mithilfe von gespeicherten Replikationsprozeduren angeben. Sie können auch die standardzuordnungen festlegen, die verwendet werden, wenn die Zuordnung von Datentypen zwischen [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] und einem nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datenbank-Managementsystem (DBMS). Weitere Informationen finden Sie unter [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
#### So definieren Sie benutzerdefinierte Datentypzuordnungen beim Erstellen eines Artikels, der zu einer Oracle-Veröffentlichung gehört  
  
1.  Erstellen Sie eine Oracle-Veröffentlichung, sofern noch nicht vorhanden.  
  
2.  Führen Sie auf dem Verteiler [Sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Geben Sie den Wert **0** für **@use_default_datatypes**. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
3.  Führen Sie auf dem Verteiler [Sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) an die vorhandene Zuordnung für eine Spalte in einem veröffentlichten Artikel anzuzeigen.  
  
4.  Führen Sie auf dem Verteiler [Sp_changearticlecolumndatatype](../../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md). Geben Sie den Namen des Oracle-Verlegers für **@publisher**sowie **@publication**, **@article**und **@column** an, um die veröffentlichte Spalte zu definieren. Geben Sie den Namen des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyps, der zugeordnet werden soll, für **@type**sowie nach Bedarf **@length**, **@precision**und **@scale**an.  
  
5.  Führen Sie auf dem Verteiler [Sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Dies erstellt die Sicht, mit der die Momentaufnahme der Oracle-Veröffentlichung generiert wird.  
  
#### So geben Sie eine Zuordnung als Standardzuordnung für einen Datentyp an  
  
1.  (Optional) Führen Sie auf dem Verteiler für jede Datenbank [Sp_getdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md). Geben Sie **@source_dbms**, **@source_type**, **@destination_dbms**, **@destination_version**, und alle anderen Parameter, die zum Identifizieren des Quell-DBMS erforderlich. Informationen über den gerade zugeordneten Datentyp im Ziel-DBMS werden mit den Ausgabeparametern zurückgegeben.  
  
2.  (Optional) Führen Sie auf dem Verteiler für jede Datenbank [Sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md). Geben Sie **@source_dbms** und alle anderen Parameter benötigt, um das Resultset zu filtern. Beachten Sie den Wert der **Mapping_id** für die gewünschte Zuordnung im Ergebnis festlegen.  
  
3.  Führen Sie auf dem Verteiler für jede Datenbank [Sp_setdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md).  
  
    -   Wenn Sie den gewünschten Wert wissen **Mapping_id** in Schritt 2 abgerufen haben, geben Sie es für **@mapping_id**.  
  
    -   Wenn Sie nicht wissen, die **Mapping_id**, geben Sie die Parameter **@source_dbms**, **@source_type**, **@destination_dbms**, **@destination_type**, und alle anderen Parameter, die zum Identifizieren einer vorhandenen Zuordnung erforderlich.  
  
#### So suchen Sie gültige Datentypen für einen bestimmten Oracle-Datentyp  
  
1.  Führen Sie auf dem Verteiler für jede Datenbank [Sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md). Geben Sie den Wert **ORACLE** für **@source_dbms** und alle anderen Parameter benötigt, um das Resultset zu filtern.  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 In diesem Beispiel wird eine Spalte mit einer Oracle-Datentyp NUMBER, damit er zugeordnet ist [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datentyp **numerischen**(38,38), anstelle des Standarddatentyps **Float**.  
  
 [!code-sql[HowTo#sp_changecolumndatatype](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_1.sql)]  
  
 Diese Beispielabfrage gibt die Standardzuordnungen sowie die alternativen Zuordnungen für den Oracle 9-Datentyp **CHAR**zurück.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_char](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_2.sql)]  
  
 Diese Beispielabfrage gibt die Standardzuordnungen für den Oracle 9-Datentyp **NUMBER** zurück, wenn er ohne Dezimalstellenangabe oder Genauigkeit angegeben wird.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_number](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_3.sql)]  
  
## Siehe auch  
 [Datentypzuordnung für Oracle-Verleger](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Heterogene Datenbankreplikation](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)  
  
  