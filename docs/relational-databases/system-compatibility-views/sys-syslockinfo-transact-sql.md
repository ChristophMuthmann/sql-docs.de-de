---
title: Sys.syslockinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- syslockinfo_TSQL
- sys.syslockinfo_TSQL
- sys.syslockinfo
- syslockinfo
dev_langs:
- TSQL
helpviewer_keywords:
- syslockinfo system table
- sys.syslockinfo compatibility view
ms.assetid: d8cae434-807a-473e-b94f-f7a0e1b2daf0
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b2ce370d209b27366889a094d064d40c615d4362
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syssyslockinfo-transact-sql"></a>sys.syslockinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält Informationen zu allen erteilten, konvertierenden und wartenden Sperranforderungen.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
> [!IMPORTANT]  
>  Diese Funktion hat sich im Vergleich zu früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geändert. Weitere Informationen finden Sie unter [fehlerhafte Änderungen an Funktionen des Datenbankmoduls in SQL Server 2016](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**rsc_text**|**NCHAR(32)**|Textbeschreibung einer Sperrressource. Enthält einen Teil des Ressourcennamens.|  
|**rsc_bin**|**Binary(16)**|Binäre Sperrressource. Enthält die tatsächliche Sperrressource, die im Sperren-Manager enthalten ist. Diese Spalte wurde für Tools, mit denen das Ressourcenformat Sperre für das Erstellen einer eigenen erfahren Sperrressource formatierten sowie zur Durchführung von Selbstjoins auf **Syslockinfo**.|  
|**rsc_valblk**|**Binary(16)**|Sperrwertblock. Einige Ressourcentypen enthalten möglicherweise zusätzliche Daten in der Sperrressource, für die vom Sperren-Manager kein Hashvorgang ausgeführt wurde, um den Besitzer einer bestimmten Sperrressource zu bestimmen. So gehören z. B. Seitensperren nicht einer bestimmten Objekt-ID an. Zur Sperrenausweitung und für andere Zwecke. Die Objekt-ID einer Seitensperre kann jedoch im Sperrenwertblock platziert werden.|  
|**rsc_dbid**|**smallint**|Zur Ressource zugeordnete Datenbank-ID.|  
|**rsc_indid**|**smallint**|Zur Ressource zugeordnete Index-ID, falls zutreffend.|  
|**rsc_objid**|**int**|Zur Ressource zugeordnete Objekt-ID, falls zutreffend.|  
|**rsc_type**|**tinyint**|Ressourcentyp:<br /><br /> 1 = NULL-Ressource (nicht verwendet)<br /><br /> 2 = Datenbank<br /><br /> 3 = Datei<br /><br /> 4 = Index<br /><br /> 5 = Tabelle<br /><br /> 6 = Seite<br /><br /> 7 = Schlüssel<br /><br /> 8 = Block<br /><br /> 9 = RID (Zeilen-ID)<br /><br /> 10 = Anwendung|  
|**rsc_flag**|**tinyint**|Interne Ressourcenflags.|  
|**req_mode**|**tinyint**|Sperranforderungsmodus. Diese Spalte ist der Sperrmodus des Anforderers und stellt entweder den erteilten Modus oder den Konvertier- bzw. Wartemodus dar.<br /><br /> 0 = NULL. Auf die Ressource wird kein Zugriff erteilt. Dient als Platzhalter.<br /><br /> 1 = Sch-S (Schema stability, Schemastabilität). Stellt sicher, dass ein Schemaelement, wie z. B. eine Tabelle oder ein Index, nicht gelöscht wird, während eine Sitzung eine Schemastabilitätssperre für das Schemaelement aufrechterhält.<br /><br /> 2 = Sch-M (Schema modification, Schemaänderung). Muss von jeder Sitzung aufrechterhalten werden, die das Schema der angegebenen Ressource ändern möchte. Stellt sicher, dass keine anderen Sitzungen auf das angegebene Objekt verweisen.<br /><br /> 3 = S (Shared, Freigegeben). Der haltenden Sitzung wird der gemeinsame Zugriff auf die Ressource erteilt.<br /><br /> 4 = U (Update). Zeigt eine Updatesperre an, die für Ressourcen ausgegeben wurde, die möglicherweise aktualisiert werden. Sie wird dazu verwendet, eine häufige Form von Deadlock zu verhindern, die auftritt, wenn mehrere Sitzungen Ressourcen sperren, um diese möglicherweise zu einem späteren Zeitpunkt zu aktualisieren.<br /><br /> 5 = X (Exclusive, Exklusiv). Der haltenden Sitzung wird exklusiver Zugriff auf die Ressource erteilt.<br /><br /> 6 = IS (Intent Shared, Beabsichtigt-Freigegeben). Gibt die Absicht an, S-Sperren für eine untergeordnete Ressource in der Sperrhierarchie zu platzieren.<br /><br /> 7 = IU (Intent Update, Beabsichtigt-Update). Gibt die Absicht an, U-Sperren für eine untergeordnete Ressource in der Sperrhierarchie zu platzieren.<br /><br /> 8 = IX (Intent Exclusive, Beabsichtigt-Exklusiv). Gibt die Absicht an, X-Sperren für eine untergeordnete Ressource in der Sperrhierarchie zu platzieren.<br /><br /> 9 = SIU (Shared Intent Update, Freigegeben-Beabsichtigt-Update). Zeigt den gemeinsamen Zugriff auf eine Ressource mit der Absicht an, Updatesperren für untergeordnete Ressourcen in der Sperrhierarchie zu erhalten.<br /><br /> 10 = SIX (Shared Intent Exclusive, Freigegeben-Beabsichtigt-Exklusiv). Zeigt den gemeinsamen Zugriff auf eine Ressource mit der Absicht an, exklusive Sperren für untergeordnete Ressourcen in der Sperrhierarchie zu erhalten.<br /><br /> 11 = UIX (Update Intent Exclusive, Update-Beabsichtigt-Exklusiv). Zeigt eine aufrechterhaltene Updatesperre für eine Ressource mit der Absicht an, exklusive Sperren für untergeordnete Ressourcen in der Sperrhierarchie zu erhalten.<br /><br /> 12 = BU. Wird von Massenvorgängen verwendet.<br /><br /> 13 = RangeS_S (Freigegebener Schlüsselbereich und freigegebene Ressourcensperre). Zeigt serialisierbaren Bereichsscan an.<br /><br /> 14 = RangeS_U (Freigegebener Schlüsselbereich und Updatesperre für Ressource). Zeigt serialisierbaren Updatescan an.<br /><br /> 15 = RangeI_N (Schlüsselbereich einfügen und keine Ressourcensperre). Wird zum Testen von Bereichen verwendet, bevor ein neuer Schlüssel in einen Index eingefügt wird.<br /><br /> 16 = RangeI_S. Konvertierungssperre für Schlüsselbereich, die durch eine Überschneidung von RangeI_N- und S-Sperren erzeugt wurde.<br /><br /> 17 = RangeI_U. Konvertierungssperre für Schlüsselbereich, die durch eine Überschneidung von RangeI_N- und U-Sperren erzeugt wurde.<br /><br /> 18 = RangeI_X. Konvertierungssperre für Schlüsselbereich, die durch eine Überschneidung von RangeI_N- und X-Sperren erzeugt wurde.<br /><br /> 19 = RangeX_S. Konvertierungssperre für Schlüsselbereich, die durch eine Überschneidung von RangeI_N- und RangeS_S.-Sperren erzeugt wurde.<br /><br /> 20 = RangeX_U. Konvertierungssperre für Schlüsselbereich, die durch eine Überschneidung von RangeI_N- und RangeS_U-Sperren erzeugt wurde.<br /><br /> 21 = RangeX_X (Exklusiver Schlüsselbereich und exklusive Ressourcensperre). Dies ist eine Konvertierungssperre, die für das Update eines Schlüssels in einem Bereich verwendet wird.|  
|**req_status**|**tinyint**|Status der Sperranforderung:<br /><br /> 1 = Erteilt<br /><br /> 2 = Konvertieren<br /><br /> 3 = Warten|  
|**req_refcnt**|**smallint**|Sperrverweiszähler. Jedes Mal, wenn eine Transaktion eine Sperre für eine bestimmte Ressource anfordert, wird ein Verweiszähler erhöht. Die Sperre kann erst dann freigegeben werden, wenn der Verweiszähler auf 0 steht.|  
|**req_cryrefcnt**|**smallint**|Zur künftigen Verwendung reserviert. Immer auf 0 festgelegt.|  
|**req_lifetime**|**int**|Sperrenlebensdauer-Bitmuster. Während bestimmter Abfrageverarbeitungsstrategien müssen Sperren für Ressourcen aufrechterhalten werden, bis der Abfrageprozessor eine bestimmte Phase der Abfrage abgeschlossen hat. Das Sperrenlebensdauer-Bitmuster wird vom Abfrageprozessor und vom Transaktions-Manager dazu verwendet, Gruppen von Sperren anzugeben. Diese können freigegeben werden, wenn eine bestimmte Phase einer Abfrage abgeschlossen ist. Bestimmte Bits im Bitmuster werden verwendet, um Sperren anzugeben, die bis zum Ende einer Transaktion aufrechterhalten werden, auch wenn ihr Verweiszähler gleich 0 ist.|  
|**req_spid**|**int**|Interne [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] Prozess-ID der Sitzung, die die Sperre anfordert.|  
|**req_ecid**|**int**|Ausführungskontext-ID (ECID, Execution Context ID). Gibt an, welcher Thread in einem parallelen Vorgang eine bestimmte Sperre besitzt.|  
|**req_ownertype**|**smallint**|Typ des der Sperre zugeordneten Objekts:<br /><br /> 1 = Transaktion<br /><br /> 2 = Cursor<br /><br /> 3 = Sitzung<br /><br /> 4 = ExSession<br /><br /> Beachten Sie, dass 3 und 4 eine besondere Version von Sitzungssperren darstellen, die entsprechend Datenbank- und Dateigruppensperren protokollieren.|  
|**req_transactionID**|**bigint**|Eindeutige Transaktions-ID verwendet wird, in **Syslockinfo** und im Profiler-Ereignis|  
|**req_transactionUOW**|**uniqueidentifier**|Identifiziert die ID der Arbeitseinheit (UOW, Unit of Work) der DTC-Transaktion. Bei Nicht-MS DTC-Transaktionen wird UOW auf 0 festgelegt.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [Zuordnen von Systemtabellen zu Systemsichten &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Kompatibilitätssichten &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
