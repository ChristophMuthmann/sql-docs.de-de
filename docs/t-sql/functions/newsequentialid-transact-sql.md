---
title: NEWSEQUENTIALID (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/08/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- NEWSEQUENTIALID
- NEWSEQUENTIALID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- NEWSEQUENTIALID function
- GUIDs [SQL Server]
ms.assetid: e06d2cab-f1ff-42f1-8550-6aaec57be36f
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ebc62c0b40e659c9e707e1ddf77b738e4ce20f9a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="newsequentialid-transact-sql"></a>NEWSEQUENTIALID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt einen GUID, der größer ist als alle GUIDs, die seit dem Start von Windows bisher von dieser Funktion auf einem angegebenen Computer generiert wurden. Nach dem Neustart von Windows kann der GUID wieder in einem niedrigeren Bereich beginnen, ist aber immer noch global eindeutig. Wenn eine GUID-Spalte als Zeilenbezeichner verwendet wird, kann die Verwendung von NEWSEQUENTIALID schneller zu Ergebnissen führen als die Verwendung der NEWID-Funktion. Dies ist darauf zurückzuführen, dass die NEWID-Funktion zufällige Aktivität erzeugt und weniger zwischengespeicherte Datenseiten verwendet. Die Verwendung von NEWSEQUENTIALID hilft auch beim vollständigen Ausfüllen der Daten- und Indexseiten.  
  
> [!IMPORTANT]  
>  Falls Datenschutz eine wichtige Überlegung ist, sollten Sie diese Funktion nicht verwenden. Der Wert der als Nächstes erstellten GUID ist vorhersagbar, daher ist auch der Zugriff auf Daten möglich, die mit dieser GUID verknüpft sind.  
  
 NEWSEQUENTIALID ist ein Wrapper über die Windows-Funktion [UuidCreateSequential](http://go.microsoft.com/fwlink/?LinkId=164027) mit [angewendeter Byte-Mischung](https://blogs.msdn.microsoft.com/dbrowne/2012/07/03/how-to-generate-sequential-guids-for-sql-server-in-net/).
  
> [!WARNING]  
>  Die UuidCreateSequential-Funktion verfügt über Hardwareabhängigkeiten. Auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können Cluster von sequenziellen Werten entstehen, wenn Datenbanken (z.B. eigenständige Datenbanken) auf andere Computer verschoben werden. Bei der Verwendung von Always On und auf [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] können Cluster von sequenziellen Werten entstehen, wenn die Datenbank ein Failover auf einen anderen Computer durchführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
NEWSEQUENTIALID ( )  
```  
  
## <a name="return-type"></a>Rückgabetyp  
 **uniqueidentifier**  
  
## <a name="remarks"></a>Remarks  
 NEWSEQUENTIALID() kann nur in Bezug auf DEFAULT-Einschränkungen für Tabellenspalten des Typs **uniqueidentifier** verwendet werden. Zum Beispiel:  
  
```  
CREATE TABLE myTable (ColumnA uniqueidentifier DEFAULT NEWSEQUENTIALID());   
```  
  
 Wenn NEWSEQUENTIALID() in DEFAULT-Ausdrücken verwendet wird, ist eine Kombination mit anderen Skalaroperatoren nicht möglich. Sie können z. B. folgende Aktionen nicht ausführen:  
  
```  
CREATE TABLE myTable (ColumnA uniqueidentifier DEFAULT dbo.myfunction(NEWSEQUENTIALID()));  
```  
  
 Im vorherigen Beispiel ist `myfunction()` eine benutzerdefinierte Skalarfunktion, die einen `uniqueidentifier`-Wert annimmt und zurückgibt.  
  
 Auf NEWSEQUENTIALID() kann in Abfragen nicht verwiesen werden.  
  
 Sie können NEWSEQUENTIALID() zum Generieren von GUIDs verwenden, um Seitenteilungen und zufällige E/A auf Blattebene von Indizes zu reduzieren.  
  
 Jede mit NEWSEQUENTIALID() generierte GUID ist auf diesem Computer eindeutig. Die mit NEWSEQUENTIALID() generierten GUIDs sind nur über mehrere Computer hinweg eindeutig, wenn der Quellcomputer über eine Netzwerkkarte verfügt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [NEWID &#40;Transact-SQL&#41;](../../t-sql/functions/newid-transact-sql.md)   
 [Vergleichsoperatoren &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md)  
  
  
