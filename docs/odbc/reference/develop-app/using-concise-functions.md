---
title: Präzise Funktionen mit | Microsoft Docs
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
- concise functions [ODBC]
- functions [ODBC], concise functions
- descriptors [ODBC], concise functions
ms.assetid: 31ac070f-8c59-4fd5-bd5a-466bb27dbca0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c53a628eaaa3ca8348ce8917ace36da35c33f653
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-concise-functions"></a>Verwenden präzise Funktionen
Einige ODBC-Funktionen zu impliziten Zugriff auf Deskriptoren erhalten. Anwendungsentwickler können finden sie einfacher als Aufruf **SQLSetDescField** oder **SQLGetDescField**. Diese Funktionen aufgerufen werden *präzise* funktioniert, da sie eine Reihe von Funktionen, einschließlich festlegen oder Abrufen von deskriptorfelder ausführen. Einige präzisen Funktionen können eine Anwendung festgelegt oder abgerufen werden mehrere verwandte Descriptor-Felder in einem einzelnen Funktionsaufruf.  
  
 Präzise Funktionen können aufgerufen werden, ohne zuerst eine Deskriptorhandles für die Verwendung als Argument abrufen. Diese Funktionen funktionieren mit der deskriptorfelder das Anweisungshandle zugeordnet, denen auf dem sie aufgerufen werden.  
  
 Die präzisen Funktionen **SQLBindCol** und **SQLBindParameter** Binden einer Spalte oder eines Parameters durch Festlegen der deskriptorfelder, die entsprechen, ihre Argumente. Jede dieser Funktionen führt mehr Aufgaben als das Festlegen der Deskriptoren. **SQLBindCol** und **SQLBindParameter** bieten eine vollständige Spezifikation der Bindung einer Datenspalte oder den dynamischen Parameter. Eine Anwendung kann jedoch die einzelnen Details einer Bindung ändern, indem Aufrufen **SQLSetDescField** oder **SQLSetDescRec** und können vollständig binden Sie eine Spalte oder Parameter machen eine Reihe von geeignete Aufrufe an Diese Funktionen.  
  
 Die präzisen Funktionen **SQLColAttribute**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLNumParams**, und  **SQLNumResultCols** Werte in deskriptorfelder abrufen.  
  
 **SQLSetDescRec** und **SQLGetDescRec** sind präzise Funktionen, die mit einem Aufruf festlegen oder Abrufen von mehreren deskriptorfelder, die den Datentyp und die Speicherung von Daten für Spalte oder Parameter beeinflussen. **SQLSetDescRec** ist eine effektive Möglichkeit für die Bindung der Spalte oder Parameter-Daten in einem Schritt zu ändern.  
  
 **SQLSetStmtAttr** und **SQLGetStmtAttr** dienen als präziser Funktionen in einigen Fällen. (Siehe [Deskriptorfelder](../../../odbc/reference/develop-app/descriptor-fields.md).)
