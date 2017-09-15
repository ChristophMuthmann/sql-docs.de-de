---
title: "Offsets für die parameterbindung | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- offsets of parameters [ODBC]
- binding offsets of parameters [ODBC]
ms.assetid: 309339e9-9ccd-4a58-8aa4-b6dc88f4eb7c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5b3fea1397710c5a65a03b3f829972f04cc63f5a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="parameter-binding-offsets"></a>Parameterbindung Offsets
Einer Anwendung angegeben werden, dass ein Offset hinzugefügt wird, gebunden Parameter Puffer Adressen und den entsprechenden Längenindikator Puffer Adressen Wenn **SQLExecDirect** oder **SQLExecute** aufgerufen wird. Das Ergebnis dieser Ergänzungen bestimmt die Adressen, die bei diesen Vorgängen verwendet.  
  
 BIND-Offsets, damit eine Anwendung so ändern Sie die Bindungen ohne Aufruf **SQLBindParameter** für zuvor gebundene Parameter. Ein Aufruf von **SQLBindParameter** ändert einen Parameter erneut binden, Pufferadresse und den Längenindikator/Zeiger. Das erneute Binden mit einem Versatz addiert andererseits, einfach einen Offset zum die vorhandenen gebundene Parameter Pufferadresse und Längenindikator/Pufferadresse. Wenn Offsets verwendet werden, die Bindungen sind "Template" des wie die Anwendungspuffer angelegt werden, und die Anwendung kann auf unterschiedliche Bereiche des Arbeitsspeichers dieser "Vorlage" verschieben, durch Ändern des Offsets. Ein neuer Offset kann zu einem beliebigen Zeitpunkt angegeben werden und wird immer auf die ursprünglich gebundenen Werte hinzugefügt.  
  
 Zum Angeben eines Bindung Offsets legt die Anwendung das Anweisungsattribut SQL_ATTR_PARAM_BIND_OFFSET_PTR an die Adresse des eine SQLINTEGER-Puffers fest. Bevor die Anwendung eine Funktion, die die Bindungen verwendet aufruft, wird einen Offset in Bytes, die in diesem Puffer solange Pufferadresse Parameter weder Pufferadresse Längenindikator / 0 beträgt und der gebundene Parameter in der SQL-Anweisung ist. Die Summe der Adresse und den Offset muss eine gültige Adresse sein. (Dies bedeutet, dass eine oder beide der Offset und die Adresse, die der Offset hinzugefügt wird, ungültig ist, werden können, solange die Summe eine gültige Adresse ist.)  
  
> [!NOTE]  
>  Bindung Offsets werden vom ODBC-2 nicht unterstützt. *x* Treiber.
