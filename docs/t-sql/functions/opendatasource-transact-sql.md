---
title: OPENDATASOURCE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- OPENDATASOURCE
- OPENDATASOURCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data sources [SQL Server]
- OPENDATASOURCE function
- remote data access [SQL Server], OPENDATASOURCE
- ad hoc distributed queries
- OLE DB data sources [SQL Server]
- ad hoc connection information
ms.assetid: 5510b846-9cde-4687-8798-be9a273aad31
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 44f5222050176deeefe489b833322c2ecfd57748
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="opendatasource-transact-sql"></a>OPENDATASOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Stellt Ad-hoc-Verbindungsinformationen als Teil eines vierteiligen Objektnamens ohne Verwendung eines Verbindungsservernamens bereit.  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
OPENDATASOURCE ( provider_name, init_string )  
```  
  
## <a name="arguments"></a>Argumente  
 *provider_name*  
 Der Namen, der als PROGID des OLE DB-Anbieters für den Zugriff auf die Datenquelle registriert ist. *provider_name* ist vom Datentyp **char** und verfügt über keinen Standardwert.  
  
 *init_string*  
 Die Verbindungszeichenfolge, die an die IDataInitialize-Schnittstelle des Zielanbieters übergeben wird. Die Syntax der Anbieterzeichenfolge basiert auf durch Semikolons getrennten Schlüssel-Wert-Paaren im folgenden Format: **'***keyword1*=* value***;***keyword2*=* value***'**.  
  
 Informationen zu bestimmten, vom Anbieter unterstützten Paaren aus Schlüsselwort und Wert finden Sie im MDAC SDK ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Data Access Components Software Development Kit). In dieser Dokumentation wird die grundlegende Syntax definiert. In der folgenden Tabelle werden die am häufigsten im *init_string*-Argument verwendeten Schlüsselwörter aufgelistet.  
  
|Schlüsselwort|OLE DB-Eigenschaft|Gültige Werte und Beschreibung|  
|-------------|---------------------|----------------------------------|  
|Datenquelle|DBPROP_INIT_DATASOURCE|Name der Datenquelle, mit der eine Verbindung hergestellt werden soll. Unterschiedliche Anbieter interpretieren diesen Namen auf unterschiedliche Arten. Für den OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client gibt er den Servernamen an. Für den OLE DB-Anbieter von Jet gibt er den vollständigen Pfad der MDB- oder XLS-Datei an.|  
|Speicherort|DBPROP_INIT_LOCATION|Speicherort der Datenbank, mit der eine Verbindung hergestellt werden soll.|  
|Extended Properties|DBPROP_INIT_PROVIDERSTRING|Anbieterspezifische Verbindungszeichenfolge.|  
|Connect timeout|DBPROP_INIT_TIMEOUT|Timeoutwert, bei dessen Erreichen der Verbindungsversuch einen Fehler erzeugt.|  
|Benutzer-ID|DBPROP_AUTH_USERID|Für die Verbindung zu verwendende Benutzer-ID.|  
|Kennwort|DBPROP_AUTH_PASSWORD|Für die Verbindung zu verwendendes Kennwort.|  
|Katalog|DBPROP_INIT_CATALOG|Name des Anfangs- oder Standardkatalogs beim Herstellen einer Verbindung mit der Datenquelle.|  
|Integrierte Sicherheit|DBPROP_AUTH_INTEGRATED|SSPI, zur Angabe der Windows-Authentifizierung|  
  
## <a name="remarks"></a>Remarks  
 OPENDATASOURCE kann nur dann für den Zugriff auf Remotedaten aus OLE DB-Datenquellen verwendet werden, wenn die DisallowAdhocAccess-Registrierungsoption explizit für den angegebenen Anbieter auf 0 festgelegt und die erweiterte Konfigurationsoption Ad Hoc Distributed Queries aktiviert wird. Wenn diese Optionen nicht festgelegt sind, ermöglicht das Standardverhalten keinen Ad-hoc-Zugriff.  
  
 Die OPENDATASOURCE-Funktion kann an denselben Stellen in der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Syntax verwendet werden wie ein Verbindungsservername. Deshalb kann OPENDATASOURCE als erster Teil eines vierteiligen Namens verwendet werden, der in einer SELECT-, INSERT-, UPDATE-, oder DELETE-Anweisung auf einen Tabellen- oder Sichtnamen bzw. in einer EXECUTE-Anweisung auf eine remote gespeicherte Prozedur verweist. Beim Ausführen von remote gespeicherten Prozeduren muss OPENDATASOURCE auf eine andere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz verweisen. Für die Argumente von OPENDATASOURCE können keine Variablen verwendet werden.  
  
 Wie die OPENROWSET-Funktion sollte OPENDATASOURCE nur auf OLE DB-Datenquellen verweisen, auf die selten zugegriffen wird. Definieren Sie Verbindungsserver für Datenquellen, auf die nicht nur ein paar Mal zugegriffen wird. Weder OPENDATASOURCE noch OPENROWSET stellen die gesamte Funktionalität einer Verbindungsserverdefinition bereit, wie die Sicherheitsverwaltung und die Möglichkeit, Kataloginformationen abzufragen. Alle Verbindungsinformationen, einschließlich Kennwörtern, müssen bei jedem Aufruf von OPENDATASOURCE bereitgestellt werden.  
  
> [!IMPORTANT]  
>  Die Windows-Authentifizierung bietet deutlich mehr Sicherheit als die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung. Verwenden Sie nach Möglichkeit die Windows-Authentifizierung. OPENDATASOURCE sollte nicht mit expliziten Kennwörtern in der Verbindungszeichenfolge verwendet werden.  
  
 Die Verbindungsanforderungen für jeden Anbieter sind vergleichbar mit den Anforderungen an die Parameter, die zum Erstellen von Verbindungsservern verwendet werden. Details für viele allgemeine Anbieter sind im Artikel [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) aufgeführt.  
  
 Jeder Aufruf von OPENDATASOURCE, OPENQUERY oder OPENROWSET in der FROM-Klausel wird einzeln und unabhängig von anderen Aufrufen dieser Funktionen ausgewertet, die als Ziel des Updates verwendet werden, auch wenn für die beiden Aufrufe identische Argumente angegeben werden. Insbesondere haben Filter- oder Joinbedingungen, die auf das Ergebnis eines dieser Aufrufe angewendet werden, keine Auswirkungen auf die Ergebnisse des jeweils anderen.  
  
## <a name="permissions"></a>Berechtigungen  
 Jeder Benutzer kann OPENDATASOURCE ausführen. Die Berechtigungen, die zum Herstellen einer Verbindung mit dem Remoteserver verwendet werden, werden anhand der Verbindungszeichenfolge bestimmt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Ad-hoc-Verbindung mit der `Payroll`-Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem Server `London` erstellt und die `AdventureWorks2012.HumanResources.Employee`-Tabelle abgefragt. (Wenn Sie SQLNCLI verwenden, leitet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zur neuesten Version des OLE DB-Anbieters von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client um.)  
  
```  
SELECT *  
FROM OPENDATASOURCE('SQLNCLI',  
    'Data Source=London\Payroll;Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Employee  
```  
  
 Im folgenden Beispiel wird eine Ad-hoc-Verbindung zu einem Excel-Arbeitsblatt im Format 1997 – 2003 hergestellt.  
  
```  
SELECT * FROM OPENDATASOURCE('Microsoft.Jet.OLEDB.4.0',  
'Data Source=C:\DataFolder\Documents\TestExcel.xls;Extended Properties=EXCEL 5.0')...[Sheet1$] ;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
  
