---
title: Abrufen von Deskriptor behandelt | Microsoft Docs
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
helpviewer_keywords: descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d94b21ff4583682e7013321b3e871aee04ce6da1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="obtaining-descriptor-handles"></a>Behandelt Deskriptor abrufen
Ruft eine Anwendung als ausgabeargument des Aufrufs an das Handle für alle explizit reservierte Deskriptor ab **SQLAllocHandle**. Das Handle für eine implizit zugeordnete Sicherheitsbeschreibung wird abgerufen, indem Aufrufen **SQLGetStmtAttr**.
