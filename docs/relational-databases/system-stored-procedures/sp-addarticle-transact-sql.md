---
title: Sp_addarticle (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/28/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_addarticle
- sp_addarticle_TSQL
helpviewer_keywords: sp_addarticle
ms.assetid: 0483a157-e403-4fdb-b943-23c1b487bef0
caps.latest.revision: "108"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: db34c4936cb02aaf65bd1c8117f54ad3b769f158
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spaddarticle-transact-sql"></a>sp_addarticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt einen Artikel und fügt ihn zu einer Veröffentlichung hinzu. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addarticle [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
    [ , [ @source_table = ] 'source_table' ]  
    [ , [ @destination_table = ] 'destination_table' ]   
    [ , [ @vertical_partition = ] 'vertical_partition' ]   
    [ , [ @type = ] 'type' ]   
    [ , [ @filter = ] 'filter' ]   
    [ , [ @sync_object= ] 'sync_object' ]   
        [ , [ @ins_cmd = ] 'ins_cmd' ]   
    [ , [ @del_cmd = ] 'del_cmd' ]   
        [ , [ @upd_cmd = ] 'upd_cmd' ]   
    [ , [ @creation_script = ] 'creation_script' ]   
    [ , [ @description = ] 'description' ]   
    [ , [ @pre_creation_cmd = ] 'pre_creation_cmd' ]   
    [ , [ @filter_clause = ] 'filter_clause' ]   
    [ , [ @schema_option = ] schema_option ]   
    [ , [ @destination_owner = ] 'destination_owner' ]   
    [ , [ @status = ] status ]   
    [ , [ @source_owner = ] 'source_owner' ]   
    [ , [ @sync_object_owner = ] 'sync_object_owner' ]   
    [ , [ @filter_owner = ] 'filter_owner' ]   
    [ , [ @source_object = ] 'source_object' ]   
    [ , [ @artid = ] article_ID  OUTPUT ]   
    [ , [ @auto_identity_range = ] 'auto_identity_range' ]   
    [ , [ @pub_identity_range = ] pub_identity_range ]   
    [ , [ @identity_range = ] identity_range ]   
    [ , [ @threshold = ] threshold ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @use_default_datatypes = ] use_default_datatypes  
    [ , [ @identityrangemanagementoption = ] identityrangemanagementoption ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @fire_triggers_on_snapshot = ] 'fire_triggers_on_snapshot' ]   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication =** ] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung, die den Artikel enthält. Der Name muss in der Datenbank eindeutig sein. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@article =** ] **"***Artikel***"**  
 Der Name des Artikels. Der Name muss innerhalb der Veröffentlichung eindeutig sein. *Artikel* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@source_table =** ] **"***Source_table***"**  
 Dieser Parameter wurde als veraltet markiert; Verwenden Sie *Source_object* stattdessen.  
  
 *Dieser Parameter wird nicht für Oracle-Verleger unterstützt.*  
  
 [  **@destination_table =** ] **"***Destination_table***"**  
 Ist der Name der Zieltabelle (Abonnementtabelle), falls abweichend vom *Source_table*oder der gespeicherten Prozedur. *Destination_table* ist **Sysname**, hat den Standardwert NULL, d. h., *Source_table* gleich *Destination_table**.*  
  
 [  **@vertical_partition =** ] **"***Vertical_partition***"**  
 Aktiviert und deaktiviert die Spaltenfilterung für einen Tabellenartikel. *Vertical_partition* ist **nchar(5)**, hat den Standardwert "false".  
  
 **"false"** zeigt an, dass keine vertikale Filterung und alle Spalten veröffentlicht.  
  
 **"true"** löscht alle Spalten außer dem deklarierten Primärschlüssel, Spalten ohne Standardwerte NULL-Werte zulässt und Spalten für eindeutige Schlüssel. Spalten werden mit hinzugefügt [Sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md).  
  
 [  **@type =** ] **"***Typ***"**  
 Entspricht dem Artikeltyp. *Typ* ist **Sysname**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**nur Aggregate schema**|Aggregatfunktion vom Typ schema only.|  
|**nur Func schema**|Funktion vom Typ schema only.|  
|**Logbased indizierte Sicht**|Artikel für protokollbasierte indizierte Sicht. Diese Option wird für Oracle-Verleger nicht unterstützt. Für diesen Artikeltyp muss die Basistabelle nicht separat veröffentlicht werden.|  
|**indizierte Sicht Logbased manualboth**|Artikel für protokollbasierte indizierte Sicht mit manuell erstelltem Filter und manuell erstellter Sicht. Diese Option erfordert, dass Sie beide geben *Sync_object* und *Filter* Parameter. Für diesen Artikeltyp muss die Basistabelle nicht separat veröffentlicht werden. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
|**indizierte Sicht Logbased manualfilter**|Artikel für protokollbasierte indizierte Sicht mit manuell erstelltem Filter. Diese Option erfordert, dass Sie beide geben *Sync_object* und *Filter* Parameter. Für diesen Artikeltyp muss die Basistabelle nicht separat veröffentlicht werden. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
|**indizierte Sicht Logbased manualview**|Artikel für protokollbasierte indizierte Sicht mit manuell erstellter Sicht. Diese Option erfordert die Angabe der *Sync_object* Parameter. Für diesen Artikeltyp muss die Basistabelle nicht separat veröffentlicht werden. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
|**nur Schema indizierte Sicht**|Indizierte Sicht vom Typ schema only. Für diesen Artikeltyp muss die Basistabelle ebenfalls veröffentlicht werden.|  
|**Logbased** (Standard)|Protokollbasierter Artikel.|  
|**Logbased manualboth**|Protokollbasierter Artikel mit manuell erstelltem Filter und manuell erstellter Sicht. Diese Option erfordert, dass Sie beide geben *Sync_object* und *Filter* Parameter. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
|**Logbased manualfilter**|Protokollbasierter Artikel mit manuell erstelltem Filter. Diese Option erfordert, dass Sie beide geben *Sync_object* und *Filter* Parameter. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
|**Logbased manualview**|Protokollbasierter Artikel mit manuell erstellter Sicht. Diese Option erfordert die Angabe der *Sync_object* Parameter. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
|**Proc exec**|Repliziert die Ausführung der gespeicherten Prozedur auf alle Abonnenten des Artikels. Diese Option wird für Oracle-Verleger nicht unterstützt. Es wird empfohlen, dass die Verwendung der Option **serializable Proc Exec** anstelle von **Proc Exec**. Weitere Informationen finden Sie im Abschnitt "Typen der gespeicherten Prozedur Artikeln für die Ausführung" in [Publishing Stored Procedure Execution in Transactional Replication](../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md). Nicht verfügbar, wenn Change Data Capture aktiviert ist.|  
|**Proc Schema nur**|Prozedur vom Typ schema only. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
|**Serializable Proc exec**|Repliziert die Ausführung der gespeicherten Prozedur nur, wenn die Prozedur im Kontext einer serialisierbaren Transaktion ausgeführt wird. Diese Option wird für Oracle-Verleger nicht unterstützt.<br /><br /> Die Prozedur muss innerhalb einer expliziten Transaktion für die Ausführung der Prozedur repliziert werden auch ausgeführt werden.|  
|**nur Schema anzeigen**|Sicht vom Typ schema only. Diese Option wird für Oracle-Verleger nicht unterstützt. Wenn diese Option verwendet wird, müssen Sie auch die Basistabelle veröffentlichen.|  
  
 [  **@filter =** ] **"***Filter***"**  
 Entspricht der gespeicherten Prozedur (erstellt mit FOR REPLICATION), mit der die Tabelle horizontal gefiltert wird. *Filter* ist **nvarchar(386)**, hat den Standardwert NULL. [Sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) und [Sp_articlefilter](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) muss manuell ausgeführt werden, um die Ansicht zu erstellen und die gespeicherte Filterprozedur. Bei einem Wert ungleich NULL wird die Filterprozedur nicht erstellt (es wird angenommen, dass die gespeicherte Prozedur manuell erstellt wird).  
  
 [  **@sync_object =** ] **"***Sync_object***"**  
 Entspricht dem Namen der Tabelle oder Sicht, die zum Erzeugen der Datendatei dient, mit der die Momentaufnahme für diesen Artikel dargestellt wird. *Sync_object* ist **nvarchar(386)**, hat den Standardwert NULL. Wenn der Wert NULL, [Sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) wird aufgerufen, um die Sicht verwendet, um die Generierung der Ausgabedatei automatisch zu erstellen. Dieser Schritt erfolgt nach jedem Hinzufügen von Spalten mit [Sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md). Bei einem Wert ungleich NULL wird keine Sicht erstellt (es wird angenommen, dass die Sicht manuell erstellt wird).  
  
 [  **@ins_cmd =** ] **"***Ins_cmd***"**  
 Ist der Replikationsbefehlstyp, der zum Replizieren von Einfügungen für diesen Artikel dient. *Ins_cmd* ist **nvarchar(255)**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**NONE**|Es wird keine Aktion ausgeführt.|  
|**CALL sp_MSins_**<br /> ***Tabelle*** (Standard)<br /><br /> -oder-<br /><br /> **Rufen Sie custom_stored_procedure_name**|Eine gespeicherte Prozedur wird aufgerufen, die auf dem Abonnenten ausgeführt werden soll. Verwenden Sie zur Verwendung dieser Methode der Replikation *Schema_option* , geben die automatische Erstellung der gespeicherten Prozedur, oder erstellen die angegebene gespeicherte Prozedur in der Zieldatenbank jedes Abonnenten des Artikels. *custom_stored_procedure_name* ist der Name einer benutzerdefinierten gespeicherten Prozedur. **Sp_MSins_*Tabelle*** enthält den Namen der Zieltabelle anstelle des dem *_table* -Teils des Parameters. Wenn *Destination_owner* angegeben ist, wird er mit dem Zieltabellennamen Namen vorangestellt. Z. B. für die **"ProductCategory"** -Tabelle im Besitz der **Produktion** Schema auf dem Abonnenten, der Parameter wäre `CALL sp_MSins_ProductionProductCategory`. Für einen Artikel in einer Peer-zu-Peer-Replikationstopologie *_table* wird mit einem GUID-Wert angefügt. Angeben von *custom_stored_procedure_name* wird für Updateabonnenten nicht unterstützt.|  
|**SQL** oder NULL|Repliziert eine INSERT-Anweisung. Für die INSERT-Anweisung werden Werte für alle in dem Artikel veröffentlichten Spalten bereitgestellt. Der folgende Befehl wird bei Einfügungen repliziert:<br /><br /> `INSERT INTO <table name> VALUES (c1value, c2value, c3value, ..., cnvalue)`|  
  
 Weitere Informationen finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)  
  
 [  **@del_cmd =**] **"***Del_cmd***"**  
 Ist der Replikationsbefehlstyp, der zum Replizieren von Löschungen für diesen Artikel dient. *Del_cmd* ist **nvarchar(255)**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**NONE**|Es wird keine Aktion ausgeführt.|  
|**CALLsp_MSdel_**<br /> ***Tabelle*** (Standard)<br /><br /> -oder-<br /><br /> **Rufen Sie custom_stored_procedure_name**|Eine gespeicherte Prozedur wird aufgerufen, die auf dem Abonnenten ausgeführt werden soll. Verwenden Sie zur Verwendung dieser Methode der Replikation *Schema_option* , geben die automatische Erstellung der gespeicherten Prozedur, oder erstellen die angegebene gespeicherte Prozedur in der Zieldatenbank jedes Abonnenten des Artikels. *custom_stored_procedure_name* ist der Name einer benutzerdefinierten gespeicherten Prozedur. **Sp_MSdel_*Tabelle*** enthält den Namen der Zieltabelle anstelle des dem *_table* -Teils des Parameters. Wenn *Destination_owner* angegeben ist, wird er mit dem Zieltabellennamen Namen vorangestellt. Z. B. für die **"ProductCategory"** -Tabelle im Besitz der **Produktion** Schema auf dem Abonnenten, der Parameter wäre `CALL sp_MSdel_ProductionProductCategory`. Für einen Artikel in einer Peer-zu-Peer-Replikationstopologie *_table* wird mit einem GUID-Wert angefügt. Angeben von *custom_stored_procedure_name* wird für Updateabonnenten nicht unterstützt.|  
|**XCALL sp_MSdel_**<br /> ***table***<br /><br /> -oder-<br /><br /> **XCALL custom_stored_procedure_name**|Ruft eine gespeicherte Prozedur auf, die XCALL-Parameter akzeptiert. Verwenden Sie zur Verwendung dieser Methode der Replikation *Schema_option* , geben die automatische Erstellung der gespeicherten Prozedur, oder erstellen die angegebene gespeicherte Prozedur in der Zieldatenbank jedes Abonnenten des Artikels. Die Angabe einer benutzerdefinierten gespeicherten Prozedur ist für Updateabonnenten nicht zulässig.|  
|**SQL** oder NULL|Repliziert eine DELETE-Anweisung. Für die DELETE-Anweisung werden alle Spaltenwerte der Primärschlüssel bereitgestellt. Der folgende Befehl wird bei Löschungen repliziert:<br /><br /> `DELETE FROM <table name> WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
 Weitere Informationen finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)  
  
 [  **@upd_cmd =**] **"***Upd_cmd***"**  
 Ist der Replikationsbefehlstyp, der zum Replizieren von Updates für diesen Artikel dient. *Upd_cmd* ist **nvarchar(255)**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**NONE**|Es wird keine Aktion ausgeführt.|  
|**CALL sp_MSupd_**<br /> ***table***<br /><br /> -oder-<br /><br /> **Rufen Sie custom_stored_procedure_name**|Eine gespeicherte Prozedur wird aufgerufen, die auf dem Abonnenten ausgeführt werden soll. Verwenden Sie zur Verwendung dieser Methode der Replikation *Schema_option* , geben die automatische Erstellung der gespeicherten Prozedur, oder erstellen die angegebene gespeicherte Prozedur in der Zieldatenbank jedes Abonnenten des Artikels.|  
|**MCALL sp_MSupd_**<br /> ***table***<br /><br /> -oder-<br /><br /> **MCALL-custom_stored_procedure_name**|Ruft eine gespeicherte Prozedur auf, die MCALL-Parameter akzeptiert. Verwenden Sie zur Verwendung dieser Methode der Replikation *Schema_option* , geben die automatische Erstellung der gespeicherten Prozedur, oder erstellen die angegebene gespeicherte Prozedur in der Zieldatenbank jedes Abonnenten des Artikels. *custom_stored_procedure_name* ist der Name einer benutzerdefinierten gespeicherten Prozedur. **Sp_MSupd_*Tabelle*** enthält den Namen der Zieltabelle anstelle des dem *_table* -Teils des Parameters. Wenn *Destination_owner* angegeben ist, wird er mit dem Zieltabellennamen Namen vorangestellt. Z. B. für die **"ProductCategory"** -Tabelle im Besitz der **Produktion** Schema auf dem Abonnenten, der Parameter wäre `MCALL sp_MSupd_ProductionProductCategory`. Für einen Artikel in einer Peer-zu-Peer-Replikationstopologie *_table* wird mit einem GUID-Wert angefügt. Die Angabe einer benutzerdefinierten gespeicherten Prozedur ist für Updateabonnenten nicht zulässig.|  
|**SCALL sp_MSupd_**<br /> ***Tabelle*** (Standard)<br /><br /> -oder-<br /><br /> **SCALL custom_stored_procedure_name**|Ruft eine gespeicherte Prozedur auf, die SCALL-Parameter akzeptiert. Verwenden Sie zur Verwendung dieser Methode der Replikation *Schema_option* , geben die automatische Erstellung der gespeicherten Prozedur, oder erstellen die angegebene gespeicherte Prozedur in der Zieldatenbank jedes Abonnenten des Artikels. *custom_stored_procedure_name* ist der Name einer benutzerdefinierten gespeicherten Prozedur. **Sp_MSupd_*Tabelle*** enthält den Namen der Zieltabelle anstelle des dem *_table* -Teils des Parameters. Wenn *Destination_owner* angegeben ist, wird er mit dem Zieltabellennamen Namen vorangestellt. Z. B. für die **"ProductCategory"** -Tabelle im Besitz der **Produktion** Schema auf dem Abonnenten, der Parameter wäre `SCALL sp_MSupd_ProductionProductCategory`. Für einen Artikel in einer Peer-zu-Peer-Replikationstopologie *_table* wird mit einem GUID-Wert angefügt. Die Angabe einer benutzerdefinierten gespeicherten Prozedur ist für Updateabonnenten nicht zulässig.|  
|**XCALL sp_MSupd_**<br /> ***table***<br /><br /> -oder-<br /><br /> **XCALL custom_stored_procedure_name**|Ruft eine gespeicherte Prozedur auf, die XCALL-Parameter akzeptiert. Verwenden Sie zur Verwendung dieser Methode der Replikation *Schema_option* , geben die automatische Erstellung der gespeicherten Prozedur, oder erstellen die angegebene gespeicherte Prozedur in der Zieldatenbank jedes Abonnenten des Artikels. Die Angabe einer benutzerdefinierten gespeicherten Prozedur ist für Updateabonnenten nicht zulässig.|  
|**SQL** oder NULL|Repliziert eine UPDATE-Anweisung. Die UPDATE-Anweisung wird für alle Spaltenwerte und für die Spaltenwerte der Primärschlüssel bereitgestellt. Der folgende Befehl wird bei Updates repliziert:<br /><br /> `UPDATE <table name> SET c1 = c1value, SET c2 = c2value, SET cn = cnvalue WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
> [!NOTE]  
>  Die CALL-, MCALL-, SCALL- und XCALL-Syntax variiert den Umfang der Daten, die an den Abonnenten weitergegeben werden. Die CALL-Syntax übergibt alle Werte für alle eingefügten und gelöschten Spalten. Die SCALL-Syntax übergibt nur die Werte für betroffene Spalten. Die XCALL-Syntax übergibt die Werte für alle Spalten, unabhängig davon, ob diese geändert wurden, einschließlich des vorherigen Werts der Spalte. Weitere Informationen finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)  
  
 [  **@creation_script =**] **"***Creation_script***"**  
 Entspricht dem Pfad und Namen eines optionalen Artikelschemaskripts, mit dem der Artikel in der Abonnementdatenbank erstellt wird. *Creation_script* ist **nvarchar(255)**, hat den Standardwert NULL.  
  
 [  **@description =**] **"***Beschreibung***"**  
 Ist ein beschreibender Eintrag für den Artikel. *Beschreibung* ist **nvarchar(255)**, hat den Standardwert NULL.  
  
 [  **@pre_creation_cmd =**] **"***Pre_creation_cmd***"**  
 Gibt die vom System durchzuführenden Schritte an, wenn es beim Anwenden der Momentaufnahme für diesen Artikel ein vorhandenes Objekt mit demselben Namen beim Abonnenten erkennt. *Pre_creation_cmd* ist **nvarchar(10)**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**keine**|Verwendet keinen Befehl.|  
|**Löschen**|Löscht Daten aus der Zieltabelle vor dem Anwenden der Momentaufnahme. Wird der Artikel horizontal gefiltert, werden nur Daten in Spalten gelöscht, die von der Filterklausel angegeben werden. Wird von Oracle-Verlegern nicht unterstützt, wenn ein horizontaler Filter definiert wurde.|  
|**Drop** (Standard)|Entfernt die Zieltabelle.|  
|**Abschneiden**|Schneidet die Zieltabelle ab. Gilt nicht für ODBC- oder OLE DB-Abonnenten.|  
  
 [  **@filter_clause=**] **"***Filter_clause***"**  
 Eine Einschränkungsklausel (WHERE), die einen horizontalen Filter definiert. Wenn Sie die Einschränkungsklausel eingeben, lassen Sie das Schlüsselwort, in denen. *Filter_clause* ist **Ntext**, hat den Standardwert NULL. Weitere Informationen finden Sie unter [Filtern von veröffentlichten Daten](../../relational-databases/replication/publish/filter-published-data.md).  
  
 [  **@schema_option =**] *Schema_option*  
 Ist eine Bitmaske der Schemagenerierungsoption für den angegebenen Artikel. *Schema_option* ist **binary(8)**, und kann die [| (Bitweises OR) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) Produkt eine oder mehrere der folgenden Werte sind:  
  
> [!NOTE]  
>  Ist dieser Wert NULL, generiert das System automatisch eine gültige Schemaoption für den Artikel, abhängig von anderen Artikeleigenschaften. Die **Default Schema Options** in den Hinweisen angegebene Tabelle wird den Wert, der ausgewählt wird, auf der Grundlage der Kombination des Artikeltyps und des Replikationstyps gezeigt.  
  
|Wert|Description|  
|-----------|-----------------|  
|**0 x 00**|Deaktiviert die Skripterstellung durch den Momentaufnahme-Agent und verwendet *Creation_script*.|  
|**0 x 01**|Generiert das Objekterstellungsskript (CREATE TABLE, CREATE PROCEDURE usw.). Dies ist der Standardwert für alle Artikel mit gespeicherten Prozeduren.|  
|**0 x 02**|Generiert die gespeicherten Prozeduren, die Änderungen für den Artikel weitergeben (falls definiert).|  
|**0 x 04**|Die Skripterstellung für Identitätsspalten erfolgt mithilfe der IDENTITY-Eigenschaft.|  
|**0 x 08**|Replizieren **Zeitstempel** Spalten. Wenn nicht festgelegt, **Zeitstempel** Spalten repliziert werden, als **binäre**.|  
|**0 x 10**|Generiert einen entsprechenden gruppierten Index. Auch wenn diese Option nicht festgelegt ist, Indizes im Zusammenhang mit Primärschlüsseln und unique-Einschränkungen werden generiert, wenn sie bereits in einer veröffentlichten Tabelle definiert sind.|  
|**0 x 20**|Konvertiert benutzerdefinierte Datentypen (UDT) auf dem Abonnenten in Basisdatentypen. Diese Option kann nicht verwendet werden, wenn eine CHECK- oder DEFAULT-Einschränkung für eine UDT-Spalte vorhanden ist, wenn eine UDT-Spalte Teil des Primärschlüssels ist oder wenn eine berechnete Spalte auf eine UDT-Spalte verweist. *Für Oracle-Verlegern nicht unterstützt*.|  
|**0 x 40**|Generiert entsprechende nicht gruppierte Indizes. Auch wenn diese Option nicht festgelegt ist, Indizes im Zusammenhang mit Primärschlüsseln und unique-Einschränkungen werden generiert, wenn sie bereits in einer veröffentlichten Tabelle definiert sind.|  
|**0 x 80**|Repliziert Primärschlüsseleinschränkungen. Alle Indizes bezüglich der Einschränkung werden ebenfalls repliziert, auch wenn Optionen **0 x 10** und **0 x 40** sind nicht aktiviert.|  
|**0 x 100**|Repliziert Benutzertrigger für einen Tabellenartikel, wenn definiert. *Für Oracle-Verlegern nicht unterstützt*.|  
|**0 x 200**|Repliziert Fremdschlüsseleinschränkungen. Wenn die Tabelle, auf die verwiesen wird, nicht Teil einer Veröffentlichung ist, werden keine Fremdschlüsseleinschränkungen für eine veröffentlichte Tabelle repliziert. *Für Oracle-Verlegern nicht unterstützt*.|  
|**0 x 400**|Repliziert CHECK-Einschränkungen. *Für Oracle-Verlegern nicht unterstützt*.|  
|**0 x 800**|Repliziert Standards. *Für Oracle-Verlegern nicht unterstützt*.|  
|**0 x 1000**|Repliziert die Sortierung auf Spaltenebene.<br /><br /> **Hinweis:** diese Option sollte für Oracle-Verleger, damit Groß-/Kleinschreibung bei Vergleichen werden festgelegt werden.|  
|**0 x 2000**|Repliziert erweiterte Eigenschaften, die dem Quellobjekt des veröffentlichten Artikels zugeordnet sind. *Für Oracle-Verlegern nicht unterstützt*.|  
|**0 x 4000**|Repliziert UNIQUE-Einschränkungen. Alle Indizes bezüglich der Einschränkung werden ebenfalls repliziert, auch wenn Optionen **0 x 10** und **0 x 40** sind nicht aktiviert.|  
|**0 x 8000**|Diese Option ist für [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Verleger nicht gültig.|  
|**0 x 10000**|Repliziert CHECK-Einschränkungen als NOT FOR REPLICATION, sodass die Einschränkungen während der Synchronisierung nicht erzwungen werden.|  
|**0 x 20000**|Repliziert FOREIGN KEY-Einschränkungen als NOT FOR REPLICATION, sodass diese Einschränkungen bei der Synchronisierung nicht erzwungen werden.|  
|**0 x 40000**|Repliziert Dateigruppen, die mit einer partitionierten Tabelle oder einem Index verbunden sind.|  
|**0 x 80000**|Repliziert das Partitionsschema für eine partitionierte Tabelle.|  
|**0 x 100000**|Repliziert das Partitionsschema für einen partitionierten Index.|  
|**0 x 200000**|Repliziert Tabellenstatistiken.|  
|**0 x 400000**|Standardbindungen|  
|**0 x 800000**|Regelbindungen|  
|**0 x 1000000**|Volltextindex|  
|**0x2000000**|XML-schemaauflistungen gebunden **Xml** Spalten werden nicht repliziert.|  
|**0x4000000**|Repliziert Indizes für **Xml** Spalten.|  
|**0x8000000**|Legt Schemas an, die auf dem Abonnent noch nicht vorhanden sind.|  
|**0 x 10000000**|Konvertiert **Xml** Spalten **Ntext** auf dem Abonnenten.|  
|**0 x 20000000**|Konvertiert, die große Objekttypen Daten (**nvarchar(max)**, **varchar(max)**, und **varbinary(max)**) eingeführten [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Datentypen, die auf unterstütztwerden[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].|  
|**0 x 40000000**|Berechtigungen für die Replikation.|  
|**0 x 80000000**|Der Versuch, Abhängigkeiten für Objekte zu löschen, die nicht Teil der Veröffentlichung sind.|  
|**0 x 100000000**|Mit dieser Option können Sie das FILESTREAM-Attribut replizieren, wenn er für angegeben wird **varbinary(max)** Spalten. Geben Sie diese Option nicht an, wenn Sie Tabellen auf [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Abonnenten replizieren. Replizieren von Tabellen mit FILESTREAM-Spalten auf [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] -Abonnenten wird unabhängig von der Festlegung dieser Schemaoption nicht unterstützt.<br /><br /> Siehe die verwandte Option **0 x 800000000**.|  
|**0x200000000**|Datum und Uhrzeit-Datentypen konvertiert (**Datum**, **Zeit**, **"DateTimeOffset"**, und **datetime2**) eingeführten [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] an Daten die in früheren Versionen von unterstützten Basisdatentypen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**0x400000000**|Repliziert die Komprimierungsoption für Daten und Indizes. Weitere Informationen finden Sie unter [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
|**0 x 800000000**|Legen Sie diese Option fest, um FILESTREAM-Daten in einer eigenen Dateigruppe auf dem Abonnenten zu speichern. Wenn diese Option nicht festgelegt wird, werden FILESTREAM-Daten in der Standarddateigruppe gespeichert. Bei der Replikation werden keine Dateigruppen erstellt. Daher müssen Sie beim Festlegen dieser Option die Dateigruppe erstellen, bevor Sie die Momentaufnahme auf dem Abonnenten anwenden. Weitere Informationen zum Erstellen von Objekten vor dem Anwenden der Momentaufnahme finden Sie unter [Ausführen von Skripts vor und nach der Momentaufnahme angewendet wird](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).<br /><br /> Siehe die verwandte Option **0 x 100000000**.|  
|**0x1000000000**|Konvertiert die common Language Runtime (CLR) eine benutzerdefinierte Typen (UDTs, die größer als 8000 Bytes in) **varbinary(max)** , sodass Spalten vom Typ UDT auf Abonnenten repliziert werden können, die ausgeführt werden [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x2000000000**|Konvertiert die **Hierarchyid** Datentyp, **varbinary(max)** sodass Spalten vom Typ **Hierarchyid** repliziert werden können, an die Abonnenten, die ausgeführt werden [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Weitere Informationen zur Verwendung von **Hierarchyid** -Spalten in replizierten Tabellen finden Sie unter [Hierarchyid &#40; Transact-SQL &#41; ](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
|**0x4000000000**|Repliziert die gefilterten Indizes in der Tabelle. Weitere Informationen zu gefilterten Indizes finden Sie unter [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).|  
|**0x8000000000**|Konvertiert die **Geography** und **Geometrie** Datentypen zu **varbinary(max)** , sodass Spalten dieser Typen auf Abonnenten repliziert werden können, die ausgeführtwerden[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x10000000000**|Repliziert Indizes für Spalten vom Typ **Geography** und **Geometrie**.|  
|**0x20000000000**|Repliziert das SPARSE-Attribut für Spalten. Weitere Informationen zu diesem Attribut finden Sie unter [Use Sparse Columns](../../relational-databases/tables/use-sparse-columns.md).|  
|**0 x 40000000000**|Aktivieren Sie die Skripterstellung durch den Momentaufnahme-Agent auf eine Speicheroptimierte Tabelle auf dem Abonnenten zu erstellen.|  
|**0x80000000000**|Konvertiert gruppierten Index, der nicht gruppierten Index für Speicheroptimierte Artikel.|  
|**0x400000000000**|Alle nicht gruppierten Columnstore-Indizes für Tabellen repliziert|  
|**0x800000000000**|Repliziert Flitered nicht gruppierten Columnstore-Indizes in Tabellen.|  
|NULL|Die Replikation automatisch aktiviert *Schema_option* auf einen Standardwert hängt dessen Wert der von anderen Artikeleigenschaften. Die in den Hinweisen enthaltene Tabelle "Default Schema Options" zeigt die Standardschemaoptionen auf der Grundlage des Artikeltyps und des Replikationstyps an.<br /><br /> Der Standard für nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Veröffentlichungen ist **0x050D3**.|  
  
 Nicht alle *Schema_option* sind Werte für alle Replikations- oder Artikeltyp gültig. Die **Valid Schema Options** Tabelle im Abschnitt "Hinweise" zeigt die gültigen Schemaoptionen an, die ausgewählt werden können auf der Grundlage der Kombination des Artikeltyps und des Replikationstyps.  
  
 [  **@destination_owner =**] **"***Destination_owner***"**  
 Entspricht dem Namen des Eigentümers des Zielobjekts. *Destination_owner* ist **Sysname**, hat den Standardwert NULL. Wenn *Destination_owner* nicht angegeben ist, wird der Besitzer automatisch anhand der folgenden Regeln angegeben:  
  
|Bedingung|Zielobjektbesitzer|  
|---------------|------------------------------|  
|Die Veröffentlichung generiert die Anfangsmomentaufnahme, die nur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten unterstützt, über das Massenkopieren im einheitlichen Modus.|Standardmäßig auf den Wert der *der Standardwert*.|  
|Veröffentlicht von einem Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verleger.|Standardmäßig wird der Besitzer der Zieldatenbank verwendet.|  
|Die Veröffentlichung generiert die Anfangsmomentaufnahme, die Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten unterstützt, über das Massenkopieren im Zeichenmodus.|Nicht zugewiesen.|  
  
 Unterstützung von nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten *Destination_owner* muss NULL sein.  
  
 [  **@status=**] *Status*  
 Gibt an, ob der Artikel aktiv ist. Zudem werden zusätzliche Optionen für die Weitergabe von Änderungen angegeben. *Status* ist **"tinyint"**, und kann die [| (Bitweises OR) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) Produkt eine oder mehrere der folgenden Werte sind.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Der Artikel ist aktiv.|  
|**8**|Bezieht den Spaltennamen in INSERT-Anweisungen mit ein.|  
|**16** (Standard)|Verwendet parametrisierte Anweisungen.|  
|**24**|Bezieht den Spaltennamen in INSERT-Anweisungen mit ein und verwendet parametrisierte Anweisungen.|  
|**64**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 Ein aktiver Artikel, der parametrisierte Anweisungen verwendet, würde in dieser Spalte beispielsweise den Wert 17 anzeigen. Der Wert **0** bedeutet, dass der Artikel inaktiv ist und keine zusätzlichen Eigenschaften definiert wurden.  
  
 [  **@source_owner =**] **"***der Standardwert***"**  
 Ist der Besitzer des Quellobjekts. *Der Standardwert* ist **Sysname**, hat den Standardwert NULL. *Der Standardwert* für Oracle-Verleger muss angegeben werden.  
  
 [  **@sync_object_owner =**] **"***der Standardwert***"**  
 Entspricht dem Namen des Eigentümers, der den veröffentlichten Artikel definiert. *Der Standardwert* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@filter_owner =**] **"***der Standardwert***"**  
 Ist der Eigentümer des Filters. *Der Standardwert* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@source_object =**] **"***Source_object***"**  
 Entspricht dem zu veröffentlichenden Datenbankobjekt. *Source_object* ist **Sysname**, hat den Standardwert NULL. Wenn *Source_table* NULL ist, *Source_object* darf nicht NULL sein. *Source_object* sollte verwendet werden, anstelle von *Source_table*. Weitere Informationen zu den Objekttypen, die mit der Momentaufnahme- oder Transaktionsreplikation veröffentlicht werden können, finden Sie unter [Veröffentlichen von Daten und Datenbankobjekte](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
 [  **@artid =** ] *Article_ID* **Ausgabe**  
 Entspricht der Artikel-ID des neuen Artikels. *Article_id* ist **Int** hat den Standardwert NULL, und es ist ein OUTPUT-Parameter.  
  
 [  **@auto_identity_range =** ] **"***Auto_identity_range***"**  
 Aktiviert und deaktiviert auf Veröffentlichungsebene die automatische Handhabung von Identitätsbereichen zum Zeitpunkt der Veröffentlichungserstellung. *Auto_identity_range* ist **nvarchar(5)**, und kann einen der folgenden Werte:  
  
|Wert|Description|  
|-----------|-----------------|  
|**true**|Aktiviert die automatische Behandlung von Identitätsbereichen|  
|**false**|Deaktiviert die automatische Behandlung von Identitätsbereichen|  
|Null(Default)|Von Identitätsbereichen wird festgelegt, indem *Identityrangemanagementoption*.|  
  
> [!NOTE]  
>  *Auto_identity_range* ist veraltet und wird nur für Abwärtskompatibilität bereitgestellt. Verwenden Sie *Identityrangemanagementoption* zum Verwaltungsoptionen für Identitätsbereiche angeben. Weitere Informationen finden Sie unter [Replizieren von Identitätsspalten](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 [  **@pub_identity_range =** ] *pub_identity_range-Spalte*  
 Steuert die Bereichsgröße auf dem Verleger aus, wenn der Artikel weist *Identityrangemanagementoption* festgelegt **Auto** oder *Auto_identity_range* festgelegt **"true"** . *Pub_identity_range* ist **"bigint"**, hat den Standardwert NULL. *Für Oracle-Verlegern nicht unterstützt*.  
  
 [  **@identity_range =** ] *Identity_range*  
 Steuert die Bereichsgröße auf dem Abonnenten, wenn der Artikel weist *Identityrangemanagementoption* festgelegt **Auto** oder *Auto_identity_range* festgelegt **"true"** . *Identity_range* ist **"bigint"**, hat den Standardwert NULL. Wird verwendet, wenn *Auto_identity_range* festgelegt ist, um **"true"**. *Für Oracle-Verlegern nicht unterstützt*.  
  
 [  **@threshold =** ] *Schwellenwert*  
 Ist der Prozentsatz-Wert, der steuert, wann der Verteilungs-Agent einen neuen Identitätsbereich zuweist. Wenn der Prozentsatz der Werte angegeben, *Schwellenwert* wird verwendet, erstellt der Verteilungs-Agent einen neuen Identitätsbereich. *Schwellenwert für* ist **"bigint"**, hat den Standardwert NULL. Wird verwendet, wenn *Identityrangemanagementoption* festgelegt ist, um **automatisch** oder *Auto_identity_range* festgelegt ist, um **"true"**. *Für Oracle-Verlegern nicht unterstützt*.  
  
 [  **@force_invalidate_snapshot =** ] *Force_invalidate_snapshot*  
 Bestätigt, dass durch die von dieser gespeicherten Prozedur ausgeführte Aktion möglicherweise eine vorhandene Momentaufnahme ungültig wird. *Force_invalidate_snapshot* ist ein **Bit**, hat den Standardwert 0.  
  
 **0** gibt an, dass durch Hinzufügen eines Artikels nicht die Momentaufnahme ungültig werden kann. Wenn die gespeicherte Prozedur erkennt, dass die Änderungen eine neue Momentaufnahme erfordern, tritt ein Fehler auf, und es werden keine Änderungen durchgeführt.  
  
 **1** gibt an, dass die Berechtigung für die vorhandene Momentaufnahme als veraltet zu markieren und eine neue Momentaufnahme generiert werden durch das Hinzufügen ein Artikels kann dazu führen, dass die Momentaufnahme ungültig wird, und wenn Abonnements vorhanden wäre, die eine neue Momentaufnahme erfordern erhalten werden.  
  
 [  **@use_default_datatypes =** ] *Use_default_datatypes*  
 Gibt an, ob die Zuordnungen des standardmäßigen Spaltendatentyps bei der Veröffentlichung eines Artikels von einem Oracle-Verleger verwendet werden. *Use_default_datatypes* bit und hat den Standardwert 1.  
  
 **1** = der Artikel Standardspalte Zuordnungen verwendet werden. Die Standard-datentypzuordnungen können angezeigt werden, durch das Ausführen [Sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md).  
  
 **0** = benutzerdefinierte artikelspaltenzuordnungen definiert wurden, und daher [Sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) wird nicht aufgerufen werden, indem **Sp_addarticle**.  
  
 Wenn *Use_default_datatypes* festgelegt ist, um **0**, müssen Sie ausführen, [Sp_changearticlecolumndatatype](../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md) einmal für jede spaltenzuordnung, die von der Standardeinstellung geändert wird. Nach der Definition aller benutzerdefinierten spaltenzuordnungen müssen Sie ausführen [Sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md).  
  
> [!NOTE]  
>  Dieser Parameter sollte nur für Oracle-Verleger verwendet werden. Festlegen von *Use_default_datatypes* auf **0** für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger wird ein Fehler generiert.  
  
 [  **@identityrangemanagementoption =** ] *Identityrangemanagementoption*  
 Gibt an, wie die Identitätsbereichsverwaltung für den Artikel gehandhabt wird. *Identityrangemanagementoption* ist **nvarchar(10)**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**keine**|Die Replikation führt keine explizite Identitätsbereichsverwaltung aus. Diese Option wird nur aus Gründen der Abwärtskompatibilität mit früheren Versionen von SQL Server verwendet. Ist für die Peer-Replikation nicht zulässig.|  
|**Manuell**|Markiert die Identitätsspalte mithilfe von NOT FOR REPLICATION, um die manuelle Identitätsbereichsverwaltung zu ermöglichen.|  
|**Auto**|Gibt die automatisierte Verwaltung von Identitätsbereichen an.|  
|Null(Default)|Wird standardmäßig auf **keine** Wenn der Wert der *Auto_identity_range* nicht **"true"**. Standardmäßig **manuelle** in einer Peer-zu-Peer-Topologie standardmäßigen (*Auto_identity_range* wird ignoriert).|  
  
 Für die Abwärtskompatibilität bei den Wert der *Identityrangemanagementoption* NULL ist, den Wert der *Auto_identity_range* aktiviert ist. Jedoch, wenn der Wert der *Identityrangemanagementoption* ist nicht NULL, und klicken Sie dann auf den Wert der *Auto_identity_range* wird ignoriert.  
  
 Weitere Informationen finden Sie unter [Replizieren von Identitätsspalten](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 [  **@publisher =** ] **"***Publisher***"**  
 Gibt einen Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verleger an. *Publisher* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  *Publisher* sollte nicht verwendet werden, beim Hinzufügen eines Artikels zu einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger.  
  
 [  **@fire_triggers_on_snapshot =** ] **"***Fire_triggers_on_snapshot***"**  
 Gibt an, ob replizierte Benutzertrigger beim Anwenden der Anfangsmomentaufnahme ausgeführt werden. *Fire_triggers_on_snapshot* ist **nvarchar(5)**, hat den Standardwert "false". **"true"** bedeutet, dass Benutzertrigger für eine replizierte Tabelle ausgeführt werden, wenn die Momentaufnahme angewendet wird. In der Reihenfolge, damit Trigger repliziert werden der Bitmaskenwert von *Schema_option* muss den Wert enthalten **0 x 100**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_addarticle** momentaufnahmereplikation oder Transaktionsreplikation verwendet wird.  
  
 Standardmäßig werden bei der Replikation keine Spalten in der Quelltabelle veröffentlicht, wenn der Spaltendatentyp nicht von der Replikation unterstützt wird. Wenn Sie eine solche Spalte veröffentlichen müssen, müssen Sie ausführen [Sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) um die Spalte hinzuzufügen.  
  
 Wird einer Veröffentlichung, die die Peer-zu-Peer-Transaktionsreplikation unterstützt, ein Artikel hinzugefügt, gelten die folgenden Einschränkungen:  
  
-   Parametrisierte Anweisungen müssen für alle logbased-Artikel angegeben werden. Müssen Sie auch **16** in der *Status* Wert.  
  
-   Name und Besitzer der Ziel- und der Quelltabelle müssen übereinstimmen.  
  
-   Der Artikel kann nicht horizontal oder vertikal gefiltert werden.  
  
-   Die automatische Identitätsbereichsverwaltung wird nicht unterstützt. Geben Sie einen Wert manuell für *Identityrangemanagementoption*.  
  
-   Wenn eine **Zeitstempel** Spalte in der Tabelle vorhanden ist, müssen Sie 0 x 08 in auch *Schema_option* zum Replizieren der Spalte als **Zeitstempel**.  
  
-   Der Wert **SQL** kann nicht angegeben werden, für die *Ins_cmd*, *Upd_cmd*, und *Del_cmd*.  
  
 Weitere Informationen finden Sie unter [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 Wenn Sie Objekte veröffentlichen, werden ihre Definitionen auf Abonnenten kopiert. Wenn Sie ein Datenbankobjekt veröffentlichen, das von mindestens einem anderen Objekt abhängig ist, müssen Sie alle Objekte veröffentlichen, auf die verwiesen wird. Wenn Sie beispielsweise eine Sicht veröffentlichen, die von einer Tabelle abhängt, muss auch die Tabelle veröffentlicht werden.  
  
 Wenn *Vertical_partition* festgelegt ist, um **"true"**, **Sp_addarticle** orientiert sich die Erstellung der Sicht, bis [Sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) (nach aufgerufen wird der letzte [Sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) hinzugefügt wird).  
  
 Wenn die Veröffentlichung updateabonnements zulässt und die veröffentlichte Tabelle verfügt nicht über eine **"uniqueidentifier"** Spalte **Sp_addarticle** Fügt eine **"uniqueidentifier"** Spalte in der Tabelle automatisch.  
  
 Wenn auf einen Abonnenten repliziert werden, die keine Instanz ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (heterogene Replikation), nur [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen unterstützt **einfügen**, **UPDATE**, und **Löschen** Befehle.  
  
 Wenn der Protokollleser-Agent ausgeführt wird, kann das Hinzufügen eines Artikel zu einer Peer-zu-Peer-Veröffentlichung einen Deadlock zwischen dem Protokolllese-Agent und dem Prozess verursachen,der den Artikel hinzufügt. Damit Sie dieses Problem vermeiden, bevor Sie einer Peer-zu-Peer-Veröffentlichung einen Artikel hinzufügen, verwenden Sie den Replikationsmonitor, um den Protokolllese-Agent auf dem Knoten zu beenden, auf dem Sie den Artikel hinzufügen möchten. Starten Sie den Protokolllese-Agent neu, nachdem Sie den Artikel hinzugefügt haben.  
  
 Beim Festlegen von `@del_cmd = 'NONE'` oder `@ins_cmd = 'NONE'`, die Weitergabe von **aktualisieren** Befehle können diese Befehle nicht gesendet werden, tritt ein begrenztes Update ebenfalls betroffen sein. (Ein begrenztes Update ist eine Art von UPDATE-Anweisung vom Verleger, die als DELETE/INSERT-Paar auf dem Abonnenten repliziert wird).  
  
## <a name="default-schema-options"></a>Default Schema Options  
 Diese Tabelle wird beschrieben, den Standardwert, wenn durch die Replikation festgelegte *Schema_options* ist nicht angegeben, durch den Benutzer, in denen dieser Wert hängt von den Replikationstyp (oben) und den Artikeltyp (in der ersten Spalte angezeigt).  
  
|Artikeltyp|Replikationstyp||  
|------------------|----------------------|------|  
||Transaktion|Momentaufnahme|  
|**nur Aggregate schema**|**0 x 01**|**0 x 01**|  
|**nur Func schema**|**0 x 01**|**0 x 01**|  
|**nur Schema indizierte Sicht**|**0 x 01**|**0 x 01**|  
|**Logbased indizierte Sicht**|**0x30F3**|**0x3071**|  
|**indizierte Sicht Logbase manualboth**|**0x30F3**|**0x3071**|  
|**indizierte Sicht Logbased manualfilter**|**0x30F3**|**0x3071**|  
|**indizierte Sicht Logbased manualview**|**0x30F3**|**0x3071**|  
|**logbased**|**0x30F3**|**0x3071**|  
|**Logbased manualfilter**|**0x30F3**|**0x3071**|  
|**Logbased manualview**|**0x30F3**|**0x3071**|  
|**Proc exec**|**0 x 01**|**0 x 01**|  
|**Proc Schema nur**|**0 x 01**|**0 x 01**|  
|**Serializable Proc exec**|**0 x 01**|**0 x 01**|  
|**nur Schema anzeigen**|**0 x 01**|**0 x 01**|  
  
> [!NOTE]  
>  Wenn eine Veröffentlichung aktiviert ist, verzögerte Update für eine *Schema_option* Wert **0 x 80** wird auf den Standardwert in der Tabelle aufgeführten hinzugefügt. Die Standardeinstellung *Schema_option* für einen nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Veröffentlichung ist **0x050D3**.  
  
## <a name="valid-schema-options"></a>Valid Schema Options  
 Diese Tabelle beschreibt die zulässigen Werte von *Schema_option* basierend auf dem Replikationstyp (oben) und den Artikeltyp (in der ersten Spalte angezeigt).  
  
|Artikeltyp|Replikationstyp||  
|------------------|----------------------|------|  
||Transaktion|Momentaufnahme|  
|**logbased**|Alle Optionen|Alle Optionen jedoch **0 x 02**|  
|**Logbased manualfilter**|Alle Optionen|Alle Optionen jedoch **0 x 02**|  
|**Logbased manualview**|Alle Optionen|Alle Optionen jedoch **0 x 02**|  
|**Logbased indizierte Sicht**|Alle Optionen|Alle Optionen jedoch **0 x 02**|  
|**indizierte Sicht Logbased manualfilter**|Alle Optionen|Alle Optionen jedoch **0 x 02**|  
|**indizierte Sicht Logbased manualview**|Alle Optionen|Alle Optionen jedoch **0 x 02**|  
|**indizierte Sicht Logbase manualboth**|Alle Optionen|Alle Optionen jedoch **0 x 02**|  
|**Proc exec**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0x8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, und **0 x 80000000**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0x8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, und **0 x 80000000**|  
|**Serializable Proc exec**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0x8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, und **0 x 80000000**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0x8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, und **0 x 80000000**|  
|**Proc Schema nur**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0x8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, und **0 x 80000000**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0x8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, und **0 x 80000000**|  
|**nur Schema anzeigen**|**0 x 01**, **0x010**, **0 x 020**, **0 x 040**, **0 x 0100**, **0 x 2000**, **0 x 40000**, **0 x 100000**, **0 x 200000**, **0 x 400000**, **0 x 800000**,  **0x2000000**, **0x8000000**, **0 x 40000000**, und **0 x 80000000**|**0 x 01**, **0x010**, **0 x 020**, **0 x 040**, **0 x 0100**, **0 x 2000**, **0 x 40000**, **0 x 100000**, **0 x 200000**, **0 x 400000**, **0 x 800000**,  **0x2000000**, **0x8000000**, **0 x 40000000**, und **0 x 80000000**|  
|**nur Func schema**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0x8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, und **0 x 80000000**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0x8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, und **0 x 80000000**|  
|**nur Schema indizierte Sicht**|**0 x 01**, **0x010**, **0 x 020**, **0 x 040**, **0 x 0100**, **0 x 2000**, **0 x 40000**, **0 x 100000**, **0 x 200000**, **0 x 400000**, **0 x 800000**,  **0x2000000**, **0x8000000**, **0 x 40000000**, und **0 x 80000000**|**0 x 01**, **0x010**, **0 x 020**, **0 x 040**, **0 x 0100**, **0 x 2000**, **0 x 40000**, **0 x 100000**, **0 x 200000**, **0 x 400000**, **0 x 800000**,  **0x2000000**, **0x8000000**, **0 x 40000000**, und **0 x 80000000**|  
  
> [!NOTE]  
>  Für aktualisierbare Veröffentlichungen in der Warteschlange die *Schema_option* Werte **0 x 8000** und **0 x 80** muss aktiviert sein. Die unterstützten *Schema_option* -Werte für nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publikationen sind: **0 x 01**, **0 x 02**, **0 x 10**,  **0 x 40**, **0 x 80**, **0 x 1000**, **0 x 4000** und **0 x 8000**.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-addarticle-transact-sql_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_addarticle**.  
  
## <a name="see-also"></a>Siehe auch  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_articlefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [Sp_articleview &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Sp_helparticlecolumns &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [Gespeicherte Replikationsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
