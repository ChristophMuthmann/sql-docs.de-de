---
title: Deskriptorhandles | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- application parameter descriptor [ODBC]
- automatically allocated descriptors [ODBC]
- implementation row descriptor [ODBC]
- descriptor handles [ODBC]
- handles [ODBC], descriptor
- implementation parameter descriptor [ODBC]
- apd [ODBC]
- ard [ODBC]
- explicitly allocated descriptors [ODBC]
- ipd [ODBC]
- ird [ODBC]
- application row descriptor [ODBC]
ms.assetid: 7741035c-f3e7-4c89-901e-fe528392f67d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 791a28ece56894c8bbe9167c8e2445da32c3e07b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="descriptor-handles"></a>Deskriptorhandles
Ein *Deskriptor* ist eine Auflistung von Metadaten, die den Parametern einer SQL-Anweisung oder die Spalten eines Resultsets beschreibt, von der Anwendung oder Treiber (auch bekannt als die *Implementierung*). Ein Deskriptor kann daher einer der vier Rollen ausfüllen:  
  
-   **Anwendungsparameterdeskriptor (APD).** Enthält Informationen über die Anwendungspuffer, der an die Parameter in einer SQL­Anweisung, wie ihre Adressen, die Länge und die C-Datentypen gebunden.  
  
-   **Implementation Parameter Descriptor (Implementierungsparameterdeskriptor, Implementierungszeilendeskriptor).** Enthält Informationen zu den Parametern in einer SQL­Anweisung, wie ihre SQL-Datentypen, Länge und NULL-Zulässigkeit.  
  
-   **Zeile Anwendungsdiensts (ARD).** Enthält Informationen über die Anwendungspuffer, die an die Spalten in einem Resultset, z. B. ihre Adressen, die Länge und die C-Datentypen gebunden.  
  
-   **Implementierungszeilendeskriptor (IRD).** Enthält Informationen zu den Spalten in einem Resultset, z. B. ihre SQL-Datentypen, Länge und NULL-Zulässigkeit.  
  
 Vier Deskriptoren (legt jede Rolle einem) werden automatisch zugeordnet, wenn eine Anweisung zugeordnet ist. Diese werden als bezeichnet *automatisch zugeordnet Deskriptoren* immer diese Anweisung zugeordnet sind. Anwendungen können auch Deskriptoren mit zuordnen **SQLAllocHandle**. Diese werden als bezeichnet *explizit reserviert Deskriptoren*. Sie werden auf eine Verbindung zugeordnet und können eine oder mehrere Anweisungen für die Verbindung zum Erfüllen der Rolle eines APD oder ARD auf diese Anweisungen zugeordnet werden.  
  
 Die meisten Vorgänge in ODBC können ohne ausdrückliche Verwendung von Deskriptoren von der Anwendung ausgeführt werden. Deskriptoren bieten jedoch eine zweckmäßig für bestimmte Vorgänge an. Nehmen Sie z. B. an, dass eine Anwendung wünscht Einfügen von Daten aus zwei verschiedenen Sätzen von Puffern. Um den ersten Satz von Puffern zu verwenden, würde es wiederholt aufrufen **SQLBindParameter** an die Parameter in binden ein **einfügen** Anweisung und führen Sie die Anweisung. Um den zweiten Satz von Puffern zu verwenden, würden sie diesen Vorgang wiederholen. Alternativ konnte er Bindungen zu den ersten Satz von Puffern in einen Deskriptor und zum zweiten Satz von Puffern in einer anderen Deskriptor einrichten. Zum Wechseln zwischen den Sätzen von Bindungen, die Anwendung einfach aufrufen würde **SQLSetStmtAttr** und die Anweisung als APD richtig Deskriptors zugeordnet.  
  
 Weitere Informationen zu Deskriptoren, finden Sie unter [Typen von Deskriptoren](../../../odbc/reference/develop-app/types-of-descriptors.md).
