---
title: Gespeicherte Prozedur Parametereinschränkungen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 8b804bcf-4cce-4e6f-aa45-00bab9ef9921
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34f3bc435a0bbd514eed4f9ce6100a9cca6b6cb7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="stored-procedure-parameter-limitations"></a>Gespeicherte Prozedur Parametereinschränkungen
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Bei der Ausführung von Oracle gespeicherte Prozeduren, die 10 nutzen oder mehr Ausgabeparameter, schlägt der gespeicherte Prozeduraufruf eine Zugriffsverletzung oder ActiveX Data Objects (ADO) Fehlermeldung fehl. Dies kann auftreten, wenn der Microsoft ODBC-Treiber für Oracle mit Versionen 8.0.4.0.0 und 8.0.4.0.4 der Oracle-Clientsoftware.  
  
 Um das Problem zu beheben, muss die Oracle-Clientsoftware ein Upgrade auf Version 8.0.4.2.0 oder höher sein. Wenden Sie sich an Oracle Corporation Weitere Informationen zu den [Patches](../../odbc/microsoft/oracle-software-patches.md).  
  
> [!NOTE]  
>  Dieses Problem tritt nicht mit der frühen Version des Oracle-Clientsoftwareversion 8.0.3.0.0.
