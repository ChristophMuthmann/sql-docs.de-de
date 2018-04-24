---
title: ADO-Java-Klassenwrapper | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- class wrappers [ADO]
ms.assetid: 1fc09dc1-9e32-412e-9f43-b8eb8bb483ca
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b77807fbdf03dd729f504e4112d205fb6cf7d6d6
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="ado-java-class-wrappers"></a>ADO-Java-Klassen-Wrapper
Dieser Code deklariert eine Instanz von der ADO [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Klassenwrapper und initialisiert alle auf die gleiche Zeile des Codes. Darüber hinaus deklariert Variablen für die einzelnen Argumente in der [öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md) -Methode, insbesondere für [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) und [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) (da Java nicht unterstützen aufgelistet Typen). Der Code öffnet und schließt die **Recordset** Objekt. Plant, diese Variable freigegeben werden, wenn Java systematische und zeitweilig auftretende Veröffentlichung nicht verwendeter Objekte führt Rs1 lediglich auf NULL festlegen.  
  
```  
public static void main( String args[])  
{  
   msado15._Recordset   Rs1 = new msado15.Recordset();  
   Variant Source     = new Variant( "SELECT * FROM Authors" );  
   Variant Connect    = new Variant( "DSN=AdoDemo;UID=admin;PWD=;" );  
   int     LockType   = msado15.CursorTypeEnum.adOpenForwardOnly;  
   int     CursorType = msado15.LockTypeEnum.adLockReadOnly;  
   int     Options    = -1;  
  
   Rs1.Open( Source, Connect, LockType,  CursorType, Options );  
   Rs1.Close();  
   Rs1 = null;  
  
   System.out.println( "Success!\n" );  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Using the Microsoft SDK for Java (Verwenden des Microsoft SDK für Java)](../../../ado/guide/appendixes/using-the-microsoft-sdk-for-java.md)
