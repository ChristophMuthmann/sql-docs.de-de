---
title: Recordset-bezogene Fehlerinformationen | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 279fcc0564f433234cbac730465e2af06a7eb5e7
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="recordset-related-error-information"></a>Recordset-bezogene Fehlerinformationen
Während der Batchverarbeitung der **Status** Eigenschaft von der **Recordset** Objekt enthält Informationen zu den einzelnen Einträgen in der **Recordset**. Bevor ein Update mithilfe der Batchverarbeitung stattfindet, die **Status** Eigenschaft von der **Recordset** gibt Informationen zu Datensätzen hinzugefügt, geändert und gelöscht werden. Nach dem **UpdateBatch** aufgerufen wurde, die **Status** Eigenschaft gibt den Erfolg oder Misserfolg des Vorgangs an. Wie beim Verschieben von Datensatz zu Datensatz, der **Recordset**, den Wert von der **Status** eigenschaftsänderungen, um den Status des aktuellen Datensatzes zu beschreiben.

