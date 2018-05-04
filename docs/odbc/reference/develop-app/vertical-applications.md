---
title: Vertikale Anwendungen | Microsoft Docs
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
- interoperability [ODBC], vertical applications
- vertical applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: d50ea3e6-7a9e-4fb6-8cd8-1d429d2f7b3c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f71f960043a843c2aad5f7e3a7eb5cc997b0a6ed
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="vertical-applications"></a>Vertikale Anwendungen
Vertikale Anwendungen führen in der Regel eine klar definierte Aufgabe für eine einzelnes DBMS. Beispielsweise wird in eine Anwendung die Bestellungen in einem Unternehmen nachverfolgt. Was diese Anwendungstypen Gemeinsamkeit aufweisen, darin, dass das Datenbankschema in der Regel vom Anwendungsentwickler entwickelt wurde und die Anwendung mit einer Reihe von verschiedenen DBMS funktioniert, zwar möglicherweise generische Vergleich mit einer einzelnen DBMS für einen einzelnen Kunden funktioniert.  
  
 Da vertikale Anwendungen in der Regel auf bestimmte Funktionen, z. B. bildlauffähige Cursor oder Transaktionen, erfordern unterstützen sie nur selten allen DBMS. Stattdessen sind eher sie sehr interoperabel zwischen einer begrenzten Anzahl von DBMS. Wählen in der Regel vertikale Anwendungsentwickler diese DBMS unterstützt, die auf einen großen Teil der Zugang zum Markt darstellen und ignoriert den Rest. Sie empfiehlt sich auch bestimmte Treiber für die entsprechenden DBMS, um ihre Tests zu reduzieren und Produkt Supportkosten zu unterstützen.  
  
 Da vertikale Anwendungen einen bekannten Satz von DBMS unterstützen, enthalten sie manchmal treiberspezifische oder DBMS-spezifischen Code. Solcher Code ist jedoch am besten auf ein Minimum reduziert, da hierfür zusätzliche Zeit zum Warten erforderlich ist.
