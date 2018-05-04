---
title: Automatische Optimierung | Microsoft Docs
description: Erfahren Sie mehr über die automatische Optimierung in SQL Server und Azure SQL-Datenbank
ms.custom: ''
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: automatic-tuning
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- performance tuning [SQL Server]
ms.assetid: ''
caps.latest.revision: ''
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: de3984b5005114a2b8644c99706dcce48ab873e0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="automatic-tuning"></a>Automatische Optimierung
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Die automatische Datenbankoptimierung bietet einen Einblick in die potentiellen Abfrageleistungsprobleme, empfiehlt Lösungen und kann identifizierte Probleme automatisch beheben.

Automatische Optimierung [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Sie benachrichtigt, sobald ein mögliches Leistungsproblem erkannt wird, und ermöglicht das Anwenden von korrekturmaßnahmen oder ermöglicht die [!INCLUDE[ssde_md](../../includes/ssde_md.md)] automatisch zu beheben von Leistungsproblemen.
Automatische Optimierung [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] ermöglicht es Ihnen, zu identifizieren und Beheben von Leistungsproblemen aufgrund **SQL Plan planauswahlregression**. Automatische Optimierung [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] erforderlichen Indizes erstellt und löscht nicht verwendete Indizes.

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] überwacht die Abfragen, die in der Datenbank ausgeführt werden und automatisch verbessert die Leistung der arbeitsauslastung an. [!INCLUDE[ssde_md](../../includes/ssde_md.md)] verfügt über einen integrierten Intelligence-Mechanismus, der automatisch zu optimieren und Verbessern der Leistung Ihrer Abfragen durch die dynamische Anpassung der Datenbank an Ihre arbeitsauslastung kann ein. Es gibt zwei Automatische Optimierung Funktionen, die verfügbar sind:

 -  **Automatische Plan Korrektur** (verfügbar in [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] und [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]), die problematischen Abfrageausführungspläne identifiziert und Korrekturen SQL Planen von Leistungsproblemen.
 -  **Automatische indexverwaltung** (verfügbar nur in [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]), Indizes, die in der Datenbank hinzugefügt werden soll, und die Indizes, die entfernt werden sollen, identifiziert.

## <a name="why-automatic-tuning"></a>Warum Automatische Optimierung?

Eine der Hauptaufgaben bei der klassischen datenbankverwaltung überwacht die Arbeitslast, identifizieren kritische [!INCLUDE[tsql_md](../../includes/tsql_md.md)] abfragt, Indizes, die hinzugefügt werden sollen, um die Leistung zu verbessern und selten verwendete Indizes. [!INCLUDE[ssde_md](../../includes/ssde_md.md)] bietet detaillierte Einblicke hinsichtlich der Abfragen und die Indizes, die Sie überwachen müssen. Kontinuierliche Überwachung der Datenbank ist jedoch eine Aufgabe schwer und mühsam insbesondere beim Umgang mit vielen Datenbanken. Verwalten einer großen Anzahl von Datenbanken möglicherweise gar nicht effizient führen. Anstelle von überwachen und optimieren die Datenbank manuell, sollten Sie delegieren einige der Überwachung und Optimierung von Aktionen an, die [!INCLUDE[ssde_md](../../includes/ssde_md.md)] mithilfe der Funktion zum automatischen Optimierung.

### <a name="how-does-automatic-tuning-works"></a>Wie funktioniert die automatische Optimierung?

Automatische Optimierung ist eine kontinuierliche Überwachung und Analyseprozess, der ständig über das Merkmal Ihrer arbeitsauslastung lernt und mögliche Probleme und Verbesserungen zu identifizieren.

![Automatische Optimierungsprozess](./media/tuning-process.png)

Dieser Prozess kann die Datenbank dynamisch angepasst an Ihre arbeitsauslastung durch suchen, welche Pläne und Indizes die Leistung Ihrer arbeitsauslastungen verbessert werden können und welche Indizes arbeitsauslastungen beeinträchtigen. Anhand dieser Ergebnisse können gilt Automatische Optimierung Optimierung Aktionen, die Leistung Ihrer arbeitsauslastung zu verbessern. Darüber hinaus überwacht Datenbank fortlaufend Leistung nach jeder Änderung am durch die automatische Optimierung, um sicherzustellen, dass es verbessert die Leistung Ihrer arbeitsauslastung. Alle Aktionen, die Leistung zu verbessern, haben nicht, wird automatisch zurückgesetzt. Diese Überprüfung ist ein wichtiges Feature, das sicherstellt, dass jede Änderung, die durch die automatische Optimierung der Leistung der arbeitsauslastung nicht abnimmt.

## <a name="automatic-plan-correction"></a>Automatische Plan Korrektur

Automatische Plan Korrektur ist eine Funktion zum automatischen Optimierung, die identifiziert **SQL plans Wahl Regression** und automatisch das Problem beheben, indem Sie den letzten bekannten guten Plan erzwingen.

### <a name="what-is-sql-plan-choice-regression"></a>Was ist SQL Plan Wahl Regression?

[!INCLUDE[ssdenoversion_md](../../includes/ssdenoversion_md.md)] Verwenden Sie verschiedene SQL-Pläne können zum Ausführen der [!INCLUDE[tsql_md](../../includes/tsql_md.md)] Abfragen. Abfragepläne hängen von den Statistiken, Indizes und anderen Faktoren ab. Der optimale Plan, die verwendet werden soll, führen Sie einige [!INCLUDE[tsql_md](../../includes/tsql_md.md)] Abfrage mit der Zeit ändern kann. In einigen Fällen der neue Plan möglicherweise nicht besser als der vorherige Schlüssel und der neue Plan kann einem Leistungsverlust führen.

 ![SQL-Plan Wahl Regression](media/plan-choice-regression.png "SQL Plan Wahl Regression") 

Wenn Sie den Plan Wahl Regression bemerken, sollten finden Sie einige gute vorherigen planen und ihn zwingen, anstatt die aktuelle eine `sp_query_store_force_plan` Prozedur.
[!INCLUDE[ssde_md](../../includes/ssde_md.md)] in [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] enthält Informationen zu zurückgestellten Pläne und korrigierende Maßnahmen empfohlen.
Darüber hinaus [!INCLUDE[ssde_md](../../includes/ssde_md.md)] können Sie diesen Prozess automatisieren, vollständig, und lassen [!INCLUDE[ssde_md](../../includes/ssde_md.md)] beheben Sie alle gefundenen Probleme im Zusammenhang mit den Änderungen an Abfrageplänen.

### <a name="automatic-plan-choice-correction"></a>Planen der automatischen Auswahl Korrektur

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] können automatisch auf die letzten bekannten guten Plan wechseln, wenn der Plan Wahl Regression erkannt wird.

![SQL-Plan Wahl Korrektur](media/force-last-good-plan.png "SQL Plan Wahl Korrektur") 

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] erkennt automatisch alle potenziellen Plan Wahl-Regression, einschließlich des Plans, der statt des falschen Plans verwendet werden soll.
Wenn die [!INCLUDE[ssde_md](../../includes/ssde_md.md)] wendet den letzten bekannten guten Plan, automatisch die Leistung des erzwungenen Plans überwacht. Wenn erzwungene Plan nicht besser als zurückgestellte Plan ist, wird der neue Plan unforced werden und die [!INCLUDE[ssde_md](../../includes/ssde_md.md)] wird einen neuen Plan kompiliert. Wenn [!INCLUDE[ssde_md](../../includes/ssde_md.md)] stellt sicher, dass der erzwungene Plan ist besser als zurückgestellte, erzwungenen Plans bis zu einer Neukompilierung (z. B. auf die nächste Änderung Statistiken oder dem Schema) beibehalten, sofern der zurückgestellten Plan besser ist.

Hinweis: Alle Pläne automatisch erzwungen werden nicht Persit auf einen Neustart des SQL Server-Instanz.

### <a name="enabling-automatic-plan-choice-correction"></a>Aktivieren der automatischen Plan Wahl Korrektur

Sie können die automatische Optimierung pro Datenbank aktivieren und angeben, dass der letzte geeignete Plan erzwungen werden soll, wenn eine Regression der Planänderung erkannt wird. Die automatische Optimierung wird durch folgenden Befehl aktiviert:

```sql   
ALTER DATABASE current
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON ); 
```
Sobald zu umgehen Sie diese option, [!INCLUDE[ssde_md](../../includes/ssde_md.md)] automatisch eine Empfehlung, bei denen die geschätzte CPU-Gewinn ist größer als 10 Sekunden, oder die Anzahl von Fehlern in den neuen Plan höher als die Anzahl von Fehlern in der empfohlenen Plan, zu erzwingen, und überprüfen Sie, ob die Erzwungene Plan ist besser als die der aktuellen Aktivität.

### <a name="alternative---manual-plan-choice-correction"></a>Alternative - manuelle Plan Wahl Korrektur

Ohne die automatische Optimierung müssen Benutzer ihr System regelmäßig überwachen und nach zurückgestellten Abfragen suchen. Plans rückläufig waren, sollten Benutzer gefunden, einige gute vorherigen planen und ihn zwingen, anstatt die aktuelle eine `sp_query_store_force_plan` Prozedur. Die bewährte Methode wäre die letzten bekannten guten Plan erzwungen werden, weil ältere Pläne möglicherweise aufgrund von Änderungen der Statistik oder der Index ungültig. Der Benutzer, der die letzten bekannten guten Plan erzwingt überwachen Leistung der Abfrage, die mit dem erzwungenen Plan ausgeführt wird, und prüfen, ob diese erzwungene Plan funktioniert wie erwartet. Abhängigkeit von den Ergebnissen der Überwachung und Analyse Plan erzwungen werden soll, oder Benutzer sollte eine andere Möglichkeit zum Optimieren der Abfrage suchen.
Manuell erzwungene Plänen sollte nicht immer erzwungen werden, da die [!INCLUDE[ssde_md](../../includes/ssde_md.md)] sollte in der Lage, Pläne zu übernehmen. Der Benutzer oder Datenbankadministrator sollte schließlich Erzwingung der Plan mit `sp_query_store_unforce_plan` Prozedur, und legen die [!INCLUDE[ssde_md](../../includes/ssde_md.md)] den optimalen Plan gefunden.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält alle erforderlichen Sichten und Prozeduren, die zum Überwachen der Leistung und Beheben von Problemen im Abfragespeicher erforderlich.

In [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], Plan planauswahlregression abfragespeichersichten System finden. In [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], [!INCLUDE[ssde_md](../../includes/ssde_md.md)] erkennt und zeigt mögliche Plan planauswahlregression und den empfohlenen Aktionen, die in angewendet werden sollen die [sys.dm_db_tuning_recommendations &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md) anzeigen. Die Ansicht zeigt Informationen über das Problem, das die Wichtigkeit der das Problem, und Details wie z. B. die identifizierten Abfrage, die zurückgestellte Plan-ID, die ID des Plans, der für den Vergleich, als Basislinie verwendet wurde und die [!INCLUDE[tsql_md](../../includes/tsql_md.md)] -Anweisung, die ausgeführt werden kann, zum Beheben der Problem.

| Typ | description | datetime | score | Details | … |
| --- | --- | --- | --- | --- | --- |
| `FORCE_LAST_GOOD_PLAN` | CPU-Zeit von 4 ms in 14 ms geändert | 3/17/2017 | 83 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |
| `FORCE_LAST_GOOD_PLAN` | CPU-Zeit in ms 84 aus 37 ms geändert | 3/16/2017 | 26 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |

Einige Spalten in dieser Ansicht werden in der folgenden Liste beschrieben:
 - Typ der empfohlenen Aktion - `FORCE_LAST_GOOD_PLAN`.
 - Beschreibung, die Informationen, warum enthält [!INCLUDE[ssde_md](../../includes/ssde_md.md)] geht davon aus, dass diese Änderung des Plans einem potenziellen Leistungsverlust ist.
 - "DateTime", wenn die potenzielle Regression erkannt wird.
 - Diese Empfehlung zum Ergebnis. 
 - Details zu den Problemen, wie z. B. ID erkannten Plan-ID der zurückgestellten Plan ID des Plans, die erzwungen werden soll, um das Problem zu beheben, [!INCLUDE[tsql_md](../../includes/tsql_md.md)]
 Skript, das zum Beheben des Problems usw. angewendet werden kann. Details sind in gespeicherten [JSON-Format](../../relational-databases/json/index.md).

Verwenden Sie die folgende Abfrage aus, um ein Skript zu erhalten, die das Problem und zusätzliche Informationen zu den geschätzten behebt erhalten:

```sql   
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount+recommendedPlanExecutionCount)
                  *(regressedPlanCpuTimeAverage-recommendedPlanCpuTimeAverage)/1000000,
      error_prone = IIF(regressedPlanErrorCount>recommendedPlanErrorCount, 'YES','NO')
FROM sys.dm_db_tuning_recommendations
  CROSS APPLY OPENJSON (Details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            [current plan_id] int '$.regressedPlanId',
            [recommended plan_id] int '$.recommendedPlanId',

            regressedPlanErrorCount int,
            recommendedPlanErrorCount int,

            regressedPlanExecutionCount int,
            regressedPlanCpuTimeAverage float,
            recommendedPlanExecutionCount int,
            recommendedPlanCpuTimeAverage float

          ) as planForceDetails;
```

[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]     

| reason | score | Skript (script) | Abfrage\_Id | aktuellen Plan\_Id | Empfohlene Plan\_Id | Geschätzte\_zu erhalten | Fehler\_fehleranfällig
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CPU-Zeit von 3 ms in 46 ms geändert | 36 | EXEC-sp\_Abfrage\_speichern\_erzwingen\_Plan 12, 17; | 12 | 28 | 17 | 11.59 | 0

`estimated_gain` Stellt die geschätzte Anzahl von Sekunden an, die gespeichert werden würde, wenn der empfohlene Plan statt des aktuellen Plans ausgeführt werden würde. Der empfohlene Plan sollte anstelle der aktuellen Plan erzwungen werden, wenn der Gewinn größer als 10 Sekunden ist. Wenn weitere Fehler vorliegen (z. B. Timeouts oder abgebrochenen Ausführungen) im aktuellen Plan als in der empfohlenen planen, die Spalte `error_prone` würde festgelegt werden, auf den Wert `YES`. Fehler fehleranfällig Plan ist ein weiterer Grund, warum der empfohlene Plan anstelle des aktuellen Geschäftsjahrs erzwungen werden soll.

Obwohl [!INCLUDE[ssde_md](../../includes/ssde_md.md)] enthält alle Informationen erforderlich, um den Plan planauswahlregression; kontinuierliche Überwachung, und Beheben von Leistungsproblemen zu identifizieren sind möglicherweise ein zeitraubender Prozess. Automatische Optimierung wird dieser Prozess wesentlich einfacher.

Hinweis: Die Daten in dieser DMV bleibt nach einem Neustart des SQL Server-Instanz nicht bestehen.

## <a name="automatic-index-management"></a>Automatische indexverwaltung

In [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], indexverwaltung ist einfach da [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] lernt über Ihre arbeitsauslastung und stellt sicher, dass Ihre Daten immer optimal indiziert ist. Richtige Indexentwurf ist entscheidend für eine optimale Leistung Ihrer arbeitsauslastung und automatische indexverwaltung ermöglicht Ihnen Ihre Indizes zu optimieren. Automatische indexverwaltung kann entweder Beheben von Leistungsproblemen in falsch indizierte Datenbanken oder verwalten und verbessern Sie die Indizes für das Datenbankschema der vorhandenen. Automatische Optimierung [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] führt die folgenden Aktionen aus:

 - Identifiziert die Indizes, die Leistung Ihrer T-SQL-Abfragen verbessern können, die Daten aus den Tabellen zu lesen.
 - Gibt das redundante Indizes bzw. Indizes, die in längeren Zeitraum nicht verwendet wurden, die entfernt werden konnte. Entfernen unnötiger Indizes verbessert die Leistung von Abfragen, die Daten in Tabellen zu aktualisieren.

### <a name="why-do-you-need-index-management"></a>Warum benötigen Sie indexverwaltung?

Indizes beschleunigen einige Abfragen, die Daten aus den Tabellen gelesen; Sie können jedoch Abfragen verlangsamt, die Daten aktualisieren. Beim Erstellen eines Indexes und welche Spalten sorgfältig analysieren, müssen Sie in den Index aufgenommen werden sollen. Einige Indizes können nicht nach einiger Zeit erforderlich sein. Aus diesem Grund müssen Sie in regelmäßigen Abständen zu identifizieren und löscht die Indizes, die keine von Vorteil sein. Wenn Sie nicht verwendete Indizes ignorieren, würde die Leistung von Abfragen, die Daten zu aktualisieren ohne keinen Vorteil darin, auf die Abfragen verringert werden, die Daten lesen. Nicht verwendete Indizes Einfluss auf auch auf die gesamtleistung des Systems aus, da zusätzliche Updates unnötige Protokollierung benötigen.

Suchen von optimalen Satzes an Indizes, die Leistung der Abfragen zu verbessern, die Lesen von Daten aus den Tabellen und wirkt sich nur minimal auf Updates möglicherweise kontinuierlichen und komplexe Analysen erforderlich.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] verwendet integrierte Intelligence und erweiterter Regeln, die Ihre Abfragen analysieren identifizieren Indizes, die optimal für Ihre aktuelle Arbeitslasten wäre, und die Indizes entfernt werden können. Azure SQL-Datenbank wird sichergestellt, dass Sie einen minimalen erforderlichen Satz von Indizes verfügen, die die Abfragen optimieren, die Daten, wobei die minimierten Auswirkungen auf die andere Abfragen zu lesen.

### <a name="automatic-index-management"></a>Automatische indexverwaltung

Zusätzlich zur Erkennung [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] identifizierte Empfehlungen automatisch anwenden können. Wenn Sie feststellen, dass die integrierten Regeln auf die Leistung Ihrer Datenbank verbessern, können Sie [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] automatisch Ihre Indizes zu verwalten.

Zum Aktivieren der automatischen Optimierung in Azure SQL-Datenbank und die Funktion zum automatischen Optimierung Ihrer arbeitsauslastung vollständig verwalten können, finden Sie unter [Aktivieren der automatischen Optimierung in Azure SQL-Datenbank, die mit Azure-Portal](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-automatic-tuning-enable).

Wenn die [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] gilt eine Empfehlung CREATE Index- oder DROP INDEX automatisch überwacht die Leistung von Abfragen, die vom Index betroffen sind. Neuer Index werden nur dann, wenn Leistungsdaten der betroffenen Abfragen verbessert werden beibehalten. Der gelöschte Index wird automatisch neu erstellt werden, wenn es gibt einige Abfragen, die aufgrund der Abwesenheit des Indexes langsamer ausgeführt.

### <a name="automatic-index-management-considerations"></a>Überlegungen zur Verwaltung von automatischen index

Schritte zum Erstellen von erforderlichen Indizes in [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] verbrauchen Ressourcen und zeitlich Arbeitsleistung auswirken kann. Um die Auswirkungen der Erstellung eines Indexes für die Arbeitsleistung zu minimieren, sucht Azure SQL-Datenbank die entsprechenden Zeitfenster für jeden Index Management-Vorgang. Tuning Aktion wird verschoben, wenn sich die Datenbank Ressourcen zum Ausführen der arbeitsauslastung und gestartet, wenn die Datenbank mit ausreichend freiem nicht verwendete Ressourcen, die für den Wartungstask verwendet werden können. Eine wichtige Funktion in die automatische indexverwaltung ist eine Überprüfung der Aktionen. Wenn Azure SQL-Datenbank erstellt oder Index löscht, analysiert ein Überwachungsprozess Leistung Ihrer arbeitsauslastung, um sicherzustellen, dass die Aktion, die Leistung verbessert. Wenn sie erhebliche Verbesserung – geschaltet haben nicht, wird die Aktion sofort zurückgesetzt. Auf diese Weise wird sichergestellt, dass Azure SQL-Datenbank, dass automatische Aktionen nicht negativ auf die Leistung Ihrer arbeitsauslastung auswirken. Durch die automatische Optimierung erstellte Indizes sind für Wartungsvorgang auf das zugrunde liegende Schema transparent. Schemaänderungen, z. B. löschen oder Umbenennen von Spalten werden durch das Vorhandensein von automatisch erstellten Indizes nicht blockiert. Indizes, die automatisch, indem Sie Azure SQL-Datenbank erstellt werden werden sofort gelöscht, wenn im Zusammenhang, Tabelle oder Spalten wird gelöscht.

### <a name="alternative---manual-index-management"></a>Alternative - manuelle indexverwaltung

Ohne automatische indexverwaltung, müssten die Benutzer manuell Abfragen [Sys. dm_db_missing_index_details &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md) Sicht zu suchen, die möglicherweise die Leistung zu verbessern, erstellen Sie Indizes, die mithilfe der Angaben Indizes in dieser Sicht und manuell Überwachen der Leistung der Abfrage bereitgestellt. Um die Indizes zu suchen, die gelöscht werden sollen, müssen Benutzer operational Verwendungsstatistik der Indizes zu suchen, die selten verwendete Indizes überwachen.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] vereinfacht diesen Vorgang. [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] Ihre Arbeitslast analysiert, die Abfragen identifiziert, die mit einem neuen Index schneller ausgeführt werden konnte und oder doppelte Tabellenindizes identifiziert. Weitere Informationen zur Identifikation von Indizes, die zur geändert werden sollte [finden Sie im Azure-Portal indexempfehlungen](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-advisor-portal).

## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_automatic_tuning_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)  
 [Sys.dm_db_tuning_recommendations &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)     
 [sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)           
 [database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON-Funktionen](../../relational-databases/json/index.md)
