---
title: Beschreibt Parameter | Microsoft Docs
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
- SQLBindParameter function [ODBC], describing parameters
ms.assetid: 118d0f47-2afd-4955-bb47-38b1e2c2f38f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f746b7df2ac3ef4de73e54c6d78df02e0c64ec34
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="describing-parameters"></a>Beschreibt die Parameter
**SQLBindParameter** enthält Argumente, die den Parameter zu beschreiben: die SQL-Datentyp, Genauigkeit und Dezimalstellen. Der Treiber verwendet diese Informationen oder *Metadaten* umzuwandelnde Wert des Parameters in den Typ, der von der Datenquelle benötigt. Auf den ersten Blick scheint es sich, dass der Treiber in einfacher als die Anwendung Parametermetadaten kennen ist; Nachdem alle kann der Treiber mühelos ermitteln, die Metadaten für ein-Spalte Resultset. Es stellt sich heraus, ist dies nicht der Fall. Zuerst die meisten Datenquellen bieten eine Möglichkeit für den Treiber zum Ermitteln von Parametermetadaten keine. Zweitens stellt die meisten Anwendungen bereits kennen, die Metadaten.  
  
 Wenn eine SQL-Anweisung in der Anwendung hartcodiert ist, weiß der Autor der Anwendung bereits den Typ jedes Parameters. Wenn eine SQL-Anweisung, die von der Anwendung zur Laufzeit erstellt wird, kann die Anwendung die Metadaten bestimmen, wie sie die Anweisung erstellt. Beispielsweise, wenn die Anwendung die-Klausel erstellt  
  
```  
WHERE OrderID = ?  
```  
  
 Er kann Aufrufen **SQLColumns** für das OrderID-Spalte.  
  
 Die einzige Situation, in der die Anwendung einfach die Parametermetadaten ermitteln kann, ist, wenn der Benutzer eine parametrisierte Anweisung gibt. In diesem Fall die Anwendung aufruft, **SQLPrepare** , die Anweisung vorzubereiten **SQLNumParams** bestimmt die Anzahl der Parameter, und **SQLDescribeParam** beschreiben Jeder Parameter. Wie bereits erwähnt wurde, die meisten Datenquellen keine bieten jedoch eine Möglichkeit für den Treiber Parametermetadaten, sodass ermitteln **SQLDescribeParam** wird nicht unterstützt.
