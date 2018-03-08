---
title: Recordset-bezogene Fehlerinformationen | Microsoft Docs
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
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b1ad53c42fa3da686de10e3254c6fa7e3916d806
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="recordset-related-error-information"></a>Recordset-bezogene Fehlerinformationen
Während der Batchverarbeitung der **Status** Eigenschaft von der **Recordset** Objekt enthält Informationen zu den einzelnen Einträgen in der **Recordset**. Bevor ein Update mithilfe der Batchverarbeitung stattfindet, die **Status** Eigenschaft von der **Recordset** gibt Informationen zu Datensätzen hinzugefügt, geändert und gelöscht werden. Nach dem **UpdateBatch** aufgerufen wurde, die **Status** Eigenschaft gibt den Erfolg oder Misserfolg des Vorgangs an. Wie beim Verschieben von Datensatz zu Datensatz, der **Recordset**, den Wert von der **Status** eigenschaftsänderungen, um den Status des aktuellen Datensatzes zu beschreiben.
