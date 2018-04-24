---
title: ALTER FULLTEXT CATALOG (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_FULLEXT_CATALOG_TSQL
- ALTER FULLEXT CATALOG
dev_langs:
- TSQL
helpviewer_keywords:
- modifying full-text catalogs
- full-text catalogs [SQL Server], rebuilding
- accent sensitivity
- ALTER FULLTEXT CATALOG statement
- full-text catalogs [SQL Server], modifying
- full-text catalogs [SQL Server], reorganizing
ms.assetid: 31a47aaf-6c7f-48a4-a86a-d57aec66c9cb
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f6d06e79d04a223a8100f0b48ab8243df44f7d4a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alter-fulltext-catalog-transact-sql"></a>ALTER FULLTEXT CATALOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Ändert die Eigenschaften eines Volltextkatalogs.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER FULLTEXT CATALOG catalog_name   
{ REBUILD [ WITH ACCENT_SENSITIVITY = { ON | OFF } ]  
| REORGANIZE  
| AS DEFAULT   
}  
```  
  
## <a name="arguments"></a>Argumente  
 *catalog_name*  
 Gibt den Namen des zu ändernden Katalogs an. Wenn kein Katalog mit dem angegebenen Namen vorhanden ist, gibt [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Fehler zurück und führt den ALTER-Vorgang nicht aus.  
  
 REBUILD  
 Weist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an, den gesamten Katalog neu zu erstellen. Bei der Neuerstellung eines Katalogs wird der vorhandene Katalog gelöscht und an seiner Stelle ein neuer Katalog erstellt. Alle Tabellen, in denen Referenzen für die Volltextindizierung vorhanden sind, werden dem neuen Katalog zugeordnet. Durch das erneute Erstellen werden die Volltextmetadaten in den Datenbanksystemtabellen zurückgesetzt.  
  
 WITH ACCENT_SENSITIVITY = {ON|OFF}  
 Gibt an, ob der zu ändernde Katalog für die Volltextindizierung und Abfrage nach Akzent unterscheidet.  
  
 Verwenden Sie die FULLTEXTCATALOGPROPERTY-Funktion mit dem **accentsensitivity**-Eigenschaftswert für *catalog_name*, um die aktuelle Eigenschaftseinstellung für die Unterscheidung nach Akzent eines Volltextkatalogs zu bestimmen. Gibt die Funktion '1' zurück, unterscheidet der Volltextkatalog nach Akzent. Gibt die Funktion '0' zurück, unterscheidet der Katalog nicht nach Akzent.  
  
 Die Standardeinstellung für die Unterscheidung nach Akzent des Katalogs und der Datenbank stimmen überein.  
  
 REORGANIZE  
 Weist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an, eine *Masterzusammenführung* auszuführen, wobei die im Verlauf der Indizierung erstellten kleineren Indizes zu einem großen Index zusammengeführt werden. Das Zusammenführen von Volltextindexfragmenten kann die Leistung verbessern und Datenträger- und Speicherressourcen freigeben. Bei häufigen Änderungen am Volltextkatalog sollten Sie diesen Befehl in regelmäßigen Abständen ausführen, um den Volltextkatalog neu zu organisieren.  
  
 REORGANIZE optimiert auch die internen Index- und Katalogstrukturen.  
  
 Abhängig vom Umfang der indizierten Daten kann bis zum Abschluss einer Masterzusammenführung einige Zeit vergehen. Die Masterzusammenführung einer großen Datenmenge kann eine Transaktion mit langer Ausführungszeit erzeugen und das Abschneiden des Transaktionsprotokolls während des Prüfpunkts verzögern. In diesem Fall kann das Transaktionsprotokoll unter dem vollständigen Wiederherstellungsmodell erheblich anwachsen. Sie sollten sicherstellen, dass das Transaktionsprotokoll vor dem Reorganisieren eines großen Volltextindexes in einer Datenbank, die das vollständige Wiederherstellungsmodell verwendet, genügend Speicherplatz für eine Transaktion mit langer Laufzeit enthält. Weitere Informationen finden Sie unter [Verwalten der Größe der Transaktionsprotokolldatei](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md).  
  
 AS DEFAULT  
 Gibt an, dass dieser Katalog der Standardkatalog ist. Werden Volltextindizes ohne Angabe von Katalogen erstellt, wird der Standardkatalog verwendet. Ist ein Standard-Volltextkatalog vorhanden, wird die vorhandene Standardeinstellung durch Festlegen von AS DEFAULT für diesen Katalog überschrieben.  
  
## <a name="permissions"></a>Berechtigungen  
 Benutzer müssen über die ALTER-Berechtigung für den Volltextkatalog verfügen oder Mitglied der festen Datenbankrollen **db_owner** oder **db_ddladmin** oder der festen Serverrolle sysadmin sein.  
  
> [!NOTE]  
>  Damit ALTER FULLTEXT CATALOG AS DEFAULT verwendet werden kann, muss der Benutzer über ALTER-Berechtigung für den Volltextkatalog und CREATE FULLTEXT CATALOG-Berechtigung für die Datenbank verfügen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die `accentsensitivity`-Eigenschaft des Standard-Volltextkatalogs `ftCatalog` geändert, der nach Akzent unterscheidet.  
  
```  
--Change to accent insensitive  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT CATALOG ftCatalog   
REBUILD WITH ACCENT_SENSITIVITY=OFF;  
GO  
-- Check Accentsensitivity  
SELECT FULLTEXTCATALOGPROPERTY('ftCatalog', 'accentsensitivity');  
GO  
--Returned 0, which means the catalog is not accent sensitive.  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sys.fulltext_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [DROP FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)   
 [Volltextsuche](../../relational-databases/search/full-text-search.md)  
  
  
