---
title: "Angeben von Datentypzuordnungen für einen Oracle-Verleger | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], data type mapping
- data types [SQL Server replication], Oracle publishing
- mapping data types [SQL Server replication]
ms.assetid: f172d631-3b8c-4912-bd0f-568366cd9870
caps.latest.revision: "37"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2589fa181a502c7eb016ce958e1fe1fe4d325a8a
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="specify-data-type-mappings-for-an-oracle-publisher"></a>Angeben von Datentypzuordnungen für einen Oracle-Verleger
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie Datentypzuordnungen für einen Oracle-Verleger in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)] angegeben werden. Obwohl eine Gruppe von Standard-Datentypzuordnungen für Oracle-Verleger bereitgestellt wird, ist es möglicherweise erforderlich, für eine bestimmte Veröffentlichung andere Zuordnungen anzugeben.  
  
 **In diesem Thema**  
  
-   **So geben Sie Datentypzuordnungen für einen Oracle-Verleger an mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
 Die Datentypzuordnungen werden auf der Registerkarte Datenzuordnung**des Dialogfelds **Artikeleigenschaften – \<Artikel>** angegeben. Diese Registerkarte ist über die Seite Artikel** des Assistenten für neue Veröffentlichung und das Dialogfeld **Veröffentlichungseigenschaften – \<Veröffentlichung>** verfügbar. Weitere Informationen zum Verwenden des Assistenten sowie zum Zugriff auf das Dialogfeld finden Sie unter [Erstellen einer Veröffentlichung aus einer Oracle-Datenbank](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md) und [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-a-data-type-mapping"></a>So geben Sie eine Datentypzuordnung an  
  
1.  Wählen Sie im Assistenten für neue Veröffentlichung auf der Seite Artikel** bzw. im Dialogfeld **Veröffentlichungseigenschaften – \<<Veröffentlichung>** eine Tabelle aus, und klicken anschließend auf **Artikeleigenschaften**.  
  
2.  Klicken Sie auf die Option **Eigenschaften des hervorgehobenen Tabelle-Artikels festlegen**.  
  
3.  Wählen Sie auf der Registerkarte Datenzuordnung** des Dialogfelds **Artikeleigenschaften – \<Artikel>** in der Spalte **Abonnentendatentyp** Zuordnungen aus:  
  
    -   Bei bestimmten Datentypen gibt es nur eine mögliche Zuordnung. In diesem Fall ist die Spalte im Eigenschaftenraster schreibgeschützt.  
  
    -   Für einige Typen sind mehrere Typen zur Auswahl vorhanden. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] empfiehlt die Verwendung der Standardzuordnung, sofern die Anwendung keine andere Zuordnung erfordert. Weitere Informationen finden Sie unter [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Sie können benutzerdefinierte Datentypzuordnungen programmgesteuert mithilfe von gespeicherten Replikationsprozeduren angeben. Sie können auch die Standardzuordnungen festlegen, die beim Zuordnen von Datentypen zwischen [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] und einem Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank-Managementsystem (DBMS) verwendet werden. Weitere Informationen finden Sie unter [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
#### <a name="to-define-custom-data-type-mappings-when-creating-an-article-belonging-to-an-oracle-publication"></a>So definieren Sie benutzerdefinierte Datentypzuordnungen beim Erstellen eines Artikels, der zu einer Oracle-Veröffentlichung gehört  
  
1.  Erstellen Sie eine Oracle-Veröffentlichung, sofern noch nicht vorhanden.  
  
2.  Führen Sie auf dem Verteiler [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)aus. Geben Sie den Wert **0** für **@use_default_datatypes**angegeben werden. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
3.  Führen Sie auf dem Verteiler [sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) aus, um die vorhandene Zuordnung für eine Spalte in einem veröffentlichten Artikel anzuzeigen.  
  
4.  Führen Sie auf dem Verteiler [sp_changearticlecolumndatatype](../../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md)aus. Geben Sie den Namen des Oracle-Verlegers für **@publisher**sowie **@publication**, **@article**und **@column** an, um die veröffentlichte Spalte zu definieren. Geben Sie den Namen des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyps, der zugeordnet werden soll, für **@type**sowie **@length**, **@precision**und **@scale**an.  
  
5.  Führen Sie auf dem Verteiler [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)aus. Dies erstellt die Sicht, mit der die Momentaufnahme der Oracle-Veröffentlichung generiert wird.  
  
#### <a name="to-specify-a-mapping-as-the-default-mapping-for-a-data-type"></a>So geben Sie eine Zuordnung als Standardzuordnung für einen Datentyp an  
  
1.  (Optional) Führen Sie auf dem Verteiler für eine beliebige Datenbank [sp_getdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)aus. Geben Sie **@source_dbms**, **@source_type**, **@destination_dbms**, **@destination_version**und andere Parameter an, die zum Identifizieren des Quell-DBMS erforderlich sind. Informationen über den gerade zugeordneten Datentyp im Ziel-DBMS werden mit den Ausgabeparametern zurückgegeben.  
  
2.  (Optional) Führen Sie auf dem Verteiler für eine beliebige Datenbank [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)aus. Geben Sie **@source_dbms** und alle anderen Parameter an, die zum Filtern des Resultsets benötigt werden. Notieren Sie den Wert von **mapping_id** für die gewünschte Zuordnung im Resultset.  
  
3.  Führen Sie auf dem Verteiler für eine beliebige Datenbank [sp_setdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)aus.  
  
    -   Wenn Sie den gewünschten Wert von **mapping_id** kennen, der in Schritt 2 ermittelt wurde, geben Sie diesen Wert für **@mapping_id**angegeben werden.  
  
    -   Wenn Sie den Wert für **mapping_id**nicht kennen, geben Sie die Parameter **@source_dbms**, **@source_type**, **@destination_dbms**, **@destination_type**sowie alle anderen Parameter an, die zum Identifizieren einer vorhandenen Zuordnung erforderlich sind.  
  
#### <a name="to-find-valid-data-types-for-a-given-oracle-data-type"></a>So suchen Sie gültige Datentypen für einen bestimmten Oracle-Datentyp  
  
1.  Führen Sie auf dem Verteiler für eine beliebige Datenbank [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)aus. Geben Sie den Wert **ORACLE** für **@source_dbms** und alle anderen Parameter an, die zum Filtern des Resultsets benötigt werden.  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 In diesem Beispiel wird eine Spalte mit dem Oracle-Datentyp NUMBER geändert, sodass er dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp **numeric**(38,38) anstelle des Standarddatentyps **float**angegeben werden.  
  
 [!code-sql[HowTo#sp_changecolumndatatype](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_1.sql)]  
  
 Diese Beispielabfrage gibt die Standardzuordnungen sowie die alternativen Zuordnungen für den Oracle 9-Datentyp **CHAR**zurück.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_char](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_2.sql)]  
  
 Diese Beispielabfrage gibt die Standardzuordnungen für den Oracle 9-Datentyp **NUMBER** zurück, wenn er ohne Dezimalstellenangabe oder Genauigkeit angegeben wird.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_number](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_3.sql)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Heterogene Datenbankreplikation](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)  
  
  
