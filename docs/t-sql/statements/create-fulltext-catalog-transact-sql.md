---
title: CREATE FULLTEXT CATALOG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CATALOG_TSQL
- CREATE_FULLTEXT_TSQL
- FULLTEXT_TSQL
- FULLTEXT CATALOG
- CREATE FULLTEXT CATALOG
- CREATE_FULLTEXT_CATALOG_TSQL
- CATALOG
- FULLTEXT_CATALOG_TSQL
- CREATE FULLTEXT
- FULLTEXT
dev_langs:
- TSQL
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- CREATE FULLTEXT CATALOG statement
ms.assetid: d7a8bd93-e2d7-4a40-82ef-39069e65523b
caps.latest.revision: 60
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 303908a306661c764b9cd258147fcc911d2d3983
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-fulltext-catalog-transact-sql"></a>CREATE FULLTEXT CATALOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt einen Volltextkatalog für eine Datenbank. Ein Volltextkatalog kann mehrere Volltextindizes besitzen, ein Volltextindex kann jedoch nur Teil eines Volltextkatalogs sein. Jede Datenbank kann keinen oder mehrere Volltextkataloge enthalten.  
  
 Sie können keine Volltextkataloge in erstellen die **master**, **Modell**, oder **Tempdb** Datenbanken.  
  
> [!IMPORTANT]  
>  Beginnend mit [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], ein Volltextkatalogs ist ein virtuelles Objekt und gehört keiner Dateigruppe. Ein Volltextkatalog ist ein logisches Konzept, das auf eine Gruppe von Volltextindizes verweist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE FULLTEXT CATALOG catalog_name  
     [ON FILEGROUP filegroup ]  
     [IN PATH 'rootpath']  
     [WITH <catalog_option>]  
     [AS DEFAULT]  
     [AUTHORIZATION owner_name ]  
  
<catalog_option>::=  
     ACCENT_SENSITIVITY = {ON|OFF}  
  
```  
  
## <a name="arguments"></a>Argumente  
 *catalog_name*  
 Der Name des neuen Katalogs. Der Katalogname muss für alle Katalognamen in der aktuellen Datenbank eindeutig sein. Zudem muss der Name der Datei, die dem Volltextkatalog entspricht (siehe ON FILEGROUP), für alle Dateien in der Datenbank eindeutig sein. Wenn der Name des Katalogs bereits für einen anderen Katalog in der Datenbank verwendet wird, wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein Fehler zurückgegeben.  
  
 Der Katalogname darf maximal 120 Zeichen enthalten.  
  
 ON FILEGROUP *filegroup*  
 Beginnend mit [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], diese Klausel hat keine Auswirkungen.  
  
 IM Pfad **"***Rootpath***"**  
 > [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Beginnend mit [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], diese Klausel hat keine Auswirkungen.  
  
 ACCENT_SENSITIVITY = {ON|OFF}  
 Gibt an, ob für den Katalog bei der Volltextindizierung nach Akzent unterschieden wird. Bei einer Änderung dieser Eigenschaft muss der Index neu erstellt werden. Standardmäßig wird die in der Datenbanksortierung angegebene Unterscheidung nach Akzent verwendet. Um die Sortierung der Datenbank anzuzeigen, verwenden Sie die **sys.databases** -Katalogsicht angezeigt.  
  
 Um die aktuelle Einstellung der Unterscheidung nach Groß-/ Kleinschreibung-Eigenschaft des eines Volltextkatalogs zu bestimmen, verwenden Sie die FULLTEXTCATALOGPROPERTY-Funktion mit dem **Accentsensitivity** -Eigenschaftswert für *Catalog_name*. Wird '1' zurückgegeben, unterscheidet der Volltextkatalog nach Akzent. Wird '0' zurückgegeben, unterscheidet der Katalog nicht nach Akzent.  
  
 AS DEFAULT  
 Gibt an, dass der Katalog als Standardkatalog verwendet wird. Wenn beim Erstellen von Volltextindizes nicht explizit ein Volltextkatalog angegeben wird, wird der Standardkatalog verwendet. Falls ein vorhandener Volltextkatalog bereits mit AS DEFAULT gekennzeichnet ist, wird durch das Festlegen von AS DEFAULT für den neuen Katalog dieser Katalog als standardmäßiger Volltextkatalog verwendet.  
  
 Autorisierung *Owner_name*  
 Legt den Namen eines Datenbankbenutzers oder einer Datenbankrolle als Besitzer des Volltextkatalogs fest. Wenn *Owner_name* ist eine Rolle, die Rolle der Name einer Rolle, die der aktuelle Benutzer ein Mitglied ist sein oder muss des Benutzers die Anweisung ausführt, der Datenbankbesitzer oder Systemadministrator sein.  
  
 Wenn *Owner_name* ein Benutzernamen ein, wird der Benutzername muss eines der folgenden sein:  
  
-   Den Namen des Benutzers, der die Anweisung ausführt.  
  
-   Den Namen eines Benutzers, für den der Benutzer, der den Befehl ausführt, IMPERSONATE-Berechtigungen besitzt.  
  
-   Oder der Benutzer, der den Befehl ausführt, muss der Datenbankbesitzer oder Systemadministrator sein.  
  
 *Owner_name* muss auch der TAKE OWNERSHIP-Berechtigung für den angegebenen Volltextkatalog erteilt werden.  
  
## <a name="remarks"></a>Hinweise  
 Volltextkatalog-IDs beginnen bei 00005 und werden mit jedem neu erstellten Katalog um eins erhöht.  
  
## <a name="permissions"></a>Berechtigungen  
 Benutzer muss über die CREATE FULLTEXT CATALOG-Berechtigung für die Datenbank oder ein Mitglied der **Db_owner**, oder **Db_ddladmin** festen Datenbankrollen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden ein Volltextkatalog und ein Volltextindex erstellt.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE FULLTEXT CATALOG ftCatalog AS DEFAULT;  
GO  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume) KEY INDEX PK_JobCandidate_JobCandidateID;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. fulltext_catalogs &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [DROP FULLTEXT CATALOG &#40; Transact-SQL &#41;](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)   
 [Volltextsuche](../../relational-databases/search/full-text-search.md)   
 [Neuer Volltextkatalog &#40; Seite "Allgemein" &#41;](http://msdn.microsoft.com/library/5ed6f7cd-d9af-4439-9f33-fc935b883d91)  
  
  
