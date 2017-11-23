---
title: "Gespeicherte Prozedur Parametereinschränkungen | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 8b804bcf-4cce-4e6f-aa45-00bab9ef9921
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0adaba03f6de2e0dc8ae91fa2035b81ed50b2618
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="stored-procedure-parameter-limitations"></a>Gespeicherte Prozedur Parametereinschränkungen
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Bei der Ausführung von Oracle gespeicherte Prozeduren, die 10 nutzen oder mehr Ausgabeparameter, schlägt der gespeicherte Prozeduraufruf eine Zugriffsverletzung oder ActiveX Data Objects (ADO) Fehlermeldung fehl. Dies kann auftreten, wenn der Microsoft ODBC-Treiber für Oracle mit Versionen 8.0.4.0.0 und 8.0.4.0.4 der Oracle-Clientsoftware.  
  
 Um das Problem zu beheben, muss die Oracle-Clientsoftware ein Upgrade auf Version 8.0.4.2.0 oder höher sein. Wenden Sie sich an Oracle Corporation Weitere Informationen zu den [Patches](../../odbc/microsoft/oracle-software-patches.md).  
  
> [!NOTE]  
>  Dieses Problem tritt nicht mit der frühen Version des Oracle-Clientsoftwareversion 8.0.3.0.0.
