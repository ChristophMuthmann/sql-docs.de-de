---
title: '@@VERSION (Transact-SQL) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/20/2018
ms.prod: sql
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
- '@@VERSION'
- '@@VERSION_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@VERSION function'
- current SQL Server installation information
- versions [SQL Server], @@VERSION
- processors [SQL Server], types
ms.assetid: 385ba80e-7c28-41a5-9cdb-5648f3785983
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4ce5f4605a4b9e7cf3046af962bda4b5d590bd44
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="x40x40version---transact-sql-configuration-functions"></a>&#x40;&#x40;Version: Transact SQL-Konfigurationsfunktionen
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt System- und Buildinformationen für die aktuelle Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@VERSION  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **nvarchar**  
  
## <a name="remarks"></a>Remarks  
 Die @@VERSION-Ergebnisse werden als eine nvarchar-Zeichenfolge dargestellt. Sie können die [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)-Funktion verwenden, um die einzelnen Eigenschaftenwerte abzurufen.  
  
 Für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden die folgenden Informationen zurückgegeben.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Version  
  
-   Architektur des Prozessors  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Erstellungsdatum  
  
-   Urheberrechtserklärung  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Edition  
  
-   Betriebssystemversion  
  
 Für [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] werden die folgenden Informationen zurückgegeben.  
  
-   Edition – Microsoft SQL Azure  
  
-   Produktebene – RTM  
  
-   Produktversion  
  
-   Erstellungsdatum  
  
-   Urheberrechtserklärung  

> [!NOTE]  
> Derzeit ist ein Problem bekannt, durch das @@VERSION die falsche Produktversion für Azure SQL-Datenbank meldet. Die von Azure SQL-Datenbank ausgeführte Version der SQL Server-Datenbank-Engine ist im Gegensatz zur lokalen Version von SQL Server immer aktuell und enthält die neuesten Sicherheitspatches. Die Patchstufe entspricht also der lokalen Version von SQL Server oder ist aktueller als diese. Außerdem sind die neuesten SQL Server-Features in Azure SQL-Datenbank verfügbar.
>
> Um die Edition der Engine programmgesteuert zu ermitteln, können Sie die Anweisung SELECT SERVERPROPERTY('EngineEdition') verwenden. Diese Abfrage gibt für eigenständige Datenbanken „5“ und für verwaltete Instanzen in Azure SQL-Datenbank „8“ zurück. 
>
> Sobald dieses Problem behoben ist, wird die Dokumentation aktualisiert.

  
## <a name="examples"></a>Beispiele  
  
### <a name="a-return-the-current-version-of-includessnoversionincludesssnoversion-mdmd"></a>A: Rückgabe der aktuellen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Im folgenden Beispiel werden die Versionsinformationen für die aktuelle Installation zurückgegeben.  
  
```  
SELECT @@VERSION AS 'SQL Server Version';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="b-return-the-current-version-of-includessdwincludesssdw-mdmd"></a>B. Rückgabe der aktuellen Version von [!INCLUDE[ssDW](../../includes/ssdw-md.md)].  
  
```  
SELECT @@VERSION AS 'SQL Server PDW Version';  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)  
  
  

