---
title: ADO-Fehlercodes | Microsoft Docs
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
- errors [ADO], error codes
ms.assetid: 3aee61c7-a9b7-4596-b78e-5828a00d0281
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 55b434f3106e8c4847aeabcec90694bd9d89a7c6
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="capture-ado-error-codes"></a>Erfassen von ADO-Fehlercodes
Zusätzlich zu den anbieterfehlern zurückgegeben, die der [Fehler](../../../ado/reference/ado-api/error-object.md) Objekte von der [Fehler](../../../ado/reference/ado-api/errors-collection-ado.md) Auflistung ADO selbst kann zurückgeben, Fehler dem Mechanismus für die Ausnahmebehandlung der Laufzeit-Umgebung. Verwenden Sie den Fehler abfangen von Mechanismus Ihre Programmiersprache, z. B. die **On Error** in Microsoft® Visual Basic-Anweisung oder der **Try-Catch-** -block in Microsoft Visual C++®, ADO-Fehler zu erfassen.

 Die Liste der ADO-Fehlercodes finden Sie [ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md).

## <a name="see-also"></a>Siehe auch
 [Error-Objekt](../../../ado/reference/ado-api/error-object.md) [Errors-Auflistung (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)
