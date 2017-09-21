---
title: "Blockieren von Cursorn, scrollfähige Cursor und Abwärtskompatibilität | Microsoft Docs"
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
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: d9d271f6-d2d9-49b9-a365-4909ca06caae
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 72c256f326366d631dada13fbfe002c8d4674eda
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>Blockcursor, scrollfähige Cursor und Abwärtskompatibilität
Das Vorhandensein beider **SQLFetchScroll** und **SQLExtendedFetch** stellt den ersten Clear Teilen in ODBC zwischen der API Application Programming Interface (), die den Satz von Funktionen ist die Ruft Anwendung und der Service Provider-Schnittstelle (SPI), also den Satz von Funktionen der Treiber implementiert. Diese Teilung ist erforderlich, damit ODBC 3. *x*, welche verwendet **SQLFetchScroll**, Bealigned mit den Standards und auch mit ODBC-2 kompatibel sein.* X*, welche verwendet **SQLExtendedFetch**.  
  
 Die ODBC 3*.x* -API, die ist der Satz von Funktionen die Anwendung ruft, umfasst **SQLFetchScroll** und verwandte Anweisungsattribute. Die ODBC 3*.x* SPI, also den Satz von Funktionen der Treiber implementiert wird, umfasst **SQLFetchScroll**, **SQLExtendedFetch**, und verwandte Anweisungsattribute. Da ODBC Teilung zwischen der API und der SPI nicht formal erzwingt, ist es möglich, ODBC 3*.x* aufrufen, **SQLExtendedFetch** und verwandte Anweisungsattribute. Es besteht jedoch kein Grund für ODBC 3*.x* Anwendung dazu. Weitere Informationen über APIs und SPIs Siehe die Einführung zu [ODBC-Architektur](../../../odbc/reference/odbc-architecture.md).  
  
 Informationen darüber, welche Funktionen und die Anweisung Attribute einer ODBC-3. *x* Anwendung sollte mit Blocks und bildlauffähigen Cursor verwenden, finden Sie unter [Blockcursor, scrollfähige Cursor und Abwärtskompatibilität für ODBC 3.x-Anwendungen](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Was bewirkt, dass der Treiber-Manager](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [Was bewirkt, dass der Treiber](../../../odbc/reference/appendixes/what-the-driver-does.md)
