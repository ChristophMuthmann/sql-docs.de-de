---
title: Explizit reserviert Deskriptoren | Microsoft Docs
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
- descriptors [ODBC], allocating and freeing
- explicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: f590251d-56a6-4d58-a405-9e85e68fbc47
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a2e3c3f2941597ed0b4ffedeccc060690110d1c3
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="explicitly-allocated-descriptors"></a>Explizit zugewiesene Deskriptoren
Eine Anwendung kann explizit ein Anwendungsdiensts für eine Verbindung zu einem beliebigen Zeitpunkt zuweisen, die sie mit der Datenbank verbunden ist. Durch diese Deskriptorhandles angeben, wie ein Attribut einer Anweisung mit **SQLSetStmtAttr**, leitet die Anwendung den Treiber verwenden diese Deskriptor anstelle der entsprechenden Anwendung implizit zugeordnet Deskriptoren. Die Anwendung kann nicht mit anderen Implementierung Deskriptoren angeben.  
  
 Eine Anwendung kann mehr als eine Anweisung einen explizit zugewiesenen Deskriptor zuordnen. Nur, wenn eine Anwendung tatsächlich mit der Datenbank verbunden ist kann ein Deskriptor, der einen explizit zugewiesenen Deskriptor sein. Die Anwendung kann solche einen Deskriptor, der explizit oder implizit freizugeben, freigegeben werden und die Verbindung sein zu müssen.
