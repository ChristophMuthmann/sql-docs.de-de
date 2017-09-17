---
title: SQLGetTypeInfo (Excel-Treiber) | Microsoft Docs
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
- SQLGetTypeInfo function [ODBC], Excel Driver
- Excel driver [ODBC], SQLGetTypeInfo
ms.assetid: 708845be-e6a1-4677-8113-c52819a43fa4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cbcc75d7a527104ced19727797e282b63af2a6ae
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgettypeinfo-excel-driver"></a>SQLGetTypeInfo (Excel-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Excel-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Der Name des Typs (TYPE_NAME) zurückgegeben, in der Tabelle von erzeugten **SQLGetTypeInfo** wird der Name, der am häufigsten von der Datenquelle verwendet werden.  
  
 SQL_ALL_EXCEPT_LIKE wird in der DURCHSUCHBAREN Spalte für das Byte, Leistungsindikator, Double, Single, lange und kurze Datentypen zurückgegeben werden. (Die LIKE-Funktion kann erreicht werden, durch Konvertieren des Werts in ein Zeichen an, indem die ODBC-kanonische Konvertierungsfunktionen, klicken Sie dann der Vergleich ausgeführt.)  
  
 Wenn der Microsoft Excel-Treiber verwendet wird, werden die ODBC-Typnamen in der TYPE_NAME-Spalte, die von zurückgegeben wird zurückgegeben **SQLGetTypeInfo**.
