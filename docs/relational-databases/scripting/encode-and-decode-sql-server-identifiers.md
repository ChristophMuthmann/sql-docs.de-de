---
title: Codierung und Decodierung von SQL Server-Bezeichnern | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bb9fe0d3-e432-42d3-b324-64dc908b544a
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9e5499ddf0c36d277068cb222a5c438c720a4c3a
ms.lasthandoff: 04/11/2017

---
# <a name="encode-and-decode-sql-server-identifiers"></a>Codierung und Decodierung von SQL Server-Bezeichnern
  Begrenzungsbezeichner von SQL Server können Zeichen enthalten, die in Windows PowerShell-Pfaden nicht unterstützt werden. Diese Zeichen können angegeben werden, indem ihre Hexadezimalwerte codiert werden.  
  
1.  **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions)  
  
2.  **To process special characters:**  [Encoding an Identifier](#EncodeIdent), [Decoding an Identifier](#DecodeIdent)  
  
## <a name="before-you-begin"></a>Vorbereitungen  
 Zeichen, die nicht in Windows PowerShell-Pfadnamen unterstützt werden, können als "%"-Zeichen gefolgt vom Hexadezimalwert des Bitmusters, das das Zeichen darstellt, dargestellt oder codiert werden (Beispiel:**%**xx). Codierung kann immer zur Verarbeitung von Zeichen verwendet werden, die in Windows PowerShell-Pfaden nicht unterstützt werden.  
  
 Das Cmdlet **Encode-SqlName** verwendet als Eingabe einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Bezeichner. Es gibt eine Zeichenfolge mit allen nicht von der Windows PowerShell-Sprache unterstützten Zeichen, die mit "%xx" codiert sind, aus. Das Cmdlet **Decode-SqlName** verwendet einen codierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Bezeichner als Eingabe und gibt den ursprünglichen Bezeichner zurück.  
  
###  <a name="LimitationsRestrictions"></a> Einschränkungen  
 Die Cmdlets **Encode-Sqlname** und **Decode-Sqlname** codieren oder decodieren nur die Zeichen, die in SQL Server-Begrenzungsbezeichnern zulässig sind, aber in PowerShell-Pfaden nicht unterstützt werden. Dies sind die Zeichen, die von **Encode-SqlName** codiert und von **Decode-SqlName**decodiert werden:  
  
|||||||||||||  
|-|-|-|-|-|-|-|-|-|-|-|-|  
|**Zeichen**|\|/|decodiert werden:|%|\<|>|*|?|[|]|&#124;|  
|**Hexadezimale Codierung**|%5C|%2F|%3A|%25|%3C|%3E|%2A|%3F|%5B|%5D|%7C|  
  
##  <a name="EncodeIdent"></a> Codieren eines Bezeichners  
 **So codieren Sie einen SQL Server-Bezeichner in einem PowerShell-Pfad**  
  
-   Codieren Sie mithilfe einer der folgenden beiden Methoden einen SQL Server-Bezeichner:  
  
    -   Geben Sie den Hexadezimalcode für das nicht unterstützte Zeichen an, indem Sie die Syntax % XX verwenden, wobei XX der Hexadezimalcode ist.  
  
    -   Übergeben Sie den Bezeichner als Zeichenfolge in Anführungszeichen an das Cmdlet **Encode-Sqlname** .  
  
### <a name="examples-encoding"></a>Beispiele (Codierung)  
 In diesem Beispiel wird die codierte Version des Zeichens ":" (%3A) dargestellt:  
  
```  
Set-Location Table%3ATest  
```  
  
 Alternativ können Sie **Encode-SqlName** verwenden, um einen von Windows PowerShell unterstützten Namen zu erstellen:  
  
```  
Set-Location (Encode-SqlName "Table:Test")  
```  
  
##  <a name="DecodeIdent"></a> Decodieren eines Bezeichners  
 **So decodieren Sie einen SQL Server-Bezeichner aus einem PowerShell-Pfad**  
  
 Verwenden Sie das Cmdlet **Decode-Sqlname** , um die Hexadezimalcodierungen durch die von der Codierung dargestellten Zeichen zu ersetzen.  
  
### <a name="examples-decoding"></a>Beispiele (Decodierung)  
 Dieses Beispiel gibt “Table:Test” zurück:  
  
```  
Decode-SqlName "Table%3ATest"  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Bezeichnern in PowerShell](../../relational-databases/scripting/sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell-Anbieter](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [SQL Server-PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
