---
title: "Bestimmen, was unterstützt wird | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- editing data [ADO], Supports method
- Supports method [ADO]
ms.assetid: 65090cba-6d46-4775-8d61-f6838e7752a6
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2e15f52d48f5870cfe4df8cd6149d56012b42abf
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="determining-what-is-supported"></a>Bestimmen, was unterstützt wird
Die **unterstützt** Methode wird verwendet, um zu bestimmen, ob ein angegebenes **Recordset** Objekt unterstützt eine bestimmte Art von Funktionen. Es hat die folgende Syntax:  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="remarks"></a>Hinweise  
 Die **unterstützt** Methode gibt einen booleschen Wert, der angibt, ob der Anbieter alle Funktionen, die durch das Argument CursorOptions identifiziert unterstützt. Können Sie die **unterstützt** Methode, um zu bestimmen, welche Arten von Funktionen einer **Recordset** -Objekt unterstützt. Wenn die **Recordset** Objekt unterstützt die Funktionen, deren entsprechenden Konstanten in sind *CursorOptions*, **unterstützt** -Methode zurückkehrt **"true"**. Andernfalls wird zurückgegeben **"false"**.  
  
 Mithilfe der **unterstützt** -Methode, sehen Sie sich für die Fähigkeit eines der **Recordset** Objekt neue Datensätze hinzufügen, Lesezeichen verwenden, verwenden Sie die **suchen** verwenden unregelmäßiger Bildlauf-Methode verwenden, die  **Index** -Eigenschaft, und zum Durchführen von Batchaktualisierungen. Eine vollständige Liste von Konstanten und ihre Bedeutungen, finden Sie unter [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md).  
  
 Obwohl die **unterstützt** Methode gelegten **"true"** für eine bestimmte Funktionalität kann nicht garantiert, dass der Anbieter das Feature unter allen Umständen verfügbar machen kann. Die **unterstützt** Methode gibt einfach auftragsantwortnachrichten zurück, ob der Anbieter unterstützt den angegebenen Funktionen können unter bestimmten Bedingungen erfüllt sind. Z. B. die **unterstützt** Methode hinweisen, die eine **Recordset** Objekt unterstützt Updates, auch wenn der Cursor auf eine Verknüpfung aus mehreren Tabellen basiert – einige Spalten der sind nicht aktualisierbar.

