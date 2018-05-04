---
title: Recordset-bezogene Fehlerinformationen | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2dab1996d2915757ba6e7834b5e41bd6eade41c6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="recordset-related-error-information"></a>Recordset-bezogene Fehlerinformationen
Während der Batchverarbeitung der **Status** Eigenschaft von der **Recordset** Objekt enthält Informationen zu den einzelnen Einträgen in der **Recordset**. Bevor ein Update mithilfe der Batchverarbeitung stattfindet, die **Status** Eigenschaft von der **Recordset** gibt Informationen zu Datensätzen hinzugefügt, geändert und gelöscht werden. Nach dem **UpdateBatch** aufgerufen wurde, die **Status** Eigenschaft gibt den Erfolg oder Misserfolg des Vorgangs an. Wie beim Verschieben von Datensatz zu Datensatz, der **Recordset**, den Wert von der **Status** eigenschaftsänderungen, um den Status des aktuellen Datensatzes zu beschreiben.
