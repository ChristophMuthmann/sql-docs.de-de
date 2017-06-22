---
title: "Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- replication [SQL Server], schema changes
- snapshot replication [SQL Server], replicating schema changes
- merge replication [SQL Server replication], replicating schema changes
- transactional replication, replicating schema changes
- schemas [SQL Server replication], replicating changes
- publishing [SQL Server replication], schema changes
ms.assetid: 926c88d7-a844-402f-bcb9-db49e5013b69
caps.latest.revision: 73
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: aa8ea65ab7ef276791e721f6f1bb5e9da6c6a4ec
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="make-schema-changes-on-publication-databases"></a>Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken
  Die Replikation unterstützt eine breite Palette von Schemaänderungen an veröffentlichten Objekten. Wenn Sie eine der folgenden Schemaänderungen am entsprechenden veröffentlichten Objekt auf einem [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verleger vornehmen, wird diese Änderung standardmäßig an alle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Abonnenten weitergegeben:  
  
-   ALTER TABLE  
  
-   ALTER TABLE SET LOCK ESCALATION darf nicht verwendet werden, wenn die Schemaänderungsreplikation aktiviert ist und eine Topologie [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] - oder [!INCLUDE[ssEWnoversion](../../../includes/ssewnoversion-md.md)] -Abonnenten enthält. ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
     ALTER TRIGGER kann nur für DML-Trigger [Data Manipulation Language] verwendet werden, da DLL-Triggers [Data Definition Language] nicht repliziert werden können.  
  
> [!IMPORTANT]  
>  Schemaänderungen an Tabellen müssen mithilfe von [!INCLUDE[tsql](../../../includes/tsql-md.md)] oder [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO) vorgenommen werden. Wenn Schemaänderungen in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]vorgenommen werden, versucht [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] die Tabelle zu löschen und neu zu erstellen. Da veröffentlichte Objekte nicht gelöscht werden können, schlägt die Schemaänderung fehl.  
  
 Bei der Transaktions- und der Mergereplikation werden Schemaänderungen inkrementell weitergegeben, sobald der Verteilungs-Agent oder der Merge-Agent ausgeführt wird. Bei der Momentaufnahmereplikation werden Schemaänderung weitergegeben, wenn eine neue Momentaufnahme auf den Abonnenten angewendet wird. Außerdem wird bei der Momentaufnahmereplikation eine neue Kopie des Schemas bei jeder Synchronisierung an den Abonnenten gesendet. Deshalb werden alle Schemaänderungen (nicht nur die oben aufgeführten) an bereits veröffentlichten Objekten automatisch bei jeder Synchronisierung weitergegeben.  
  
 Informationen zu Überlegungen zum Hinzufügen und Löschen von Artikeln aus Veröffentlichungen finden Sie unter [Hinzufügen und Löschen von Artikeln aus vorhandenen Veröffentlichungen](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
 **So replizieren Sie Schemaänderungen**  
  
 Die oben aufgeführten Schemaänderungen werden standardmäßig repliziert. Informationen zum Deaktivieren der Replikation von Schemaänderungen finden Sie unter [Replicate Schema Changes](../../../relational-databases/replication/publish/replicate-schema-changes.md).  
  
## <a name="considerations-for-schema-changes"></a>Überlegungen zu Schemaänderungen  
 Beachten Sie beim Replizieren von Schemaänderungen Folgendes:  
  
### <a name="general-considerations"></a>Allgemeine Überlegungen  
  
-   Schemaänderungen unterliegen den Einschränkungen von [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Beispielsweise können Sie mit ALTER TABLE keine Primärschlüsselspalten ändern.  
  
-   Datentypzuordnung wird nur für die Anfangsmomentaufnahme ausgeführt. Schemaänderungen werden nicht vorherigen Versionen von Datentypen zugeordnet. Beispiel: Wenn die `ALTER TABLE ADD datetime2 column` -Anweisung in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]verwendet wird, wird der Datentyp nicht für **ssVersion2005** -Abonnenten in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] umgewandelt. In einigen Fällen werden Schemaänderungen auf dem Verleger blockiert.  
  
-   Wenn für eine Veröffentlichung die Weitergabe von Schemaänderungen festgelegt ist, werden die Schemaänderungen unabhängig davon weitergegeben, wie die verbundene Schemaoption für einen Artikel in der Veröffentlichung festgelegt ist. Beispiel: Sie entscheiden sich, FOREIGN KEY-Einschränkungen für einen Tabellenartikel nicht zu replizieren, geben dann jedoch einen ALTER TABLE-Befehl aus, mit dem der Tabelle auf dem Verleger ein Fremdschlüssel hinzugefügt wird. In diesem Fall wird der Fremdschlüssel der Tabelle auf dem Abonnenten hinzugefügt. Um das zu verhindern, deaktivieren Sie die Weitergabe von Schemaänderungen, bevor Sie den ALTER TABLE-Befehl ausgeben.  
  
-   Schemaänderungen sollten nur auf dem Verleger und nicht auf den Abonnenten (einschließlich Wiederveröffentlichungsabonnenten) ausgegeben werden. Die Mergereplikation verhindert Schemaänderungen auf dem Abonnenten. Die Transaktionsreplikation verhindert die Änderungen zwar nicht, es können jedoch Fehler bei der Replikation auftreten.  
  
-   An einen Wiederveröffentlichungsabonnenten weitergegebene Änderungen werden standardmäßig an dessen Abonnenten weitergegeben.  
  
-   Verweist die Schemaänderung auf Objekte oder Einschränkungen, die auf dem Verleger, aber nicht auf dem Abonnenten vorhanden sind, ist die Schemaänderung auf dem Verleger erfolgreich, schlägt jedoch auf dem Abonnenten fehl.  
  
-   Alle Objekte auf dem Abonnenten, auf die beim Hinzufügen eines Fremdschlüssels verwiesen wird, müssen denselben Namen und Besitzer aufweisen wie das entsprechende Objekt auf dem Verleger.  
  
-   Ein explizites Hinzufügen, Löschen oder Ändern von Indizes wird nicht unterstützt. Implizit für Einschränkungen erstellte Indizes (wie z. B. Primärschlüsseleinschränkungen) werden unterstützt.  
  
-   Das Ändern oder Löschen von Identitätsspalten, die von der Replikation verwaltet werden, wird nicht unterstützt. Weitere Informationen zur automatischen Verwaltung von Identitätsspalten finden Sie unter [Replizieren von Identitätsspalten](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
-   Schemaänderungen, die nicht deterministische Funktionen einschließen, werden nicht unterstützt, da daraus unterschiedliche Daten auf dem Verleger und dem Abonnenten resultieren können (eine so genannte mangelnde Konvergenz). Wenn Sie beispielsweise folgenden Befehl auf dem Verleger ausgeben: `ALTER TABLE SalesOrderDetail ADD OrderDate DATETIME DEFAULT GETDATE()`, und der Befehl wird auf den Abonnenten repliziert und ausgeführt, dann unterscheiden sich die Werte. Weitere Informationen zu nicht deterministischen Funktionen finden Sie unter [Deterministic and Nondeterministic Functions](../../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
-   Es wird empfohlen, Einschränkungen explizit zu benennen. Wenn eine Einschränkung nicht explizit benannt wird, generiert [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] einen Namen für die Einschränkung, und diese Namen sind auf dem Verleger und jedem Abonnenten unterschiedlich. Dies kann bei der Replikation von Schemaänderungen zu Problemen führen. Wenn Sie z. B. auf dem Verleger eine Spalte löschen und eine abhängige Einschränkung ebenfalls gelöscht wird, wird bei der Replikation versucht, die Einschränkung auf dem Abonnenten zu löschen. Der Löschvorgang auf dem Abonnenten erzeugt jedoch einen Fehler, da die Einschränkung einen anderen Namen hat. Löschen Sie die Einschränkung manuell auf dem Abonnenten, und führen Sie den Merge-Agent anschließend erneut aus, wenn die Synchronisierung aufgrund eines Problems mit dem Einschränkungsnamen einen Fehler erzeugt.  
  
-   Wenn eine Tabelle für die Replikation veröffentlicht wird, ist es nicht möglich, eine Spalte in dieser Tabelle in den Datentyp XML zu ändern, wenn bereits eine Veröffentlichungsmomentaufnahme generiert wurde. Um die Spalte zu ändern, müssen Sie die Replikation zuerst entfernen.  
  
-   READ UNCOMMITTED ist keine unterstützte Isolationsstufe, wenn Sie DDL auf einer veröffentlichten Tabelle ausführen.  
  
-   **SET CONTEXT_INFO** sollte nicht verwendet werden, um den Transaktionskontext zu ändern, in dem Schemaänderungen für veröffentlichte Objekte ausgeführt werden.  
  
#### <a name="adding-columns"></a>Hinzufügen von Spalten  
  
-   Wenn Sie einer Tabelle eine neue Spalte hinzufügen und die Spalte in eine vorhandene Veröffentlichung einschließen möchten, führen Sie ALTER TABLE \<Table> ADD \<Column> aus. Die Spalte wird dann standardmäßig auf alle Abonnenten repliziert. Die Spalte muss NULL-Werte zulassen oder eine Standardeinschränkung einschließen. Weitere Informationen über das Hinzufügen von Spalten finden Sie im Abschnitt "Mergereplikation" in diesem Thema.  
  
-   Wenn Sie einer Tabelle eine neue Spalte hinzufügen und diese Spalte nicht in eine vorhandene Veröffentlichung einschließen möchten, führen Sie ALTER TABLE \<Table> ADD \<Column> aus.  
  
-   Verwenden Sie [sp_articlecolumn &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md), [sp_mergearticlecolumn &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) oder das Dialogfeld **Veröffentlichungseigenschaften – \<Veröffentlichung>**, um eine vorhandene Spalte in eine vorhandene Veröffentlichung einzuschließen.  
  
     Weitere Informationen finden Sie unter [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md). Dies erfordert, dass Sie Abonnements erneut initialisieren.  
  
-   Das Hinzufügen einer Identitätsspalte zu einer veröffentlichten Tabelle wird nicht unterstützt, da ein solcher Vorgang zu Nichtkonvergenz führen kann, wenn die Spalte auf den Abonnenten repliziert wird. Die Werte in der Identitätsspalte auf dem Verleger richten sich nach der Ordnung, in der die Zeilen für die betreffende Tabelle physisch gespeichert sind. Es ist möglich, dass die Zeilen auf dem Abonnenten anders gespeichert sind, sodass der Wert für die Identitätsspalte für dieselben Zeilen unterschiedlich sein kann.  
  
#### <a name="dropping-columns"></a>Löschen von Spalten  
  
-   Wenn Sie eine Spalte aus einer vorhandenen Veröffentlichung löschen und die Spalte aus der Tabelle auf dem Verleger löschen möchten, führen Sie ALTER TABLE \<Table> DROP \<Column> aus. Standardmäßig wird die Spalte dann aus der Tabelle auf allen Abonnenten gelöscht.  
  
-   Verwenden Sie [sp_articlecolumn &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md), [sp_mergearticlecolumn &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) oder das Dialogfeld **Veröffentlichungseigenschaften – \<Veröffentlichung>**, um eine Spalte aus einer vorhandenen Veröffentlichung zu löschen, die Spalte jedoch in der Tabelle auf dem Verleger beizubehalten.  
  
     Weitere Informationen finden Sie unter [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md). Dies erfordert, dass Sie eine neue Momentaufnahme generieren.  
  
-   Die zu löschende Spalte darf nicht in den Filterklauseln eines Artikels einer Veröffentlichung in der Datenbank verwendet werden.  
  
-   Beim Löschen einer Spalte aus einem veröffentlichten Artikel sollten Sie alle Einschränkungen, Indizes oder Eigenschaften der Spalte berücksichtigen, die sich auf die Datenbank auswirken können. Beispiel:  
  
    -   Sie können keine in einem Primärschlüssel verwendeten Spalten aus Artikeln in Transaktionsveröffentlichungen löschen, da die Spalten von der Replikation verwendet werden.  
  
    -   Sie können die rowguid-Spalte nicht aus Artikeln in Mergeveröffentlichungen oder die mstran_repl_version-Spalte aus Artikeln in Transaktionsveröffentlichungen löschen, die das Aktualisieren von Abonnements unterstützen, da diese Spalten von der Replikation verwendet werden.  
  
    -   Indexänderungen werden nicht an die Abonnenten weitergegeben: Wenn Sie eine Spalte auf dem Verleger löschen und ein abhängiger Index ebenfalls gelöscht wird, wird das Löschen des Indexes nicht repliziert. Sie sollten den Index auf dem Abonnenten löschen, bevor Sie die Spalte auf dem Verleger löschen, damit das Löschen der Spalte erfolgreich ausgeführt wird, wenn es vom Verleger auf den Abonnenten repliziert wird. Löschen Sie den Index manuell, und führen Sie den Merge-Agent anschließend erneut aus, wenn die Synchronisierung aufgrund eines Indexes auf dem Abonnenten einen Fehler erzeugt.  
  
    -   Einschränkungen sollten explizit benannt werden, um Löschvorgänge zu ermöglichen. Weitere Informationen finden Sie im Abschnitt "Allgemeine Überlegungen" weiter oben in diesem Thema.  
  
### <a name="transactional-replication"></a>Transaktionsreplikation  
  
-   Schemaänderungen werden zwar an Abonnenten weitergegeben, auf denen frühere Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ausgeführt werden, die DDL-Anweisung sollte jedoch nur Syntax einschließen, die von der Version auf dem Abonnenten unterstützt wird.  
  
     Wenn der Abonnent Daten erneut veröffentlicht, bestehen die einzigen Schemaänderungen im Hinzufügen und Löschen einer Spalte. Diese Änderungen sollten auf dem Verleger mithilfe von [sp_repladdcolumn &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql.md) und [sp_repldropcolumn &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql.md) statt mit der DDL-Syntax ALTER TABLE vorgenommen werden.  
  
-   Schemaänderungen werden auf Nicht-SQL-Server-Abonnenten nicht repliziert.  
  
-   Von Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verlegern werden keine Schemaänderungen weitergegeben.  
  
-   Sie können indizierte Sichten, die als Tabellen repliziert werden, nicht ändern. Indizierte Sichten, die als indizierte Sichten repliziert werden, können geändert werden. Durch die Änderung sind sie jedoch keine indizierten Sichten mehr, sondern werden zu herkömmlichen Sichten.  
  
-   Wenn die Veröffentlichung mit sofort aktualisierbaren Abonnements oder mit Abonnements mit verzögertem Aktualisieren über eine Warteschlange unterstützt, muss das System in einen inaktiven Status versetzt werden, bevor Schemaänderungen vorgenommen werden: jede Aktivität an der veröffentlichten Tabelle muss auf dem Verleger und den Abonnenten angehalten und ausstehende Datenänderungen müssen an alle Knoten weitergegeben werden. Nach der Weitergabe der Schemaänderungen an alle Knoten können die Aktivitäten an den veröffentlichten Tabellen fortgesetzt werden.  
  
-   Befindet sich die Veröffentlichung in einer Peer-zu-Peer-Topologie, muss das System in einen inaktiven Status versetzt werden, bevor Schemaänderungen vorgenommen werden. Weitere Informationen finden Sie unter [Versetzen einer Replikationstopologie in einen inaktiven Status &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md).  
  
-   Wenn Sie einer Tabelle eine timestamp-Spalte hinzufügen und diese wird einer binary(8)-Spalte zugeordnet, dann wird der Artikel für alle aktiven Abonnements erneut initialisiert.  
  
### <a name="merge-replication"></a>Mergereplikation  
  
-   Wie Mergereplikation Schemaänderungen behandeln, hängt ab vom Veröffentlichungskompatibilitätsgrad, und ob die Momentaufnahme auf einheitlichen Modus (Standard) oder auf Zeichenmodus eingestellt ist:  
  
    -   Zum Replizieren von Schemaänderungen muss die Veröffentlichung mindestens einen Kompatibilitätsgrad von 90RTM aufweisen. Wenn Abonnenten frühere Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ausführen oder der Kompatibilitätsgrad niedriger als 90RTM ist, können Sie [sp_repladdcolumn &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql.md) und [sp_repldropcolumn &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql.md) zum Hinzufügen und Löschen von Spalten verwenden. Allerdings sind diese Prozeduren veraltet.  
  
    -   Wenn Sie versuchen, zu einem Artikel eine Spalte mit einem Datentyp hinzuzufügen, der in [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]eingeführt wurde, verhält sich [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] wie folgt:  
  
        ||100RTM, systemeigene Momentaufnahme|100RTM, Momentaufnahme im Zeichenmodus|Alle übrigen Kompatibilitätsgrade|  
        |-|-----------------------------|--------------------------------|------------------------------------|  
        |**hierarchyid**|Änderung zulassen|Änderung blockieren|Änderung blockieren|  
        |**geography** und **geometry**|Änderung zulassen|Änderung zulassen*|Änderung blockieren|  
        |**Filestream**|Änderung zulassen|Änderung blockieren|Änderung blockieren|  
        |**date**, **time**, **datetime2**und **datetimeoffset**|Änderung zulassen|Änderung zulassen*|Änderung blockieren|  
  
         *Abonnenten von SQL Server Compact konvertieren diese Datentypen beim Abonnenten.  
  
-   Falls beim Anwenden einer Schemaänderung ein Fehler auftritt, schlägt die Synchronisierung fehl, und das Abonnement muss erneut initialisiert werden. (Ein Fehler kann z. B. auftreten, wenn ein hinzugefügter Fremdschlüssel auf eine Tabelle verweist, die auf dem Abonnenten nicht verfügbar ist.)  
  
-   Wird eine Schemaänderung an einer Spalte vorgenommen, die von einem Joinfilter oder parametrisierten Filter betroffen ist, müssen Sie alle Abonnements erneut initialisieren und die Momentaufnahme neu generieren.  
  
-   Die Mergereplikation stellt gespeicherte Prozeduren bereit, mit denen Schemaänderungen bei der Problembehandlung ausgelassen werden können. Weitere Informationen finden Sie unter [sp_markpendingschemachange &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md) und [sp_enumeratependingschemachanges &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER VIEW &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-view-transact-sql.md)   
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-procedure-transact-sql.md)   
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-function-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-trigger-transact-sql.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Erneutes Generieren von Transaktionsprozeduren zur Erfassung von Schemaänderungen](../../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md)  
  
  
