---
title: Unicode-Treiber | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode [ODBC], drivers
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: 3b4742d5-74fb-4aff-aa21-d83a0064d73d
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e73a559545a870d83e3d8e2e94dd20f6731f72eb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="unicode-drivers"></a>Unicode-Treiber
Ob ein Treiber, einen Unicode-Treiber oder eine ANSI-Treiber sein soll hängt ausschließlich die Art der Datenquelle. Wenn die Datenquelle Unicode-Daten unterstützt, muss der Treiber einen Unicode-Treiber. Wenn die Datenquelle nur ANSI-Daten unterstützt, sollte der Treiber eine ANSI-Treiber bleiben.  
  
 Ein Unicode-Treiber muss exportieren **SQLConnectW** als Unicode-Treiber vom Treiber-Manager erkannt werden.  
  
 Ein Unicode-Treiber muss Unicode-Funktionen akzeptieren (mit dem Suffix *W*) und Unicode-Daten zu speichern. ANSI-Funktionen können auch übernehmen, aber ist nicht erforderlich. (Der Treiber-Manager übergibt keinen ANSI-Funktionsaufruf mit den *ein* suffix auf den Treiber, sondern konvertiert es in ein ANSI-Funktionsaufruf ohne das Suffix und übergibt dann diese an den Treiber.)  
  
 Ein Unicode-Treiber muss Resultsets in Unicode oder ANSI, abhängig von der Anwendung Bindung zurückgeben können. Wenn eine Anwendung SQL_C_CHAR gebunden werden soll, muss der Unicode-Treiber SQL_WCHAR-Daten in SQL_CHAR konvertieren. Der Treiber-Manager wird zuordnen SQL_C_WCHAR SQL_C_CHAR für ANSI-Treiber, jedoch wird keine Zuordnung für Unicode-Treiber.  
  
> [!NOTE]  
>  Wenn den Treibertyp ermittelt wurde, wird der Treiber-Manager aufrufen **SQLSetConnectAttr** und legen Sie das Attribut SQL_ATTR_ANSI_APP beim Herstellen der Verbindung. Wenn die Anwendung die ANSI-APIs verwendet wird, wird SQL_ATTR_ANSI_APP auf SQL_AA_TRUE festgelegt werden, und wenn Unicode verwendet wird, wird er auf einen Wert von SQL_AA_FALSE festgelegt sein. Dieses Attribut wird verwendet, damit der Treiber anderes Verhalten basierend auf den Anwendungstyp aufweisen kann. Das Attribut kann nicht direkt von der Anwendung festgelegt werden, und es wird nicht von **SQLGetConnectAttr**. Wenn ein Treiber für ANSI- und Unicode-Anwendungen das gleiche Verhalten aufweist, sollte er SQL_ERROR für dieses Attribut zurück. Wenn der Treiber gibt SQL_SUCCESS zurück, wird der Treiber-Manager ANSI- und Unicode-Verbindungen trennen, wenn Verbindungspooling verwendet wird.
