---
title: Dialect-Eigenschaft | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Command::Dialect
helpviewer_keywords:
- Dialect property
ms.assetid: 329c3a71-ba88-4009-b04f-2f52195a5957
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 73c7dfd6fe5aec706d5e27ce6d55f489285748c4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="dialect-property"></a>Dialect-Eigenschaft
Der Dialekt der gibt an, die [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) oder [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) Eigenschaften. Der Dialekt definiert die Syntax und die allgemeinen Regeln, die der Anbieter verwendet, um die Zeichenfolge oder den Stream zu analysieren.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Die **Dialekt** Eigenschaft enthält eine gültige GUID, die den Dialekt der Befehlstext oder Stream darstellt. Der Standardwert für diese Eigenschaft ist {C8B521FB-5CF3-11CE-ADE5-00AA0044773D}, was bedeutet, dass der Anbieter wählen soll, die Befehlstext oder den Stream zu interpretieren.  
  
## <a name="remarks"></a>Hinweise  
 ADO werden den Anbieter keine abgefragt, wenn der Benutzer den Wert dieser Eigenschaft liest; Es gibt eine Zeichenfolgendarstellung des Werts, der derzeit im gespeicherten der [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt.  
  
 Wenn der Benutzer legt die **Dialekt** ADO-Eigenschaft überprüft die GUID und löst einen Fehler aus, wenn der angegebene Wert kein gültiger GUID ist. Finden Sie in der Dokumentation für den Anbieter zur Bestimmung der GUID-Werte, die von unterstützt die **Dialekt** Eigenschaft.  
  
## <a name="applies-to"></a>Gilt für  
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Execute-Methode (ADO-Befehl)](../../../ado/reference/ado-api/execute-method-ado-command.md)

