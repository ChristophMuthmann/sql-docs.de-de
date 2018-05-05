---
title: Serialisierbarkeit | Microsoft Docs
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
- transaction isolation [ODBC]
- transactions [ODBC], serialization
- serialization [ODBC]
- transactions [ODBC], isolation
ms.assetid: 142e4ac0-2977-4a2b-96ae-c9e5bd2c448a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6e912ec51bc0b7c77d73aae1b473dee9242b3f4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="serializability"></a>Serialisierbarkeit
Im Idealfall sollte Transaktionen *serialisierbar*. Transaktionen werden als serialisierbar, wenn die Ergebnisse der gleichzeitig ausgeführte Transaktionen sind identisch mit die Ergebnisse seriell ressourcenaufwändig – d. h. eine nach dem anderen. Es ist nicht wichtig, welche Transaktion führt zunächst nur, die das Ergebnis jeder Mischen von Transaktionen nicht wiedergibt.  
  
 Nehmen wir beispielsweise an die Transaktion A Datenwerte mit 2 multipliziert und Transaktion B Datenwerte 1 hinzugefügt. Nehmen wir jetzt an, dass zwei Datenwerte vorhanden sind: 0 und 10. Wenn diese Transaktionen nacheinander ausgeführt werden, werden die neuen Werte 1 und 21, wenn Transaktion A zuerst ausgeführt wird, oder 2 und 22 sein, wenn Transaktion B zuerst ausgeführt wird. Aber was geschieht, wenn die Reihenfolge, in der die beiden Transaktionen ausgeführt werden, für jeden Wert unterscheidet? Wenn die Transaktion ist ein auf dem ersten Wert zuerst ausgeführt wird und die Transaktion B zuerst auf dem zweiten Wert ausgeführt werden, werden die neuen Werte 1 und 22. Wenn diese Reihenfolge umgekehrt wird, werden die neuen Werte 2 und 21. Transaktionen sind serialisierbar, wenn 1, 21 und 2 sind 22 die einzig mögliche Ergebnisse. Die Transaktionen sind, ist nicht serialisierbar, wenn 1, 22 oder 2, 21 ein mögliches Ergebnis.  
  
 Warum ist Serialisierbarkeit wünschenswert? Das heißt, warum es wichtig ist, dass es, eine Transaktion angezeigt wird beendet wird, bevor die nächste Transaktion startet? Nehmen Sie das folgende Problem. Ein Vertriebsmitarbeiter ist Aufträge zur selben Zeit eingeben, die eine Clerk out Wechsel gesendet werden. Nehmen Sie an der Handlungsreisenden gibt eine Bestellung von Unternehmen X jedoch keinen commit; der Vertriebsmitarbeiter kommuniziert von Unternehmen X weiterhin für die Vertriebsmitarbeiter. Die clerkgröße fordert eine Liste mit allen offenen Bestellungen und ermittelt die Reihenfolge für Unternehmen X und sendet sie eine Rechnung. Nachdem die Vertreter des Unternehmens X entscheidet sich, dass die Reihenfolge zu ändern, damit die Handlungsreisenden war schon immer vor dem Commit der Transaktion geändert werden soll. Unternehmen X Ruft eine falsche Rechnung ab.  
  
 Wären die des Handlungsreisenden und des Sachbearbeiters Transaktionen serialisierbar, würde dieses Problem nie stattgefunden haben. Der Vertriebsmitarbeiter Transaktion würde abgeschlossen haben, bevor der Clerk Transaktionsbeginn in diesem Fall die Clerk haben, die richtige Abrechnung gesendet würde oder den Clerk Transaktion würde abgeschlossen haben, bevor die Handlungsreisenden Transaktion begonnen, in diesem Fall hat die Clerk würde keine Rechnung an Unternehmen X überhaupt gesendet haben.
