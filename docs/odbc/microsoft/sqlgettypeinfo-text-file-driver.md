---
title: SQLGetTypeInfo (Text-Datei-Treiber) | Microsoft Docs
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
- SQLGetTypeInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetTypeInfo
ms.assetid: 05a58975-093c-4bd9-bd72-b5f0026a6e36
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4b84e9e826eb2ad3104f00d9d39224fb2da6303
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgettypeinfo-text-file-driver"></a>SQLGetTypeInfo (Text-Datei-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Textdatei treiberspezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Der Name des Typs (TYPE_NAME) zurückgegeben, in der Tabelle von erzeugten **SQLGetTypeInfo** wird der Name, der am häufigsten von der Datenquelle verwendet werden.  
  
 SQL_ALL_EXCEPT_LIKE wird in der DURCHSUCHBAREN Spalte für das Byte, Leistungsindikator, Double, Single, lange und kurze Datentypen zurückgegeben werden. (Die LIKE-Funktion kann erreicht werden, durch Konvertieren des Werts in ein Zeichen an, indem die ODBC-kanonische Konvertierungsfunktionen, klicken Sie dann der Vergleich ausgeführt.)  
  
 Wenn der Text-Treiber verwendet wird, **SQLGetTypeInfo** gibt CASE_SENSITIVE Wert "false" für den Text-Datentypen (CHAR und LONGCHAR), wenn die Datentypen tatsächlich sind Groß-/Kleinschreibung beachtet.
