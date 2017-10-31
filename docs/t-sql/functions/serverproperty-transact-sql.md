---
title: SERVERPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 128
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7060a8aaf668a69184503fa0995dd4f37085d5f1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="serverproperty-transact-sql"></a>SERVERPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt Eigenschaftsinformationen über die Serverinstanz zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SERVERPROPERTY ( 'propertyname' )  
```  
  
## <a name="arguments"></a>Argumente  
 *Eigenschaftenname*  
 Ein Ausdruck, der die Eigenschafteninformationen enthält, die für Server zurückgegeben werden sollen. *PropertyName* kann einen der folgenden Werte sein.  
  
|Eigenschaft|Zurückgegebene Werte|  
|--------------|---------------------|  
|BuildClrVersion|Version der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] common Language Runtime (CLR, die beim Erstellen der Instanz des verwendeten) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **vom Datentyp nvarchar(128)**|  
|Sortierung|Der Name der Standardsortierung für den Server.<br /><br /> NULL = Eingabe ist nicht gültig ist, oder einen Fehler.<br /><br /> Basisdatentyp: **vom Datentyp nvarchar(128)**|  
|CollationID|ID der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sortierung.<br /><br /> Basisdatentyp: **Int**|  
|ComparisonStyle|Windows-Vergleichsart der Sortierung.<br /><br /> Basisdatentyp: **Int**|  
|ComputernamePhysischerNetBIOS|NetBIOS-Name des lokalen Computers, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] derzeit ausgeführt wird.<br /><br /> Für eine gruppierte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in einem Failovercluster ändert sich dieser Wert, wenn für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein Failover zu anderen Knoten im Failovercluster ausgeführt wird.<br /><br /> Bei einer eigenständigen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bleibt dieser Wert konstant und gibt denselben Wert zurück wie die MachineName-Eigenschaft.<br /><br /> **Hinweis:** Wenn die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist in einem Failovercluster befindet und soll rufen Sie den Namen der Failover-Clusterinstanz, verwenden Sie die MachineName-Eigenschaft.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **vom Datentyp nvarchar(128)**|  
|Edition|Installierte Produktedition der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Verwenden Sie den Wert dieser Eigenschaft die Funktionen und Beschränkungen, bestimmen, wie z. B. [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md). 64-Bit-Versionen des [!INCLUDE[ssDE](../../includes/ssde-md.md)]s fügen "(64-Bit)" an die Version an.<br /><br /> Rückgabewerte:<br /><br /> 'Enterprise Edition'<br /><br /> 'Enterprise Edition: Kernbasierte Lizenzierung'<br /><br /> 'Enterprise Evaluation Edition'<br /><br /> "Business Intelligence Edition"<br /><br /> 'Developer Edition'<br /><br /> 'Express Edition'<br /><br /> 'Express Edition with Advanced Services'<br /><br /> 'Standard Edition'<br /><br /> 'Web Edition'<br /><br /> Gibt an, "SQL Azure" [!INCLUDE[ssSDS](../../includes/sssds-md.md)] oder[!INCLUDE[ssDW](../../includes/ssdw-md.md)]<br /><br /> Basisdatentyp: **vom Datentyp nvarchar(128)**|  
|EditionID|EditionID stellt die installierte Produktedition der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dar. Verwenden Sie den Wert dieser Eigenschaft Funktionen und Einschränkungen, wie z. B. bestimmen [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).<br /><br /> 1804890536 = Enterprise<br /><br /> 1872460670 = Enterprise Edition: Kernbasierte Lizenzierung<br /><br /> 610778273 = Enterprise (Evaluation)<br /><br /> 284895786 = Business Intelligence<br /><br /> -2117995310 = Developer<br /><br /> -1592396055 = Express<br /><br /> -133711905 = Express with Advanced Services<br /><br /> -1534726760 = Standard<br /><br /> 1293598313 = Web<br /><br /> 1674378470 = SQL-Datenbank oder SQL Datawarehouse<br /><br /> Basisdatentyp: **"bigint"**|  
|EngineEdition|[!INCLUDE[ssDE](../../includes/ssde-md.md)]-Edition der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die auf dem Server installiert ist.<br /><br /> 1 = Personal oder Desktop Engine (nicht verfügbar in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höhere Versionen.)<br /><br /> 2 = Standard (Rückgabewert für Standard, Web und Business Intelligence)<br /><br /> 3 = Enterprise (Rückgabewert für Evaluation, Developer und beide Enterprise Editionen)<br /><br /> 4 = Express (Rückgabewert für Express, Express with Tools und Express with Advanced Services)<br /><br /> 5 = [!INCLUDE[ssSDS](../../includes/sssds-md.md)]<br /><br /> 6 - [!INCLUDE[ssDW](../../includes/ssdw-md.md)]<br /><br /> Basisdatentyp: **Int**|  
|HadrManagerStatus|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt an, ob der [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]-Manager gestartet wurde.<br /><br /> 0 = Nicht gestartet, ausstehende Kommunikation.<br /><br /> 1 = Gestartet und wird ausgeführt.<br /><br /> 2 = Nicht gestartet und fehlgeschlagen.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.|  
|InstanceDefaultDataPath|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über die aktuelle Version in Updates spät 2015 ab.<br /><br /> Name des der Standardpfad für die Instanz-Datendateien.|  
|InstanceDefaultLogPath|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über die aktuelle Version in Updates spät 2015 ab.<br /><br /> Name des der Standardpfad für die Instanz-Protokolldateien.|  
|InstanceName|Der Name der Instanz, mit der der Benutzer verbunden ist.<br /><br /> Wenn der Instanzname der Standardinstanz entspricht, die Eingabe ungültig ist oder ein Fehler auftritt, wird NULL zurückgegeben.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **vom Datentyp nvarchar(128)**|  
|IsAdvancedAnalyticsInstalled|Gibt 1, wenn während des Setups; die Advanced Analytics-Funktion installiert wurde 0, wenn Advanced Analytics nicht installiert wurde.|  
|IsClustered|Die Serverinstanz ist als Teil eines Failoverclusters konfiguriert.<br /><br /> 1 = Gruppiert.<br /><br /> 0 = Nicht gruppiert.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **Int**|  
|IsFullTextInstalled|Der Komponenten der Volltext- und semantischen Indizierung sind in der aktuellen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert.<br /><br /> 1 = Komponenten der Volltext- und semantischen Indizierung sind installiert.<br /><br /> 0 = Komponenten der Volltext- und semantischen Indizierung sind nicht installiert.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **Int**|  
|IsHadrEnabled|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] ist für diese Serverinstanz aktiviert.<br /><br /> 0 = Die [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]-Funktion ist deaktiviert.<br /><br /> 1 = Die [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]-Funktion ist aktiviert.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **Int**<br /><br /> Damit Verfügbarkeitsreplikate in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt und ausgeführt werden können, muss [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] auf der Serverinstanz aktiviert sein. Weitere Informationen finden Sie unter [aktivieren und Deaktivieren von AlwaysOn-Verfügbarkeitsgruppen (SQL Server)](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).<br /><br /> **Hinweis:** die IsHadrEnabled-Eigenschaft bezieht sich nur auf [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]. Auf andere Hochverfügbarkeitsfunktionen oder Funktionen für die Wiederherstellung im Notfall, z. B. Datenbankspiegelung oder Protokollversand, hat diese Servereigenschaft keine Auswirkung.|  
|IsIntegratedSecurityOnly|Gibt an, ob der Server sich im integrierten Sicherheitsmodus befindet.<br /><br /> 1 = Integrierte Sicherheit (Windows-Authentifizierung)<br /><br /> 0 = Keine integrierte Sicherheit. (Sowohl Windows-Authentifizierung als auch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung.)<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **Int**|  
|IsLocalDB|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Server ist eine Instanz von [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] LocalDB.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.|  
|IsPolybaseInstalled|**Gilt für**: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt zurück, ob die Server-Instanz die PolyBase-Funktion installiert wurde.<br /><br /> 0 = PolyBase ist nicht installiert.<br /><br /> 1 = PolyBase installiert ist.<br /><br /> Basisdatentyp: **Int**|  
|IsSingleUser|Gibt an, ob der Server sich im Einzelbenutzermodus befindet.<br /><br /> 1 = Einzelbenutzermodus.<br /><br /> 0 = Kein Einzelbenutzermodus<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **Int**|  
|IsXTPSupported|**Gilt für**: SQLServer ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].<br /><br /> Server unterstützt In-Memory OLTP.<br /><br /> 1= Server unterstützt In-Memory OLTP.<br /><br /> 0= Server unterstützt In-Memory OLTP nicht.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **Int**|  
|LCID|Windows-Gebietsschemabezeichner (LCID, Locale Identifier) der Sortierung.<br /><br /> Basisdatentyp: **Int**|  
|LicenseType|Nicht verwendet. Lizenzinformationen werden vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Produkt weder beibehalten noch aufbewahrt. Gibt immer DISABLED zurück.<br /><br /> Basisdatentyp: **vom Datentyp nvarchar(128)**|  
|MachineName|Der Name des Windows-Computers, auf dem die Serverinstanz ausgeführt wird.<br /><br /> Für eine Clusterinstanz, d. h. eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die auf einem virtuellen Server unter Microsoft Cluster Service ausgeführt wird, wird der Name des virtuellen Servers zurückgegeben.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **vom Datentyp nvarchar(128)**|  
|NumLicenses|Nicht verwendet. Lizenzinformationen werden vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Produkt weder beibehalten noch aufbewahrt. Gibt immer NULL zurück.<br /><br /> Basisdatentyp: **Int**|  
|ProcessID|Prozess-ID des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Diensts. ProcessID ist nützlich, um die zu dieser Instanz gehörende Datei Sqlservr.exe zu identifizieren.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **Int**|  
|ProductBuild|**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ab Oktober 2015.<br /><br /> Die Buildnummer.|  
|ProductBuildType|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über die aktuelle Version in Updates spät 2015 ab.<br /><br /> Typ des Build des aktuellen Builds.<br /><br /> Gibt einen der folgenden Werte zurück:<br /><br /> OD = On Demand-Version ein bestimmtes Kunden.<br /><br /> GDR = allgemeine General Distribution Release, die über Windows Update veröffentlicht werden.<br /><br /> NULL<br />= Nicht zutreffend.|  
|ProductLevel|Ebene der Version der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Gibt einen der folgenden Werte zurück:<br /><br /> 'RTM' = Ursprüngliche Version<br /><br /> ' SP*n*' = Service Pack-Version<br /><br /> ' CTP*n*', = Community Technology Preview-Version<br /><br /> Basisdatentyp: **vom Datentyp nvarchar(128)**|  
|ProductMajorVersion|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über die aktuelle Version in Updates spät 2015 ab.<br /><br /> Die Hauptversion.|  
|ProductMinorVersion|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über die aktuelle Version in Updates spät 2015 ab.<br /><br /> Die Nebenversion.|  
|ProductUpdateLevel|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über die aktuelle Version in Updates spät 2015 ab.<br /><br /> Aktualisieren Sie die Ebene des aktuellen Builds. CU gibt ein kumulatives Update an.<br /><br /> Gibt einen der folgenden Werte zurück:<br /><br /> CU *n*  = Kumulatives Update<br /><br /> NULL<br />= Nicht zutreffend.|  
|ProductUpdateReference|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über die aktuelle Version in Updates spät 2015 ab.<br /><br /> KB-Artikel für diese Version zugreifen.|  
|ProductVersion|Version der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], in Form von "*" Hauptversion.Nebenversion.Build.Revision "vorliegen*".<br /><br /> Basisdatentyp: **vom Datentyp nvarchar(128)**|  
|ResourceLastUpdateDateTime|Gibt das Datum und die Zeit des letzten Updates der Ressourcendatenbank zurück.<br /><br /> Basisdatentyp: **"DateTime"**|  
|ResourceVersion|Gibt die Version der Ressourcendatenbank zurück.<br /><br /> Basisdatentyp: **vom Datentyp nvarchar(128)**|  
|ServerName|Einer angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugeordnete Informationen zum Windows-Server und zur Instanz.<br /><br /> NULL = Eingabe ist nicht gültig ist, oder einen Fehler.<br /><br /> Basisdatentyp: **vom Datentyp nvarchar(128)**|  
|SqlCharSet|Die ID des SQL-Zeichensatzes aus der Sortierungs-ID.<br /><br /> Basisdatentyp: **"tinyint"**|  
|SqlCharSetName|Der Name des SQL-Zeichensatzes aus der Sortierung.<br /><br /> Basisdatentyp: **vom Datentyp nvarchar(128)**|  
|SqlSortOrder|ID der SQL-Sortierreihenfolge aus der Sortierung<br /><br /> Basisdatentyp: **"tinyint"**|  
|SqlSortOrderName|Der Name der SQL-Sortierreihenfolge aus der Sortierung.<br /><br /> Basisdatentyp: **vom Datentyp nvarchar(128)**|  
|FilestreamShareName|Der Name der von FILESTREAM verwendeten Freigabe.<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.|  
|FilestreamConfiguredLevel|Die konfigurierte FILESTREAM-Zugriffsebene. Weitere Informationen finden Sie unter [Filestream-Zugriffsebene](../../database-engine/configure-windows/filestream-access-level-server-configuration-option.md).|  
|FilestreamEffectiveLevel|Die effektive FILESTREAM-Zugriffsebene. Dieser Wert kann sich von FilestreamConfiguredLevel unterscheiden, wenn die Ebene geändert wurde und ein Neustart der Instanz oder des Computers aussteht. Weitere Informationen finden Sie unter [Filestream-Zugriffsebene](../../database-engine/configure-windows/filestream-access-level-server-configuration-option.md).|  
  
## <a name="return-types"></a>Rückgabetypen  
 **sql_variant**  
  
## <a name="remarks"></a>Hinweise  
  
### <a name="servername-property"></a>ServerName-Eigenschaft  
 Die `ServerName` Eigenschaft von der `SERVERPROPERTY` Funktion und [@@SERVERNAME ](../../t-sql/functions/servername-transact-sql.md) geben ähnliche Informationen zurück. Die `ServerName`-Eigenschaft stellt den Namen des Windows-Servers und den Instanznamen bereit, die zusammen die eindeutige Serverinstanz bezeichnen. [@@SERVERNAME ](../../t-sql/functions/servername-transact-sql.md) stellt den aktuell konfigurierten lokalen Servernamen bereit.  
  
 Die `ServerName` Eigenschaft und [@@SERVERNAME ](../../t-sql/functions/servername-transact-sql.md) die gleichen Informationen zurück, wenn der Standardservername zum Zeitpunkt der Installation nicht geändert wurde. Der lokale Servername kann durch Ausführen der folgenden Anweisung konfiguriert werden:  
  
```  
EXEC sp_dropserver 'current_server_name';  
GO  
EXEC sp_addserver 'new_server_name', 'local';  
GO  
```  
  
 Wenn der Name des lokalen Servers von den standardmäßigen Servernamen zur Installationszeit geändert wurde [@@SERVERNAME ](../../t-sql/functions/servername-transact-sql.md) den neuen Namen zurück.  
  
### <a name="version-properties"></a>Versionseigenschaften  
 Die `SERVERPROPERTY` idatabasebackupreadstream einzelne Eigenschaften, die sich auf Versionsinformationen beziehen, wohingegen die [@@VERSION ](../../t-sql/functions/version-transact-sql-configuration-functions.md) Funktion die Ausgabe in einer Zeichenfolge kombiniert. Wenn Ihre Anwendung einzelne Eigenschaftenzeichenfolge erfordert, können Sie mithilfe der `SERVERPROPERTY` Funktion, um sie zurückkehren, anstatt die Analyse der [@@VERSION ](../../t-sql/functions/version-transact-sql-configuration-functions.md) Ergebnisse.  

## <a name="permissions"></a>Berechtigungen

Alle Benutzer können die Servereigenschaften Abfragen. 
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die `SERVERPROPERTY` -Funktion in einer `SELECT` Anweisung zum Zurückgeben von Informationen über die aktuelle Instanz von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].   
  
```  
SELECT  
  SERVERPROPERTY('MachineName') AS ComputerName,
  SERVERPROPERTY('ServerName') AS InstanceName,  
  SERVERPROPERTY('Edition') AS Edition,
  SERVERPROPERTY('ProductVersion') AS ProductVersion,  
  SERVERPROPERTY('ProductLevel') AS ProductLevel;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Editionen und Komponenten von SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)  
  
  

