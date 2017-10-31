---
title: SET-Anweisungen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET
- SET_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ISO SET statements
- queries [SQL Server], executing
- dates [SQL Server], SET statements
- time [SQL Server], SET statements
- SET statement, about SET statement
- SET statement
- statistical information [SQL Server], SET statements
- locking [SQL Server], SET statements
ms.assetid: f7e107f8-0fcf-408b-b30f-da2323eeb714
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f0426730b33f0b70fda11a8cb07242a365d10fae
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-statements-transact-sql"></a>SET-Anweisungen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die Programmiersprache [!INCLUDE[tsql](../../includes/tsql-md.md)] bietet eine Reihe von SET-Anweisungen, mit denen die Verarbeitung bestimmter Informationen durch die aktuelle Sitzung geändert werden kann. Die SET-Anweisungen sind in die in der folgenden Tabelle gezeigten Kategorien unterteilt.  
  
 Informationen zum Festlegen von lokalen Variablen mit der SET-Anweisung finden Sie unter [festgelegt @local_variable &#40; Transact-SQL &#41; ](../../t-sql/language-elements/set-local-variable-transact-sql.md).  
  
|Kategorie|Anweisungen|  
|--------------|----------------|  
|Datums- und Zeitanweisungen|[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)<br /><br /> [SET DATEFORMAT-EINSTELLUNG](../../t-sql/statements/set-dateformat-transact-sql.md)|  
|Sperranweisungen|[SET DEADLOCK_PRIORITY](../../t-sql/statements/set-deadlock-priority-transact-sql.md)<br /><br /> [SET LOCK_TIMEOUT](../../t-sql/statements/set-lock-timeout-transact-sql.md)|  
|Verschiedene Anweisungen|[SET CONCAT_NULL_YIELDS_NULL](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)<br /><br /> [SET CURSOR_CLOSE_ON_COMMIT](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)<br /><br /> [SET FIPS_FLAGGER](../../t-sql/statements/set-fips-flagger-transact-sql.md)<br /><br /> [SET IDENTITY_INSERT](../../t-sql/statements/set-identity-insert-transact-sql.md)<br /><br /> [SET-SPRACHE](../../t-sql/statements/set-language-transact-sql.md)<br /><br /> [SET OFFSETS](../../t-sql/statements/set-offsets-transact-sql.md)<br /><br /> [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md)|  
|Abfrageausführungsanweisungen|[SET ARITHABORT](../../t-sql/statements/set-arithabort-transact-sql.md)<br /><br /> [SET ARITHIGNORE](../../t-sql/statements/set-arithignore-transact-sql.md)<br /><br /> [SET FMTONLY](../../t-sql/statements/set-fmtonly-transact-sql.md)<br /><br /> Hinweis:[!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]<br /><br /> [SET NOCOUNT](../../t-sql/statements/set-nocount-transact-sql.md)<br /><br /> [SET NOEXEC](../../t-sql/statements/set-noexec-transact-sql.md)<br /><br /> [SET NUMERIC_ROUNDABORT](../../t-sql/statements/set-numeric-roundabort-transact-sql.md)<br /><br /> [SET PARSEONLY](../../t-sql/statements/set-parseonly-transact-sql.md)<br /><br /> [SET QUERY_GOVERNOR_COST_LIMIT](../../t-sql/statements/set-query-governor-cost-limit-transact-sql.md)<br /><br /> [SET ROWCOUNT](../../t-sql/statements/set-rowcount-transact-sql.md)<br /><br /> [SET TEXTSIZE](../../t-sql/statements/set-textsize-transact-sql.md)|  
|Anweisungen für ISO-Einstellungen|[SET ANSI_DEFAULTS](../../t-sql/statements/set-ansi-defaults-transact-sql.md)<br /><br /> [SET ANSI_NULL_DFLT_OFF](../../t-sql/statements/set-ansi-null-dflt-off-transact-sql.md)<br /><br /> [SET ANSI_NULL_DFLT_ON](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)<br /><br /> [SET ANSI_NULLS](../../t-sql/statements/set-ansi-nulls-transact-sql.md)<br /><br /> [SET ANSI_PADDING](../../t-sql/statements/set-ansi-padding-transact-sql.md)<br /><br /> [SET ANSI_WARNINGS](../../t-sql/statements/set-ansi-warnings-transact-sql.md)|  
|Statistikanweisungen|[SET FORCEPLAN](../../t-sql/statements/set-forceplan-transact-sql.md)<br /><br /> [SET SHOWPLAN_ALL](../../t-sql/statements/set-showplan-all-transact-sql.md)<br /><br /> [SET SHOWPLAN_TEXT](../../t-sql/statements/set-showplan-text-transact-sql.md)<br /><br /> [SET SHOWPLAN_XML](../../t-sql/statements/set-showplan-xml-transact-sql.md)<br /><br /> [SET STATISTICS IO](../../t-sql/statements/set-statistics-io-transact-sql.md)<br /><br /> [SET STATISTICS XML](../../t-sql/statements/set-statistics-xml-transact-sql.md)<br /><br /> [SET STATISTICS PROFILE](../../t-sql/statements/set-statistics-profile-transact-sql.md)<br /><br /> [SET STATISTICS TIME](../../t-sql/statements/set-statistics-time-transact-sql.md)|  
|Transaktionsanweisungen|[SET IMPLICIT_TRANSACTIONS](../../t-sql/statements/set-implicit-transactions-transact-sql.md)<br /><br /> [SET REMOTE_PROC_TRANSACTIONS](../../t-sql/statements/set-remote-proc-transactions-transact-sql.md)<br /><br /> [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)<br /><br /> [SET XACT_ABORT](../../t-sql/statements/set-xact-abort-transact-sql.md)|  
  
## <a name="considerations-when-you-use-the-set-statements"></a>Überlegungen beim Verwenden von SET-Anweisungen  
  
-   Alle SET-Anweisungen außer SET FIPS_FLAGGER, SET OFFSETS, SET PARSEONLY und SET QUOTED_IDENTIFIER werden zur Ausführungs- oder Laufzeit implementiert. Die genannten Anweisungen werden zur Analysezeit implementiert.  
  
-   Wenn eine SET-Anweisung in einer gespeicherten Prozedur oder einem Trigger ausgeführt wird, so wird der Wert der SET-Option wiederhergestellt, nachdem die gespeicherte Prozedur oder der Trigger die Steuerung zurückgegeben hat. Auch wenn eine SET-Anweisung in einer dynamischen SQL-Zeichenfolge angegeben wird, die ausgeführt wird, indem Sie entweder **Sp_executesql** oder ausführen, den Wert der Option "SET" wird wiederhergestellt, wenn in der dynamischen SQL-Zeichenfolge angegebene Batch die Steuerung zurückgegeben hat.  
  
-   Gespeicherte Prozeduren werden mit den SET-Einstellungen ausgeführt, die zur Ausführungszeit angegeben wurden. Ausgenommen hiervon sind SET ANSI_NULLS und SET QUOTED_IDENTIFIER. Gespeicherte Prozeduren, für die SET ANSI_NULLS oder SET QUOTED_IDENTIFIER angegeben ist, verwenden die Einstellung, die zur Erstellungszeit der gespeicherten Prozedur angegeben wurde. Bei Verwendung innerhalb einer gespeicherten Prozedur werden SET-Einstellungen ignoriert.  
  
-   Die **Benutzeroptionen** Einstellung des **Sp_configure** ermöglicht serverweite Einstellungen, und arbeitet datenbankübergreifend. Diese Einstellung wirkt außerdem wie eine explizite SET-Anweisung, mit der Ausnahme, dass sie zur Anmeldezeit erfolgt.  
  
-   Datenbankeinstellungen, die mithilfe von ALTER DATABASE festgelegt werden, sind nur auf Datenbankebene gültig und treten nur dann in Kraft, wenn sie explizit festgelegt werden. Datenbankeinstellungen überschreiben instanzoptionseinstellungen, die mithilfe von festgelegt sind **Sp_configure**.  
  
-   Bei jeder SET-Anweisung, die über die Einstellungen ON und OFF verfügt, können Sie die Einstellung ON oder OFF für mehrere SET-Optionen gleichzeitig angeben.  
  
    > [!NOTE]  
    >  Dies gilt nicht für die statistikbezogenen SET-Optionen.  
  
     Beispielsweise `SET QUOTED_IDENTIFIER, ANSI_NULLS ON` Legt QUOTED_IDENTIFIER und ANSI_NULLS auf ON fest.  
  
-   Einstellungen von SET-Anweisungen überschreiben die entsprechenden Einstellungen der Datenbankoptionen, die mithilfe von ALTER DATABASE festgelegt werden. Beispielsweise überschreibt der in einer SET ANSI_NULLS-Anweisung angegebene Wert die Datenbankeinstellung für ANSI_NULLs. Darüber hinaus einige Verbindungseinstellungen werden automatisch festgelegt auf, wenn ein Benutzer mit einer Datenbank auf Grundlage der Werte, die durch vorherige Verwendung der in Kraft getreten verbindet die **Sp_configure Benutzeroptionen** Einstellung oder die Werte, die für alle ODBC gelten und OLE DB-Verbindungen.  
  
-   Die Anweisungen ALTER, CREATE und DROP DATABASE berücksichtigen die Einstellung von SET LOCK_TIMEOUT nicht.  
  
-   Wenn eine globale oder zusammengefasste SET-Anweisung, wie z. B. SET ANSI_DEFAULTS, mehrere Einstellungen festlegt, setzt das Ausgeben einer solchen SET-Anweisung die vorherigen Einstellungen aller Optionen außer Kraft, auf die sich die zusammengefasste SET-Anweisung auswirkt. Wenn eine einzelne von einer zusammengefassten SET-Anweisung betroffene SET-Option explizit festgelegt wird, nachdem die zusammengefasste SET-Anweisung ausgegeben wurde, überschreibt die individuelle SET-Anweisung die entsprechenden Einstellungen der zusammengefassten SET-Anweisung.  
  
-   Wenn Batches verwendet werden, wird der Datenbankkontext durch den Batch bestimmt, der mithilfe der USE-Anweisung eingerichtet wurde. Ad-hoc-Abfragen und alle anderen Anweisungen, die außerhalb der gespeicherten Prozedur ausgeführt werden und sich in Batches befinden, übernehmen die Optionseinstellungen der Datenbank und der Verbindung, die mit der USE-Anweisung eingerichtet wurden.  
  
-   MARS-Anforderungen (Multiple Active Result Set) nutzen gemeinsam einen globalen Status, der die jeweils aktuellen Einstellungen der SET-Optionen für die Sitzung enthält. Bei der Ausführung kann jede Anforderung die SET-Optionen ändern. Die Änderungen gelten speziell für den Anforderungskontext, in dem sie festgelegt werden, und haben keine Auswirkungen auf andere gleichzeitige MARS-Anforderungen. Nachdem die Anforderungsausführung abgeschlossen ist, werden die neuen SET-Optionen jedoch in den globalen Status der Sitzung kopiert. Neue Anforderungen, die nach dieser Änderung unter der gleichen Sitzung ausgeführt werden, verwenden diese neuen SET-Optionseinstellungen.  
  
-   Wird eine gespeicherte Prozedur aus einem Batch oder einer anderen gespeicherten Prozedur heraus ausgeführt, so wird sie anhand der aktuellen Optionswerte der Datenbank ausgeführt, die die gespeicherte Prozedur enthält. Beispielsweise, wenn die gespeicherte Prozedur **db1.dbo. SP1** ruft gespeicherte Prozedur **db2.dbo.sp2**, gespeicherte Prozedur **sp1** unter den aktuellen Kompatibilitätsgrad ausgeführt wird Festlegen der Datenbank **db1**, sowie die gespeicherte Prozedur **sp2** wird innerhalb der aktuellen Einstellung des Kompatibilitätsgrades der Datenbank ausgeführt **db2**.  
  
-   Wenn eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung auf Objekte verweist, die in mehreren Datenbanken gespeichert sind, gelten der aktuelle Datenbankkontext und der aktuelle Verbindungskontext für die Anweisung. Befindet sich die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung in diesem Fall in einem Batch, handelt es sich bei dem aktuellen Verbindungskontext um die durch die USE-Anweisung definierte Datenbank. Befindet sich die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung in einer gespeicherten Prozedur, handelt es sich bei dem Verbindungskontext um die Datenbank, die die gespeicherte Prozedur enthält.  
  
-   Beim Erstellen und Bearbeiten von Indizes für berechnete Spalten oder indizierten Sichten müssen die SET-Optionen ARITHABORT, CONCAT_NULL_YIELDS_NULL, QUOTED_IDENTIFIER, ANSI_NULLS, ANSI_PADDING und ANSI_WARNINGS auf ON festgelegt sein. Die Option NUMERIC_ROUNDABORT muss auf OFF festgelegt sein.  
  
     Wenn eine dieser Optionen nicht auf die erforderlichen Werte festgelegt ist, schlagen die Aktionen INSERT, UPDATE, DELETE, DBCC CHECKDB und DBCC CHECKTABLE für die indizierten Sichten oder Tabellen mit Indizes für berechnete Spalten fehl. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] löst einen Fehler aus, wobei alle Optionen aufgelistet werden, die nicht ordnungsgemäß festgelegt sind. Außerdem verarbeitet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die SELECT-Anweisungen in diesen Tabellen oder indizierten Sichten so, als seien die Indizes auf den berechneten Spalten oder Sichten nicht vorhanden.  
  
  

