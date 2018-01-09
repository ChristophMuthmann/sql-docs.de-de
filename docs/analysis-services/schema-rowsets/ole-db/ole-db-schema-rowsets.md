---
title: OLE DB-Schemarowsets | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- schema rowsets [OLE DB]
- schema rowsets [Analysis Services], OLE DB
- OLE DB schema rowsets
- rowsets [Analysis Services], OLE DB
ms.assetid: ca2ee87a-ba04-4501-9125-33934c58ab31
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 59d17cb1345f7ba32a2cbaac27f5ec002aadfa40
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="ole-db-schema-rowsets"></a>OLE DB-Schemarowsets
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Die folgenden OLE DB-Schemarowsets werden vom unterstützt die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA)-Anbieter. Verwenden der **DISCOVER_ENUMERATORS** Rowset mit der [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) -Methode überprüft, ob ein bestimmter Datenquellenanbieter ein Rowset unterstützt.  
  
 Weitere Informationen über diese Rowsets finden Sie im Thema "Schema Rowsets" im Abschnitt "OLE DB Programmer's Reference" der MSDN® Library auf der [!INCLUDE[msCoName](../../../includes/msconame-md.md)]-Website.  
  
 In der folgenden Tabelle werden diese Schemarowsets beschrieben.  
  
|Rowset|Description|  
|------------|-----------------|  
|**DBSCHEMA_ASSERTIONS**|Gibt die im Katalog definierten Assertionen an, deren Eigentümer ein angegebener Benutzer ist.|  
|[DBSCHEMA_CATALOGS-Rowset](../../../analysis-services/schema-rowsets/ole-db/dbschema-catalogs-rowset.md) <sup>1</sup>|Identifiziert die physischen Attribute zugeordneten Kataloge, die von der Datenbank-Managementsystem (DBMS) zugegriffen werden kann. Für einige Systeme, beispielsweise [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Access, ist möglicherweise nur ein Katalog verfügbar. Für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] listet dieses Rowset alle in der Systemdatenbank definierten Kataloge (Datenbanken) auf.|  
|**DBSCHEMA_CHARACTER_SETS**|Gibt die im Katalog definierten Zeichensätze an, auf die ein angegebener Benutzer zugreifen kann.|  
|**DBSCHEMA_CHECK_CONSTRAINTS**|Gibt die CHECK-Einschränkungen an, die in dem Katalog definierten sind, dessen Eigentümer ein angegebener Benutzer ist.|  
|**DBSCHEMA_CHECK_CONSTRAINTS_BY_TABLE**|Gibt die CHECK-Einschränkungen für eine bestimmte Tabelle an, die in einem Katalog definiert sind, dessen Eigentümer ein angegebener Benutzer ist.|  
|**DBSCHEMA_COLLATIONS**|Gibt die im Katalog definierten Sortierungen an, auf die ein angegebener Benutzer zugreifen kann.|  
|**DBSCHEMA_COLUMN_DOMAIN_USAGE**|Gibt die im Katalog definierten Spalten an, die von einer im Katalog definierten Domäne abhängig sind und deren Eigentümer ein angegebener Benutzer ist.|  
|**DBSCHEMA_COLUMN_PRIVILEGES**|Gibt die im Katalog definierten Berechtigungen für Tabellenspalten an, die für einen angegebenen Benutzer verfügbar sind oder von diesem erteilt wurden.|  
|[DBSCHEMA_COLUMNS-Rowset](../../../analysis-services/schema-rowsets/ole-db/dbschema-columns-rowset.md) <sup>1</sup>|Stellt Spalteninformationen für alle Spalten bereit, die den bereitgestellten Einschränkungskriterien entsprechen.|  
|**DBSCHEMA_CONSTRAINT_COLUMN_USAGE**|Gibt die im Katalog definierten Spalten an, die von referenziellen Einschränkungen, UNIQUE-Einschränkungen, CHECK-Einschränkungen und Assertionen verwendet werden und deren Eigentümer ein angegebener Benutzer ist.|  
|**DBSCHEMA_CONSTRAINT_TABLE_USAGE**|Gibt die im Katalog definierten Tabellen an, die von referenziellen Einschränkungen, UNIQUE-Einschränkungen, CHECK-Einschränkungen und Assertionen verwendet werden und deren Eigentümer ein angegebener Benutzer ist.|  
|**DBSCHEMA_FOREIGN_KEYS**|Gibt die im Katalog von einem angegebenen Benutzer definierten Fremdschlüsselspalten an. Dieses Schemarowset wird auf der Grundlage mehrerer ISO-Schemasichten zur Erleichterung von Nicht-SQL-Programmierern erstellt Wenn unterstützt, muss dieses Schemarowset mit den zugehörigen ISO-Sichten synchronisiert werden (**REFERENTIAL_CONSTRAINTS** und **CONSTRAINT_COLUMN_USAGE**).|  
|**DBSCHEMA_INDEXES**|Gibt die im Katalog definierten Indizes an, deren Eigentümer ein angegebener Benutzer ist.|  
|**DBSCHEMA_KEY_COLUMN_USAGE**|Gibt die Spalten an, die im Katalog definiert sind und von einem bestimmten Benutzer als Schlüssel eingeschränkt wurden.|  
|**DBSCHEMA_PRIMARY_KEYS**|Gibt die im Katalog von einem angegebenen Benutzer definierten Primärschlüsselspalten an. Dieses Schemarowset wird auf der Grundlage einer ISO-Schemasicht zur Erleichterung von Nicht-SQL-Programmierern erstellt. Wenn unterstützt, muss dieses Schemarowset mit den zugehörigen ISO-Sicht synchronisiert werden (**CONSTRAINT_COLUMN_USAGE**).|  
|**DBSCHEMA_PROCEDURE_COLUMNS**|Gibt Informationen zu den Spalten von Rowsets zurück, die von Prozeduren zurückgegeben werden.|  
|**DBSCHEMA_PROCEDURE_PARAMETERS**|Gibt Informationen zu den Parametern und Rückgabecodes von Prozeduren zurück.|  
|**DBSCHEMA_PROCEDURES**|Gibt die im Katalog definierten Prozeduren an, deren Eigentümer ein angegebener Benutzer ist. Dies ist eine Erweiterung von OLE DB.|  
|[DBSCHEMA_PROVIDER_TYPES-Rowset](../../../analysis-services/schema-rowsets/ole-db/dbschema-provider-types-rowset.md) <sup>1</sup>|Gibt die von dem Datenanbieter unterstützten (Basis-)Datentypen an.|  
|**DBSCHEMA_REFERENTIAL_CONSTRAINTS**|Gibt die referenziellen Einschränkungen an, die in dem Katalog definiert sind, dessen Eigentümer ein angegebener Benutzer ist.|  
|**DBSCHEMA_SCHEMATA**|Gibt die Schemas an, dessen Eigentümer ein angegebener Benutzer ist.|  
|**DBSCHEMA_SQL_LANGUAGES**|Gibt die definierten Übereinstimmungsebenen, Optionen und Dialekte an, die von der SQL-Implementierung unterstützt werden, die die im Katalog definierten Daten verarbeitet.|  
|**DBSCHEMA_STATISTICS**|Gibt die im Katalog definierten Statistiken an, deren Eigentümer ein angegebener Benutzer ist.<br /><br /> In dieser Tabelle bezieht sich nicht auf die **TABLE_STATISTICS** Rowset.|  
|**DBSCHEMA_TABLE_CONSTRAINTS**|Gibt die Tabelleneinschränkungen an, die in dem Katalog definiert sind, dessen Eigentümer ein angegebener Benutzer ist.|  
|**DBSCHEMA_TABLE_PRIVILEGES**|Gibt die im Katalog definierten Berechtigungen für Tabellen an, die für einen angegebenen Benutzer verfügbar sind oder von diesem erteilt wurden.|  
|**DBSCHEMA_TABLE_STATISTICS**|Beschreibt den beim Anbieter verfügbaren Satz von Statistiken für Tabellen.<br /><br /> Dieses Rowset gehört nicht zum der **Statistiken** Rowset.|  
|[DBSCHEMA_TABLES-Rowset](../../../analysis-services/schema-rowsets/ole-db/dbschema-tables-rowset.md) <sup>1</sup>|Gibt die Measuregruppen und Dimensionen, die in als Tabellen verfügbar gemacht [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|**DBSCHEMA_TABLES_INFO** <sup>1</sup>|Gibt die im Katalog definierten Tabellen (einschließlich Sichten) an, auf die ein angegebener Benutzer zugreifen kann.|  
|**DBSCHEMA_TRANSLATIONS**|Gibt die im Katalog definierten Übersetzungen an, auf die ein angegebener Benutzer zugreifen kann.|  
|**DBSCHEMA_TRUSTEE**|Listet die Vertrauensnehmer einer Datenquelle auf.|  
|**DBSCHEMA_USAGE_PRIVILEGES**|Identifiziert die **Verwendung** Berechtigungen für Objekte, die im Katalog definierten sind und stehen oder von diesem erteilt von einem angegebenen Benutzer.|  
|**DBSCHEMA_VIEW_COLUMN_USAGE**|Gibt die im Katalog definierten Sichten an, auf die ein angegebener Benutzer zugreifen kann.|  
|**DBSCHEMA_VIEW_TABLE_USAGE**|Gibt die Tabellen an, von denen im Katalog definierte Tabellen in Sichten, deren Eigentümer ein angegebener Benutzer ist, abhängig sind.|  
|**DBSCHEMA_VIEWS**|Gibt die im Katalog definierten Sichten an, auf die ein angegebener Benutzer zugreifen kann.|  
  
 <sup>1</sup> gibt Schemarowsets unterstützt, indem Sie die MSOLAP-Datenquellenanbieter für den [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA-Anbieter.  
  
## <a name="see-also"></a>Siehe auch  
 [DISCOVER_ENUMERATORS-Rowset](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)   
 [Analysis Services-Schemarowsets](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
