---
title: SQUARE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SQUARE
- SQUARE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SQUARE
- square values
ms.assetid: 007b6b12-da86-4229-8f5c-fdd4fa839f5f
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e73ef776e4318b0957838f95bb78601c3de55840
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="square-transact-sql"></a>SQUARE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Gibt das Quadrat des angegebenen float-Werts zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SQUARE ( float_expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *float_expression*  
 Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) des Typs **"float"** oder eines Typs, der implizit in Float konvertiert werden kann.  
  
## <a name="return-types"></a>Rückgabetypen  
 **float**  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird das Volumen eines Zylinders mit einem Radius von `1` Zoll und der Höhe von `5` Zoll zurückgegeben.  
  
```  
DECLARE @h float, @r float;  
SET @h = 5;  
SET @r = 1;  
SELECT PI()* SQUARE(@r)* @h AS 'Cyl Vol';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Cyl Vol  
--------------------------  
15.707963267948966  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Das folgende Beispiel gibt das Quadrat jedes Werts in der `volume` Spalte in der `containers` Tabelle.  
  
```  
-- Uses AdventureWorks  
  
CREATE TABLE Containers (  
    ID int NOT NULL,  
    Name varchar(20),  
    Volume float(24));  
  
INSERT INTO Containers VALUES (1, 'Cylinder', '125.22');  
INSERT INTO Containers VALUES (2, 'Cube', '23.98');  
  
SELECT Name, SQUARE(Volume) AS VolSquared   
FROM Containers;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Name           VolSquared`  
  
 `-------------  ----------`  
  
 `Cylinder       15680.05`  
  
 `Cube             575.04`  
  
## <a name="see-also"></a>Siehe auch  
 [Mathematische Funktionen &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  


