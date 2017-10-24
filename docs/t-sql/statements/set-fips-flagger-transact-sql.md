---
title: SET FIPS_FLAGGER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4c28fd5419aec8bf15745150288b6878fd65ac1f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-fipsflagger-transact-sql"></a>SET FIPS_FLAGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt an, dass die Kompatibilität mit dem FIPS 127-2-Standard überprüft wird. Diese basiert auf dem ISO-Standard. Weitere Informationen zur SQL Server-FIPS-Kompatibilität finden Sie unter [zum Verwenden von SQL Server 2016 im FIPS 140-2-kompatiblen Modus](https://support.microsoft.com/help/4014354/how-to-use-sql-server-2016-in-fips-140-2-compliant-mode). 
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SET FIPS_FLAGGER ( 'level' |  OFF )  
```  
  
## <a name="arguments"></a>Argumente  
 **"** *Ebene* **"**  
 Der Grad der Kompatibilität mit dem FIPS 127-2-Standard, auf den alle Datenbankoperationen überprüft werden. Wenn ein Datenbankvorgang mit der Stufe des ISO-Standards ausgewählt ist, steht in Konflikt [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird eine Warnung generiert.  
  
 *Ebene* muss eines der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|ENTRY|Überprüfen der Kompatibilität mit der Eingangsstufe (Entry level) des ISO-Standards.|  
|FULL|Überprüfen der vollständigen Kompatibilität mit dem ISO-Standard.|  
|INTERMEDIATE|Überprüfen der Kompatibilität mit der INTERMEDIATE-Stufe des ISO-Standards.|  
|OFF|Kein Überprüfen des Standards.|  
  
## <a name="remarks"></a>Hinweise  
 Die Einstellung der `SET FIPS_FLAGGER` festlegen zur Analysezeit und nicht zum Ausführen oder zur Laufzeit ist. Festlegen zur Analysezeit bedeutet, dass wenn die SET-Anweisung des Batches oder gespeicherte Prozedur vorhanden ist, er wirksam wird, unabhängig davon, ob die codeausführung tatsächlich diesen Punkt erreicht; und die `SET` -Anweisung wird wirksam, bevor Anweisungen ausgeführt werden. Angenommen, selbst wenn die `SET` -Anweisung liegt im ein `IF...ELSE` Anweisungsblock, die während der Ausführung niemals erreicht wird der `SET` Anweisung ist weiterhin wirksam, da die `IF...ELSE` -Anweisungsblock analysiert wird.  
  
 Wenn `SET FIPS_FLAGGER` festgelegt ist, in einer gespeicherten Prozedur, die den Wert des `SET FIPS_FLAGGER` wird wiederhergestellt, nachdem die gespeicherte Prozedur die Steuerung zurückgegeben wird. Aus diesem Grund eine `SET FIPS_FLAGGER` angegebene in dynamischem SQL-Anweisung hat keinen Einfluss auf die Anweisungen, dynamische SQL-Anweisung.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="see-also"></a>Siehe auch  
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

