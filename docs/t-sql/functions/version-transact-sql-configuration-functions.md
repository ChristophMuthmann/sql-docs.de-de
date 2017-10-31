---
title: '@@VERSION (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: c9fc3634abc5ca23c96f46adf2a52881ee15c40c
ms.contentlocale: de-de
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40version---transact-sql-configuration-functions"></a>& #x 40; & #x 40; Version - Transact-SQL-Konfigurationsfunktionen
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt System- und Buildinformationen für die aktuelle Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@VERSION  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **nvarchar**  
  
## <a name="remarks"></a>Hinweise  
 Der @@VERSION Ergebnisse als eine Nvarchar-Zeichenfolge dargestellt werden. Sie können die [SERVERPROPERTY &#40; Transact-SQL &#41; ](../../t-sql/functions/serverproperty-transact-sql.md) Funktion, um die einzelnen Eigenschaftenwerte abzurufen.  
  
 Für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden die folgenden Informationen zurückgegeben.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Version  
  
-   Architektur des Prozessors  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Erstellungsdatum  
  
-   Urheberrechtserklärung  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Edition  
  
-   Betriebssystemversion  
  
 Für [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] werden die folgenden Informationen zurückgegeben.  
  
-   Edition: Windows Azure SQL-Datenbank  
  
-   Produktebene:  "(CTP)" oder "(RTM)"  
  
-   Produktversion  
  
-   Erstellungsdatum  
  
-   Urheberrechtserklärung  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-return-the-current-version-of-includessnoversionincludesssnoversion-mdmd"></a>A: Zurückgeben der aktuellen Version von[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Im folgenden Beispiel werden die Versionsinformationen für die aktuelle Installation zurückgegeben.  
  
```  
SELECT @@VERSION AS 'SQL Server Version';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-return-the-current-version-of-includessdwincludesssdw-mdmd"></a>B. Zurückgeben der aktuellen Version von[!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
  
```  
SELECT @@VERSION AS 'SQL Server PDW Version';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)  
  
  


