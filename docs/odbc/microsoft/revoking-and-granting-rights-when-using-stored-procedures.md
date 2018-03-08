---
title: Aufheben und die Rechte erteilt, bei Verwendung von gespeicherten Prozeduren | Microsoft Docs
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
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 24070039-03ab-4623-a681-6308802eb399
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8b2a34667e08e767a77f31917f5c373b795c7324
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>Entziehen und Erteilen von Berechtigungen beim Verwenden gespeicherter Prozeduren
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Der Microsoft ODBC-Treiber für Oracle gibt die folgende Fehlermeldung zurück, wenn Benutzerrechte erteilt und klicken Sie dann auf eine Tabelle, die von einer gespeicherten Prozedur zugegriffen gesperrt sind:  
  
 SQL_ERROR =-1  
  
 von SQLDiagRec() = "Falsche Anzahl von Parametern [Microsoft] [ODBC-Treiber für Oracle]"  
  
 von SQLDiagRec() = "[Microsoft] [ODBC-Treiber für Oracle] Syntaxfehler oder zugriffsverletzung"  
  
 Der Aufruf an die Oracle OCI-Funktion Odessp() in diesem Szenario schlägt fehl, jedoch ist erforderlich, um die Standardparameter zu implementieren. Nachdem die zugrunde liegende Tabellenberechtigungen geändert werden, muss die gespeicherte Prozedur neu kompiliert werden, bevor er erneut ausführen.
