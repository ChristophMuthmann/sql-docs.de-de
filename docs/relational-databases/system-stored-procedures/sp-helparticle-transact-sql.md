---
title: Sp_helparticle (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helparticle_TSQL
- sp_helparticle
helpviewer_keywords:
- sp_helparticle
ms.assetid: 9c4a1a88-56f1-45a0-890c-941b8e0f0799
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 823862d782cafd605dd7f4686dcdb3b4baa6a0b8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sphelparticle-transact-sql"></a>sp_helparticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt Informationen zu einem Artikel an. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt. Für Oracle-Verleger wird diese gespeicherte Prozedur auf dem Verteiler auf jeder Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helparticle [ @publication = ] 'publication'   
    [ , [ @article = ] 'article' ]  
    [ , [ @returnfilter = ] returnfilter ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @found = ] found OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication =**] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@article=**] **"***Artikel***"**  
 Der Name eines Artikels in der Veröffentlichung. *Artikel* ist **Sysname**, hat den Standardwert  **%** . Wenn *Artikel* ist nicht angegeben wird, werden Informationen zu allen Artikeln für die angegebene Veröffentlichung zurückgegeben.  
  
 [  **@returnfilter=**] *Returnfilter*  
 Gibt an, ob die Filterklausel zurückgegeben werden soll. *Returnfilter* ist **Bit**, hat den Standardwert **1**, wobei die Filterklausel zurückgegeben.  
  
 [  **@publisher** =] **"***Publisher***"**  
 Gibt einen nicht-[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger. *Publisher* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  *Publisher* nicht angegeben werden beim Anfordern von Informationen für einen Artikel von veröffentlicht eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger.  
  
 [  **@found=** ] *gefunden* Ausgabe  
 Nur interne Verwendung.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Artikel-id**|**int**|ID des Artikels.|  
|**Artikelnamen**|**sysname**|Der Name des Artikels.|  
|**Basisobjekt**|**nvarchar(257)**|Name der zugrunde liegenden Tabelle, dargestellt durch den Artikel oder die gespeicherte Prozedur.|  
|**Zielobjekt**|**sysname**|Name der Zieltabelle (Abonnement).|  
|**Synchronisierungsobjekt**|**nvarchar(257)**|Name der Sicht, die den veröffentlichten Artikel definiert.|  
|**Typ**|**smallint**|Der Artikeltyp:<br /><br /> **1** = Protokollbasierter.<br /><br /> **3** = Protokollbasierter mit manuell erstelltem Filter.<br /><br /> **5** = Protokollbasierter mit manuell erstellter Sicht.<br /><br /> **7** = Protokollbasierter mit manuell erstelltem Filter und manuell erstellter Sicht.<br /><br /> **8** = Ausführung einer gespeicherten Prozedur.<br /><br /> **24** = Ausführung einer serialisierbaren gespeicherten Prozedur.<br /><br /> **32** = gespeicherte Prozedur (Schema only).<br /><br /> **64** = Sicht (Schema only).<br /><br /> **96** = Aggregatfunktion (nur Schema).<br /><br /> **128** = Funktion (Schema only).<br /><br /> **257** = protokollbasierte indizierte Sicht.<br /><br /> **259** = protokollbasierte indizierte Sicht mit manuell erstelltem Filter.<br /><br /> **261** = protokollbasierte indizierte Sicht mit manuell erstellter Sicht.<br /><br /> **263** = protokollbasierte indizierte Sicht mit manuell erstelltem Filter und manuell erstellter Sicht.<br /><br /> **320** = indizierte Sicht (Schema only).<br /><br />|  
|**status**|**tinyint**|Kann die [& (bitweises AND)](../../t-sql/language-elements/bitwise-and-transact-sql.md) Ergebnis von einer oder mehrerer dieser Artikeleigenschaften:<br /><br /> **0 x 00** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **0 x 01** = Artikel ist aktiv.<br /><br /> **0 x 08** = den Spaltennamen in Einfügeanweisungen einschließen.<br /><br /> **0 x 16** = parametrisierte Anweisungen verwenden.<br /><br /> **0 x 32** = parametrisierte Anweisungen verwenden und den Spaltennamen in Einfügeanweisungen einschließen.|  
|**filter**|**nvarchar(257)**|Die gespeicherte Prozedur, mit der die Tabelle horizontal gefiltert wird. Diese gespeicherte Prozedur muss mit der FOR REPLICATION-Klausel erstellt werden.|  
|**Beschreibung**|**nvarchar(255)**|Beschreibungseintrag für den Artikel.|  
|**insert_command**|**nvarchar(255)**|Der Replikationsbefehlstyp, der zur Replikation von Einfügungen bei Tabellenartikeln verwendet wird. Weitere Informationen finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)|  
|**update_command**|**nvarchar(255)**|Der Replikationsbefehlstyp, der zur Replikation von Updates bei Tabellenartikeln verwendet wird. Weitere Informationen finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)|  
|**delete_command**|**nvarchar(255)**|Der Replikationsbefehlstyp, der zur Replikation von Löschungen bei Tabellenartikeln verwendet wird. Weitere Informationen finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)|  
|**Pfad zum Erstellen eines Skripts**|**nvarchar(255)**|Pfad und Name eines Artikelschemaskripts, mit dem Zieltabellen erstellt werden.|  
|**vertikale Partitionierung**|**bit**|Ist, gibt an, ob die vertikale Partitionierung für den Artikel aktiviert ist. ein Wert von **1** bedeutet, dass die vertikale Partitionierung aktiviert ist.|  
|**pre_creation_cmd**|**tinyint**|Der Vorabbefehl für die Anweisungen DROP TABLE, DELETE TABLE oder TRUNCATE TABLE.|  
|**filter_clause**|**ntext**|WHERE-Klausel für das horizontale Filtern.|  
|**schema_option**|**Binary(8)**|Bitmuster der Option zur Schemaerstellung für den angegebenen Artikel. Eine vollständige Liste der **Schema_option** -Werte finden Sie in [Sp_addarticle &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).|  
|**dest_owner**|**sysname**|Name des Besitzers des Zielobjekts.|  
|**Der Standardwert**|**sysname**|Besitzer des Quellobjekts.|  
|**unqua_source_object**|**sysname**|Name des Quellobjekts, ohne den Namen des Besitzers.|  
|**Der Standardwert**|**sysname**|Besitzer der Sicht, die den veröffentlichten Artikel definiert. zugreifen.|  
|**unqualified_sync_object**|**sysname**|Name der Sicht, die den veröffentlichten Artikel definiert, ohne den Namen des Besitzers.|  
|**Der Standardwert**|**sysname**|Besitzer des Filters.|  
|**unqua_filter**|**sysname**|Name des Filters, ohne den Namen des Besitzers.|  
|**auto_identity_range**|**int**|Flag, das anzeigt, ob die automatische Behandlung von Identitätsbereichen für die Veröffentlichung bei ihrer Erstellung aktiviert wurde. **1** bedeutet, dass der automatische Identitätsbereich aktiviert ist; **0** bedeutet, dass er deaktiviert ist.|  
|**publisher_identity_range**|**int**|Bereichsgröße des Identitätsbereichs auf dem Verleger, wenn der Artikel weist *Identityrangemanagementoption* festgelegt **Auto** oder **Auto_identity_range** festgelegt  **"true"**.|  
|**identity_range**|**bigint**|Bereichsgröße des Identitätsbereichs auf dem Abonnenten, wenn der Artikel weist *Identityrangemanagementoption* festgelegt **Auto** oder **Auto_identity_range** festgelegt  **"true"**.|  
|**Schwellenwert**|**bigint**|Prozentwert, der anzeigt, wann der Verteilungs-Agent einen neuen Identitätsbereich zuweist.|  
|**identityrangemanagementoption**|**int**|Gibt die für den Artikel behandelte Identitätsbereichsverwaltung an.|  
|**fire_triggers_on_snapshot**|**bit**|Gibt an, ob replizierte Benutzertrigger beim Anwenden der Anfangsmomentaufnahme ausgeführt werden.<br /><br /> **1** = Benutzertrigger werden ausgeführt.<br /><br /> **0** = Benutzertrigger werden nicht ausgeführt.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helparticle** wird bei Momentaufnahme- und Transaktionsreplikation verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** festen Serverrolle, die **Db_owner** festen Datenbankrolle oder der veröffentlichungszugriffsliste für die aktuelle Veröffentlichung kann ausführen **Sp_helparticle**.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_helptranarticle](../../relational-databases/replication/codesnippet/tsql/sp-helparticle-transact-_1.sql)]  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Ändern von Artikeleigenschaften](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [Sp_addarticle &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
