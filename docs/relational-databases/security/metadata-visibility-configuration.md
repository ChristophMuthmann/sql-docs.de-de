---
title: Konfigurieren der Sichtbarkeit von Metadaten | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subcomponents visibility [SQL Server]
- metadata [SQL Server], visibility
- permissions [SQL Server], metadata access
- viewing metadata
- objects [SQL Server], metadata
- displaying metadata
- database metadata [SQL Server]
- metadata [SQL Server], permissions
ms.assetid: 50d2e015-05ae-4014-a1cd-4de7866ad651
caps.latest.revision: "51"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.openlocfilehash: f487f1add0343573ff70fd7fee49f28628c3da59
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="metadata-visibility-configuration"></a>Konfigurieren der Sichtbarkeit von Metadaten
  Die Sichtbarkeit von Metadaten ist auf sicherungsfähige Elemente eingeschränkt, bei denen der Benutzer entweder der Besitzer ist oder für die dem Benutzer eine Berechtigung erteilt wurde. Beispielsweise gibt die folgende Abfrage eine Zeile zurück, wenn dem Benutzer eine Berechtigung, wie etwa SELECT, für die `myTable`-Tabelle erteilt wurde.  
  
```  
SELECT name, object_id  
FROM sys.tables  
WHERE name = 'myTable';  
GO  
```  
  
 Wenn der Benutzer jedoch keine Berechtigungen für `myTable`hat, gibt die Abfrage ein leeres Resultset zurück.  
  
## <a name="scope-and-impact-of-metadata-visibility-configuration"></a>Gültigkeitsbereich und Auswirkung der Konfiguration der Metadatensichtbarkeit  
 Die Konfiguration der Metadatensichtbarkeit gilt nur für die folgenden sicherungsfähigen Elemente:  
  
|||  
|-|-|  
|Katalogsichten|[!INCLUDE[ssDE](../../includes/ssde-md.md)] **sp_help** -Prozeduren|  
|Metadaten ausgebende integrierte Funktionen|Informationsschemasichten|  
|Kompatibilitätssichten|Erweiterte Eigenschaften|  
  
 Die Konfiguration der Metadatensichtbarkeit gilt nicht für die folgenden sicherungsfähigen Elemente:  
  
|||  
|-|-|  
|Protokollversandsystemtabellen|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents|  
|Systemtabellen für Datenbank-Wartungspläne|Sicherungssystemtabellen|  
|Replikationssystemtabellen|Gespeicherte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_help **-Prozeduren für Replikations- und** -Agents|  
  
 Der eingeschränkte Metadatenzugriff bedeutet Folgendes:  
  
-   Anwendungen, die einen **public** -Metadatenzugriff voraussetzen, funktionieren nicht.  
  
-   Abfragen für Systemsichten geben möglicherweise nur eine Teilmenge von Zeilen zurück oder manchmal ein leeres Resultset.  
  
-   Metadaten ausgebende integrierte Funktionen, wie z. B. OBJECTPROPERTYEX, können NULL zurückgeben.  
  
-   Die gespeicherten [!INCLUDE[ssDE](../../includes/ssde-md.md)] **sp_help** geben möglicherweise nur eine Teilmenge von Zeilen oder NULL zurück.  
  
 SQL-Module, wie z. B. gespeicherte Prozeduren und Trigger, werden im Sicherheitskontext des Aufrufers ausgeführt und haben deshalb einen eingeschränkten Metadatenzugriff. Wenn z. B. im folgenden Code die gespeicherte Prozedur versucht, auf Metadaten aus der Tabelle `myTable` zuzugreifen, für die der Aufrufer keine Berechtigung hat, wird ein leeres Resultset zurückgegeben. In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wird eine Zeile zurückgegeben.  
  
```  
CREATE PROCEDURE assumes_caller_can_access_metadata  
BEGIN  
SELECT name, id   
FROM sysobjects   
WHERE name = 'myTable';  
END;  
GO  
```  
  
 Um Aufrufern das Anzeigen von Metadaten zu ermöglichen, können Sie ihnen die VIEW DEFINITION-Berechtigung für einen geeigneten Gültigkeitsbereich erteilen: für die Objektebene, für die Datenbankebene oder für die Serverebene. Wenn der Aufrufer im vorigen Beispiel über die VIEW DEFINITION-Berechtigung für `myTable` verfügt, gibt die gespeicherte Prozedur eine Zeile zurück. Weitere Informationen finden Sie unter [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md) und [GRANT (Datenbankberechtigungen)&#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
 Sie können die gespeicherte Prozedur auch so ändern, dass sie unter den Anmeldeinformationen des Besitzers ausgeführt wird. Wenn der Besitzer der Prozedur und der Besitzer der Tabelle identisch sind, gilt die Besitzverkettung, und der Sicherheitskontext des Prozedurbesitzers ermöglicht den Zugriff auf die Metadaten von `myTable`. In diesem Szenario gibt der folgende Code eine Zeile aus Metadaten an den Aufrufer zurück.  
  
> [!NOTE]  
>  Das folgende Beispiel verwendet die [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) -Katalogsicht anstelle der [sys.sysobjects](../../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md) -Kompatibilitätssicht.  
  
```  
CREATE PROCEDURE does_not_assume_caller_can_access_metadata  
WITH EXECUTE AS OWNER  
AS  
BEGIN  
SELECT name, id  
FROM sys.objects   
WHERE name = 'myTable'   
END;  
GO  
```  
  
> [!NOTE]  
>  Sie können EXECUTE AS verwenden, um vorübergehend zum Sicherheitskontext des Aufrufers zu wechseln. Weitere Informationen finden Sie unter [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md).  
  
## <a name="benefits-and-limits-of-metadata-visibility-configuration"></a>Vorteile und Einschränkungen der Konfiguration der Metadatensichtbarkeit  
 Die Konfiguration der Metadatensichtbarkeit kann eine wichtige Rolle in Ihrem allgemeinen Sicherheitsplan spielen. Es gibt jedoch Fälle, in denen ein technisch versierter Benutzer das Anzeigen einiger Metadaten erzwingen kann, wenn er das will. Wir empfehlen deshalb, dass Sie neben anderen Schutzmaßnahmen Metadatenberechtigungen bereitstellen.  
  
 Es ist theoretisch möglich, die Ausgabe von Metadaten in Fehlermeldungen zu erzwingen, indem die Reihenfolge der Prädikatauswertung in Abfragen verändert wird. Die Möglichkeit solcher *Trial and Error-Angriffe* ist nicht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-spezifisch. Dies wird durch die in relationaler Algebra zulässigen, assoziativen und kommutativen Transformationen impliziert. Sie können dieses Risiko verringern, indem Sie die in Fehlermeldungen zurückgegebenen Informationen einschränken. Um die Sichtbarkeit von Metadaten auf diese Weise noch stärker einzuschränken, können Sie den Server mit dem Ablaufverfolgungsflag 3625 starten. Mit diesem Ablaufverfolgungsflag wird die in Fehlermeldungen angezeigte Menge an Informationen eingeschränkt. Auf diese Weise können Sie die erzwungene Anzeige von Daten verhindern. Der Nachteil hierbei ist jedoch, dass die Fehlermeldungen nicht ausführlich sind und sie u. U. nicht zu Debugzwecken verwendet werden können. Weitere Informationen finden Sie unter [Startoptionen für den Datenbankmoduldienst](../../database-engine/configure-windows/database-engine-service-startup-options.md) und [Ablaufverfolgungsflags &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
 Für die folgenden Metadaten ist die erzwungene Anzeige nicht möglich:  
  
-   Der in der **provider_string** -Spalte von **sys.servers**gespeicherte Wert. Ein Benutzer, der keine ALTER ANY LINKED SERVER-Berechtigung hat, sieht in dieser Spalte einen NULL-Wert.  
  
-   Quellendefinition eines benutzerdefinierten Objekts wie z. B. eine gespeicherte Prozedur oder ein Trigger. Der Quellencode ist nur sichtbar, wenn eine der folgenden Aussagen zutrifft:  
  
    -   Der Benutzer hat die VIEW DEFINITION-Berechtigung für das Objekt.  
  
    -   Dem Benutzer wurde nicht die VIEW DEFINITION-Berechtigung für das Objekt verweigert, und er hat die CONTROL-, ALTER- oder TAKE OWNERSHIP-Berechtigung für das Objekt. Alle anderen Benutzer sehen NULL.  
  
-   Die Definitionsspalten in den folgenden Katalogsichten:  
  
    |||  
    |-|-|  
    |**sys.all_sql_modules**|**sys.sql_modules**|  
    |**sys.server_sql_modules**|**sys.check_constraints**|  
    |**sys.default_constraints**|**sys.computed_columns**|  
    |**sys.numbered_procedures**||  
  
-   Die **ctext** -Spalte in der **syscomments** -Kompatibilitätssicht.  
  
-   Die Ausgabe der **sp_helptext** -Prozedur.  
  
-   Die folgenden Spalten in den Informationsschemasichten:  
  
    |||  
    |-|-|  
    |INFORMATION_SCHEMA.CHECK_CONSTRAINTS.CHECK_CLAUSE|INFORMATION_SCHEMA.COLUMNS.COLUMN_DEFAULT|  
    |INFORMATION_SCHEMA.DOMAINS.DOMAIN_DEFAULT|INFORMATION_SCHEMA.ROUTINE_COLUMNS.COLUMN_DEFAULT|  
    |INFORMATION_SCHEMA.ROUTINES.ROUTINE_DEFINITION|INFORMATION_SCHEMA.VIEWS.VIEW_DEFINITION|  
  
-   OBJECT_DEFINITION()-Funktion  
  
-   Der in der password_hash-Spalte von **sys.sql_logins**gespeicherte Wert.  Einem Benutzer, der nicht über die CONTROL SERVER-Berechtigung verfügt, wird in dieser Spalte ein NULL-Wert angezeigt.  
  
> [!NOTE]  
>  Die SQL-Definitionen von integrierten Systemprozeduren und -funktionen sind über die **sys.system_sql_modules** -Katalogsicht, die gespeicherte Prozedur **sp_helptext** und mithilfe der OBJECT_DEFINITION()-Funktion öffentlich sichtbar.  
  
## <a name="general-principles-of-metadata-visibility"></a>Allgemeine Prinzipien der Sichtbarkeit von Metadaten  
 Es folgen einige allgemeine Prinzipien, die im Hinblick auf die Sichtbarkeit von Metadaten beachtet werden müssen:  
  
-   Feste Rollen und implizite Berechtigungen  
  
-   Geltungsbereich von Berechtigungen  
  
-   Vorrang von DENY  
  
-   Sichtbarkeit der Metadaten von Teilkomponenten  
  
### <a name="fixed-roles-and-implicit-permissions"></a>Feste Rollen und implizite Berechtigungen  
 Auf welche Metadaten feste Rollen zugreifen können, richtet sich nach den impliziten Berechtigungen der jeweiligen Rolle.  
  
### <a name="scope-of-permissions"></a>Geltungsbereich von Berechtigungen  
 Berechtigungen in einem Geltungsbereich implizieren die Sichtbarkeit von Metadaten in diesem Geltungsbereich sowie in allen eingeschlossenen Geltungsbereichen. So impliziert z. B. die SELECT-Berechtigung für ein Schema, dass der Empfänger dieser Berechtigung die SELECT-Berechtigung auch für alle in diesem Schema enthaltenen sicherungsfähigen Elemente hat. Das Erteilen der SELECT-Berechtigung für ein Schema ermöglicht deshalb einem Benutzer, die Metadaten des Schemas sowie aller Tabellen, Sichten, Funktionen, Prozeduren, Warteschlangen, Synonyme, Typen und XML-Schemaauflistungen, die im Schema enthalten sind, anzuzeigen. Weitere Informationen zu Bereichen finden Sie unter [Berechtigungshierarchie &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md).  
  
### <a name="precedence-of-deny"></a>Vorrang von DENY  
 DENY hat üblicherweise Vorrang vor anderen Berechtigungen. Wenn einem Datenbankbenutzer z. B. die EXECUTE-Berechtigung für ein Schema erteilt wurde, ihm aber die EXECUTE-Berechtigung für eine gespeicherte Prozedur in diesem Schema verweigert wurde, kann der Benutzer die Metadaten für diese gespeicherte Prozedur nicht anzeigen.  
  
 Wenn andererseits einem Benutzer die EXECUTE-Berechtigung für ein Schema verweigert wurde, ihm aber die EXECUTE-Berechtigung für eine gespeicherte Prozedur in diesem Schema erteilt wurde, kann der Benutzer die Metadaten für diese gespeicherte Prozedur nicht sehen.  
  
 Wenn in einem anderen Beispiel einem Benutzer die EXECUTE-Berechtigung erteilt und verweigert wurde (was über die verschiedenen Rollenmitgliedschaften möglich ist), dann hat DENY Vorrang, und der Benutzer kann die Metadaten für die gespeicherte Prozedur nicht anzeigen.  
  
### <a name="visibility-of-subcomponent-metadata"></a>Sichtbarkeit der Metadaten von Teilkomponenten  
 Die Sichtbarkeit von Teilkomponenten wie z. B. Indizes, CHECK-Einschränkungen und Triggern wird durch die Berechtigungen für das übergeordnete Element bestimmt. Für diese Teilkomponenten gibt es keine erteilbaren Berechtigungen. Wenn einem Benutzer z. B. einige Berechtigungen für eine Tabelle erteilt wurden, kann der Benutzer die Metadaten für Tabellen, Spalten, Indizes, CHECK-Einschränkungen, Trigger und andere Teilkomponenten der Tabelle anzeigen.  
  
#### <a name="metadata-that-is-accessible-to-all-database-users"></a>Metadaten, auf die alle Datenbankbenutzer Zugriff haben  
 Auf einige Metadaten muss der Zugriff durch alle Benutzer in einer bestimmten Datenbank gewährt werden. So haben z. B. Dateigruppen keine übertragbaren Berechtigungen. Deshalb kann einem Benutzer nicht die Berechtigung zum Zugriff auf die Metadaten einer Dateigruppe erteilt werden. Allerdings muss jeder Benutzer, der eine Tabelle erstellen kann, auch in der Lage sein, auf die Metadaten der Dateigruppe zuzugreifen, um die ON *filegroup* - oder TEXTIMAGE_ON *filegroup* -Klauseln der CREATE TABLE-Anweisung zu verwenden.  
  
 Die von den Funktionen DB_ID() und DB_NAME() zurückgegebenen Metadaten sind für alle Benutzer sichtbar.  
  
 In der folgenden Tabelle sind die Katalogsichten aufgeführt, die für die **public** -Rolle sichtbar sind.  
  
|||  
|-|-|  
|**sys.partition_functions**|**sys.partition_range_values**|  
|**sys.partition_schemes**|**sys.data_spaces**|  
|**sys.filegroups**|**sys.destination_data_spaces**|  
|**sys.database_files**|**sys.allocation_units**|  
|**sys.partitions**|**sys.messages**|  
|**sys.schemas**|**sys.configurations**|  
|**sys.sql_dependencies**|**sys.type_assembly_usages**|  
|**sys.parameter_type_usages**|**sys.column_type_usages**|  
  
## <a name="see-also"></a>Siehe auch  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [EXECUTE AS-Klausel &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Kompatibilitätssichten &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
