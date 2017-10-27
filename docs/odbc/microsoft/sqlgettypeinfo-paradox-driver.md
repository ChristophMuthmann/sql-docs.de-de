---
title: SQLGetTypeInfo (Paradox-Treiber) | Microsoft Docs
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
- SQLGetTypeInfo function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLGetTypeInfo
ms.assetid: e65063c7-ba9e-4cf0-ac13-4bb5bd2937db
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1c95d4c4519b420324e9ec1364d2ac9f352ba346
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgettypeinfo-paradox-driver"></a>SQLGetTypeInfo (Paradox-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Paradox treiberspezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Der Name des Typs (TYPE_NAME) zurückgegeben, in der Tabelle von erzeugten **SQLGetTypeInfo** wird der Name, der am häufigsten von der Datenquelle verwendet werden.  
  
 SQL_ALL_EXCEPT_LIKE wird in der DURCHSUCHBAREN Spalte für das Byte, Leistungsindikator, Double, Single, lange und kurze Datentypen zurückgegeben werden. (Die LIKE-Funktion kann durch Konvertieren des Werts in ein Zeichen mit der kanonischen ODBC-Konvertierungsfunktionen erzielt werden und anschließend Ausführen des Vergleichs.)

