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
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- explicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: f590251d-56a6-4d58-a405-9e85e68fbc47
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7a4679fa6c6d2185f6e474407882080fea6b7c8a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="explicitly-allocated-descriptors"></a>Explizit zugewiesene Deskriptoren
Eine Anwendung kann explizit ein Anwendungsdiensts für eine Verbindung zu einem beliebigen Zeitpunkt zuweisen, die sie mit der Datenbank verbunden ist. Durch diese Deskriptorhandles angeben, wie ein Attribut einer Anweisung mit **SQLSetStmtAttr**, leitet die Anwendung den Treiber verwenden diese Deskriptor anstelle der entsprechenden Anwendung implizit zugeordnet Deskriptoren. Die Anwendung kann nicht mit anderen Implementierung Deskriptoren angeben.  
  
 Eine Anwendung kann mehr als eine Anweisung einen explizit zugewiesenen Deskriptor zuordnen. Nur, wenn eine Anwendung tatsächlich mit der Datenbank verbunden ist kann ein Deskriptor, der einen explizit zugewiesenen Deskriptor sein. Die Anwendung kann solche einen Deskriptor, der explizit oder implizit freizugeben, freigegeben werden und die Verbindung sein zu müssen.

