---
title: Als veraltet markierte Funktionen der Volltextsuche in SQL Server 2016 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/19/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- deprecated features [full-text search]
- full-text search [SQL Server], deprecated features
- full-text queries [SQL Server], proximity
ms.assetid: ab0d799c-ba79-4459-837b-c4862730dafd
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d3d2f146e006853a12e3cda5e94fca3f1d6d2380
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="deprecated-full-text-search-features-in-sql-server-2016"></a>Als veraltet markierte Funktionen der Volltextsuche in SQL Server 2016
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In diesem Thema werden die als veraltet markierten Funktionen der Volltextsuche beschrieben, die in SQL Server noch verfügbar sind. Diese Funktionen werden voraussichtlich in einer zukünftigen Version entfernt. Verwenden Sie in neuen Anwendungen keine veralteten Funktionen.  
  
Sie können die Nutzung von als veralteten Funktionen mithilfe des Objektleistungsindikators **SQL Server: Als veraltet markierte Funktionen** und mithilfe von Ablaufverfolgungsereignissen überwachen. Weitere Informationen finden Sie unter [Verwenden von SQL Server-Objekten](../../relational-databases/performance-monitor/use-sql-server-objects.md).  
  
## <a name="features-no-longer-supported"></a>Funktionen werden nicht mehr unterstützt  

  
|Als veraltet markierte Funktion|Ersatz|Feature name|Feature ID|  
|------------------------|-----------------|------------------|----------------|  
|FULLTEXTCATALOGPROPERTY-Eigenschaft: LogSize|Keine.|FULLTEXTCATALOGPROPERTY**('LogSize')**|211|  
|FULLTEXTSERVICEPROPERTY-Eigenschaft:<br /><br /> ConnectTimeout<br /><br /> DataTimeout|Keine.|FULLTEXTSERVICEPROPERTY**('ConnectTimeout')**<br /><br /> FULLTEXTSERVICEPROPERTY**('DataTimeout'**)|210<br /><br /> 209|  
|sp_fulltext_catalog|CREATE FULL CATALOG<br /><br /> ALTER FULLTEXT CATALOG<br /><br /> DROP FULLTEXT CATALOG|sp_fulltext_catalog|84|  
|sp_fulltext_column<br /><br /> sp_fulltext_database<br /><br /> sp_fulltext_table|CREATE FULL INDEX<br /><br /> ALTER FULLTEXT INDEX<br /><br /> DROP FULLTEXT INDEX|sp_fulltext_column<br /><br /> sp_fulltext_database<br /><br /> sp_fulltext_table|86<br /><br /> 87<br /><br /> 85|  
|sp_help_fulltext_catalogs<br /><br /> sp_help_fulltext_catalog_components<br /><br /> sp_help_fulltext_catalogs_cursor<br /><br /> sp_help_fulltext_columns<br /><br /> sp_help_fulltext_columns_cursor<br /><br /> sp_help_fulltext_tables<br /><br /> sp_help_fulltext_tables_cursor|sys.fulltext_catalogs<br /><br /> sys.fulltext_index_columns<br /><br /> sys.fulltext_indexes|sp_help_fulltext_catalogs<br /><br /> sp_help_fulltext_catalog_components<br /><br /> sp_help_fulltext_catalogs_cursor<br /><br /> sp_help_fulltext_columns<br /><br /> sp_help_fulltext_columns_cursor<br /><br /> sp_help_fulltext_table<br /><br /> sp_help_fulltext_tables_cursor|88<br /><br /> 203<br /><br /> 90<br /><br /> 92<br /><br /> 93<br /><br /> 91<br /><br /> 89|  
|sp_fulltext_service action-Werte: clean_up, connect_timeout und data_timeout geben 0 (null) zurück|InclusionThresholdSetting|sp_fulltext_service @action=clean_up<br /><br /> sp_fulltext_service @action=connect_timeout<br /><br /> sp_fulltext_service @action=data_timeout|116<br /><br /> 117<br /><br /> 118|  
|sys.dm_fts_active_catalogs-Spalten:<br /><br /> is_paused<br /><br /> previous_status<br /><br /> previous_status_description<br /><br /> row_count_in_thousands<br /><br /> status<br /><br /> status_description<br /><br /> worker_count|Keine.|dm_fts_active_catalogs.is_paused<br /><br /> dm_fts_active_catalogs.previous_status<br /><br /> dm_fts_active_catalogs.previous_status_description<br /><br /> dm_fts_active_catalogs.row_count_in_thousands<br /><br /> dm_fts_active_catalogs.status<br /><br /> dm_fts_active_catalogs.status_description<br /><br /> dm_fts_active_catalogs.worker_count|218<br /><br /> 221<br /><br /> 222<br /><br /> 224<br /><br /> 219<br /><br /> 220<br /><br /> 223|  
|sys.dm_fts_memory_buffers-Spalte:<br /><br /> row_count|Keine.|dm_fts_memory_buffers.row_count|225|  
|sys.fulltext_catalogs-Spalten:<br /><br /> path<br /><br /> data_space_id<br /><br /> file_id-Spalten|Keine.|fulltext_catalogs.path<br /><br /> fulltext_catalogs.data_space_id<br /><br /> fulltext_catalogs.file_id|215<br /><br /> 216<br /><br /> 217|  
  
## <a name="features-not-supported-in-a-future-version-of-sql-server"></a>Funktionen, die in einer zukünftigen Version von SQL Server nicht unterstützt werden  
 Die folgenden Funktionen der Volltextsuche werden in der nächsten Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]noch unterstützt, aber in einer zukünftigen Version entfernt. Die betreffende Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wurde noch nicht festgelegt.  
  
 Der **Feature name** -Wert wird in Ablaufverfolgungsereignissen als ObjectName und in Leistungsindikatoren sowie sys.dm_os_performance_counters als Instanzname angezeigt. Der **Feature ID** -Wert wird in Ablaufverfolgungsereignissen als ObjectId angezeigt.  
  
|Als veraltet markierte Funktion|Ersatz|Feature name|Feature ID|  
|------------------------|-----------------|------------------|----------------|  
|Generischer NEAR-Operator für CONTAINS and CONTAINSTABLE:<br /><br /> {<simple_term> &#124; <prefix_term>}<br /><br /> {<br /><br /> { { NEAR &#124; ~ }    {<simple_term> &#124; <prefix_term>} } [...*n*]<br /><br /> }|Der benutzerdefinierte NEAR-Operator:<br /><br /> NEAR(<br /><br /> {   {<simple_term> &#124; <prefix_term>} [ ,…*n* ]<br /><br /> &#124; ( {<simple_term> &#124; <prefix_term>} [,…*n*] )<br /><br /> [,<distance> [,<order>] ]<br /><br /> }<br /><br /> )<br /><br /> <distance> ::= {*integer* &#124; **MAX**}<br /><br /> <order> ::= {TRUE &#124; **FALSE**}|FULLTEXT_OLD_NEAR_SYNTAX|247|  
|CREATE FULLTEXT CATALOG (Option):<br /><br /> IN PATH '*rootpath*'<br /><br /> ON FILEGROUP *filegroup*|Keine.|CREATE FULLTEXT CATLOG IN PATH<br /><br /> Keine.<sup>*</sup>|237<br /><br /> Keine.*|  
|DATABASEPROPERTYEX-Eigenschaft: IsFullTextEnabled|Keine.|DATABASEPROPERTYEX**('IsFullTextEnabled')**|202|  
|sp_detach_db-Option:<br /><br /> [ @keepfulltextindexfile = ] '*KeepFulltextIndexFile*'|Keine.|sp_detach_db @keepfulltextindexfile|226|  
|sp_fulltext_service action-Werte: resource_usage hat keine Funktion.|InclusionThresholdSetting|sp_fulltext_service @action= resource_usage|200|  
  
 *Das Objekt **SQL Server: Als veraltet markierte Funktionen**  überwacht keine Vorkommen der *filegroup* CREATE FULLTEXT CATALOG ON FILEGROUP.  
  
  
