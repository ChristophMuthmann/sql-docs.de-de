---
title: SQLGetTypeInfo (Paradox-Treiber) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLGetTypeInfo
ms.assetid: e65063c7-ba9e-4cf0-ac13-4bb5bd2937db
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5908d86bd7c42aeb92340a825df0f62e2cb233af
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgettypeinfo-paradox-driver"></a>SQLGetTypeInfo (Paradox-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Paradox treiberspezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Der Name des Typs (TYPE_NAME) zurückgegeben, in der Tabelle von erzeugten **SQLGetTypeInfo** wird der Name, der am häufigsten von der Datenquelle verwendet werden.  
  
 SQL_ALL_EXCEPT_LIKE wird in der DURCHSUCHBAREN Spalte für das Byte, Leistungsindikator, Double, Single, lange und kurze Datentypen zurückgegeben werden. (Die LIKE-Funktion kann durch Konvertieren des Werts in ein Zeichen mit der kanonischen ODBC-Konvertierungsfunktionen erzielt werden und anschließend Ausführen des Vergleichs.)
