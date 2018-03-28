---
title: SERVERPROPERTY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SERVERPROPERTY_TSQL
- SERVERPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- SERVERPROPERTY function
- server instance property information [SQL Server]
- IsHadrEnabled server property
- instances of SQL Server, property information
- server properties [SQL Server]
ms.assetid: 11e166fa-3dd2-42d8-ac4b-04f18c612c4a
caps.latest.revision: ''
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: be72828789c74d599c003100c98db93b1ec937e4
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="serverproperty-transact-sql"></a>SERVERPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt Eigenschaftsinformationen über die Serverinstanz zurück.  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SERVERPROPERTY ( 'propertyname' )  
```  
  
## <a name="arguments"></a>Argumente  
 *propertyname*  
 Ein Ausdruck, der die Eigenschafteninformationen enthält, die für Server zurückgegeben werden sollen. Für*propertyname* sind die folgenden Werte möglich.  
  
|Eigenschaft|Zurückgegebene Werte|  
|--------------|---------------------|  
|BuildClrVersion|Version der Common Language Runtime (CLR) von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], die beim Erstellen der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet wurde.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **nvarchar(128)**|  
|Sortierung|Der Name der Standardsortierung für den Server.<br /><br /> NULL = Eingabe ist ungültig oder ein Fehler.<br /><br /> Basisdatentyp: **nvarchar(128)**|  
|CollationID|ID der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sortierung.<br /><br /> Basisdatentyp: **int**|  
|ComparisonStyle|Die Windows-Vergleichsart der Sortierung.<br /><br /> Basisdatentyp: **int**|  
|ComputernamePhysischerNetBIOS|NetBIOS-Name des lokalen Computers, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] derzeit ausgeführt wird.<br /><br /> Für eine gruppierte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in einem Failovercluster ändert sich dieser Wert, wenn für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein Failover zu anderen Knoten im Failovercluster ausgeführt wird.<br /><br /> Bei einer eigenständigen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bleibt dieser Wert konstant und gibt denselben Wert zurück wie die MachineName-Eigenschaft.<br /><br /> **Hinweis:** Wenn sich die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in einem Failovercluster befindet und der Name der Failoverclusterinstanz abgerufen werden soll, verwenden Sie die MachineName-Eigenschaft.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **nvarchar(128)**|  
|Edition|Installierte Produktedition der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Verwenden Sie den Wert dieser Eigenschaft, um die Features und Beschränkungen zu ermitteln, z.B. [Rechenkapazitätsgrenzen von bestimmten Editionen von SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md). 64-Bit-Versionen des [!INCLUDE[ssDE](../../includes/ssde-md.md)]s fügen "(64-Bit)" an die Version an.<br /><br /> Rückgabewerte:<br /><br /> 'Enterprise Edition'<br /><br /> 'Enterprise Edition: Kernbasierte Lizenzierung'<br /><br /> 'Enterprise Evaluation Edition'<br /><br /> "Business Intelligence Edition"<br /><br /> 'Developer Edition'<br /><br /> 'Express Edition'<br /><br /> 'Express Edition with Advanced Services'<br /><br /> 'Standard Edition'<br /><br /> 'Web Edition'<br /><br /> „SQL Azure“ gibt [!INCLUDE[ssSDS](../../includes/sssds-md.md)] oder [!INCLUDE[ssDW](../../includes/ssdw-md.md)] an.<br /><br /> Basisdatentyp: **nvarchar(128)**|  
|EditionID|EditionID stellt die installierte Produktedition der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dar. Verwenden Sie den Wert dieser Eigenschaft, um Features und Beschränkungen zu ermitteln, z.B. [Rechenkapazitätsgrenzen von bestimmten Editionen von SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).<br /><br /> 1804890536 = Enterprise<br /><br /> 1872460670 = Enterprise Edition: Kernbasierte Lizenzierung<br /><br /> 610778273 = Enterprise (Evaluation)<br /><br /> 284895786 = Business Intelligence<br /><br /> -2117995310 = Developer<br /><br /> -1592396055 = Express<br /><br /> -133711905 = Express with Advanced Services<br /><br /> –1534726760 = Standard<br /><br /> 1293598313 = Web<br /><br /> 1674378470 = SQL Database oder SQL Data Warehouse<br /><br /> Basisdatentyp: **bigint**|  
|EngineEdition|[!INCLUDE[ssDE](../../includes/ssde-md.md)]-Edition der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die auf dem Server installiert ist.<br /><br /> 1 = Personal oder Desktop Engine (Nicht verfügbar in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen.)<br /><br /> 2 = Standard (Rückgabewert für Standard, Web und Business Intelligence)<br /><br /> 3 = Enterprise (Rückgabewert für Evaluation, Developer und beide Enterprise Editionen)<br /><br /> 4 = Express (Rückgabewert für Express, Express with Tools und Express with Advanced Services)<br /><br /> 5 = [!INCLUDE[ssSDS](../../includes/sssds-md.md)]<br /><br /> 6 – [!INCLUDE[ssDW](../../includes/ssdw-md.md)]<br /><br /> Basisdatentyp: **int**|  
|HadrManagerStatus|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt an, ob der [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]-Manager gestartet wurde.<br /><br /> 0 = Nicht gestartet, ausstehende Kommunikation.<br /><br /> 1 = Gestartet und wird ausgeführt.<br /><br /> 2 = Nicht gestartet und fehlgeschlagen.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.|  
|InstanceDefaultDataPath|**Gilt für:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis zur aktuellen Version, ab den Updates vom Spätjahr 2015.<br /><br /> Name des Standardpfads zu den Datendateien der Instanz.|  
|InstanceDefaultLogPath|**Gilt für:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis zur aktuellen Version, ab den Updates vom Spätjahr 2015.<br /><br /> Name des Standardpfads zu den Protokolldateien der Instanz.|  
|InstanceName|Der Name der Instanz, mit der der Benutzer verbunden ist.<br /><br /> Wenn der Instanzname der Standardinstanz entspricht, die Eingabe ungültig ist oder ein Fehler auftritt, wird NULL zurückgegeben.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **nvarchar(128)**|  
|IsAdvancedAnalyticsInstalled|Gibt 1 zurück, wenn das Advanced Analytics-Feature während des Setups installiert wurde. Wenn Advanced Analytics nicht installiert wurde, wird 0 zurückgegeben.|  
|IsClustered|Die Serverinstanz ist als Teil eines Failoverclusters konfiguriert.<br /><br /> 1 = Gruppiert.<br /><br /> 0 = Nicht gruppiert.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **int**|  
|IsFullTextInstalled|Der Komponenten der Volltext- und semantischen Indizierung sind in der aktuellen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert.<br /><br /> 1 = Komponenten der Volltext- und semantischen Indizierung sind installiert.<br /><br /> 0 = Komponenten der Volltext- und semantischen Indizierung sind nicht installiert.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **int**|  
|IsHadrEnabled|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] ist für diese Serverinstanz aktiviert.<br /><br /> 0 = Die [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]-Funktion ist deaktiviert.<br /><br /> 1 = Die [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]-Funktion ist aktiviert.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **int**<br /><br /> Damit Verfügbarkeitsreplikate in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt und ausgeführt werden können, muss [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] auf der Serverinstanz aktiviert sein. Weitere Informationen finden Sie unter [Aktivieren und Deaktivieren von Always On-Verfügbarkeitsgruppen (SQL Server)](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).<br /><br /> **Hinweis:** Die Eigenschaft „IsHadrEnabled“ bezieht sich nur auf [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]. Auf andere Hochverfügbarkeitsfunktionen oder Funktionen für die Wiederherstellung im Notfall, z. B. Datenbankspiegelung oder Protokollversand, hat diese Servereigenschaft keine Auswirkung.|  
|IsIntegratedSecurityOnly|Gibt an, ob der Server sich im integrierten Sicherheitsmodus befindet.<br /><br /> 1 = Integrierte Sicherheit (Windows-Authentifizierung)<br /><br /> 0 = Keine integrierte Sicherheit. (Sowohl Windows-Authentifizierung als auch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung.)<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **int**|  
|IsLocalDB|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Server ist eine Instanz von [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] LocalDB.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.|  
|IsPolybaseInstalled|**Gilt für**: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt zurück, ob das PolyBase-Feature für die Serverinstanz installiert wurde.<br /><br /> 0 = PolyBase ist nicht installiert.<br /><br /> 1 = PolyBase ist installiert.<br /><br /> Basisdatentyp: **int**|  
|IsSingleUser|Gibt an, ob der Server sich im Einzelbenutzermodus befindet.<br /><br /> 1 = Einzelbenutzermodus.<br /><br /> 0 = Kein Einzelbenutzermodus<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **int**|  
|IsXTPSupported|**Gilt für:** SQL Server ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].<br /><br /> Server unterstützt In-Memory OLTP.<br /><br /> 1= Server unterstützt In-Memory OLTP.<br /><br /> 0= Server unterstützt In-Memory OLTP nicht.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **int**|  
|LCID|Windows-Gebietsschemabezeichner (LCID, Locale Identifier) der Sortierung.<br /><br /> Basisdatentyp: **int**|  
|LicenseType|Nicht verwendet. Lizenzinformationen werden vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Produkt weder beibehalten noch aufbewahrt. Gibt immer DISABLED zurück.<br /><br /> Basisdatentyp: **nvarchar(128)**|  
|MachineName|Der Name des Windows-Computers, auf dem die Serverinstanz ausgeführt wird.<br /><br /> Für eine Clusterinstanz, d. h. eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die auf einem virtuellen Server unter Microsoft Cluster Service ausgeführt wird, wird der Name des virtuellen Servers zurückgegeben.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **nvarchar(128)**|  
|NumLicenses|Nicht verwendet. Lizenzinformationen werden vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Produkt weder beibehalten noch aufbewahrt. Gibt immer NULL zurück.<br /><br /> Basisdatentyp: **int**|  
|ProcessID|Prozess-ID des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Diensts. ProcessID ist nützlich, um die zu dieser Instanz gehörende Datei Sqlservr.exe zu identifizieren.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **int**|  
|ProductBuild|**Gilt für:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (ab Oktober 2015)<br /><br /> Die Buildnummer.|  
|ProductBuildType|**Gilt für:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis zur aktuellen Version, ab den Updates vom Spätjahr 2015.<br /><br /> Der Buildtyp des aktuellen Builds.<br /><br /> Gibt einen der folgenden Werte zurück:<br /><br /> OD = Bedarfsgesteuertes Release eines bestimmten Kunden<br /><br /> GDR = Die allgemeine Vertriebsversion, die über Windows Update veröffentlicht wurde.<br /><br /> NULL<br />= Nicht zutreffend|  
|ProductLevel|Ebene der Version der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Gibt einen der folgenden Werte zurück:<br /><br /> 'RTM' = Ursprüngliche Version<br /><br /> 'SP*n*' = Service Pack-Version<br /><br /> 'CTP*n*' = Community Technology Preview-Version<br /><br /> Basisdatentyp: **nvarchar(128)**|  
|ProductMajorVersion|**Gilt für:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis zur aktuellen Version, ab den Updates vom Spätjahr 2015.<br /><br /> Die Hauptversion.|  
|ProductMinorVersion|**Gilt für:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis zur aktuellen Version, ab den Updates vom Spätjahr 2015.<br /><br /> Die Nebenversion.|  
|ProductUpdateLevel|**Gilt für:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis zur aktuellen Version, ab den Updates vom Spätjahr 2015.<br /><br /> Updateebene des aktuellen Builds. CU gibt ein kumulatives Update an.<br /><br /> Gibt einen der folgenden Werte zurück:<br /><br /> CU*n* = kumulatives Update<br /><br /> NULL<br />= Nicht zutreffend|  
|ProductUpdateReference|**Gilt für:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis zur aktuellen Version, ab den Updates vom Spätjahr 2015.<br /><br /> KB-Artikel für dieses Release.|  
|ProductVersion|Version der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Format '*major.minor.build.revision*'.<br /><br /> Basisdatentyp: **nvarchar(128)**|  
|ResourceLastUpdateDateTime|Gibt das Datum und die Zeit des letzten Updates der Ressourcendatenbank zurück.<br /><br /> Basisdatentyp: **datetime**|  
|ResourceVersion|Gibt die Version der Ressourcendatenbank zurück.<br /><br /> Basisdatentyp: **nvarchar(128)**|  
|ServerName|Einer angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugeordnete Informationen zum Windows-Server und zur Instanz.<br /><br /> NULL = Eingabe ist ungültig oder ein Fehler.<br /><br /> Basisdatentyp: **nvarchar(128)**|  
|SqlCharSet|Die ID des SQL-Zeichensatzes aus der Sortierungs-ID.<br /><br /> Basisdatentyp: **tinyint**|  
|SqlCharSetName|Der Name des SQL-Zeichensatzes aus der Sortierung.<br /><br /> Basisdatentyp: **nvarchar(128)**|  
|SqlSortOrder|Die ID der SQL-Sortierreihenfolge aus der Sortierung<br /><br /> Basisdatentyp: **tinyint**|  
|SqlSortOrderName|Der Name der SQL-Sortierreihenfolge aus der Sortierung.<br /><br /> Basisdatentyp: **nvarchar(128)**|  
|FilestreamShareName|Der Name der von FILESTREAM verwendeten Freigabe.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.|  
|FilestreamConfiguredLevel|Die konfigurierte FILESTREAM-Zugriffsebene. Weitere Informationen finden Sie unter [Filestream-Zugriffsebene](../../database-engine/configure-windows/filestream-access-level-server-configuration-option.md).|  
|FilestreamEffectiveLevel|Die effektive FILESTREAM-Zugriffsebene. Dieser Wert kann sich von FilestreamConfiguredLevel unterscheiden, wenn die Ebene geändert wurde und ein Neustart der Instanz oder des Computers aussteht. Weitere Informationen finden Sie unter [Filestream-Zugriffsebene](../../database-engine/configure-windows/filestream-access-level-server-configuration-option.md).|  
  
## <a name="return-types"></a>Rückgabetypen  
 **sql_variant**  
  
## <a name="remarks"></a>Remarks  
  
### <a name="servername-property"></a>ServerName-Eigenschaft  
 Die `ServerName`-Eigenschaft der `SERVERPROPERTY`-Funktion und [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md) geben ähnliche Informationen zurück. Die `ServerName`-Eigenschaft stellt den Namen des Windows-Servers und den Instanznamen bereit, die zusammen die eindeutige Serverinstanz bezeichnen. [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md) stellt den aktuell konfigurierten lokalen Servernamen bereit.  
  
 Die `ServerName`-Eigenschaft und [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md) geben die gleichen Informationen zurück, wenn der zur Installationszeit gültige Standardservername nicht geändert wurde. Der lokale Servername kann durch Ausführen der folgenden Anweisung konfiguriert werden:  
  
```  
EXEC sp_dropserver 'current_server_name';  
GO  
EXEC sp_addserver 'new_server_name', 'local';  
GO  
```  
  
 Wenn der lokale Servername gegenüber dem zur Installationszeit gültigen Standardservernamen geändert wurde, gibt [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md) den neuen Namen zurück.  
  
### <a name="version-properties"></a>Versionseigenschaften  
 Die `SERVERPROPERTY`-Funktion gibt die einzelnen, sich auf Versionsinformationen beziehenden Eigenschaften zurück, während die Funktion [@@VERSION](../../t-sql/functions/version-transact-sql-configuration-functions.md) die Ausgabe in einer Zeichenfolge kombiniert. Wenn Ihre Anwendung die einzelnen Eigenschaftszeichenfolgen getrennt voneinander benötigt, können Sie diese mithilfe der `SERVERPROPERTY`-Funktion ermitteln, statt die Ergebnisse der Funktion [@@VERSION](../../t-sql/functions/version-transact-sql-configuration-functions.md) zu analysieren.  

## <a name="permissions"></a>Berechtigungen

Alle Benutzer können die Servereigenschaften abfragen. 
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel verwendet die `SERVERPROPERTY`-Funktion in einer `SELECT`-Anweisung, um Informationen zur aktuellen Instanz von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]zurückzugeben.   
  
```  
SELECT  
  SERVERPROPERTY('MachineName') AS ComputerName,
  SERVERPROPERTY('ServerName') AS InstanceName,  
  SERVERPROPERTY('Edition') AS Edition,
  SERVERPROPERTY('ProductVersion') AS ProductVersion,  
  SERVERPROPERTY('ProductLevel') AS ProductLevel;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Editionen und Komponenten von SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)  
  
  
