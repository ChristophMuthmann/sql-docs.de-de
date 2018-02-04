---
title: Sys.dm_db_tuning_recommendations (Transact-SQL) | Microsoft Docs
description: Erfahren Sie, wie potenzielle Leistungsprobleme zu finden und empfohlene Updates in SQL Server und Azure SQL-Datenbank
ms.custom: 
ms.date: 07/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_db_tuning_recommendations
- dm_db_tuning_recommendations
- sys.dm_db_tuning_recommendations_TSQL
- dm_db_tuning_recommendations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database tuning recommendations feature [SQL Server], sys.dm_db_tuning_recommendations dynamic management view
- sys.dm_db_tuning_recommendations dynamic management view
ms.assetid: ced484ae-7c17-4613-a3f9-6d8aba65a110
caps.latest.revision: 
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 43acc4c2bfbcb9458f93f2ad89414e3781a7836d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmdbtuningrecommendations-transact-sql"></a>Sys.DM\_Db\_Optimierung\_Empfehlungen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Gibt ausführliche Informationen zu den Empfehlungen für die Optimierung.  
  
 In [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]können dynamische Verwaltungssichten keine Informationen verfügbar machen, die sich auf die Datenbankkapselung auswirken würden oder die sich auf andere Datenbanken beziehen, auf die der Benutzer Zugriff hat. Um zu vermeiden, dass diese Informationen verfügbar gemacht werden, wird jede Zeile mit Daten, die zum verbundenen Mandanten gehören, herausgefiltert.

| **Spaltenname** | **Datentyp** | **Beschreibung** |
| --- | --- | --- |
| **name** | **nvarchar(4000)** | Eindeutiger Name der Empfehlung. |
| **type** | **nvarchar(4000)** | Der Name der automatischen Optimierung Option, die die Empfehlung, z. B. erzeugt,`FORCE_LAST_GOOD_PLAN` |
| **reason** | **nvarchar(4000)** | Der Grund, warum diese Empfehlung bereitgestellt wurde. |
| **valid\_since** | **datetime2** | Beim ersten Start wurde diese Empfehlung generiert. |
| **last\_refresh** | **datetime2** | Zeitpunkt der letzten wurde diese Empfehlung generiert. |
| **state** | **nvarchar(4000)** | JSON-Dokument, das den Zustand der Empfehlung beschreibt. Folgende Felder sind verfügbar:<br />-   `currentValue`-aktuellen Status der Empfehlung.<br />-   `reason`– Konstante, die beschreibt, warum die Empfehlung im aktuellen Zustand ist.|
| **is\_executable\_action** | **bit** | 1 = die Empfehlung kann ausgeführt werden, für die Datenbank über [!INCLUDE[tsql_md](../../includes/tsql_md.md)] Skript.<br />0 = die Empfehlung kann nicht in der Datenbank ausgeführt werden (z. B.: Informationen nur oder wiederhergestellten Empfehlung) |
| **ist\_revertable\_Aktion** | **bit** | 1 = die Empfehlung automatisch überwacht und vom Datenbankmodul zurückgesetzt.<br />0 = die Empfehlung nicht automatisch überwacht oder zurückgesetzt. Die meisten &quot;ausführbare&quot; Maßnahmen &quot;revertable&quot;. |
| **execute\_action\_start\_time** | **datetime2** | Datum, an die Empfehlung angewendet wird. |
| **Führen Sie\_Aktion\_Dauer** | **Uhrzeit** | Die Dauer der Aktion ausführen. |
| **execute\_action\_initiated\_by** | **nvarchar(4000)** | `User`= Benutzer erzwungen manuell Plan in der Empfehlung. <br /> `System`= System wird automatisch Empfehlung angewendet. |
| **execute\_action\_initiated\_time** | **datetime2** | Datum, an die Empfehlung angewendet wurde. |
| **revert\_action\_start\_time** | **datetime2** | Datum, an die Empfehlung wiederhergestellt wurde. |
| **REVERT\_Aktion\_Dauer** | **Uhrzeit** | Die Dauer der Aktion wieder her. |
| **revert\_action\_initiated\_by** | **nvarchar(4000)** | `User`= Plan für die manuell unforced empfohlene Benutzer. <br /> `System`= Automatisch wiederhergestellt System Empfehlung. |
| **REVERT\_Aktion\_initiiert\_Zeit** | **datetime2** | Datum, an die Empfehlung wiederhergestellt wurde. |
| **score** | **int** | Für diese Empfehlung für den 0-100 Wert/Auswirkungen geschätzte Skalierung (je größer die besser) |
| **details** | **nvarchar(max)** | JSON-Dokument, das weitere Details über die Empfehlung zurück. Folgende Felder sind verfügbar:<br /><br />`planForceDetails`<br />-    `queryId`-Abfrage\_-Id der zurückgestellte Abfrage.<br />-    `regressedPlanId`-"Plan_id" zurückgestellte Plans.<br />-   `regressedPlanExecutionCount`-Anzahl der Ausführungen der Abfrage mit zurückgestellte Plan verfügen, bevor die Regression erkannt wird.<br />-    `regressedPlanAbortedCount`-Anzahl der Fehler während der Ausführung des Plans zurückgestellte gefunden.<br />-    `regressedPlanCpuTimeAverage`-Durchschnittliche CPU-Zeit von der zurückgestellte Abfrage genutzt werden, bevor die Regression erkannt wird.<br />-    `regressedPlanCpuTimeStddev`-Standardabweichung CPU-Zeit, die von der zurückgestellte Abfrage vor der Regression genutzt wurde erkannt.<br />-    `recommendedPlanId`-"Plan_id" des Plans, die erzwungen werden soll.<br />-   `recommendedPlanExecutionCount`-Anzahl der Ausführungen der Abfrage mit dem Plan, der erzwungen werden soll, bevor die Regression erkannt wird.<br />-    `recommendedPlanAbortedCount`-Anzahl der erkannten Fehler während der Ausführung des Plans, die erzwungen werden soll.<br />-    `recommendedPlanCpuTimeAverage`-Durchschnittliche CPU-Zeit verbraucht, die von der Abfrage, die mit dem Plan erzwungen werden soll (wird berechnet, bevor die Regression erkannt wird) ausgeführt.<br />-    `recommendedPlanCpuTimeStddev`Standardabweichung der CPU-Zeit, die von der zurückgestellte Abfrage vor der Regression genutzt wurde erkannt.<br /><br />`implementationDetails`<br />-  `method`– Die Methode, die verwendet werden soll, um die Regression zu korrigieren. Ist der Wert immer `TSql`.<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql_md.md)]Skript, das ausgeführt werden soll, um die empfohlenen Plan zu erzwingen. |
  
## <a name="remarks"></a>Hinweise  
 Zurückgegebene Informationen `sys.dm_db_tuning_recommendations` wird aktualisiert, wenn das Datenbankmodul identifiziert potenzielle Regression der abfrageleistung und wird nicht beibehalten. Empfehlungen werden nur bis zum beibehalten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu gestartet wird. Datenbankadministratoren sollten regelmäßig Sicherungskopien von der optimierungsempfehlung des Datenbankoptimierungsratgebers erstellen, wenn sie nach dem wiederverwenden des Servers beibehalten werden soll. 

 `currentValue`Feld in der `state` Spalte möglicherweise die folgenden Werte aufweisen:
 | Status | Description |
 |--------|-------------|
 | `Active` | Es wird empfohlen, aktive und noch nicht angewendet. Benutzer kann Empfehlungsskript und manuell ausführen. |
 | `Verifying` | Empfehlung angewendet, indem [!INCLUDE[ssde_md](../../includes/ssde_md.md)] und interne Überprüfungsvorgang vergleicht die Leistung des erzwungenen Plans mit dem zurückgestellte Plan. |
 | `Success` | Empfehlung wird erfolgreich angewendet. |
 | `Reverted` | Empfehlung wird zurückgesetzt, da es keine deutliche Leistungssteigerungen sind. |
 | `Expired` | Empfehlung ist abgelaufen und kann nicht mehr angewendet werden. |

JSON-Dokument in `state` Spalte enthält den Grund, die beschreibt, warum die Empfehlung im aktuellen Zustand ist. Werte in das Feld "Grund" können sein: 

| Reason | Description |
|--------|-------------|
| `SchemaChanged` | Empfehlung ist abgelaufen, da das Schema einer Tabelle verwiesen wird, geändert wird. |
| `StatisticsChanged`| Empfehlung abgelaufen aufgrund der Änderung der Statistik für eine Tabelle verwiesen wird. |
| `ForcingFailed` | Empfohlene Plan kann nicht auf einer Abfrage erzwungen werden. Suchen der `last_force_failure_reason` in der [Sys. query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) Ansicht, um die Ursache des Fehlers gefunden. |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN`Option ist während der Überprüfung durch den Benutzer deaktiviert. Aktivieren Sie `FORCE_LAST_GOOD_PLAN` -Option [ALTER DATABASE legen AUTOMATIC_TUNING &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) -Anweisung oder erzwingen Sie den Plan manuell mithilfe des Skripts im `[details]` Spalte. |
| `UnsupportedStatementType` | Plan kann nicht in der Abfrage nicht erzwungen werden. Beispiele für nicht unterstützte Abfragen sind Cursor und `INSERT BULK` Anweisung. |
| `LastGoodPlanForced` | Empfehlung wird erfolgreich angewendet. |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)] identifiziert potenzielle Leistungsverlust, aber die `FORCE_LAST_GOOD_PLAN` Option ist nicht aktiviert – siehe [ALTER DATABASE legen AUTOMATIC_TUNING &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md). Empfehlung manuell anzuwenden, oder aktivieren Sie `FORCE_LAST_GOOD_PLAN` Option. |
| `VerificationAborted`| Überprüfung wird aufgrund der Neustart oder ein Cleanup der Abfragespeicher abgebrochen. |
| `VerificationForcedQueryRecompile`| Abfrage wird neu kompiliert werden, da es keine deutliche leistungsverbesserung ist. |
| `PlanForcedByUser`| Benutzer manuell erzwungen der Plan mit [Sp_query_store_force_plan &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md) Prozedur. |
| `PlanUnforcedByUser` | Benutzer manuell unforced der Plan mit [Sp_query_store_unforce_plan &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md) Prozedur. |

 Statistik in der Spalte "Details" (z. B. aktuelle CPU-Zeit) Laufzeitstatistiken Plan nicht anzeigen. Zum Zeitpunkt der Erkennung von Regression stammen und eine Beschreibung für verdeutlichen, warum die Empfehlung Details [!INCLUDE[ssde_md](../../includes/ssde_md.md)] Leistungsverlust identifiziert. Verwendung `regressedPlanId` und `recommendedPlanId` abzufragende [Katalogsichten des Abfragespeichers](../../relational-databases/performance/how-query-store-collects-data.md) genaue Plan Laufzeitstatistiken gefunden.

## <a name="using-tuning-recommendations-information"></a>Verwenden die Optimierung Empfehlungsinformationen  
 Sie können die folgende Abfrage verwenden, beim Abrufen des T-SQL-Skripts, mit denen das Problem behoben wird:  
 
```
SELECT name, reason, score,
        JSON_VALUE(details, '$.implementationDetails.script') as script,
        details.* 
FROM sys.dm_db_tuning_recommendations
    CROSS APPLY OPENJSON(details, '$.planForceDetails')
                WITH (  query_id int '$.queryId',
                        regressed_plan_id int '$.regressedPlanId',
                        last_good_plan_id int '$.recommendedPlanId') as details
WHERE JSON_VALUE(state, '$.currentValue') = 'Active'
```
  
 Weitere Informationen zu JSON-Funktionen, die zum Abfragewerte in der Empfehlung-Ansicht verwendet werden können, finden Sie unter [JSON-Unterstützung](../../relational-databases/json/index.md) in [!INCLUDE[ssde_md](../../includes/ssde_md.md)].
  
## <a name="permissions"></a>Berechtigungen  
Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] benötigen Premium-Ebenen der `VIEW DATABASE STATE` Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die `Server admin` oder ein `Azure Active Directory admin` Konto.  
  
## <a name="see-also"></a>Siehe auch  
 [Automatische Optimierung](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [sys.database_automatic_tuning_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON-Unterstützung](../../relational-databases/json/index.md)
 
