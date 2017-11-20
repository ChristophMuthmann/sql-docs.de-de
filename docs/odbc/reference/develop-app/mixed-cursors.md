---
title: Gemischte Cursor | Microsoft Docs
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
- mixed cursors [ODBC]
- cursors [ODBC], dynamic
- keyset-driven cursors [ODBC]
- dynamic cursors [ODBC]
- cursors [ODBC], key-set driven
- cursors [ODBC], mixed
ms.assetid: 9beb2db9-0b6d-491d-9529-d64e64e59014
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 16369d96931bd2b01d644756ab7e1e22fd325a85
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="mixed-cursors"></a>Gemischte Cursor
Ein gemischter Cursor ist eine Kombination eines keysetgesteuerten Cursors und einen dynamischen Cursor. Es wird verwendet, wenn das Resultset zu groß für den Schlüssel für das gesamte Resultset vernünftigerweise speichern ist. Gemischten Cursor werden eine Keyset, die kleiner als das gesamte Resultset jedoch größer als das Rowset ist erstellen implementiert.  
  
 Solange die Anwendung innerhalb des Keysets scrollt, ist das Verhalten keysetgesteuerte. Wenn die Anwendung außerhalb der Keyset ein Bildlauf durchgeführt, ist das Verhalten dynamisch: der Cursor die angeforderten Zeilen und erstellt eine neue Keyset. Nachdem das neue Keyset erstellt wurde, wird das Verhalten in keysetgesteuerte innerhalb dieser Keyset wiederhergestellt.  
  
 Nehmen wir beispielsweise an einem Resultset 1.000 Zeilen hat und verwendet einen gemischten Cursor ein Keysetgröße von 100 mit einer Rowsetgröße von 10. Wenn das erste Rowset abgerufen wird, erstellt den Cursor eine Keyset, die die Schlüssel für die ersten 100 Zeilen besteht. Anschließend wird die ersten 10 Zeilen zurückgegeben, wie angefordert.  
  
 Nehmen wir jetzt an eine andere Anwendung löscht Zeilen 11 und 101. Wenn der Cursor versucht, die Zeile 11 abgerufen werden, wird es eine Lücke auftreten, weil er verfügt über einen Schlüssel für diese Zeile aber keine Zeile vorhanden ist; Dieses ist Verhalten keysetgesteuerte. Wenn der Cursor versucht, die Zeile 101 abgerufen werden, erkennt der Cursor nicht, dass die Zeile nicht vorhanden ist, da sie nicht über einen Schlüssel für die Zeile verfügt. Stattdessen werden sie abgerufen, welche Zeile 102 zuvor. Dies trifft dynamic-Cursor.  
  
 Ein gemischte Cursor entspricht eines keysetgesteuerten Cursors wird die Keysetgröße gleich der Größe des Resultsets. Ein gemischte Cursor entspricht in einen dynamischen Cursor, wenn die Keysetgröße gleich 1 ist.

