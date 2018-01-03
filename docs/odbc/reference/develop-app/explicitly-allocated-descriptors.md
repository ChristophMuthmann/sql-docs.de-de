---
title: Explizit reserviert Deskriptoren | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
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
ms.openlocfilehash: 791d7620afc4f952ccb99c80cad980ebd2e2e9ea
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="explicitly-allocated-descriptors"></a>Explizit zugewiesene Deskriptoren
Eine Anwendung kann explizit ein Anwendungsdiensts für eine Verbindung zu einem beliebigen Zeitpunkt zuweisen, die sie mit der Datenbank verbunden ist. Durch diese Deskriptorhandles angeben, wie ein Attribut einer Anweisung mit **SQLSetStmtAttr**, leitet die Anwendung den Treiber verwenden diese Deskriptor anstelle der entsprechenden Anwendung implizit zugeordnet Deskriptoren. Die Anwendung kann nicht mit anderen Implementierung Deskriptoren angeben.  
  
 Eine Anwendung kann mehr als eine Anweisung einen explizit zugewiesenen Deskriptor zuordnen. Nur, wenn eine Anwendung tatsächlich mit der Datenbank verbunden ist kann ein Deskriptor, der einen explizit zugewiesenen Deskriptor sein. Die Anwendung kann solche einen Deskriptor, der explizit oder implizit freizugeben, freigegeben werden und die Verbindung sein zu müssen.
