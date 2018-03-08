---
title: Prepared-Eigenschaft (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
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
- Command15::Prepared
helpviewer_keywords:
- Prepared property [ADO]
ms.assetid: 11ca8825-765e-4bb4-a6ce-3f6564ad8755
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c5b45f14d0513dfda61688dc664affbf760c8598
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="prepared-property-ado"></a>Vorbereitete-Eigenschaft (ADO)
Gibt an, ob eine kompilierte Version des Speichern einer [Befehl](../../../ado/reference/ado-api/command-object-ado.md) vor der Ausführung.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **booleschen** -Wert, wenn auf festgelegt **"true"**, gibt an, dass der Befehl vorbereitet werden soll.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **Prepared** Eigenschaft so, dass den Anbieter eine vorbereitete (oder kompilierte) Version der Abfrage im angegebenen speichern die [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) Eigenschaft, bevor ein [Befehl](../../../ado/reference/ado-api/command-object-ado.md) des Objekts erste Ausführung. Verlangsamung dieser ersten Ausführung des Befehls, aber nachdem der Anbieter einen Befehl kompiliert wird, verwendet des Anbieters die kompilierte Version des Befehls für alle nachfolgenden Ausführungen, die verbesserte Leistung führt.  
  
 Wenn die Eigenschaft **"false"**, führt der Anbieter die **Befehl** Objekt direkt, ohne eine kompilierte Version erstellen.  
  
 Wenn der Anbieter die befehlsvorbereitung nicht unterstützt, kann es einen Fehler zurück, wenn diese Eigenschaft, um festgelegt wird **"true"**. Wenn der Anbieter keine Fehler zurückgegeben wird, ignoriert er einfach die Anforderung zum Vorbereiten der Befehl und legt die **Prepared** Eigenschaft **"false"**.  
  
## <a name="applies-to"></a>Gilt für  
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiel für vorbereitete-Eigenschaft (VB)](../../../ado/reference/ado-api/prepared-property-example-vb.md)   
 [Prepared-Eigenschaft – Beispiel (VC++)](../../../ado/reference/ado-api/prepared-property-example-vc.md)   
