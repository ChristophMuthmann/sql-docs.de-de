---
title: ADO-Java-Klassenwrapper | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- class wrappers [ADO]
ms.assetid: 1fc09dc1-9e32-412e-9f43-b8eb8bb483ca
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 08cbd288ba9f64816ae0c8fd62c18171967c4d0d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
 [Mithilfe des Microsoft-SDK für Java](../../../ado/guide/appendixes/using-the-microsoft-sdk-for-java.md)

