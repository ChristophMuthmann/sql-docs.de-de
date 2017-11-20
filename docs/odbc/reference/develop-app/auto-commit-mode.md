---
title: Autocommit-Modus | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rolling back transactions [ODBC]
- auto-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: c8de5b60-d147-492d-b601-2eeae8511d00
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb9b6d354657578f7188481a2e7ff7566f725c80
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="auto-commit-mode"></a>Autocommit-Modus
*Im Autocommit-Modus* jeder Datenbankvorgang ist eine Transaktion, die ein Commit ausgeführt wird, wenn ausgeführt. Dieser Modus eignet sich für viele reale Transaktionen, die aus einer einzelnen SQL­Anweisung bestehen. Es ist nicht erforderlich ist, trennen oder Abschluss dieser Transaktionen angeben. Bei Datenbanken ohne Unterstützung von Transaktionen ist Autocommit-Modus der einzige unterstützte Modus. In solchen Datenbanken sind Anweisungen ein Commit ausgeführt, wenn sie ausgeführt werden, und es keine Möglichkeit gibt, diese zurückzusetzen; Sie sind daher immer im Autocommit Modus.  
  
 Wenn das zugrunde liegende DBMS Autocommit-Modus Transaktionen nicht unterstützt, kann der Treiber emulieren sie durch jede SQL-Anweisung manuell zu übernehmen, während der Ausführung.  
  
 Wenn ein Batch von SQL-Anweisungen im Autocommit Modus ausgeführt wird, ist sie Daten datenquellenspezifischen, wenn die Anweisungen im Batch ein Commit ausgeführt werden. Sie können ein Commit ausgeführt werden während der Ausführung oder als Ganzes, nachdem der gesamte Batch ausgeführt wurde. Einige Datenquellen unterstützen möglicherweise diese beiden und möglicherweise eine Möglichkeit, einen oder anderen auszuwählen. Insbesondere wenn ein Fehler in der Mitte der Batch auftritt, ist es Daten datenquellenspezifischen, ob die bereits ausgeführten Anweisungen sind ein Commit oder Rollback. Daher sollte interoperable Anwendungen ausführen können, die erforderlich ist, damit ein Commit oder Rollback als Ganzes und Verwenden von Batches, Batches nur im Manualcommit-Modus ausführen.

