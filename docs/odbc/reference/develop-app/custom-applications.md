---
title: Benutzerdefinierte Anwendungen | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 634c0988707b52e5517dcc90e006a5513eb90d97
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="custom-applications"></a>Benutzerdefinierte Anwendungen
Benutzerdefinierte Anwendungen werden in der Regel eine bestimmte Aufgabe für einige DBMS ausführen. Z. B. eine Anwendung möglicherweise Abrufen von Daten aus einer einzelnen DBMS und einen Bericht generieren, oder es kann Daten zwischen mehreren DBMS übertragen. Was diese Anwendungen gemeinsam haben darin, dass diese DBMS bekannt sind, bevor die Anwendung geschrieben werden i. d. r. während der Lebensdauer der Anwendung ändern.  
  
 Die benutzerdefinierte Anwendung erfordert daher nur wenig oder keine Interoperabilität. Der Anwendungsentwickler kann einen einzelnen Treiber für jedes DBMS und den Code direkt für Treiber auswählen. Die Anwendung treiberspezifische Code aus, um die Funktionen der Treiber nutzen kann problemlos enthalten und möglicherweise auch Aufrufe an die systemeigenen Datenbank-API nicht von ODBC unterstützten Funktionen zu verwenden.  
  
 Die wichtigsten Interoperabilität die meisten benutzerdefinierter Anwendungen Rolle spielt, ob das Ziel-DBMS in der Zukunft ändern. Wenn dies der Fall ist, kann dieser Prozess vereinfacht werden, indem interoperablere Code zu schreiben. Allerdings wird eine solche Änderung des DBMS ist selten und im Allgemeinen umfasst eine große Menge an Arbeit. Wählen Sie aus diesem Grund Entwickler benutzerdefinierter Anwendungen selten Interoperabilität zu Lasten der Funktionalität erhöhen; in der Regel möchten sie diese Funktion bei einer Änderung eines DBMS umgeschrieben werden müssen.
