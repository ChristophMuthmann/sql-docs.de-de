---
title: EINDEUTIGE SET-Befehls | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SET UNIQUE command [ODBC]
ms.assetid: 1f69e31e-4599-47cc-ac89-b86fba8703c5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bed7fb14102c754d16409259fe7e1f5177652d05
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="set-unique-command"></a>EINDEUTIGE SET-Befehl
Gibt an, ob Datensätze mit doppelte Indexschlüsselwerte werden in eine Indexdatei verwaltet.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>Argumente  
 ON  
 Gibt an, dass ein Datensatz mit einem doppelten Schlüssel Indexwert nicht in der Indexdatei aufgenommen werden. Die Indexdatei ist nur der erste Datensatz mit der ursprünglichen Indexschlüsselwert Teil.  
  
 OFF  
 (Standard). Gibt an, dass die Indexdatei Datensätze mit doppelten Indexschlüsselwerten berücksichtigt werden.  
  
## <a name="remarks"></a>Hinweise  
 Eine Indexdatei behält seine eindeutige festgelegt Einstellung beim REINDEX ausgeben. Weitere Informationen finden Sie unter [INDEX](../../odbc/microsoft/index-command.md).

