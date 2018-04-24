---
title: Als veraltet markierte Funktionen des Datenbankmoduls in SQL Server 2017 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/09/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- deprecated features [SQL Server]
- Database Engine [SQL Server], backward compatibility
- deprecation [SQL Server], feature list
ms.assetid: ''
caps.latest.revision: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 345c1e8766c1136577848b5fd5bae31f53ac4478
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="deprecated-database-engine-features-in-sql-server-2017"></a>Als veraltet markierte Funktionen des Datenbankmoduls in SQL Server 2017
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

  In diesem Thema werden die als veraltet markierten Funktionen von [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] beschrieben, die in [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]noch verfügbar sind. Diese Funktionen werden voraussichtlich in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]entfernt. Als veraltet markierte Funktionen sollten in neuen Anwendungen nicht verwendet werden.  
  
 Sie können die Nutzung als veraltet markierter Funktionen mithilfe des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Objektleistungsindikators "Als veraltet markierte Funktion" und Ablaufverfolgungsereignissen überwachen. Weitere Informationen finden Sie unter [Verwenden von SQL Server-Objekten](../relational-databases/performance-monitor/use-sql-server-objects.md).  
  
 Die Werte dieser Indikatoren sind auch durch Ausführung folgender Anweisung verfügbar:  
  
```  
SELECT * FROM sys.dm_os_performance_counters   
WHERE object_name = 'SQLServer:Deprecated Features';  
```  

>  [!NOTE]  
>  Diese Liste ist identisch mit der [!INCLUDE[sssql15-md](../includes/sssql15-md.md)]-Liste. Es gibt keine Datenbankmodulfunktionen, die neu für [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] als veraltet markiert oder eingestellt wurden.

## <a name="features-not-supported-in-the-next-version-of-sql-server"></a>Funktionen, die in der nächsten Version von SQL Server nicht unterstützt werden  
 Die folgenden [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] -Funktionen werden in der nächsten Version von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]nicht mehr unterstützt. Verwenden Sie diese Funktionen nicht zum Entwickeln neuer Anwendungen, und ändern Sie so bald wie möglich die Anwendungen, in denen diese Funktionen zurzeit verwendet werden. Der **Feature name** -Wert wird in Ablaufverfolgungsereignissen als ObjectName und in Leistungsindikatoren sowie sys.dm_os_performance_counters als Instanzname angezeigt. Der **Feature ID** -Wert wird in Ablaufverfolgungsereignissen als ObjectId angezeigt.  
  
|Kategorie|Als veraltet markierte Funktion|Ersatz|Feature name|Feature ID|  
|--------------|------------------------|-----------------|------------------|----------------|  
|Sichern und Wiederherstellen|RESTORE { DATABASE &#124; LOG } WITH [MEDIA]PASSWORD ist weiterhin veraltet. BACKUP { DATABASE &#124; LOG } WITH PASSWORD und BACKUP { DATABASE &#124; LOG } WITH MEDIAPASSWORD werden eingestellt.|Keine.|BACKUP DATABASE oder LOG WITH PASSWORD<br /><br /> BACKUP DATABASE oder LOG WITH MEDIAPASSWORD|104<br /><br /> 103|  
|Kompatibilitätsgrad|Upgrade von Version 110 ([!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] und [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]).|Kompatibilitätsgrade sind nur für die letzten beiden Versionen verfügbar. Weitere Informationen zu den Kompatibilitätsgraden finden Sie unter [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md).|Datenbank-Kompatibilitätsgrad 100|108|  
|Datenbankobjekte|Funktionalität zum Zurückgeben von Resultsets von Triggern|InclusionThresholdSetting|Zurückgeben von Ergebnissen aus Triggern|12|  
|Verschlüsselung|Die Verschlüsselung mit RC4 oder RC4_128 ist veraltet. Die Entfernung ist für die nächste Version geplant. Die Entschlüsselung von RC4 und RC4_128 sind nicht veraltet.|Verwenden Sie einen anderen Verschlüsselungsalgorithmus, z. B. AES.|Veralteter Verschlüsselungsalgorithmus|253|  
|Remoteserver|sp_addremotelogin<br /><br /> sp_addserver<br /><br /> sp_dropremotelogin<br /><br /> sp_helpremotelogin<br /><br /> sp_remoteoption|Ersetzen Sie Remoteserver mithilfe von Verbindungsservern. sp_addserver kann nur mit der lokalen Option verwendet werden.|sp_addremotelogin<br /><br /> sp_addserver<br /><br /> sp_dropremotelogin<br /><br /> sp_helpremotelogin<br /><br /> sp_remoteoption|70<br /><br /> 69<br /><br /> 71<br /><br /> 72<br /><br /> 73|  
|Remoteserver|\@\@remserver|Ersetzen Sie Remoteserver mithilfe von Verbindungsservern.|InclusionThresholdSetting|InclusionThresholdSetting|  
|Remoteserver|SET REMOTE_PROC_TRANSACTIONS|Ersetzen Sie Remoteserver mithilfe von Verbindungsservern.|SET REMOTE_PROC_TRANSACTIONS|110|  
|SET-Optionen|**SET ROWCOUNT** für die **INSERT**-, **UPDATE**-Anweisung und die **DELETE** -Anweisung|TOP-Schlüsselwort|SET ROWCOUNT|109|  
|Tabellenhinweise|HOLDLOCK-Tabellenhinweis ohne Klammern.|Verwenden Sie HOLDLOCK mit Klammern.|HOLDLOCK-Tabellenhinweis ohne Klammern|167|  
  
## <a name="features-not-supported-in-a-future-version-of-sql-server"></a>Funktionen, die in einer zukünftigen Version von SQL Server nicht unterstützt werden  
 Die folgenden Funktionen von [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] werden in der nächsten Version von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]noch unterstützt, aber in zukünftigen Versionen entfernt. Die betreffende Version von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] wurde noch nicht festgelegt.  
  
|Kategorie|Als veraltet markierte Funktion|Ersatz|Feature name|Funktions-ID|  
|--------------|------------------------|-----------------|------------------|----------------|  
|Kompatibilitätsgrad|sp_dbcmptlevel|ALTER DATABASE … SET COMPATIBILITY_LEVEL. Weitere Informationen finden Sie unter [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md).|sp_dbcmptlevel|80|  
|Kompatibilitätsgrad|Datenbank-Kompatibilitätsgrad 110 und 120|Planen Sie, in einer zukünftigen Version die Datenbank und die Anwendung zu aktualisieren.|Datenbank-Kompatibilitätsgrad 110<br /><br /> Datenbank-Kompatibilitätsgrad 120||  
|XML|XDR-Inlineschemagenerierung|Die XMLDATA-Direktive zur FOR XML-Option ist veraltet. Verwenden Sie XSD-Generierung für RAW- und AUTO-Modus. Es gibt keinen Ersatz für die XMLDATA-Direktive im EXPLICIT-Modus.|XMLDATA|181|  
|Sichern und Wiederherstellen|BACKUP { DATABASE &#124; LOG } TO TAPE<br /><br /> BACKUP { DATABASE &#124; LOG } TO *Bandgerät*|BACKUP { DATABASE &#124; LOG } TO DISK<br /><br /> BACKUP { DATABASE &#124; LOG } TO *Datenträger*|BACKUP DATABASE oder LOG TO TAPE|235|  
|Sichern und Wiederherstellen|sp_addumpdevice '**tape**'|sp_addumpdevice '**disk**'|ADDING TAPE DEVICE|236|  
|Sichern und Wiederherstellen|sp_helpdevice|sys.backup_devices|sp_helpdevice|100|  
|Sortierungen|Korean_Wansung_Unicode<br /><br /> Lithuanian_Classic<br /><br /> SQL_AltDiction_CP1253_CS_AS|Keine. Diese Sortierungen sind in [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]vorhanden, aber nicht über fn_helpcollations sichtbar.|Korean_Wansung_Unicode<br /><br /> Lithuanian_Classic<br /><br /> SQL_AltDiction_CP1253_CS_AS|191<br /><br /> 192<br /><br /> 194|  
|Sortierungen|Hindi<br /><br /> Macedonian|Diese Sortierungen sind in [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] und höher vorhanden, aber über fn_helpcollations nicht sichtbar. Verwenden Sie stattdessen Macedonian_FYROM_90 und Indic_General_90.|Hindi<br /><br /> Macedonian|190<br /><br /> 193|  
|Sortierungen|Azeri_Latin_90<br /><br /> Azeri_Cyrilllic_90|Azeri_Latin_100<br /><br /> Azeri_Cyrilllic_100|Azeri_Latin_90<br /><br /> Azeri_Cyrilllic_90|232<br /><br /> 233|  
|Konfiguration|SET ANSI_NULLS OFF und ANSI_NULLS OFF-Datenbankoption<br /><br /> SET ANSI_PADDING OFF und ANSI_PADDING OFF-Datenbankoption<br /><br /> SET CONCAT_NULL_YIELDS_NULL OFF und CONCAT_NULL_YIELDS_NULL OFF-Datenbankoption<br /><br /> SET OFFSETS|Keine.<br /><br /> ANSI_NULLS, ANSI_PADDING und CONCAT_NULLS_YIELDS_NULL werden stets auf ON festgelegt. SET OFFSETS ist nicht verfügbar.|SET ANSI_NULLS OFF<br /><br /> SET ANSI_PADDING OFF<br /><br /> SET CONCAT_NULL_YIELDS_NULL OFF<br /><br /> SET OFFSETS<br /><br /> ALTER DATABASE SET ANSI_NULLS OFF<br /><br /> ALTER DATABASE SET ANSI_PADDING OFF<br /><br /> ALTER DATABASE SET CONCAT_NULL_YIELDS_NULL OFF|111<br /><br /> 113<br /><br /> 112<br /><br /> 36<br /><br /> 111<br /><br /> 113<br /><br /> 112|  
|Datentypen|sp_addtype<br /><br /> sp_droptype|CREATE TYPE<br /><br /> DROP TYPE|sp_addtype<br /><br /> sp_droptype|62<br /><br /> 63|  
|Datentypen|**timestamp** -Syntax für **rowversion** -Datentyp|**rowversion** -Datentypsyntax|timestamp|158|  
|Datentypen|Fähigkeit, NULL-Werte in **timestamp** -Spalten einzufügen|Verwenden Sie stattdessen DEFAULT.|INSERT NULL in TIMESTAMP-Spalten|179|  
|Datentypen|Tabellenoption 'text in row'|Verwenden Sie stattdessen die Datentypen **varchar(max)**, **nvarchar(max)** und **varbinary(max)**. Weitere Informationen finden Sie unter [sp_tableoption &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md).|Tabellenoption 'text in row'|9|  
|Datentypen|Datentypen:<br /><br /> **text**<br /><br /> **ntext**<br /><br /> **image**|Verwenden Sie stattdessen die Datentypen **varchar(max)**, **nvarchar(max)**und **varbinary(max)** .|Datentypen: **text**, **ntext** oder **image**.|4|  
|Datenbankverwaltung|sp_attach_db<br /><br /> sp_attach_single_file_db|CREATE DATABASE-Anweisung mit der FOR ATTACH-Option. Verwenden Sie die FOR ATTACH_REBUILD_LOG-Option, um mehrere Protokolldateien neu zu erstellen, wenn mindestens eine Datei einen neuen Speicherort aufweist.|sp_attach_db<br /><br /> sp_attach_single_file_db|81<br /><br /> 82|  
|Datenbankobjekte|CREATE DEFAULT<br /><br /> DROP DEFAULT<br /><br /> sp_bindefault<br /><br /> sp_unbindefault|DEFAULT-Schlüsselwort in CREATE TABLE und ALTER TABLE|CREATE_DROP_DEFAULT<br /><br /> sp_bindefault<br /><br /> sp_unbindefault|162<br /><br /> 64<br /><br /> 65|  
|Datenbankobjekte|CREATE RULE<br /><br /> DROP RULE<br /><br /> sp_bindrule<br /><br /> sp_unbindrule|CHECK-Schlüsselwort in CREATE TABLE und ALTER TABLE|CREATE_DROP_RULE<br /><br /> sp_bindrule<br /><br /> sp_unbindrule|161<br /><br /> 66<br /><br /> 67|  
|Datenbankobjekte|sp_change_users_login|Verwenden Sie ALTER USER.|sp_change_users_login|231|  
|Datenbankobjekte|sp_depends|sys.dm_sql_referencing_entities und sys.dm_sql_referenced_entities|sp_depends|19|  
|Datenbankobjekte|sp_renamedb|MODIFY NAME in ALTER DATABASE|sp_renamedb|79|  
|Datenbankobjekte|sp_getbindtoken|Verwenden Sie MARS oder verteilte Transaktionen.|sp_getbindtoken|98|  
|Datenbankoptionen|sp_bindsession|Verwenden Sie MARS oder verteilte Transaktionen.|sp_bindsession|97|  
|Datenbankoptionen|sp_resetstatus|ALTER DATABASE SET { ONLINE &#124; EMERGENCY }|sp_resetstatus|83|  
|Datenbankoptionen|Option TORN_PAGE_DETECTION von ALTER DATABASE|Option PAGE_VERIFY TORN_PAGE DETECTION von ALTER DATABASE|ALTER DATABASE WITH TORN_PAGE_DETECTION|102|  
|DBCC|DBCC DBREINDEX|Option REBUILD von ALTER INDEX|DBCC DBREINDEX|11|  
|DBCC|DBCC INDEXDEFRAG|Option REORGANIZE von ALTER INDEX|DBCC INDEXDEFRAG|18|  
|DBCC|DBCC SHOWCONTIG|sys.dm_db_index_physical_stats|DBCC SHOWCONTIG|10|  
|DBCC|DBCC PINTABLE<br /><br /> DBCC UNPINTABLE|Hat keinerlei Auswirkungen.|DBCC [UN]PINTABLE|189|  
|Erweiterte Eigenschaften|Level0type = 'type' und Level0type = 'USER', um erweiterte Eigenschaften Objekten auf der ersten oder zweiten Ebene hinzuzufügen.|Verwenden Sie Level0type = 'USER' nur, um eine erweiterte Eigenschaft direkt einem Benutzer oder einer Rolle hinzuzufügen.<br /><br /> Verwenden Sie Level0type = 'SCHEMA' zum Hinzufügen einer erweiterten Eigenschaft zu Objekten auf der ersten Ebene, wie TABLE oder VIEW, bzw. zu Objekten auf der zweiten Ebene, wie COLUMN oder TRIGGER. Weitere Informationen finden Sie unter [sp_addextendedproperty &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md).|EXTPROP_LEVEL0TYPE<br /><br /> EXTPROP_LEVEL0USER|13<br /><br /> 14|  
|Programmierung der erweiterten gespeicherten Prozedur|srv_alloc<br /><br /> srv_convert<br /><br /> srv_describe<br /><br /> srv_getbindtoken<br /><br /> srv_got_attention<br /><br /> srv_message_handler<br /><br /> srv_paramdata<br /><br /> srv_paraminfo<br /><br /> srv_paramlen<br /><br /> srv_parammaxlen<br /><br /> srv_paramname<br /><br /> srv_paramnumber<br /><br /> srv_paramset<br /><br /> srv_paramsetoutput<br /><br /> srv_paramstatus<br /><br /> srv_paramtype<br /><br /> srv_pfield<br /><br /> srv_pfieldex<br /><br /> srv_rpcdb<br /><br /> srv_rpcname<br /><br /> srv_rpcnumber<br /><br /> srv_rpcoptions<br /><br /> srv_rpcowner<br /><br /> srv_rpcparams<br /><br /> srv_senddone<br /><br /> srv_sendmsg<br /><br /> srv_sendrow<br /><br /> srv_setcoldata<br /><br /> srv_setcollen<br /><br /> srv_setutype<br /><br /> srv_willconvert<br /><br /> srv_wsendmsg|Verwenden Sie stattdessen die CLR-Integration.|XP_API|20|  
|Programmierung der erweiterten gespeicherten Prozedur|sp_addextendedproc<br /><br /> sp_dropextendedproc<br /><br /> sp_helpextendedproc|Verwenden Sie stattdessen die CLR-Integration.|sp_addextendedproc<br /><br /> sp_dropextendedproc<br /><br /> sp_helpextendedproc|94<br /><br /> 95<br /><br /> 96|  
|Erweiterte gespeicherte Prozeduren|xp_grantlogin<br /><br /> xp_revokelogin<br /><br /> xp_loginConfig|Verwenden Sie CREATE_LOGIN<br /><br /> Verwenden Sie DROP LOGIN und das IsIntegratedSecurityOnly-Argument von SERVERPROPERTY.|xp_grantlogin<br /><br /> xp_revokelogin<br /><br /> xp_loginConfig|44<br /><br /> 45<br /><br /> 59|  
|Funktionen|fn_get_sql|sys.dm_exec_sql_text|fn_get_sql|151|  
|Hashalgorithmen|Die Algorithmen MD2, MD4, MD5, SHA und SHA1. Diese sind bei einem Kompatibilitätsgrad unterhalb 130 nicht verfügbar.|Verwenden Sie SHA2_256 oder SHA2_512.|Veralteter Hashalgorithmus||  
|Hohe Verfügbarkeit|Datenbankspiegelung|[!INCLUDE[ssHADR](../includes/sshadr-md.md)]<br /><br /> Wenn die Edition von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../includes/sshadr-md.md)]nicht unterstützt, verwenden Sie den Protokollversand.|DATABASE_MIRRORING|267|  
|Indexoptionen|sp_indexoption|ALTER INDEX|sp_indexoption|78|  
|Indexoptionen|CREATE TABLE-, ALTER TABLE- oder CREATE INDEX-Syntax ohne Klammern um die Optionen|Schreiben Sie Anweisung so um, dass sie die aktuelle Syntax verwendet.|INDEX_OPTION|33|  
|Instanzoptionen|sp_configure-Option 'Updates zulassen'|Systemtabellen sind nicht mehr aktualisierbar. Die Einstellung hat keine Auswirkungen.|sp_configure 'allow updates'|173|  
|Instanzoptionen|sp_configure-Optionen:<br /><br /> 'locks'<br /><br /> 'Geöffnete Objekte'<br /><br /> 'Festgelegte Workingsetgröße'|Wird jetzt automatisch konfiguriert. Die Einstellung hat keine Auswirkungen.|sp_configure 'locks'<br /><br /> sp_configure 'open objects'<br /><br /> sp_configure 'set working set size'|174<br /><br /> 175<br /><br /> 176|  
|Instanzoptionen|sp_configure-Option 'Prioritätserhöhung'|Systemtabellen sind nicht mehr aktualisierbar. Die Einstellung hat keine Auswirkungen. Verwenden Sie stattdessen die start /high … program.exe-Option von Windows.|sp_configure 'priority boost'|199|  
|Instanzoptionen|sp_configure-Option 'remote proc trans'|Systemtabellen sind nicht mehr aktualisierbar. Die Einstellung hat keine Auswirkungen.|sp_configure 'remote proc trans'|37|  
|Verbindungsserver|Angeben des SQLOLEDB-Anbieters für Verbindungsserver.|SQL Server Native Client (SQLNCLI)|SQLOLEDDB für Verbindungsserver|19|  
|Sperren|sp_lock|sys.dm_tran_locks|sp_lock|99|  
|Metadaten|FILE_ID<br /><br /> INDEXKEY_PROPERTY|FILE_IDEX<br /><br /> sys.index_columns|FILE_ID<br /><br /> INDEXKEY_PROPERTY|15<br /><br /> 17|  
|Systemeigene XML-Webdienste|Die CREATE ENDPOINT-Anweisung oder ALTER ENDPOINT-Anweisung mit der FOR SOAP-Option.<br /><br /> sys.endpoint_webmethods<br /><br /> sys.soap_endpoints|Verwenden Sie stattdessen Windows Communications Foundation (WCF) oder ASP.NET.|CREATE/ALTER ENDPOINT<br /><br /> sys.endpoint_webmethods<br /><br /> EXT_soap_endpoints<br /><br /> sys.soap_endpoints|21<br /><br /> 22<br /><br /> 23|  
|Austauschbare Datenbanken|sp_certify_removable<br /><br /> sp_create_removable|sp_detach_db|sp_certify_removable<br /><br /> sp_create_removable|74<br /><br /> 75|  
|Austauschbare Datenbanken|sp_dbremove|DROP DATABASE|sp_dbremove|76|  
|Security|Die ALTER LOGIN WITH SET CREDENTIAL-Syntax|Wurde durch die neue ALTER LOGIN ADD- und DROP CREDENTIAL-Syntax ersetzt|ALTER LOGIN WITH SET CREDENTIAL|230|  
|Security|sp_addapprole<br /><br /> sp_dropapprole|CREATE APPLICATION ROLE<br /><br /> DROP APPLICATION ROLE|sp_addapprole<br /><br /> sp_dropapprole|53<br /><br /> 54|  
|Security|sp_addlogin<br /><br /> sp_droplogin|CREATE LOGIN<br /><br /> DROP LOGIN|sp_addlogin<br /><br /> sp_droplogin|39<br /><br /> 40|  
|Security|sp_adduser<br /><br /> sp_dropuser|CREATE USER<br /><br /> DROP USER|sp_adduser<br /><br /> sp_dropuser|49<br /><br /> 50|  
|Security|sp_grantdbaccess<br /><br /> sp_revokedbaccess|CREATE USER<br /><br /> DROP USER|sp_grantdbaccess<br /><br /> sp_revokedbaccess|51<br /><br /> 52|  
|Security|sp_addrole<br /><br /> sp_droprole|CREATE ROLE<br /><br /> DROP ROLE|sp_addrole<br /><br /> sp_droprole|56<br /><br /> 57|  
|Security|sp_approlepassword<br /><br /> sp_password|ALTER APPLICATION ROLE<br /><br /> ALTER LOGIN|sp_approlepassword<br /><br /> sp_password|55<br /><br /> 46|  
|Security|sp_changeobjectowner|ALTER SCHEMA oder ALTER AUTHORIZATION|sp_changeobjectowner|58|  
|Security|sp_control_dbmasterkey_password|Es muss ein Hauptschlüssel vorhanden sein, und das richtige Kennwort muss angegeben werden.|sp_control_dbmasterkey_password|274|  
|Security|sp_defaultdb<br /><br /> sp_defaultlanguage|ALTER LOGIN|sp_defaultdb<br /><br /> sp_defaultlanguage|47<br /><br /> 48|  
|Security|sp_denylogin<br /><br /> sp_grantlogin<br /><br /> sp_revokelogin|ALTER LOGIN DISABLE<br /><br /> CREATE LOGIN<br /><br /> DROP LOGIN|sp_denylogin<br /><br /> sp_grantlogin<br /><br /> sp_revokelogin|42<br /><br /> 41<br /><br /> 43|  
|Security|USER_ID|DATABASE_PRINCIPAL_ID|USER_ID|16|  
|Security|sp_srvrolepermission<br /><br /> sp_dbfixedrolepermission|Diese gespeicherten Prozeduren geben Informationen zurück, die in [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]richtig waren. Die Ausgabe spiegelt keine Änderungen an der Berechtigungshierarchie wider, die in [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]implementiert wurde. Weitere Informationen finden Sie unter [Berechtigungen fester Serverrollen](http://msdn.microsoft.com/library/ms175892\(SQL.100\).aspx).|sp_srvrolepermission<br /><br /> sp_dbfixedrolepermission|61<br /><br /> 60|  
|Security|GRANT ALL<br /><br /> DENY ALL<br /><br /> REVOKE ALL|Spezielle GRANT-, DENY- und REVOKE-Berechtigungen|ALL-Berechtigung|35|  
|Security|Intrinsische PERMISSIONS-Funktion|Fragen Sie stattdessen sys.fn_my_permissions ab.|PERMISSIONS|170|  
|Security|SETUSER|EXECUTE AS|SETUSER|165|  
|Security|RC4- und DESX-Verschlüsselungsalgorithmen|Verwenden Sie einen anderen Algorithmus, z. B. AES.|DESX-Algorithmus|238|  
|SET-Optionen|SET FMTONLY|[sys.dm_exec_describe_first_result_set &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md), [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md), [sp_describe_first_result_set &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) und [sp_describe_undeclared_parameters &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md).|SET FMTONLY|250|  
|Serverkonfigurationsoptionen|C2-Überwachungsoption<br /><br /> Standardablaufverfolgung aktiviert (Option)|[Common Criteria-Kompatibilität aktiviert (Serverkonfigurationsoption)](../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md)<br /><br /> [Erweiterte Ereignisse](../relational-databases/extended-events/extended-events.md)|sp_configure 'c2 audit mode'<br /><br /> sp_configure 'default trace enabled'|252<br /><br /> 253|  
|SMO-Klassen|**Microsoft.SQLServer. Management.Smo.Information**-Klasse<br /><br /> **Microsoft.SQLServer. Management.Smo.Settings**-Klasse<br /><br /> **Microsoft.SQLServer.Management. Smo.DatabaseOptions**-Klasse<br /><br /> **Microsoft.SqlServer.Management.Smo. DatabaseDdlTrigger.NotForReplication**-Eigenschaft|**Microsoft.SQLServer.  Management.Smo.Server**-Klasse<br /><br /> **Microsoft.SQLServer.  Management.Smo.Server**-Klasse<br /><br /> **Microsoft.SQLServer. Management.Smo.Database**-Klasse<br /><br /> InclusionThresholdSetting|InclusionThresholdSetting|InclusionThresholdSetting|  
|SQL Server-Agent|**net send** -Benachrichtigung<br /><br /> Pagerbenachrichtigung|E-Mail-Benachrichtigung<br /><br /> E-Mail-Benachrichtigung |InclusionThresholdSetting|InclusionThresholdSetting|  
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]|Integration von Projektmappen-Explorer in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]||InclusionThresholdSetting|InclusionThresholdSetting|  
|Gespeicherte Systemprozeduren|sp_db_increased_partitions|Keine Unterstützung für mehr Partitionen ist in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]standardmäßig verfügbar.|sp_db_increased_partitions|253|  
|Systemtabellen|sysaltfiles<br /><br /> syscacheobjects<br /><br /> syscolumns<br /><br /> syscomments<br /><br /> sysconfigures<br /><br /> sysconstraints<br /><br /> syscurconfigs<br /><br /> sysdatabases<br /><br /> sysdepends<br /><br /> sysdevices<br /><br /> sysfilegroups<br /><br /> sysfiles<br /><br /> sysforeignkeys<br /><br /> sysfulltextcatalogs<br /><br /> sysindexes<br /><br /> sysindexkeys<br /><br /> syslockinfo<br /><br /> syslogins<br /><br /> sysmembers<br /><br /> sysmessages<br /><br /> sysobjects<br /><br /> sysoledbusers<br /><br /> sysopentapes<br /><br /> sysperfinfo<br /><br /> syspermissions<br /><br /> sysprocesses<br /><br /> sysprotects<br /><br /> sysreferences<br /><br /> sysremotelogins<br /><br /> sysservers<br /><br /> systypes<br /><br /> sysusers|Kompatibilitätssichten Weitere Informationen finden Sie unter [Kompatibilitätssichten &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md).<br /><br /> **\*\* Wichtig \*\*** Die Kompatibilitätssichten machen keine Metadaten für in [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] eingeführte Funktionen verfügbar. Es wird empfohlen, die Anwendungen für die Verwendung von Katalogsichten zu aktualisieren. Weitere Informationen finden Sie unter [Katalogsichten &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/catalog-views-transact-sql.md).|sysaltfiles<br /><br /> syscacheobjects<br /><br /> syscolumns<br /><br /> syscomments<br /><br /> sysconfigures<br /><br /> sysconstraints<br /><br /> syscurconfigs<br /><br /> sysdatabases<br /><br /> sysdepends<br /><br /> sysdevices<br /><br /> sysfilegroups<br /><br /> sysfiles<br /><br /> sysforeignkeys<br /><br /> sysfulltextcatalogs<br /><br /> sysindexes<br /><br /> sysindexkeys<br /><br /> syslockinfo<br /><br /> syslogins<br /><br /> sysmembers<br /><br /> sysmessages<br /><br /> sysobjects<br /><br /> sysoledbusers<br /><br /> sysopentapes<br /><br /> sysperfinfo<br /><br /> syspermissions<br /><br /> sysprocesses<br /><br /> sysprotects<br /><br /> sysreferences<br /><br /> sysremotelogins<br /><br /> sysservers<br /><br /> systypes<br /><br /> sysusers|141<br /><br /> InclusionThresholdSetting<br /><br /> 133<br /><br /> 126<br /><br /> 146<br /><br /> 131<br /><br /> 147<br /><br /> 142<br /><br /> 123<br /><br /> 144<br /><br /> 128<br /><br /> 127<br /><br /> 130<br /><br /> 122<br /><br /> 132<br /><br /> 134<br /><br /> 143<br /><br /> 140<br /><br /> 119<br /><br /> 137<br /><br /> 125<br /><br /> 139<br /><br /> 145<br /><br /> 157<br /><br /> 121<br /><br /> 153<br /><br /> 120<br /><br /> 129<br /><br /> 138<br /><br /> 136<br /><br /> 135<br /><br /> 124|  
|Systemtabellen|sys.numbered_procedures<br /><br /> sys.numbered_procedure_parameters|InclusionThresholdSetting|numbered_procedures<br /><br /> numbered_procedure_parameters|148<br /><br /> 149|  
|Systemfunktionen|fn_virtualservernodes<br /><br /> fn_servershareddrives|sys.dm_os_cluster_nodes<br /><br /> sys.dm_io_cluster_shared_drives|fn_virtualservernodes<br /><br /> fn_servershareddrives|155<br /><br /> 156|  
|Systemsichten|sys.sql_dependencies|sys.sql_expression_dependencies|sys.sql_dependencies|198|  
|Tabellenkomprimierung|Verwendung des vardecimal-Speicherformats|Das Vardecimal-Speicherformat ist veraltet. Bei der[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] -Datenkomprimierung werden Dezimalwerte sowie andere Datentypen komprimiert. Es wird empfohlen, dass Sie die Datenkomprimierung statt des vardecimal-Speicherformats verwenden.|Vardecimal-Speicherformat|200|  
|Tabellenkomprimierung|Verwenden Sie die sp_db_vardecimal_storage_format-Prozedur.|Das Vardecimal-Speicherformat ist veraltet. Bei der[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] -Datenkomprimierung werden Dezimalwerte sowie andere Datentypen komprimiert. Es wird empfohlen, dass Sie die Datenkomprimierung statt des vardecimal-Speicherformats verwenden.|sp_db_vardecimal_storage_format|201|  
|Tabellenkomprimierung|sp_estimated_rowsize_reduction_for_vardecimal (Transact-SQL)|Verwenden Sie stattdessen die Datenkomprimierung und die sp_estimate_data_compression_savings-Prozedur.|sp_estimated_rowsize_reduction_for_vardecimal|202|  
|Tabellenhinweise|Angeben von NOLOCK oder READUNCOMMITTED in der FROM-Klausel einer UPDATE- oder DELETE-Anweisung|Entfernen Sie die NOLOCK- oder READUNCOMMITTED-Tabellenhinweise aus der FROM-Klausel.|NOLOCK oder READUNCOMMITTED in UPDATE oder DELETE|1|  
|Tabellenhinweise|Angeben von Tabellenhinweisen ohne das WITH-Schlüsselwort|Verwenden Sie WITH.|Tabellenhinweis ohne WITH|8|  
|Tabellenhinweise|INSERT_HINTS||INSERT_HINTS|34|  
|TextPointer|WRITETEXT<br /><br /> UPDATETEXT<br /><br /> READTEXT|InclusionThresholdSetting|UPDATETEXT oder WRITETEXT<br /><br /> READTEXT|115<br /><br /> 114|  
|TextPointer|TEXTPTR()<br /><br /> TEXTVALID()|InclusionThresholdSetting|TEXTPTR<br /><br /> TEXTVALID|5<br /><br /> 6|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|:: Funktionsaufrufsequenz|Ersetzt durch SELECT *Spaltenliste* FROM sys.\<*Funktionsname*>().<br /><br /> Ersetzen Sie beispielsweise `SELECT * FROM ::fn_virtualfilestats(2,1)`durch `SELECT * FROM sys.fn_virtualfilestats(2,1)`.|Funktionsaufrufsyntax '::'|166|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Spaltenverweise mit 3 Teilen und 4 Teilen.|Namen mit 2 Teilen sind mit dem Standard kompatibel.|Mehr als zweiteiliger Spaltenname|3|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Eine in Anführungszeichen eingeschlossene Zeichenfolge, die als Spaltenalias für einen Ausdruck in einer SELECT-Liste verwendet wird:<br /><br /> '*Zeichenfolgenalias*' = *Ausdruck*|*Ausdruck* [AS] *Spaltenalias*<br /><br /> *Ausdruck* [AS] [*Spaltenalias*]<br /><br /> *Ausdruck* [AS] "*Spaltenalias*"<br /><br /> *Ausdruck* [AS] '*Spaltenalias*'<br /><br /> *Spaltenalias* = *Ausdruck*|Zeichenfolgenliterale als Spaltenaliase|184|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Nummerierte Prozeduren|Keine. Darf nicht verwendet werden.|ProcNums|160|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Syntax für*Tabellenname.Indexname* in DROP INDEX|Syntax für*Indexname* ON *Tabellenname* in DROP INDEX.|DROP INDEX mit zweiteiligem Namen|163|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Nicht beendete [!INCLUDE[tsql](../includes/tsql-md.md)] -Anweisungen mit einem Semikolon|Beenden Sie [!INCLUDE[tsql](../includes/tsql-md.md)] -Anweisungen mit einem Semikolon ( ; ).|InclusionThresholdSetting|InclusionThresholdSetting|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|GROUP BY ALL|Verwenden Sie eine benutzerdefinierte einzelfallspezifische Lösung mit UNION oder abgeleiteter Tabelle.|GROUP BY ALL|169|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|ROWGUIDCOL als Spaltenname in DML-Anweisungen|Verwenden Sie $rowguid.|ROWGUIDCOL|182|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|IDENTITYCOL als Spaltenname in DML-Anweisungen|Verwenden Sie $identity.|IDENTITYCOL|183|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Verwendung von #, ## als Name für eine temporäre Tabelle oder eine temporäre gespeicherte Prozedur|Verwenden Sie mindestens ein zusätzliches Zeichen.|'#' und '##' als Namen von temporären Tabellen und gespeicherten Prozeduren|185|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Verwendung von \@, \@\@ oder \@\@ als [!INCLUDE[tsql](../includes/tsql-md.md)]-Bezeichner.|\@, \@\@ oder Namen, die mit \@\@ beginnen, dürfen nicht als Bezeichner verwendet werden.|\@ und Namen, die mit \@\@ beginnen, als [!INCLUDE[tsql](../includes/tsql-md.md)]-Bezeichner|186.|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Verwendung des DEFAULT-Schlüsselworts als Standardwert.|Verwenden Sie das Wort DEFAULT nicht als Standardwert.|DEFAULT-Schlüsselwort als Standardwert|187|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Verwendung eines Leerzeichens als Trennzeichen zwischen Tabellenhinweisen|Trennen Sie die Tabellenhinweise durch Kommas.|Mehrere Tabellenhinweise ohne Komma|168|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Die Auswahlliste einer indizierten Aggregatsicht muss im Kompatibilitätsmodus '90' oder höher den Wert COUNT_BIG (*) enthalten.|Verwenden Sie COUNT_BIG(*).|Indexsicht-Auswahlliste ohne COUNT_BIG(*)|2|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Das indirekte Anwenden von Tabellenhinweisen auf einen Aufruf einer Tabellenwertfunktion (Table Valued Function, TVF) mit mehreren Anweisungen über eine Sicht.|Keine.|Indirekte TVF-Hinweise|7|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|ALTER DATABASE-Syntax:<br /><br /> MODIFY FILEGROUP READONLY<br /><br /> MODIFY FILEGROUP READWRITE|MODIFY FILEGROUP READ_ONLY<br /><br /> MODIFY FILEGROUP READ_WRITE|MODIFY FILEGROUP READONLY<br /><br /> MODIFY FILEGROUP READWRITE|195<br /><br /> 196|  
|Andere|DB-Library<br /><br /> Embedded SQL für C|Zwar werden Verbindungen von vorhandenen Anwendungen, die die DB-Library- und Embedded SQL-APIs verwenden, weiterhin von [!INCLUDE[ssDE](../includes/ssde-md.md)] unterstützt, aber die Dateien bzw. die Dokumentationen, die zum Programmieren von Anwendungen erforderlich sind, die diese APIs verwenden, gehören nicht mehr zum Lieferumfang. In zukünftigen Versionen von [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] werden Verbindungen von DB-Library- oder Embedded SQL-Anwendungen nicht mehr unterstützt. Verwenden Sie DB-Library bzw. Embedded SQL nicht zum Entwickeln neuer Anwendungen. Entfernen Sie alle Abhängigkeiten von DB-Library bzw. Embedded SQL, wenn Sie vorhandene Anwendungen ändern. Verwenden Sie anstelle dieser APIs den SQLClient-Namespace oder eine API wie ODBC. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] enthält die DB-Library-DLL nicht, die zum Ausführen dieser Anwendungen erforderlich ist. Zum Ausführen von DB-Library- oder Embedded SQL-Anwendungen muss die DB-Library-DLL von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Version 6.5, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 7.0 oder [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]verfügbar sein.|InclusionThresholdSetting|InclusionThresholdSetting|  
|Tools|SQL Server Profiler für die Ablaufverfolgungssammlung|Verwenden Sie den in SQL Server Management Studio eingebetteten Profiler für erweiterte Ereignisse.|SQL Server Profiler|InclusionThresholdSetting|  
|Tools|SQL Server Profiler für die Ablaufverfolgungswiedergabe|[SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md)|SQL Server Profiler|InclusionThresholdSetting|  
|Verwaltungsobjekte für die Ablaufverfolgung|Microsoft.SqlServer.Management.Trace-Namespace (enthält die APIs für die SQL Server-Ablaufverfolgungsobjekte und -Wiedergabeobjekte)|Ablaufverfolgungskonfiguration: <xref:Microsoft.SqlServer.Management.XEvent><br /><br /> Ablaufverfolgungslesevorgänge: <xref:Microsoft.SqlServer.XEvent.Linq><br /><br /> Ablaufverfolgungswiedergabe: keine Angabe|||  
|SQL-Ablaufverfolgung - gespeicherte Prozeduren, Funktionen und Katalogsichten|sp_trace_create<br /><br /> sp_trace_setevent<br /><br /> sp_trace_setfilter<br /><br /> sp_trace_setstatus<br /><br /> fn_trace_geteventinfo<br /><br /> fn_trace_getfilterinfo<br /><br /> fn_trace_getinfo<br /><br /> fn_trace_gettable<br /><br /> sys.traces<br /><br /> sys.trace_events<br /><br /> sys.trace_event_bindings<br /><br /> sys.trace_categories<br /><br /> sys.trace_columns<br /><br /> sys.trace_subclass_values|[Erweiterte Ereignisse](../relational-databases/extended-events/extended-events.md)|sp_trace_create<br /><br /> sp_trace_setevent<br /><br /> sp_trace_setfilter<br /><br /> sp_trace_setstatus<br /><br /> fn_trace_geteventinfo<br /><br /> fn_trace_getfilterinfo<br /><br /> fn_trace_getinfo<br /><br /> fn_trace_gettable<br /><br /> sys.traces<br /><br /> sys.trace_events<br /><br /> sys.trace_event_bindings<br /><br /> sys.trace_categories<br /><br /> sys.trace_columns<br /><br /> sys.trace_subclass_values|258<br /><br /> 260<br /><br /> 261<br /><br /> 259<br /><br /> 256<br /><br /> 257|  
  
> [!NOTE]  
>  Der **OUTPUT** -Cookieparameter für **sp_setapprole** ist zurzeit als **varbinary(8000)** dokumentiert, was der korrekten maximalen Länge entspricht. Die aktuelle Implementierung gibt jedoch **varbinary(50)**zurück. Wenn Entwickler **varbinary(50)** zugeordnet haben, erfordert die Anwendung möglicherweise Änderungen, wenn die Cookierückgabegröße in einer zukünftigen Version steigt. Obwohl es sich nicht um ein Veraltungsproblem handelt, wird dies in diesem Thema erwähnt, da die Anwendungsanpassungen ähnlich sind. Weitere Informationen finden Sie unter [sp_setapprole &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Nicht mehr unterstützte Datenbankmodul-Funktionalität in SQL Server 2016](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)  
  
  

