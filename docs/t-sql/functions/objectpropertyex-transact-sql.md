---
title: OBJECTPROPERTYEX (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OBJECTPROPERTYEX
- OBJECTPROPERTYEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- displaying schema-scoped object information
- viewing schema-scoped object information
- OBJECTPROPERTYEX function
- schema-scoped objects [SQL Server]
- objects [SQL Server], schema-scoped
ms.assetid: be36b3e3-3309-4332-bfb5-c7e9cf8dc8bd
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 63854d22cf1285fee6758ee0e78da0c13bb21dc6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="objectpropertyex-transact-sql"></a>OBJECTPROPERTYEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt Informationen zu schemabezogenen Objekten in der aktuellen Datenbank zurück. Eine Liste dieser Objekte finden Sie unter [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md). OBJECTPROPERTYEX kann nicht für Objekte verwendet werden, die keine schemabezogenen Objekte sind, wie z. B. Trigger der Datendefinitionssprache (DDL, Data Definition Language) und Ereignisbenachrichtigungen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
OBJECTPROPERTYEX ( id , property )  
```  
  
## <a name="arguments"></a>Argumente  
 *id*  
 Ein Ausdruck, der die ID des Objekts in der aktuellen Datenbank darstellt. *id* ist vom Datentyp **int**, und es wird davon ausgegangen, dass es ein schemabezogenes Objekt im aktuellen Datenbankkontext ist.  
  
 *property*  
 Ein Ausdruck, der die Informationen enthält, die für das durch id angegebene Objekt zurückgegeben werden sollen. Der Rückgabetyp ist **sql_variant**. In der folgenden Tabelle ist der Basisdatentyp für die einzelnen Eigenschaftswertswerte aufgeführt.  
  
> [!NOTE]  
>  Wenn nicht anders angegeben, wird NULL zurückgegeben, wenn *property* kein gültiger Eigenschaftsname ist, *id* keine gültige Objekt-ID ist, *id* ein nicht unterstützter Objekttyp für die angegebene *Eigenschaft* ist oder der Aufrufer nicht über die Berechtigung zum Anzeigen der Metadaten des Objekts verfügt.  
  
|Eigenschaftenname|Objekttyp|Beschreibung und Rückgabewerte|  
|-------------------|-----------------|-------------------------------------|  
|BaseType|Ein beliebiges schemabezogenes Objekt|Identifiziert den Basistyp des Objekts. Wenn das angegebene Objekt vom Typ SYNONYM ist, wird der Basistyp des zugrunde liegenden Objekts zurückgegeben.<br /><br /> Ungleich NULL = Objekttyp<br /><br /> Basisdatentyp: **char(2)**|  
|CnstIsClustKey|Einschränkung|PRIMARY KEY-Einschränkung mit einem gruppierten Index.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|CnstIsColumn|Einschränkung|Einschränkung CHECK, DEFAULT oder FOREIGN KEY für eine einzelne Spalte.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|CnstIsDeleteCascade|Einschränkung|FOREIGN KEY-Einschränkung mit der ON DELETE CASCADE-Option.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|CnstIsDisabled|Einschränkung|Deaktivierte Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|CnstIsNonclustKey|Einschränkung|PRIMARY KEY-Einschränkung mit einem nicht gruppierten Index.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|CnstIsNotRepl|Einschränkung|Die Einschränkung wird mithilfe der Schlüsselwörter NOT FOR REPLICATION definiert.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|CnstIsNotTrusted|Einschränkung|Die Einschränkung wurde ohne Überprüfung der vorhandenen Zeilen aktiviert. Daher gilt die Einschränkung möglicherweise nicht für alle Zeilen.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|CnstIsUpdateCascade|Einschränkung|FOREIGN KEY-Einschränkung mit der ON UPDATE CASCADE-Option.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|ExecIsAfterTrigger|Trigger|AFTER-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|ExecIsAnsiNullsOn|[!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Trigger, Sicht|Die Einstellung von ANSI_NULLS zum Zeitpunkt der Erstellung.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|ExecIsDeleteTrigger|Trigger|DELETE-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|ExecIsFirstDeleteTrigger|Trigger|Der erste Trigger, der beim Ausführen einer DELETE-Anweisung für die Tabelle ausgelöst wird.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|ExecIsFirstInsertTrigger|Trigger|Der erste Trigger, der beim Ausführen einer INSERT-Anweisung für die Tabelle ausgelöst wird.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|ExecIsFirstUpdateTrigger|Trigger|Der erste Trigger, der beim Ausführen einer UPDATE-Anweisung für die Tabelle ausgelöst wird.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|ExecIsInsertTrigger|Trigger|INSERT-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|ExecIsInsteadOfTrigger|Trigger|INSTEAD OF-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|ExecIsLastDeleteTrigger|Trigger|Der letzte Trigger, der beim Ausführen einer DELETE-Anweisung für die Tabelle ausgelöst wird.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|ExecIsLastInsertTrigger|Trigger|Der letzte Trigger, der beim Ausführen einer INSERT-Anweisung für die Tabelle ausgelöst wird.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|ExecIsLastUpdateTrigger|Trigger|Der letzte Trigger, der beim Ausführen einer UPDATE-Anweisung für die Tabelle ausgelöst wird.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|ExecIsQuotedIdentOn|[!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Trigger, Sicht|Einstellung von QUOTED_IDENTIFIER zum Zeitpunkt der Erstellung.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|ExecIsStartup|Verfahren|Autostartprozedur.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|ExecIsTriggerDisabled|Trigger|Deaktivierter Trigger.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|ExecIsTriggerNotForRepl|Trigger|Als NOT FOR REPLICATION definierter Trigger.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|ExecIsUpdateTrigger|Trigger|UPDATE-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|ExecIsWithNativeCompilation|[!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur|**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die Prozedur wird systemintern kompiliert.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|HasAfterTrigger|Tabelle, Sicht|Die Tabelle oder Sicht besitzt einen AFTER-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|HasDeleteTrigger|Tabelle, Sicht|Die Tabelle oder Sicht besitzt einen DELETE-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|HasInsertTrigger|Tabelle, Sicht|Die Tabelle oder Sicht besitzt einen INSERT-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|HasInsteadOfTrigger|Tabelle, Sicht|Die Tabelle oder Sicht besitzt einen INSTEAD OF-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|HasUpdateTrigger|Tabelle, Sicht|Die Tabelle oder Sicht besitzt einen UPDATE-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsAnsiNullsOn|[!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur, Tabelle, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Trigger, Sicht|Gibt an, dass die Einstellung der Option ANSI_NULLS für die Tabelle ON ist, d. h. alle Vergleiche mit einem NULL-Wert zu UNKNOWN ausgewertet werden. Diese Einstellung gilt für alle Ausdrücke in der Tabellendefinition, einschließlich berechneter Spalten und Einschränkungen, solange die Tabelle vorhanden ist.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsCheckCnst|Ein beliebiges schemabezogenes Objekt|CHECK-Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsConstraint|Ein beliebiges schemabezogenes Objekt|Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsDefault|Ein beliebiges schemabezogenes Objekt|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gebundener Standard.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsDefaultCnst|Ein beliebiges schemabezogenes Objekt|DEFAULT-Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsDeterministic|Skalare Funktionen und Tabellenwertfunktionen, Sicht|Die Determinismuseigenschaft der Funktion oder Sicht.<br /><br /> 1 = Deterministisch<br /><br /> 0 = Nicht deterministisch<br /><br /> Basisdatentyp: **int**|  
|IsEncrypted|[!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur, Tabelle, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Trigger, Sicht|Gibt an, dass der Originaltext der Modulanweisung in ein verborgenes Format umgewandelt wurde. Die Ausgabe der Verbergung ist nicht direkt in den Katalogsichten in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] sichtbar. Benutzer, die keinen Zugriff auf Systemtabellen oder Datenbankdateien haben, können den verborgenen Text nicht abrufen. Der Text ist jedoch für Benutzer verfügbar, die entweder auf die Systemtabellen über den [DAC-Port](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md) oder direkt auf die Datenbankdateien zugreifen können. Des Weiteren können Benutzer, die einen Debugger an den Serverprozess anfügen können, die ursprüngliche Prozedur zur Laufzeit aus dem Arbeitsspeicher abrufen.<br /><br /> 1 = Verschlüsselt.<br /><br /> 0 = Nicht verschlüsselt<br /><br /> Basisdatentyp: **int**|  
|IsExecuted|Ein beliebiges schemabezogenes Objekt|Gibt an, dass das Objekt ausgeführt werden kann (Sicht, Prozedur, Funktion oder Trigger).<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsExtendedProc|Ein beliebiges schemabezogenes Objekt|Erweiterte Prozedur.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsForeignKey|Ein beliebiges schemabezogenes Objekt|FOREIGN KEY-Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsIndexed|Tabelle, Sicht|Tabelle oder Sicht mit einem Index.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsIndexable|Tabelle, Sicht|Tabelle oder Sicht, für die ein Index erstellt werden kann.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsInlineFunction|Funktion|Inlinefunktion.<br /><br /> 1 = Inlinefunktion<br /><br /> 0 = Keine Inlinefunktion<br /><br /> Basisdatentyp: **int**|  
|IsMSShipped|Ein beliebiges schemabezogenes Objekt|Ein während der Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstelltes Objekt.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsPrecise|Berechnete Spalte, Funktion, benutzerdefinierter Typ, Sicht|Zeigt an, ob das Objekt eine unpräzise Berechnung, wie z. B. Gleitkommaoperationen, enthält.<br /><br /> 1 = Genau<br /><br /> 0 = Unpräzise<br /><br /> Basisdatentyp: **int**|  
|IsPrimaryKey|Ein beliebiges schemabezogenes Objekt|PRIMARY KEY-Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsProcedure|Ein beliebiges schemabezogenes Objekt|Prozedur.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsQuotedIdentOn|CHECK-Einschränkung, DEFAULT-Definition, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur, Tabelle, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Trigger, Sicht|Gibt an, dass die Einstellung für Bezeichner in Anführungszeichen für das Objekt ON ist, d. h., dass doppelte Anführungszeichen Bezeichner in allen an der Objektdefinition beteiligten Ausdrücken begrenzen.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsQueue|Ein beliebiges schemabezogenes Objekt|Service Broker-Warteschlange.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsReplProc|Ein beliebiges schemabezogenes Objekt|Replikationsprozedur.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsRule|Ein beliebiges schemabezogenes Objekt|Gebundene Regel.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsScalarFunction|Funktion|Skalarwertfunktion.<br /><br /> 1 = Skalarwertfunktion<br /><br /> 0 = Keine Skalarwertfunktion<br /><br /> Basisdatentyp: **int**|  
|IsSchemaBound|Funktion, Prozedur, Sicht|Schemagebundene Funktion oder mithilfe von SCHEMABINDING erstellte Sicht.<br /><br /> 1 = Schemagebunden<br /><br /> 0 = Nicht schemagebunden<br /><br /> Basisdatentyp: **int**|  
|IsSystemTable|Tabelle|Systemtabelle.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsSystemVerified|Berechnete Spalte, Funktion, benutzerdefinierter Typ, Sicht|Die Genauigkeits- und Determinismuseigenschaften des Objekts können von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] überprüft werden.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsTable|Tabelle|Tabelle.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsTableFunction|Funktion|Tabellenwertfunktion.<br /><br /> 1 = Tabellenwertfunktion<br /><br /> 0 = Keine Tabellenwertfunktion<br /><br /> Basisdatentyp: **int**|  
|IsTrigger|Ein beliebiges schemabezogenes Objekt|Trigger.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsUniqueCnst|Ein beliebiges schemabezogenes Objekt|UNIQUE-Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsUserTable|Tabelle|Benutzerdefinierte Tabelle.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|IsView|Anzeigen|Sicht.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|OwnerId|Ein beliebiges schemabezogenes Objekt|Besitzer des Objekts.<br /><br /> **Hinweis:** Der Schemabesitzer ist nicht notwendigerweise der Objektbesitzer. Beispielsweise geben untergeordnete Objekte (Objekte, bei denen der Wert von *parent_object_id* ungleich NULL ist) immer die gleiche Besitzer-ID zurück wie das übergeordnete Objekt.<br /><br /> Ungleich NULL = Datenbankbenutzer-ID des Objektbesitzers.<br /><br /> NULL = Nicht unterstützter Objekttyp oder ungültige Objekt-ID.<br /><br /> Basisdatentyp: **int**|  
|SchemaId|Ein beliebiges schemabezogenes Objekt|Die ID des dem Objekt zugeordneten Schemas.<br /><br /> Ungleich NULL = Schema-ID des Objekts.<br /><br /> Basisdatentyp: **int**|  
|SystemDataAccess|Funktion, Sicht|Das Objekt greift auf Systemdaten, Systemkataloge oder virtuelle Systemtabellen in der lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu.<br /><br /> 0 = Keine<br /><br /> 1 = Lesen<br /><br /> Basisdatentyp: **int**|  
|TableDeleteTrigger|Tabelle|Die Tabelle besitzt einen DELETE-Trigger.<br /><br /> >1 = ID des ersten Triggers vom angegebenen Typ.<br /><br /> Basisdatentyp: **int**|  
|TableDeleteTriggerCount|Tabelle|Die Tabelle besitzt die angegebene Anzahl von DELETE-Triggern.<br /><br /> Ungleich NULL = Anzahl von DELETE-Triggern<br /><br /> Basisdatentyp: **int**|  
|TableFullTextMergeStatus|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt an, ob eine Tabelle über einen Volltextindex verfügt, der gerade zusammengeführt wird.<br /><br /> 0 = Tabelle hat keinen Volltextindex, oder der Volltextindex wird derzeit nicht zusammengeführt.<br /><br /> 1 = Der Volltextindex wird derzeit zusammengeführt.|  
|TableFullTextBackgroundUpdateIndexOn|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Das Update von Volltextindizes im Hintergrund (automatische Änderungsnachverfolgung) ist für die Tabelle aktiviert.<br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> Basisdatentyp: **int**|  
|TableFulltextCatalogId|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID des Volltextkatalogs, in dem die Daten des Volltextindexes für die Tabelle gespeichert sind.<br /><br /> Ungleich 0 = ID des Volltextkatalogs, die dem eindeutigen Index zugeordnet ist, der die Zeilen in einer volltextindizierten Tabelle identifiziert.<br /><br /> 0 = Die Tabelle besitzt keinen Volltextindex.<br /><br /> Basisdatentyp: **int**|  
|TableFullTextChangeTrackingOn|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die Volltext-Änderungsnachverfolgung ist für die Tabelle aktiviert.<br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> Basisdatentyp: **int**|  
|TableFulltextDocsProcessed|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die Anzahl der seit dem Start der Volltextindizierung verarbeiteten Zeilen. In einer Tabelle, die für die Volltextsuche indiziert wird, werden alle Spalten einer Zeile als Teil eines zu indizierenden Dokuments betrachtet.<br /><br /> 0 = Keine aktive Durchforstungs- oder Volltextindizierung wurde abgeschlossen.<br /><br /> >0 = Eine der folgenden Möglichkeiten (A oder B): A) Die Anzahl der seit dem Start der vollständigen, inkrementellen oder manuellen Änderungsnachverfolgung mithilfe von Einfüge- und Updatevorgängen verarbeiteten Dokumente; B) Die Anzahl der Zeilen, die mithilfe von Einfüge- und Updatevorgängen verarbeitet wurden, seit die Änderungsnachverfolgung mit Auffüllung mithilfe von Indexupdates im Hintergrund aktiviert wurde, das Schema für den Volltextindex geändert wurde, der Volltextkatalog erneut erstellt wurde oder die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu gestartet wurde usw.<br /><br /> NULL = Die Tabelle besitzt keinen Volltextindex.<br /><br /> Basisdatentyp: **int**<br /><br /> **Hinweis:** Diese Eigenschaft überwacht oder zählt gelöschte Eigenschaften nicht.|  
|TableFulltextFailCount|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die Anzahl der Zeilen, die von der Volltextsuche nicht indiziert wurden.<br /><br /> 0 = Die Auffüllung ist abgeschlossen.<br /><br /> >0 = Eine der folgenden Möglichkeiten (A oder B): A) Die Anzahl der Dokumente, die seit dem Start der Auffüllung mithilfe der vollständigen, inkrementellen und manuellen Änderungsnachverfolgung nicht indiziert wurden; B) Bei der Änderungsnachverfolgung mit Indexupdate im Hintergrund die Anzahl der Zeilen, die seit dem Start der Auffüllung oder dem Neustart der Auffüllung nicht indiziert wurden. Dies könnte durch eine Schemaänderung, eine erneute Erstellung des Katalogs, einen Neustart des Servers usw. verursacht werden.<br /><br /> NULL = Die Tabelle besitzt keinen Volltextindex.<br /><br /> Basisdatentyp: **int**|  
|TableFulltextItemCount|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Ungleich NULL = Anzahl der Zeilen, die erfolgreich volltextindiziert wurden.<br /><br /> NULL = Die Tabelle besitzt keinen Volltextindex.<br /><br /> Basisdatentyp: **int**|  
|TableFulltextKeyColumn|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID der Spalte, die dem eindeutigen einspaltigen Index zugeordnet ist, der Teil der Definition des Volltextindex und des semantischen Index ist.<br /><br /> 0 = Die Tabelle besitzt keinen Volltextindex.<br /><br /> Basisdatentyp: **int**|  
|TableFulltextPendingChanges|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Anzahl der zu verarbeitenden ausstehenden Änderungsnachverfolgungseinträge.<br /><br /> 0 = Änderungsnachverfolgung ist nicht aktiviert.<br /><br /> NULL = Die Tabelle besitzt keinen Volltextindex.<br /><br /> Basisdatentyp: **int**|  
|TableFulltextPopulateStatus|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 0 = Im Leerlauf.<br /><br /> 1 = Vollständige Auffüllung wird ausgeführt.<br /><br /> 2 = Inkrementelle Auffüllung wird ausgeführt.<br /><br /> 3 = Propagierung der Überarbeitungen wird ausgeführt.<br /><br /> 4 = Indexupdate im Hintergrund wird ausgeführt, z. B. automatische Änderungsnachverfolgung.<br /><br /> 5 = Volltextindizierung wurde gedrosselt oder angehalten.<br /><br /> 6 = Ein Fehler ist aufgetreten. Überprüfen Sie das Auffüllungsprotokoll für Details. Weitere Informationen finden Sie im Abschnitt **Beheben von Fehlern in einer Volltextauffüllung (Crawl)** unter [Auffüllen von Volltextindizes](../../relational-databases/search/populate-full-text-indexes.md).<br /><br /> Basisdatentyp: **int**|  
|TableFullTextSemanticExtraction|Tabelle|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die Tabelle ist für die semantische Indizierung aktiviert.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableHasActiveFulltextIndex|Tabelle|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die Tabelle besitzt einen aktiven Volltextindex.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableHasCheckCnst|Tabelle|Die Tabelle besitzt eine CHECK-Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableHasClustIndex|Tabelle|Die Tabelle besitzt einen gruppierten Index.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableHasDefaultCnst|Tabelle|Die Tabelle besitzt eine DEFAULT-Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableHasDeleteTrigger|Tabelle|Die Tabelle besitzt einen DELETE-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableHasForeignKey|Tabelle|Die Tabelle besitzt eine FOREIGN KEY-Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableHasForeignRef|Tabelle|Auf die Tabelle wird mit einer FOREIGN KEY-Einschränkung verwiesen.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableHasIdentity|Tabelle|Die Tabelle besitzt eine Identitätsspalte.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableHasIndex|Tabelle|Die Tabelle besitzt einen Index beliebigen Typs.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableHasInsertTrigger|Tabelle|Das Objekt besitzt einen INSERT-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableHasNonclustIndex|Tabelle|Die Tabelle besitzt einen nicht gruppierten Index.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableHasPrimaryKey|Tabelle|Die Tabelle besitzt einen Primärschlüssel.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableHasRowGuidCol|Tabelle|Die Tabelle besitzt eine ROWGUIDCOL-Eigenschaft für eine **uniqueidentifier**-Spalte.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableHasTextImage|Tabelle|Die Tabelle besitzt eine **text**-, **ntext**- oder **image**-Spalte.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableHasTimestamp|Tabelle|Die Tabelle besitzt eine **timestamp**-Spalte.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableHasUniqueCnst|Tabelle|Die Tabelle besitzt eine UNIQUE-Einschränkung.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableHasUpdateTrigger|Tabelle|Das Objekt besitzt einen UPDATE-Trigger.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableHasVarDecimalStorageFormat|Tabelle|Die Tabelle lässt das **vardecimal**-Speicherformat zu.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableInsertTrigger|Tabelle|Die Tabelle besitzt einen INSERT-Trigger.<br /><br /> >1 = ID des ersten Triggers vom angegebenen Typ.<br /><br /> Basisdatentyp: **int**|  
|TableInsertTriggerCount|Tabelle|Die Tabelle besitzt die angegebene Anzahl von INSERT-Triggern.<br /><br /> >0 = Die Anzahl von INSERT-Triggern.<br /><br /> Basisdatentyp: **int**|  
|TableIsFake|Tabelle|Die Tabelle ist in Wirklichkeit nicht vorhanden. Sie wird bei Bedarf durch [!INCLUDE[ssDE](../../includes/ssde-md.md)] intern materialisiert.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableIsLockedOnBulkLoad|Tabelle|Die Tabelle ist aufgrund eines **bcp**- oder BULK INSERT-Auftrags gesperrt.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**|  
|TableIsMemoryOptimized|Tabelle|**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Tabelle ist speicheroptimiert<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Basisdatentyp: **int**<br /><br /> Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).|  
|TableIsPinned|Tabelle|Die Tabelle ist fixiert, damit sie im Datencache gespeichert wird.<br /><br /> 0 = False<br /><br /> Dieses Feature wird in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen nicht unterstützt.|  
|TableTextInRowLimit|Tabelle|Für die Tabelle wurde die text in row-Option festgelegt.<br /><br /> > 0 = Maximale Anzahl von Bytes, die für text in row zulässig sind.<br /><br /> 0 = Die Option text in row ist nicht festgelegt.<br /><br /> Basisdatentyp: **int**|  
|TableUpdateTrigger|Tabelle|Die Tabelle besitzt einen UPDATE-Trigger.<br /><br /> > 1 = ID des ersten Triggers vom angegebenen Typ.<br /><br /> Basisdatentyp: **int**|  
|TableUpdateTriggerCount|Tabelle|Die Tabelle besitzt die angegebene Anzahl von UPDATE-Triggern.<br /><br /> > 0 = Die Anzahl von UPDATE-Triggern.<br /><br /> Basisdatentyp: **int**|  
|UserDataAccess|Funktion, Sicht|Zeigt an, dass das Objekt auf Benutzerdaten und Benutzertabellen in der lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugreift.<br /><br /> 1 = Lesen<br /><br /> 0 = Keine<br /><br /> Basisdatentyp: **int**|  
|TableHasColumnSet|Tabelle|Die Tabelle besitzt einen Spaltensatz.<br /><br /> 0 = False<br /><br /> 1 = True<br /><br /> Weitere Informationen finden Sie unter [Verwenden von Spaltensätzen](../../relational-databases/tables/use-column-sets.md).|  
|Cardinality|Tabelle (System oder benutzerdefiniert), Sicht oder Index|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die Anzahl von Zeilen im angegebenen Objekt.|  
|TableTemporalType|Tabelle|**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt den Typ der Tabelle an.<br /><br /> 0 = Nicht temporale Tabelle<br /><br /> 1 = Verlaufstabelle für die Tabelle mit Systemversionsverwaltung<br /><br /> 2 = Temporale Tabelle mit Systemversionsverwaltung|  
  
## <a name="return-types"></a>Rückgabetypen  
 **sql_variant**  
  
## <a name="exceptions"></a>Ausnahmen  
 Gibt NULL bei einem Fehler zurück oder wenn ein Aufrufer nicht über Berechtigungen zum Anzeigen des Objekts verfügt.  
  
 Ein Benutzer kann nur die Metadaten sicherungsfähiger Elemente anzeigen, bei denen der Benutzer entweder der Besitzer ist oder für die dem Benutzer eine Berechtigung erteilt wurde. Dies bedeutet, dass Metadaten ausgebende integrierte Funktionen, z. B. OBJECTPROPERTYEX, möglicherweise NULL zurückgeben, wenn dem Benutzer für das Objekt keine Berechtigung erteilt wurde. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] setzt voraus, dass sich *object_id* im aktuellen Datenbankkontext befindet. Eine Abfrage, die auf *object_id* in einer anderen Datenbank verweist, gibt NULL oder falsche Ergebnisse zurück. Beispielsweise ist der aktuelle Datenbankkontext in der folgenden Abfrage die Masterdatenbank. [!INCLUDE[ssDE](../../includes/ssde-md.md)] versucht, den Eigenschaftswert für den angegebenen Wert von *object_id* in dieser Datenbank statt in der Datenbank zurückzugeben, die in der Abfrage angegeben ist. Die Abfrage gibt falsche Ergebnisse zurück, da sich die `vEmployee`-Sicht nicht in der Masterdatenbank befindet.  
  
```  
USE master;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID(N'AdventureWorks2012.HumanResources.vEmployee'), 'IsView');  
GO  
```  
  
 OBJECTPROPERTYEX(*view_id*, 'IsIndexable') hat möglicherweise einen hohen Verbrauch an Computerressourcen, da die Auswertung der IsIndexable-Eigenschaft das Analysieren der Sichtdefinition, die Normalisierung und die partielle Optimierung erfordert. Obwohl die IsIndexable-Eigenschaft Tabellen oder Sichten identifiziert, die indiziert werden können, kann die tatsächliche Erstellung des Indexes dennoch fehlschlagen, wenn bestimmte Indexschlüsselanforderungen nicht erfüllt sind. Weitere Informationen finden Sie unter [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 OBJECTPROPERTYEX(*table_id*, 'TableHasActiveFulltextIndex') gibt den Wert 1 (TRUE) zurück, wenn mindestens eine Spalte einer Tabelle für die Indizierung hinzugefügt wurde. Die Volltextindizierung wird für das Auffüllen aktiviert, sobald die erste Spalte für die Indizierung hinzugefügt wird.  
  
 Einschränkungen für die Sichtbarkeit von Metadaten werden auf das Resultset angewendet. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-finding-the-base-type-of-an-object"></a>A. Suchen des Basistyps eines Objekts  
 Im folgenden Beispiel wird mithilfe von SYNONYM `MyEmployeeTable` ein Synonym für die `Employee`-Tabelle in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank erstellt und anschließend der Basistyp von SYNONYM zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE SYNONYM MyEmployeeTable FOR HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX ( object_id(N'MyEmployeeTable'), N'BaseType')AS [Base Type];  
GO  
```  
  
 Das Resultset zeigt, dass es sich bei dem Basistyp des zugrunde liegenden Objekts, der `Employee`-Tabelle, um eine Benutzertabelle handelt.  
  
 ```
Base Type 
--------  
U
```  
  
### <a name="b-returning-a-property-value"></a>B. Zurückgeben eines Eigenschaftswerts  
 Im folgenden Beispiel wird die Anzahl der UPDATE-Trigger für die angegebene Tabelle zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID(N'HumanResources.Employee'), N'TABLEUPDATETRIGGERCOUNT');  
GO  
  
```  
  
### <a name="c-finding-tables-that-have-a-foreign-key-constraint"></a>C. Suchen von Tabellen, die eine FOREIGN KEY-Einschränkung aufweisen  
 Im folgenden Beispiel wird die `TableHasForeignKey`-Eigenschaft verwendet, um alle Tabellen zurückzugeben, die eine FOREIGN KEY-Einschränkung aufweisen.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT name, object_id, schema_id, type_desc  
FROM sys.objects   
WHERE OBJECTPROPERTYEX(object_id, N'TableHasForeignKey') = 1  
ORDER BY name;  
GO  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="d-finding-the-base-type-of-an-object"></a>D: Suchen des Basistyps eines Objekts  
 Das folgende Beispiel gibt den Basistyp des `dbo.DimReseller`-Objekts zurück.  
  
```  
-- Uses AdventureWorks  
  
SELECT OBJECTPROPERTYEX ( object_id(N'dbo.DimReseller'), N'BaseType')AS BaseType;  
```  
  
 Das Resultset zeigt, dass es sich bei dem Basistyp des zugrunde liegenden Objekts, der `dbo.DimReseller`-Tabelle, um eine Benutzertabelle handelt.  
  
```  
BaseType   
--------   
U   
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/create-synonym-transact-sql.md)   
 [Metadata Functions &#40;Transact-SQL&#41; (Metadatenfunktionen &#40;Transact-SQL&#41;)](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [OBJECT_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md)  
  
  

