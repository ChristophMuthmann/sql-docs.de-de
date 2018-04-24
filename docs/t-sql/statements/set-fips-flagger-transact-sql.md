---
title: SET FIPS_FLAGGER (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/29/2017
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
- FIPS_FLAGGER
- SET_FIPS_FLAGGER_TSQL
- FIPS_FLAGGER_TSQL
- SET FIPS_FLAGGER
dev_langs:
- TSQL
helpviewer_keywords:
- SET FIPS_FLAGGER statement
- FIPS 127-2 standard
- FIPS_FLAGGER option
ms.assetid: e82f6bee-6cf6-4061-be22-9ad2e8e9d3d6
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8fd983e15d7dba5d0811433e81809c7941bc379a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="set-fipsflagger-transact-sql"></a>SET FIPS_FLAGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt an, dass die Kompatibilität mit dem FIPS 127-2-Standard überprüft wird. Diese basiert auf dem ISO-Standard. Informationen zur FIPS-Konformität mit SQL Server finden Sie unter [How to use SQL Server 2016 in FIPS 140-2-compliant mode (Verwendung von SQL Server 2016 in einem mit FIPS 140-2 konformen Modus)](https://support.microsoft.com/help/4014354/how-to-use-sql-server-2016-in-fips-140-2-compliant-mode). 
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SET FIPS_FLAGGER ( 'level' |  OFF )  
```  
  
## <a name="arguments"></a>Argumente  
 **'** *level* **'**  
 Der Grad der Kompatibilität mit dem FIPS 127-2-Standard, auf den alle Datenbankoperationen überprüft werden. Wenn bei einem Datenbankvorgang ein Konflikt mit der gewählten Stufe des ISO-Standards auftritt, generiert [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Warnung.  
  
 *level* muss einer der folgenden Werte sein.  
  
|value|Description|  
|-----------|-----------------|  
|ENTRY|Überprüfen der Kompatibilität mit der Eingangsstufe (Entry level) des ISO-Standards.|  
|FULL|Überprüfen der vollständigen Kompatibilität mit dem ISO-Standard.|  
|INTERMEDIATE|Überprüfen der Kompatibilität mit der INTERMEDIATE-Stufe des ISO-Standards.|  
|OFF|Kein Überprüfen des Standards.|  
  
## <a name="remarks"></a>Remarks  
 Die Einstellung von `SET FIPS_FLAGGER` wird zur Analysezeit und nicht zur Ausführungs- oder Laufzeit festgelegt. Das Festlegen zur Analysezeit bedeutet Folgendes: Wenn sich die SET-Anweisung im Batch oder in der gespeicherten Prozedur befindet, wird sie unabhängig davon wirksam, ob die Codeausführung tatsächlich diesen Punkt erreicht, und die `SET`-Anweisung wird wirksam, bevor Anweisungen ausgeführt werden. Auch wenn sich die `SET`-Anweisung z.B. in einem `IF...ELSE`-Anweisungsblock befindet, der während der Ausführung niemals erreicht wird, ist die `SET`-Anweisung dennoch wirksam, da der `IF...ELSE`-Anweisungsblock analysiert wird.  
  
 Wird `SET FIPS_FLAGGER` in einer gespeicherten Prozedur festgelegt, so wird der Wert von `SET FIPS_FLAGGER` wiederhergestellt, nachdem die gespeicherte Prozedur die Steuerung zurückgegeben hat. Daher hat eine `SET FIPS_FLAGGER`-Anweisung, die in einer dynamischem SQL-Anweisung angegeben wird, keine Auswirkung auf die Anweisungen, die der dynamischen SQL-Anweisung folgen.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
