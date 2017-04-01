---
title: "TRIM (SSIS-Ausdruck) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Führende Leerzeichen"
  - "TRIM-Funktion"
  - "Nachfolgende Leerzeichen"
ms.assetid: 7dd9081d-a3d4-483a-bf7e-bf2bd7692d39
caps.latest.revision: 34
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 34
---
# TRIM (SSIS-Ausdruck)
  Gibt einen Zeichenausdruck zurück, nachdem führende und nachfolgende Leerzeichen entfernt wurden.  
  
> [!NOTE]  
>  Mit TRIM werden keine Leerzeichen entfernt, wie z. B. Tabulatoren oder Zeilenvorschubzeichen. Unicode stellt Codeelemente für viele verschiedene Arten von Leerzeichen bereit, diese Funktion erkennt jedoch nur das Unicode-Codeelement 0x0020. DBCS-Zeichenfolgen, die in Unicode konvertiert werden, enthalten u. U. andere Leerzeichen als 0x0020. Diese Leerzeichen können von der Funktion nicht entfernt werden. Zum Entfernen aller Arten von Leerzeichen können Sie die Trim-Methode von Microsoft Visual Basic .NET in einem Skript verwenden, das aus der Skriptkomponente ausgeführt wird.  
  
## Syntax  
  
```  
  
TRIM(character_expression)  
```  
  
## Argumente  
 *character_expression*  
 Ein Zeichenausdruck, aus dem Leerzeichen entfernt werden sollen.  
  
## Ergebnistypen  
 DT_WSTR  
  
## Hinweise  
 TRIM gibt ein NULL-Ergebnis zurück, wenn das Element NULL ist.  
  
 TRIM kann nur mit dem DT_WSTR-Datentyp verwendet werden. Ein *character_expression*-Argument, das ein Zeichenfolgenliteral oder eine Datenspalte mit dem DT_STR-Datentyp ist, wird implizit in den DT_WSTR-Datentyp umgewandelt, bevor TRIM ausgeführt wird. Andere Datentypen müssen explizit in den DT_WSTR-Datentyp umgewandelt werden. Weitere Informationen finden Sie unter [Integration Services-Datentypen](../../integration-services/data-flow/integration-services-data-types.md) und [CAST &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
## Beispiele für Ausdrücke  
 In diesem Beispiel werden führende und nachfolgende Leerzeichen aus einem Zeichenfolgenliteral entfernt. Als Ergebnis wird "New York" zurückgegeben.  
  
```  
TRIM("   New York   ")  
```  
  
 In diesem Beispiel werden führende und nachfolgende Leerzeichen aus dem Ergebnis der Verkettung der Spalten **FirstName** und **LastName** entfernt. Die leere Zeichenfolge zwischen **FirstName** und **LastName** wird nicht entfernt.  
  
```  
TRIM(FirstName + " "+ LastName)  
```  
  
## Siehe auch  
 [LTRIM &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/ltrim-ssis-expression.md)   
 [RTRIM &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/rtrim-ssis-expression.md)   
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  