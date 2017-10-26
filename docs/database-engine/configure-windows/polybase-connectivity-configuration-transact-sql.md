---
title: "Konfiguration der PolyBase-Netzwerkkonnektivität (Transact-SQL) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PolyBase
ms.assetid: 82252e4f-b1d0-49e5-aa0b-3624aade2add
caps.latest.revision: 14
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 74f73ab33a010583b4747fcc2d9b35d6cdea14a2
ms.openlocfilehash: b57b1e802969995f87d5663e5e7dbdc92700a9b5
ms.contentlocale: de-de
ms.lasthandoff: 08/04/2017

---
# <a name="polybase-connectivity-configuration-transact-sql"></a>Konfiguration der PolyBase-Netzwerkkonnektivität (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-pdw-md.md)]

  Stellt globale Konfigurationseinstellungen für die PolyBase-Hadoop- und Azure Blob Storage-Konnektivität dar oder ändert diese.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
--List all of the configuration options  
sp_configure  
[;]  
  
--Configure Hadoop connectivity  
sp_configure [ @configname = ] 'hadoop connectivity',  
             [ @configvalue = ] { 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 }  
[;]  
  
RECONFIGURE  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@configname=** ] **'***option_name***'**  
 Der Name einer Konfigurationsoption. *option_name* ist vom Datentyp **varchar(35)**. Der Standardwert ist NULL. Erfolgt keine Angabe, wird die gesamte Liste der Optionen zurückgegeben.  
  
 [ **@configvalue=** ] **'***value***'**  
 Die neue Konfigurationseinstellung. *value* ist vom Datentyp **int**. Der Standardwert ist NULL. Der Maximalwert kann je nach Option unterschiedlich sein.  
  
 **'hadoop connectivity'**  
 Gibt den Typ der Hadoop-Datenquelle für alle Verbindungen von PolyBase mit Hadoop-Clustern oder Azure Blob Storage (WASB) an. Diese Einstellung wird benötigt, um eine externe Datenquelle für eine externe Tabelle zu erstellen. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md),  
  
 Dies sind die Hadoop-Konnektivitätseinstellungen und die entsprechenden unterstützten Hadoop-Datenquellen. Es kann immer nur eine Einstellung zu einer Zeit wirksam sein. Die Optionen 1, 4 und 7 ermöglichen das Erstellen mehrerer externer Datenquellen und das Verwenden dieser über alle Sitzungen auf dem Server hinweg.  
  
-   Option 0: Hadoop-Konnektivität deaktivieren  
  
-   Option 1: Hortonworks HDP 1.3 unter Windows Server  
  
-   Option 1: Azure Blob Storage (WASB[S])  
  
-   Option 2: Hortonworks HDP 1.3 unter Linux  
  
-   Option 3: Cloudera CDH 4.3 unter Linux  
  
-   Option 4: Hortonworks HDP 2.0 unter Windows Server  
  
-   Option 4: Azure Blob Storage (WASB[S])  
  
-   Option 5: Hortonworks HDP 2.0 unter Linux  
  
-   Option 6: Cloudera 5.1, 5.2, 5.3, 5.4, 5.5, 5.9, 5.10, 5.11 und 5.12 unter Linux  
  
-   Option 7: Hortonworks 2.1, 2.2, 2.3, 2.4, 2.5 und 2.6 unter Linux  
  
-   Option 7: Hortonworks 2.1, 2.2 und 2.3 unter Windows Server  
  
-   Option 7: Azure Blob Storage (WASB[S])  
  
 **RECONFIGURE**  
 Aktualisiert den Ausführungswert (run_value), damit er mit dem Konfigurationswert (config_value) übereinstimmt. Definitionen von „run_value“ und „config_value“ finden Sie unter [Resultsets](#ResultSets) . Der neue Konfigurationswert, der von sp_configure festgelegt wird, wird erst dann wirksam, wenn der Ausführungswert durch die RECONFIGURE-Anweisung festgelegt wird.  
  
 Nach der Ausführung von RECONFIGURE müssen Sie den SQL Server-Dienst beenden und neu starten. Beachten Sie, dass beim Beenden des SQL Server-Diensts die zwei zusätzlichen PolyBase-Modul- und Datenverschiebungsdienste automatisch beendet werden. Starten Sie diese zwei Dienste nach dem Neustart des SQL Server-Moduldiensts neu (sie starten nicht automatisch).  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
##  <a name="ResultSets"></a> Resultsets  
 Bei der Ausführung ohne Parameter gibt **sp_configure** ein Resultset mit fünf Spalten zurück.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(35)**|Der Name der Konfigurationsoption.|  
|**minimum**|**int**|Der Mindestwert der Konfigurationsoption.|  
|**maximum**|**int**|Der Höchstwert der Konfigurationsoption.|  
|**config_value**|**int**|Mithilfe von **sp_configure**festgelegter Wert.|  
|**run_value**|**int**|Von PolyBase aktuell verwendeter Wert. Dieser Wert wird durch Ausführen von RECONFIGURE festgelegt.<br /><br /> **config_value** und **run_value** sind in der Regel gleich, sofern der Wert nicht gerade geändert wird.<br /><br /> Bevor dieser Ausführungswert richtig ist, ist möglicherweise ein Neustart erforderlich, falls gerade eine Neukonfiguration ausgeführt wird.|  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]müssen Sie nach der Ausführung von RECONFIGURE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]neu starten, damit der Ausführungswert von „hadoop connectivity“ wirksam wird.  
In [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]müssen Sie nach der Ausführung von RECONFIGURE die Region [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] neu starten, damit der Ausführungswert von „hadoop connectivity“ wirksam wird.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 RECONFIGURE ist in einer expliziten oder impliziten Transaktion nicht zulässig.  
  
## <a name="permissions"></a>Berechtigungen  
 Alle Benutzer können **sp_configure** ohne Parameter oder mit dem Parameter @configname ausführen.  
  
 Erfordert die **ALTER SETTINGS** -Berechtigung auf Serverebene oder die Mitgliedschaft in der festen **sysadmin** -Serverrolle, um einen Konfigurationswert zu ändern oder RECONFIGURE auszuführen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-list-all-available-configuration-settings"></a>A. Auflisten aller verfügbaren Konfigurationseinstellungen  
 Im folgenden Beispiel wird dargestellt, wie alle Konfigurationsoptionen aufgelistet werden.  
  
```  
EXEC sp_configure;  
```  
  
 Das Ergebnis gibt den Optionsnamen zurück, gefolgt von den minimalen und maximalen Werten für die Option. **config_value** ist der Wert, den SQL oder PolyBase verwenden werden, wenn die Neukonfiguration abgeschlossen ist. **run_value** ist der Wert, der gerade verwendet wird. **config_value** und **run_value** sind in der Regel gleich, sofern der Wert nicht gerade geändert wird.  
  
### <a name="b-list-the-configuration-settings-for-one-configuration-name"></a>B. Auflisten der Konfigurationseinstellungen für einen Konfigurationsnamen  
  
```  
EXEC sp_configure @configname='hadoop connectivity';  
```  
  
### <a name="c-set-hadoop-connectivity"></a>C. Festlegen der Hadoop-Konnektivität  
 In diesem Beispiel wird PolyBase auf die Option 7 festgelegt. Diese Option ermöglicht es PolyBase, externe Tabellen unter Hortonworks 2.1, 2.2, und 2.3 unter Linux und Windows Server und unter Azure Blob Storage zu erstellen und zu verwenden. Beispielsweise könnte SQL über 30 externe Tabellen verfügen, wobei 7 davon auf Daten in Hortonworks 2.1 unter Linux, 4 auf Daten in Hortonworks 2.2 unter Linux, 7 auf Daten in Hortonworks 2.3 unter Linux und die restlichen 12 auf Daten in Azure Blob Storage verweisen würden.  
  
```  
--Configure external tables to reference data on Hortonworks 2.1, 2.2, and 2.3 on Linux, and Azure blob storage  
  
sp_configure @configname = 'hadoop connectivity', @configvalue = 7;  
GO  
  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  

