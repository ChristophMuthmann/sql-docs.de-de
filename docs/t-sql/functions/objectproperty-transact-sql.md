---
title: OBJECTPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OBJECTPROPERTY
- OBJECTPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- displaying schema-scoped object information
- viewing schema-scoped object information
- OBJECTPROPERTY function
- schema-scoped objects [SQL Server]
- objects [SQL Server], schema-scoped
ms.assetid: 27569888-f8b5-4cec-a79f-6ea6d692b4ae
caps.latest.revision: 81
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 2189ba0ca7245fcd098d2af55b381afc465a7fab
ms.contentlocale: de-de
ms.lasthandoff: 10/17/2017

---
# <a name="objectproperty-transact-sql"></a>OBJECTPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt Informationen zu schemabezogenen Objekten in der aktuellen Datenbank zurück. Eine Liste der Objekte mit Schemabereich, finden Sie unter [sys.objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md). Diese Funktion kann nicht für Objekte ohne Schemabereich verwendet werden, wie z. B. DDL-Trigger (DDL, Data Definition Language) und Ereignisbenachrichtigungen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
OBJECTPROPERTY ( id , property )   
```  
  
## <a name="arguments"></a>Argumente  
 *id*  
 Ein Ausdruck, der die ID des Objekts in der aktuellen Datenbank darstellt. *ID* ist **Int** und wird davon ausgegangen, dass ein Objekt mit Schemabereich in der aktuellen Datenbank verwendet werden.  
  
 *Eigenschaft*  
 Ist ein Ausdruck, der die Informationen darstellt, die für das angegebene vom Objekt zurückgegeben werden *Id*. *Eigenschaft* kann einen der folgenden Werte sein.  
  
> [!NOTE]  
>  Sofern nicht anders angegeben, NULL zurückgegeben, wenn *Eigenschaft* ist kein gültiger Eigenschaftsname *Id* ist keine gültige ObjectID, *Id* ist ein nicht unterstützter Objekttyp für den angegebenen *Eigenschaft*, oder der Aufrufer verfügt nicht über die Berechtigung zum Anzeigen der Metadaten des Objekts.  
  
|Eigenschaftsname|Objekttyp|Beschreibung und Rückgabewerte|  
|-------------------|-----------------|-------------------------------------|  
|CnstIsClustKey|Einschränkung|PRIMARY KEY-Einschränkung mit einem gruppierten Index.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsColumn|Einschränkung|Einschränkung CHECK, DEFAULT oder FOREIGN KEY für eine einzelne Spalte.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsDeleteCascade|Einschränkung|FOREIGN KEY-Einschränkung mit der ON DELETE CASCADE-Option.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsDisabled|Einschränkung|Deaktivierte Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsNonclustKey|Einschränkung|PRIMARY KEY- oder UNIQUE-Einschränkung mit einem nicht gruppierten Index.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsNotRepl|Einschränkung|Die Einschränkung wird mithilfe der Schlüsselwörter NOT FOR REPLICATION definiert.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsNotTrusted|Einschränkung|Die Einschränkung wurde ohne Überprüfung der vorhandenen Zeilen aktiviert und gilt daher möglicherweise nicht für alle Zeilen.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsUpdateCascade|Einschränkung|FOREIGN KEY-Einschränkung mit der ON UPDATE CASCADE-Option.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsAfterTrigger|Trigger|AFTER-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsAnsiNullsOn|[!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Trigger, Sicht|Einstellung von ANSI_NULLS zum Zeitpunkt der Erstellung.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsDeleteTrigger|Trigger|DELETE-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsFirstDeleteTrigger|Trigger|Erste Trigger, die ausgelöst wird, wenn ein Löschvorgang für die Tabelle ausgeführt wird.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsFirstInsertTrigger|Trigger|Erste Trigger, die ausgelöst wird, wenn eine Einfügung für die Tabelle ausgeführt wird.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsFirstUpdateTrigger|Trigger|Der erste Trigger, der beim Ausführen einer UPDATE-Anweisung für die Tabelle ausgelöst wird.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsInsertTrigger|Trigger|INSERT-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsInsteadOfTrigger|Trigger|INSTEAD OF-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsLastDeleteTrigger|Trigger|Der letzte Trigger, der beim Ausführen einer DELETE-Anweisung für die Tabelle ausgelöst wird.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsLastInsertTrigger|Trigger|Der letzte Trigger, der beim Ausführen einer INSERT-Anweisung für die Tabelle ausgelöst wird.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsLastUpdateTrigger|Trigger|Der letzte Trigger, der beim Ausführen einer UPDATE-Anweisung für die Tabelle ausgelöst wird.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsQuotedIdentOn|[!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Trigger, Sicht|Einstellung von QUOTED_IDENTIFIER zum Zeitpunkt der Erstellung.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsStartup|Verfahren|Autostartprozedur.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsTriggerDisabled|Trigger|Deaktivierter Trigger.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsTriggerNotForRepl|Trigger|Als NOT FOR REPLICATION definierter Trigger.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsUpdateTrigger|Trigger|UPDATE-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsWithNativeCompilation|[!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur|**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die Prozedur wird systemintern kompiliert.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **Int**|  
|HasAfterTrigger|Tabelle, Sicht|Die Tabelle oder Sicht besitzt einen AFTER-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False|  
|HasDeleteTrigger|Tabelle, Sicht|Die Tabelle oder Sicht besitzt einen DELETE-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False|  
|HasInsertTrigger|Tabelle, Sicht|Die Tabelle oder Sicht besitzt einen INSERT-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False|  
|HasInsteadOfTrigger|Tabelle, Sicht|Die Tabelle oder Sicht besitzt einen INSTEAD OF-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False|  
|HasUpdateTrigger|Tabelle, Sicht|Die Tabelle oder Sicht besitzt einen UPDATE-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsAnsiNullsOn|[!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur, Tabelle, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Trigger, Sicht|Gibt an, dass die Option ANSI NULLS für die Tabelle auf ON gesetzt wurde. Das bedeutet, dass alle Vergleiche mit einem Nullwert UNKNOWN ergeben. Diese Einstellung gilt für alle Ausdrücke in der Tabellendefinition, einschließlich berechneter Spalten und Einschränkungen, solange die Tabelle vorhanden ist.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsCheckCnst|Ein beliebiges schemabezogenes Objekt|CHECK-Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsConstraint|Ein beliebiges schemabezogenes Objekt|Eine einspaltige CHECK-, DEFAULT- oder FOREIGN KEY-Einschränkung für eine Spalte oder Tabelle.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsDefault|Ein beliebiges schemabezogenes Objekt|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gebundener Standard.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsDefaultCnst|Ein beliebiges schemabezogenes Objekt|DEFAULT-Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsDeterministic|Funktion, Sicht|Die Determinismuseigenschaft der Funktion oder Sicht.<br /><br /> 1 = Deterministisch<br /><br /> 0 = Nicht deterministisch|  
|IsEncrypted|[!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur, Tabelle, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Trigger, Sicht|Gibt an, dass der Originaltext der Modulanweisung in ein verborgenes Format umgewandelt wurde. Die Ausgabe der Verbergung ist nicht direkt in den Katalogsichten in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] sichtbar. Benutzer ohne Zugriff auf Systemtabellen oder Datenbankdateien können den verborgenen Text nicht abrufen. Der Text ist jedoch verfügbar für Benutzer, die entweder Systemtabellen, über zugreifen können die [DAC-Port](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md) oder direkt auf die Datenbankdateien zugreifen. Des Weiteren können Benutzer, die einen Debugger an den Serverprozess anfügen können, die ursprüngliche Prozedur zur Laufzeit aus dem Arbeitsspeicher abrufen.<br /><br /> 1 = Verschlüsselt.<br /><br /> 0 = nicht verschlüsselt<br /><br /> Basisdatentyp: **Int**|  
|IsExecuted|Ein beliebiges schemabezogenes Objekt|Das Objekt kann ausgeführt werden (Sicht, Prozedur, Funktion oder Trigger).<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsExtendedProc|Ein beliebiges schemabezogenes Objekt|Erweiterte Prozedur.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsForeignKey|Ein beliebiges schemabezogenes Objekt|FOREIGN KEY-Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsIndexed|Tabelle, Sicht|Eine Tabelle oder Sicht, die über einen Index verfügt.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsIndexable|Tabelle, Sicht|Eine Tabelle oder Sicht, für die ein Index erstellt werden kann.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsInlineFunction|Funktion|Inlinefunktion.<br /><br /> 1 = Inlinefunktion<br /><br /> 0 = Keine Inlinefunktion|  
|IsMSShipped|Ein beliebiges schemabezogenes Objekt|Ein Objekt, das bei der Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt wurde.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsPrimaryKey|Ein beliebiges schemabezogenes Objekt|PRIMARY KEY-Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> NULL = Keine Funktion oder ungültige Objekt-ID|  
|IsProcedure|Ein beliebiges schemabezogenes Objekt|Prozedur.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsQuotedIdentOn|[!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur, Tabelle, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Trigger, Sicht, CHECK-Einschränkung, DEFAULT-Definition|Gibt an, dass ON die Einstellung von quoted identifier für das Objekt ist. Das bedeutet, dass Begrenzungsbezeichner mit doppelten Anführungszeichen in allen Ausdrücken gekennzeichnet sind, die an der Objektdefinition beteiligt sind.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|IsQueue|Ein beliebiges schemabezogenes Objekt|Service Broker-Warteschlange.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsReplProc|Ein beliebiges schemabezogenes Objekt|Replikationsprozedur.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsRule|Ein beliebiges schemabezogenes Objekt|Gebundene Regel.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsScalarFunction|Funktion|Skalarwertfunktion.<br /><br /> 1 = Skalarwertfunktion<br /><br /> 0 = Keine Skalarwertfunktion|  
|IsSchemaBound|Funktion, Sicht|Schemagebundene Funktion oder mithilfe von SCHEMABINDING erstellte Sicht.<br /><br /> 1 = Schemagebunden<br /><br /> 0 = Nicht schemagebunden|  
|IsSystemTable|Tabelle|Systemtabelle.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsTable|Tabelle|Tabelle.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsTableFunction|Funktion|Tabellenwertfunktion.<br /><br /> 1 = Tabellenwertfunktion<br /><br /> 0 = Keine Tabellenwertfunktion|  
|IsTrigger|Ein beliebiges schemabezogenes Objekt|Trigger.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsUniqueCnst|Ein beliebiges schemabezogenes Objekt|UNIQUE-Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsUserTable|Tabelle|Benutzerdefinierte Tabelle.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsView|Sicht|Sicht.<br /><br /> 1 = True<br /><br /> 0 = False|  
|OwnerId|Ein beliebiges schemabezogenes Objekt|Besitzer des Objekts.<br /><br /> **Hinweis:** der schemabesitzer ist nicht notwendigerweise der Objektbesitzer. Z. B. untergeordnete Objekte (solche, auf denen *"parent_object_id"* ist ungleich null) gibt stets den gleichen Besitzer-ID als übergeordnetes Element.<br /><br /> Nicht NULL = Die Datenbankbenutzer-ID des Objektbesitzers.|  
|TableDeleteTrigger|Tabelle|Die Tabelle besitzt einen DELETE-Trigger.<br /><br /> >1 = ID des ersten Triggers vom angegebenen Typ.|  
|TableDeleteTriggerCount|Tabelle|Die Tabelle besitzt die angegebene Anzahl DELETE-Trigger.<br /><br /> >0 = Die Anzahl DELETE-Trigger.|  
|TableFullTextMergeStatus|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt an, ob eine Tabelle über einen Volltextindex verfügt, der gerade zusammengeführt wird.<br /><br /> 0 = Tabelle hat keinen Volltextindex, oder der Volltextindex wird derzeit nicht zusammengeführt.<br /><br /> 1 = Der Volltextindex wird derzeit zusammengeführt.|  
|TableFullTextBackgroundUpdateIndexOn|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Updates im Hintergrund für den Volltextindex der Tabelle sind aktiviert (automatisches Nachverfolgen von Änderungen).<br /><br /> 1 = "TRUE"<br /><br /> 0 = FALSE|  
|TableFulltextCatalogId|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID des Volltextkatalogs, in dem die Daten des Volltextindexes für die Tabelle gespeichert sind.<br /><br /> Ungleich 0 = ID des Volltextkatalogs, die dem eindeutigen Index zugeordnet ist, der die Zeilen in einer volltextindizierten Tabelle identifiziert.<br /><br /> 0 = Die Tabelle besitzt keinen Volltextindex.|  
|TableFulltextChangeTrackingOn|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die Volltext-Änderungsnachverfolgung ist für die Tabelle aktiviert.<br /><br /> 1 = "TRUE"<br /><br /> 0 = FALSE|  
|TableFulltextDocsProcessed|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die Anzahl der seit dem Start der Volltextindizierung verarbeiteten Zeilen. In einer Tabelle, die für die Volltextsuche indiziert wird, werden alle Spalten einer Zeile als Teil eines zu indizierenden Dokuments betrachtet.<br /><br /> 0 = Keine aktive Durchforstungs- oder Volltextindizierung wurde abgeschlossen.<br /><br /> > 0 = eine der folgenden (A oder B): A) die Anzahl von verarbeiteten Dokumenten einfügen oder Aktualisieren der Operationen seit dem Start vollständig, inkrementell oder manuellen änderungsnachverfolgung der Auffüllung. (B) die Anzahl der Zeilen, die von INSERT- oder Update-Vorgänge, da die änderungsnachverfolgung mit indexupdate im Hintergrund aktiviert wurde, die Volltextindex-Schema geändert, der Volltextkatalog neu erstellt oder die Instanz von verarbeitet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Neustart und so weiter.<br /><br /> NULL = Die Tabelle besitzt keinen Volltextindex.<br /><br /> Diese Eigenschaft überwacht die Anzahl gelöschter Zeilen nicht und zählt sie auch nicht.|  
|TableFulltextFailCount|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die Anzahl von Zeilen, für die die Volltextsuche keinen Index erstellt hat.<br /><br /> 0 = Die Auffüllung ist abgeschlossen.<br /><br /> > 0 = eine der folgenden (A oder B): A) die Anzahl der Dokumente, die seit dem Start des Full, Incremental und manuelle Aktualisierung änderungsnachverfolgung der Auffüllung nicht indiziert wurden. B) aktualisieren Sie die Anzahl der Zeilen, die seit dem Start der Auffüllung oder dem Neustart der Auffüllung nicht indiziert wurden, für die änderungsnachverfolgung mit Hintergrund. Ursache dafür kann eine Schemaänderung, eine Neuerstellung des Katalogs, ein Neustart des Servers usw. sein.<br /><br /> NULL = Die Tabelle besitzt keinen Volltextindex.|  
|TableFulltextItemCount|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die Anzahl von Zeilen, für die ein Volltextindex erfolgreich erstellt wurde.|  
|TableFulltextKeyColumn|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID der Spalte, die dem eindeutigen einspaltigen Index zugeordnet ist, der Teil der Definition des Volltextindexes ist.<br /><br /> 0 = Die Tabelle besitzt keinen Volltextindex.|  
|TableFulltextPendingChanges|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Anzahl der zu verarbeitenden ausstehenden Änderungsnachverfolgungseinträge.<br /><br /> 0 = Änderungsnachverfolgung ist nicht aktiviert.<br /><br /> NULL = Die Tabelle besitzt keinen Volltextindex.|  
|TableFulltextPopulateStatus|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 0 = Im Leerlauf.<br /><br /> 1 = Vollständige Auffüllung wird ausgeführt.<br /><br /> 2 = Inkrementelle Auffüllung wird ausgeführt.<br /><br /> 3 = Propagierung der Überarbeitungen wird ausgeführt.<br /><br /> 4 = Indexupdate im Hintergrund wird ausgeführt, z. B. automatische Änderungsnachverfolgung.<br /><br /> 5 = Volltextindizierung wurde gedrosselt oder angehalten.|  
|TableHasActiveFulltextIndex|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die Tabelle besitzt einen aktiven Volltextindex.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasCheckCnst|Tabelle|Die Tabelle besitzt eine CHECK-Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasClustIndex|Tabelle|Die Tabelle besitzt einen gruppierten Index.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasDefaultCnst|Tabelle|Die Tabelle besitzt eine DEFAULT-Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasDeleteTrigger|Tabelle|Die Tabelle besitzt einen DELETE-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasForeignKey|Tabelle|Die Tabelle besitzt eine FOREIGN KEY-Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasForeignRef|Tabelle|Auf die Tabelle wird mit einer FOREIGN KEY-Einschränkung verwiesen.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasIdentity|Tabelle|Die Tabelle besitzt eine Identitätsspalte.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasIndex|Tabelle|Die Tabelle besitzt einen Index beliebigen Typs.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasInsertTrigger|Tabelle|Das Objekt besitzt einen INSERT-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasNonclustIndex|Tabelle|Die Tabelle besitzt einen nicht gruppierten Index.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasPrimaryKey|Tabelle|Die Tabelle besitzt einen Primärschlüssel.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasRowGuidCol|Tabelle|Tabelle besitzt eine ROWGUIDCOL-Eigenschaft für eine **"uniqueidentifier"** Spalte.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasTextImage|Tabelle|Tabelle besitzt eine **Text**, **Ntext**, oder **Image** Spalte.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasTimestamp|Tabelle|Tabelle besitzt eine **Zeitstempel** Spalte.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasUniqueCnst|Tabelle|Die Tabelle besitzt eine UNIQUE-Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasUpdateTrigger|Tabelle|Objekt besitzt einen updatetrigger.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasVarDecimalStorageFormat|Tabelle|Für die Tabelle aktiviert ist **Vardecimal** Speicherformat.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableInsertTrigger|Tabelle|Die Tabelle besitzt einen INSERT-Trigger.<br /><br /> >1 = ID des ersten Triggers vom angegebenen Typ.|  
|TableInsertTriggerCount|Tabelle|Die Tabelle besitzt die angegebene Anzahl INSERT-Trigger.<br /><br /> >0 = Die Anzahl von INSERT-Triggern.|  
|TableIsFake|Tabelle|Die Tabelle ist in Wirklichkeit nicht vorhanden. Sie wird bei Bedarf durch [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] intern materialisiert.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableIsLockedOnBulkLoad|Tabelle|Tabelle wird gesperrt, da eine **Bcp** oder BULK INSERT-Auftrags.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableIsMemoryOptimized|Tabelle|**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Tabelle ist speicheroptimiert<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **Int**<br /><br /> Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).|  
|TableIsPinned|Tabelle|Die Tabelle ist fixiert, damit sie im Datencache gespeichert wird.<br /><br /> 0 = False<br /><br /> Diese Funktion wird in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen nicht unterstützt.|  
|TableTextInRowLimit|Tabelle|Die maximal zulässige Anzahl Byte für text in row.<br /><br /> Hat den Wert 0, wenn die Option text in row nicht festgelegt wurde.|  
|TableUpdateTrigger|Tabelle|Die Tabelle besitzt einen UPDATE-Trigger.<br /><br /> > 1 = ID des ersten Triggers vom angegebenen Typ.|  
|TableUpdateTriggerCount|Tabelle|Die Tabelle besitzt die angegebene Anzahl UPDATE-Trigger.<br /><br /> > 0 = Die Anzahl von UPDATE-Triggern.|  
|TableHasColumnSet|Tabelle|Die Tabelle besitzt einen Spaltensatz.<br /><br /> 0 = False<br /><br /> 1 = True<br /><br /> Weitere Informationen finden Sie unter [Verwenden von Spaltensätzen](../../relational-databases/tables/use-column-sets.md).|  
|TableTemporalType|Tabelle|**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt den Typ der Tabelle.<br /><br /> 0 = nicht temporalen Tabelle<br /><br /> 1 = Verlaufstabelle für die Tabelle mit systemversionsverwaltung<br /><br /> 2 = temporale Tabelle mit systemversionsverwaltung|  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="exceptions"></a>Ausnahmen  
 Gibt NULL bei einem Fehler zurück oder wenn ein Aufrufer nicht über Berechtigungen zum Anzeigen des Objekts verfügt.  
  
 Ein Benutzer kann nur die Metadaten sicherungsfähiger Elemente anzeigen, bei denen der Benutzer entweder der Besitzer ist oder für die dem Benutzer eine Berechtigung erteilt wurde. Dies bedeutet, dass Metadaten ausgebende integrierte Funktionen, z. B. OBJECTPROPERTY, möglicherweise NULL zurückgeben, wenn dem Benutzer für das Objekt keine Berechtigung erteilt wurde. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Hinweise  
 Die [!INCLUDE[ssDE](../../includes/ssde-md.md)] setzt voraus, dass *Object_id* befindet sich im Kontext aktuellen Datenbank. Eine Abfrage, die verweist auf ein *Object_id* in einer anderen Datenbank NULL oder falsche Ergebnisse zurück. In der folgenden Abfrage wird z. B. im aktuellen Datenbankkontext der master-Datenbank an. Die [!INCLUDE[ssDE](../../includes/ssde-md.md)] versucht, den Eigenschaftswert für das angegebene zurückzusetzen *Object_id* in dieser Datenbank statt in der Abfrage angegebenen Datenbank. Die Abfrage gibt falsche Ergebnisse zurück, da die Sicht `vEmployee` befindet sich nicht in der master-Datenbank.  
  
```  
USE master;  
GO  
SELECT OBJECTPROPERTY(OBJECT_ID(N'AdventureWorks2012.HumanResources.vEmployee'), 'IsView');  
GO  
```  
  
 OBJECTPROPERTY (*View_id*, 'IsIndexable') beanspruchen möglicherweise Computerressourcen, da die Auswertung der IsIndexable-Eigenschaft das Analysieren der Sichtdefinition, die Normalisierung und die partielle Optimierung erfordert. Obwohl die IsIndexable-Eigenschaft Tabellen oder Sichten identifiziert, die indiziert werden können, kann die tatsächliche Erstellung des Indexes dennoch fehlschlagen, wenn bestimmte Indexschlüsselanforderungen nicht erfüllt sind. Weitere Informationen finden Sie unter [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 OBJECTPROPERTY (*Table_id*, 'TableHasActiveFulltextIndex') gibt einen Wert von 1 (True) zurück, wenn mindestens eine Spalte einer Tabelle für die Indizierung hinzugefügt wird. Die Volltextindizierung wird für das Auffüllen aktiviert, sobald die erste Spalte für die Indizierung hinzugefügt wird.  
  
 Beim Erstellen einer Tabelle wird die Option QUOTED IDENTIFIER immer als ON in den Metadaten der Tabelle gespeichert, selbst wenn die Option beim Erstellen der Tabelle auf OFF festgelegt war. Deshalb gibt OBJECTPROPERTY (*Table_id*, 'IsQuotedIdentOn') werden immer den Wert 1 (True) zurück.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-verifying-that-an-object-is-a-table"></a>A. Überprüfen, ob ein Objekt in einer Tabelle vorhanden ist  
 Im folgenden Beispiel wird getestet, ob `UnitMeasure` in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank eine Tabelle ist.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECTPROPERTY (OBJECT_ID(N'Production.UnitMeasure'),'ISTABLE') = 1  
   PRINT 'UnitMeasure is a table.'  
ELSE IF OBJECTPROPERTY (OBJECT_ID(N'Production.UnitMeasure'),'ISTABLE') = 0  
   PRINT 'UnitMeasure is not a table.'  
ELSE IF OBJECTPROPERTY (OBJECT_ID(N'Production.UnitMeasure'),'ISTABLE') IS NULL  
   PRINT 'ERROR: UnitMeasure is not a valid object.';  
GO  
  
```  
  
### <a name="b-verifying-that-a-scalar-valued-user-defined-function-is-deterministic"></a>B. Überprüfen, ob eine benutzerdefinierte Skalarwertfunktion deterministisch ist  
 Im folgenden Beispiel wird getestet, ob die benutzerdefinierte skalarwertige Funktion `ufnGetProductDealerPrice`, welche gibt eine **Money** Wert, deterministisch ist.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECTPROPERTY(OBJECT_ID('dbo.ufnGetProductDealerPrice'), 'IsDeterministic');  
GO  
```  
  
 Das Resultset zeigt, dass `ufnGetProductDealerPrice` keine deterministische Funktion ist.  
  
 ```
-----  
0
```  
  
### <a name="c-finding-the-tables-that-belong-to-a-specific-schema"></a>"C:" Suchen in den Tabellen, die zu einem bestimmten Schema gehören  
 Im folgenden Beispiel werden alle Tabellen im Dbo-Schema zurückgegeben.  
  
```  
-- Uses AdventureWorks  
  
SELECT name, object_id, type_desc  
FROM sys.objects   
WHERE OBJECTPROPERTY(object_id, N'SchemaId') = SCHEMA_ID(N'dbo')  
ORDER BY type_desc, name;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-verifying-that-an-object-is-a-table"></a>Überprüfen, dass ein Objekt eine Tabelle D:  
 Im folgenden Beispiel wird getestet, ob `dbo.DimReseller` in der [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)]-Datenbank eine Tabelle ist.  
  
```  
-- Uses AdventureWorks  
  
IF OBJECTPROPERTY (OBJECT_ID(N'dbo.DimReseller'),'ISTABLE') = 1  
   SELECT 'DimReseller is a table.'  
ELSE   
   SELECT 'DimReseller is not a table.';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [COLUMNPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [Metadatenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECTPROPERTYEX &#40; Transact-SQL &#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)   
 [ALTER AUTHORIZATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [TYPEPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)   
 [Sys.Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  


