---
title: Sp_changearticle (Transact-SQL) | Microsoft Docs
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
- sp_changearticle
- sp_changearticle_TSQL
helpviewer_keywords: sp_changearticle
ms.assetid: 24c33ca5-f03a-4417-a267-131ca5ba6bb5
caps.latest.revision: "77"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3dacb8a0f83084d61c7ca55c5ae093bb57876b82
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="spchangearticle-transact-sql"></a>sp_changearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Eigenschaften eines Artikels in einer Transaktions- oder Momentaufnahmeveröffentlichung. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_changearticle [ [@publication= ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication=**] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung, die den Artikel enthält. *Veröffentlichung* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@article=**] **"***Artikel***"**  
 Entspricht dem Namen des Artikels, dessen Eigenschaft zu ändern ist. *Artikel* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@property=**] **"***Eigenschaft***"**  
 Entspricht einer zu ändernden Artikeleigenschaft. *Eigenschaft* ist **nvarchar(100)**.  
  
 [  **@value=**] **"***Wert***"**  
 Entspricht dem neuen Wert der Artikeleigenschaft. *Wert* ist **nvarchar(255)**.  
  
 Diese Tabelle beschreibt die Eigenschaften von Artikeln und die Werte für diese Eigenschaften.  
  
|Eigenschaft|Werte|Description|  
|--------------|------------|-----------------|  
|**creation_script**||Pfad und Name eines Artikelschemaskripts, mit dem Zieltabellen erstellt werden. Die Standardeinstellung ist NULL.|  
|**del_cmd**||Die auszuführende DELETE-Anweisung; andernfalls wird die Löschoperation aus dem Protokoll hergeleitet.|  
|**Beschreibung**||Ein neuer Beschreibungseintrag für den Artikel.|  
|**dest_object**||Dieser Parameter wird aus Gründen der Abwärtskompatibilität bereitgestellt. Verwendung **Dest_table**.|  
|**dest_table**||Die neue Zieltabelle.|  
|**destination_owner**||Name des Besitzers des Zielobjekts.|  
|**filter**||Die neue gespeicherte Prozedur, mit der die Tabelle gefiltert werden soll (horizontales Filtern). Die Standardeinstellung ist NULL. Kann bei der Peer-zu-Peer-Replikation für Veröffentlichungen nicht geändert werden.|  
|**fire_triggers_on_snapshot**|**true**|Replizierte Benutzertrigger werden ausgeführt, wenn die Anfangsmomentaufnahme angewendet wird.<br /><br /> Hinweis: für Trigger repliziert werden der Bitmaskenwert von *Schema_option* muss den Wert enthalten **0 x 100**.|  
||**false**|Replizierte Benutzertrigger werden nicht ausgeführt, wenn die Anfangsmomentaufnahme angewendet wird.|  
|**identity_range**||Steuert die Größe der zugeordneten Identitätsbereiche, die am Abonnent zugeordnet wurden. Wird für die Peer-zu-Peer-Replikation nicht unterstützt.|  
|**ins_cmd**||Die auszuführende INSERT-Anweisung; andernfalls wird die Operation aus dem Protokoll hergeleitet.|  
|**pre_creation_cmd**||Ein Vorabbefehl, mit dem die Zieltabelle entfernt, gelöscht oder abgeschnitten werden kann, bevor die Synchronisierung angewendet wird.|  
||**keine**|Verwendet keinen Befehl.|  
||**Löschen**|Entfernt die Zieltabelle.|  
||**Löschen**|Löscht die Zieltabelle.|  
||**Abschneiden**|Schneidet die Zieltabelle ab.|  
|**pub_identity_range-Spalte**||Steuert die Größe der zugeordneten Identitätsbereiche, die am Abonnent zugeordnet wurden. Wird für die Peer-zu-Peer-Replikation nicht unterstützt.|  
|**schema_option**||Gibt die Bitmap der Schemagenerierungsoption für den angegebenen Artikel an. *Schema_option* ist **binary(8)**. Weitere Informationen finden Sie im Abschnitt mit den Hinweisen weiter unten in diesem Thema.|  
||**0 x 00**|Beschreibt die Skripterstellung durch den Momentaufnahme-Agent.|  
||**0 x 01**|Generiert die Objekterstellung (CREATE TABLE, CREATE PROCEDURE usw.).|  
||**0 x 02**|Generiert die gespeicherten Prozeduren, die Änderungen für den Artikel weitergeben (falls definiert).|  
||**0 x 04**|Die Skripterstellung für Identitätsspalten erfolgt mithilfe der IDENTITY-Eigenschaft.|  
||**0 x 08**|Replizieren **Zeitstempel** Spalten. Wenn nicht festgelegt, **Zeitstempel** Spalten repliziert werden, als **binäre**.|  
||**0 x 10**|Generiert einen entsprechenden gruppierten Index.|  
||**0 x 20**|Konvertiert benutzerdefinierte Datentypen (UDT) auf dem Abonnenten in Basisdatentypen. Diese Option kann nicht verwendet werden, wenn eine CHECK- oder DEFAULT-Einschränkung für eine UDT-Spalte vorhanden ist, wenn eine UDT-Spalte Teil des Primärschlüssels ist oder wenn eine berechnete Spalte auf eine UDT-Spalte verweist. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
||**0 x 40**|Generiert entsprechende nicht gruppierte Indizes.|  
||**0 x 80**|Schließt die deklarative referenzielle Integrität für die Primärschlüssel ein.|  
||**0 x 100**|Repliziert Benutzertrigger für einen Tabellenartikel, wenn definiert.|  
||**0 x 200**|Repliziert FOREIGN KEY-Einschränkungen. Wenn die Tabelle, auf die verwiesen wird, nicht Teil einer Veröffentlichung ist, werden für eine veröffentlichte Tabelle keine FOREIGN KEY-Einschränkungen repliziert.|  
||**0 x 400**|Repliziert CHECK-Einschränkungen.|  
||**0 x 800**|Repliziert Standards.|  
||**0 x 1000**|Repliziert die Sortierung auf Spaltenebene.|  
||**0 x 2000**|Repliziert erweiterte Eigenschaften, die dem Quellobjekt des veröffentlichten Artikels zugeordnet sind.|  
||**0 x 4000**|Repliziert eindeutige Schlüssel, wenn auf einem Tabellenartikel definiert.|  
||**0 x 8000**|Repliziert den Primärschlüssel und eindeutige Schlüssel eines Tabellenartikels als Einschränkungen mithilfe von ALTER TABLE-Anweisungen.<br /><br /> Hinweis: Diese Option ist veraltet. Verwendung **0 x 80** und **0 x 4000** stattdessen.|  
||**0 x 10000**|Repliziert CHECK-Einschränkungen als NOT FOR REPLICATION, sodass die Einschränkungen während der Synchronisierung nicht erzwungen werden.|  
||**0 x 20000**|Repliziert FOREIGN KEY-Einschränkungen als NOT FOR REPLICATION, sodass diese Einschränkungen bei der Synchronisierung nicht erzwungen werden.|  
||**0 x 40000**|Repliziert Dateigruppen, die mit einer partitionierten Tabelle oder einem Index verbunden sind.|  
||**0 x 80000**|Repliziert das Partitionsschema für eine partitionierte Tabelle.|  
||**0 x 100000**|Repliziert das Partitionsschema für einen partitionierten Index.|  
||**0 x 200000**|Repliziert Tabellenstatistiken.|  
||**0 x 400000**|Standardbindungen|  
||**0 x 800000**|Regelbindungen|  
||**0 x 1000000**|Volltextindex|  
||**0x2000000**|XML-schemaauflistungen gebunden **Xml** Spalten werden nicht repliziert.|  
||**0x4000000**|Repliziert Indizes für **Xml** Spalten.|  
||**0x8000000**|Legt Schemas an, die auf dem Abonnent noch nicht vorhanden sind.|  
||**0 x 10000000**|Konvertiert **Xml** Spalten **Ntext** auf dem Abonnenten.|  
||**0 x 20000000**|Konvertiert, die große Objekttypen Daten (**nvarchar(max)**, **varchar(max)**, und **varbinary(max)**), die in eingeführt wurden [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Datentypen, die unterstützt werden auf [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].|  
||**0 x 40000000**|Berechtigungen für die Replikation.|  
||**0 x 80000000**|Der Versuch, Abhängigkeiten für Objekte zu löschen, die nicht Teil der Veröffentlichung sind.|  
||**0 x 100000000**|Mit dieser Option können Sie das FILESTREAM-Attribut replizieren, wenn er für angegeben wird **varbinary(max)** Spalten. Geben Sie diese Option nicht an, wenn Sie Tabellen auf [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Abonnenten replizieren. Replizieren von Tabellen mit FILESTREAM-Spalten auf [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] -Abonnenten wird unabhängig von der Festlegung dieser Schemaoption nicht unterstützt.<br /><br /> Siehe die verwandte Option **0 x 800000000**.|  
||**0x200000000**|Datum und Uhrzeit-Datentypen konvertiert (**Datum**, **Zeit**, **"DateTimeOffset"**, und **datetime2**), die in eingeführt wurden [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Datentypen, die in früheren Versionen von unterstützt werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**0x400000000**|Repliziert die Komprimierungsoption für Daten und Indizes. Weitere Informationen finden Sie unter [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
||**0 x 800000000**|Legen Sie diese Option fest, um FILESTREAM-Daten in einer eigenen Dateigruppe auf dem Abonnenten zu speichern. Wenn diese Option nicht festgelegt wird, werden FILESTREAM-Daten in der Standarddateigruppe gespeichert. Bei der Replikation werden keine Dateigruppen erstellt. Daher müssen Sie beim Festlegen dieser Option die Dateigruppe erstellen, bevor Sie die Momentaufnahme auf dem Abonnenten anwenden. Weitere Informationen zum Erstellen von Objekten vor dem Anwenden der Momentaufnahme finden Sie unter [Ausführen von Skripts vor und nach der Momentaufnahme angewendet wird](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).<br /><br /> Siehe die verwandte Option **0 x 100000000**.|  
||**0x1000000000**|Konvertiert die common Language Runtime (CLR) eine benutzerdefinierte Typen (UDTs größer als 8000 Bytes in) **varbinary(max)** , sodass Spalten vom Typ UDT auf Abonnenten repliziert werden können, die ausgeführt werden [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||**0x2000000000**|Konvertiert die **Hierarchyid** Datentyp, **varbinary(max)** sodass Spalten vom Typ **Hierarchyid** repliziert werden können, an die Abonnenten, die ausgeführt werden [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Weitere Informationen zur Verwendung von **Hierarchyid** -Spalten in replizierten Tabellen finden Sie unter [Hierarchyid &#40; Transact-SQL &#41; ](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
||**0x4000000000**|Repliziert die gefilterten Indizes in der Tabelle. Weitere Informationen zu gefilterten Indizes finden Sie unter [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).|  
||**0x8000000000**|Konvertiert die **Geography** und **Geometrie** Datentypen zu **varbinary(max)** , sodass Spalten dieser Typen auf Abonnenten repliziert werden können, die ausgeführtwerden[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||**0x10000000000**|Repliziert Indizes für Spalten vom Typ **Geography** und **Geometrie**.|  
||**0x20000000000**|Repliziert das SPARSE-Attribut für Spalten. Weitere Informationen zu diesem Attribut finden Sie unter [Use Sparse Columns](../../relational-databases/tables/use-sparse-columns.md).|  
||**0 x 40000000000**|Aktivieren Sie die Skripterstellung durch den Momentaufnahme-Agent zum Erstellen einer speicheroptimierten Tabelle auf dem Abonnenten.|  
||**0x80000000000**|Konvertiert gruppierten Index, der nicht gruppierten Index für Speicheroptimierte Artikel.|  
|**status**||Gibt den neuen Status der Eigenschaft an.|  
||**horizontale Partitionen von DTS**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
||**Einschließen von Spaltennamen**|Spaltennamen sind in der replizierten INSERT-Anweisung enthalten.|  
||**keine Spaltennamen**|Spaltennamen sind nicht in der replizierten INSERT-Anweisung enthalten.|  
||**keine horizontale Partitionen von dts**|Die horizontale Partition für den Artikel wird nicht durch ein transformierbares Abonnement definiert.|  
||**keine**|Löscht alle Statusoptionen in der [Sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md) -Tabelle und kennzeichnet den Artikel als inaktiv.|  
||**Parameter**|Änderungen werden an den Abonnenten mit parametrisierten Befehlen weitergegeben. Dies ist die Standardeinstellung für einen neuen Artikel.|  
||**Zeichenfolgenliterale**|Änderungen werden an den Abonnenten mit Werten von Literalzeichenfolgen weitergegeben.|  
|**sync_object**||Der Name der Tabelle oder Sicht, mit der eine Synchronisierungsausgabedatei erstellt wird. Die Standardeinstellung ist NULL. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
|**Tabellenbereich**||Gibt den Tabellenbereich an, der von der Protokollierungstabelle für einen Artikel verwendet wird, der von einer Oracle-Datenbank veröffentlicht wird. Weitere Informationen finden Sie unter [Verwalten von Oracle-Tabellenbereichen](../../relational-databases/replication/non-sql/manage-oracle-tablespaces.md).|  
|**Schwellenwert**||Der Prozentwert, der steuert, wann der Verteilungs-Agent einen neuen Identitätsbereich zuweist. Wird für die Peer-zu-Peer-Replikation nicht unterstützt.|  
|**type**||Diese Option wird für Oracle-Verleger nicht unterstützt.|  
||**logbased**|Protokollbasierter Artikel.|  
||**Logbased manualboth**|Protokollbasierter Artikel mit manuell erstelltem Filter und manuell erstellter Sicht. Diese Option erfordert, dass die *Sync_object* und *Filter* Eigenschaften auch festgelegt werden. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
||**Logbased manualfilter**|Protokollbasierter Artikel mit manuell erstelltem Filter. Diese Option erfordert, dass die *Sync_object* und *Filter* Eigenschaften auch festgelegt werden. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
||**Logbased manualview**|Protokollbasierter Artikel mit manuell erstellter Sicht. Diese Option erfordert, dass die *Sync_object* Eigenschaft auch festgelegt werden. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
||**indizierte viewlogbased**|Artikel für protokollbasierte indizierte Sicht. Diese Option wird für Oracle-Verleger nicht unterstützt. Für diesen Artikeltyp muss die Basistabelle nicht separat veröffentlicht werden.|  
||**indizierte Viewlogbased manualboth**|Artikel für protokollbasierte indizierte Sicht mit manuell erstelltem Filter und manuell erstellter Sicht. Diese Option erfordert, dass die *Sync_object* und *Filter* Eigenschaften auch festgelegt werden. Für diesen Artikeltyp muss die Basistabelle nicht separat veröffentlicht werden. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
||**indizierte Viewlogbased manualfilter**|Artikel für protokollbasierte indizierte Sicht mit manuell erstelltem Filter. Diese Option erfordert das *Sync_object* und *Filter* Eigenschaften auch festgelegt werden. Für diesen Artikeltyp muss die Basistabelle nicht separat veröffentlicht werden. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
||**indizierte Viewlogbased manualview**|Artikel für protokollbasierte indizierte Sicht mit manuell erstellter Sicht. Diese Option erfordert, dass die *Sync_object* Eigenschaft auch festgelegt werden. Für diesen Artikeltyp muss die Basistabelle nicht separat veröffentlicht werden. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
|**upd_cmd**||Die auszuführende UPDATE-Anweisung; andernfalls wird die Operation aus dem Protokoll hergeleitet.|  
|NULL|NULL|Gibt eine Liste von Artikeleigenschaften zurück, die geändert werden können.|  
  
 [  **@force_invalidate_snapshot =** ] *Force_invalidate_snapshot*  
 Bestätigt, dass durch die von dieser gespeicherten Prozedur ausgeführte Aktion möglicherweise eine vorhandene Momentaufnahme ungültig wird. *Force_invalidate_snapshot* ist ein **Bit**, hat den Standardwert **0**.  
  
 **0** gibt an, dass Änderungen am Artikel bewirken nicht, die Momentaufnahme ungültig wird. Wenn die gespeicherte Prozedur erkennt, dass die Änderungen eine neue Momentaufnahme erfordern, tritt ein Fehler auf und es werden keine Änderungen vorgenommen.  
  
 **1** gibt an, dass Änderungen am Artikel kann dazu führen, dass die Momentaufnahme ungültig wird, und wenn es sind Abonnements vorhanden, die eine neue Momentaufnahme erfordern die Berechtigung erteilt, für die vorhandene Momentaufnahme als veraltet zu markieren und eine neue Momentaufnahme zu generieren.  
  
 Weitere Informationen zu den Eigenschaften, bei deren Änderung die Generierung einer neuen Momentaufnahme erforderlich ist, finden Sie im Abschnitt "Hinweise".  
  
 [  **@force_reinit_subscription=]***Force_reinit_subscription*  
 Bestätigt, dass die von dieser gespeicherten Prozedur ausgeführte Aktion die erneute Initialisierung vorhandener Abonnements erfordern kann. *Force_reinit_subscription* ist ein **Bit** hat den Standardwert **0**.  
  
 **0** gibt an, dass Änderungen am Artikel nicht das Abonnement erneut initialisiert werden können. Wenn die gespeicherte Prozedur erkennt, dass die Änderung die Neuinitialisierung vorhandener Abonnements erfordert, tritt ein Fehler auf, und es werden keine Änderungen durchgeführt.  
  
 **1** gibt an, dass Änderungen am Artikel bewirken, vorhandene Abonnements erneut initialisiert werden dass, und die Berechtigung für den erneuten Initialisierung der Abonnements erteilt.  
  
 Weitere Informationen zu den Eigenschaften, bei deren Änderung die erneute Initialisierung aller vorhandenen Abonnements erforderlich ist, finden Sie im Abschnitt "Hinweise".  
  
 [  **@publisher** =] **"***Publisher***"**  
 Gibt einen Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verleger an. *Publisher* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  *Publisher* sollte nicht verwendet werden, beim Ändern von Artikeleigenschaften auf einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_changearticle** wird bei Momentaufnahme- und Transaktionsreplikation verwendet.  
  
 Wenn ein Artikel einer Veröffentlichung, die die Peer-zu-Peer-Transaktionsreplikation unterstützt gehört, können Sie nur ändern die **Beschreibung**, **Ins_cmd**, **Upd_cmd**, und **Del_cmd** Eigenschaften.  
  
 Ändern die folgenden Eigenschaften erfordert, dass eine neue Momentaufnahme generiert werden, und geben Sie einen Wert von **1** für die *Force_invalidate_snapshot* Parameter:  
  
-   **del_cmd**  
  
-   **dest_table**  
  
-   **destination_owner**  
  
-   **ins_cmd**  
  
-   **pre_creation_cmd**  
  
-   **schema_options**  
  
-   **upd_cmd**  
  
 Ändern die folgenden Eigenschaften muss vorhandene Abonnements erneut initialisiert werden, und geben Sie einen Wert von **1** für die *Force_reinit_subscription* Parameter.  
  
-   **del_cmd**  
  
-   **dest_table**  
  
-   **destination_owner**  
  
-   **filter**  
  
-   **ins_cmd**  
  
-   **status**  
  
-   **upd_cmd**  
  
 Innerhalb einer vorhandenen Veröffentlichung können Sie **Sp_changearticle** einen Artikel ändern, ohne Sie zu löschen und die gesamte Veröffentlichung neu erstellen.  
  
> [!NOTE]  
>  Beim Ändern des Werts von *Schema_option*, das System führt ein bitweises Update nicht. Dies bedeutet, dass beim Festlegen der *Schema_option* mit **Sp_changearticle**vorhandene biteinstellungen möglicherweise deaktiviert. Um die vorhandenen Einstellungen beizubehalten, sollten Sie ausführen [| (Bitweises OR) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) zwischen dem Wert festlegen und der aktuelle Wert der *Schema_option*, dem kann bestimmt werden, durch das Ausführen [Sp_helparticle](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md).  
  
## <a name="valid-schema-options"></a>Valid Schema Options  
 Die folgende Tabelle beschreibt die zulässigen Werte von *Schema_option* basierend auf dem Replikationstyp (oben) und den Artikeltyp (in der ersten Spalte angezeigt).  
  
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
>  Für aktualisierbare Veröffentlichungen in der Warteschlange die *Schema_option* Wert **0 x 80** muss aktiviert sein. Die unterstützten *Schema_option* -Werte für nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publikationen sind: **0 x 01**, **0 x 02**, **0 x 10**,  **0 x 40**, **0 x 80**, **0 x 1000** und **0 x 4000**.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_changetranarticle](../../relational-databases/replication/codesnippet/tsql/sp-changearticle-transac_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_changearticle**.  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Ändern von Artikeleigenschaften](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Sp_addarticle &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Sp_helparticlecolumns &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)  
  
  
