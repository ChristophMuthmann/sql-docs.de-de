---
title: WOBEI Klausel Einschränkungen | Microsoft Docs
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
- ODBC SQL grammar, WHERE clause limitations
- WHERE clause limitations [ODBC]
ms.assetid: 46b54f74-e4a3-4318-87cf-8a97c38a2718
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1a9b9485004b46cd6563835e880f801d36dc0eb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="where-clause-limitations"></a>WOBEI Klausel Einschränkungen
Die maximale Anzahl der Klauseln in einer WHERE-Klausel ist 40.  
  
 "LONGVARBINARY" und LONGVARCHAR Spalten verglichen werden können, um Literale von bis zu 255 Zeichen lang, aber Sie können nicht mit Parametern verglichen werden.
