---
title: "Herstellen einer Verbindung mit einer Datenquelle (ODBC-Treiber für Oracle) | Microsoft Docs"
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
- connecting to data source [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connecting to data sources
ms.assetid: f724a9c5-342a-4f4e-a030-ec34f7378eaf
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a2b087ef77a00947c4e270861fffd27108389839
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>Herstellen einer Verbindung mit einer Datenquelle (ODBC-Treiber für Oracle)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Eine ODBC-Anwendung kann die Verbindungsinformationen auf vielfältige Weise übergeben. Die Anwendung kann z. B. den Treiber den Benutzer zur Verbindung immer eine Aufforderung aufweisen. Oder die Anwendung erwarten wahrscheinlich eine Verbindungszeichenfolge, die Verbindung mit der Datenquelle angibt. Wie Sie eine Verbindung mit einer Datenquelle herstellen, hängt die Verbindungsmethode, die von der ODBC-Anwendung verwendet.  
  
 Eine allgemeine Methode für die Verbindung mit einer Datenquelle wird über das Dialogfeld "Datenquelle". Wenn die ODBC-Anwendung so eingerichtet ist, verwenden Sie ein Dialogfeld, das Dialogfeld angezeigt, und Sie werden aufgefordert, die entsprechenden Datenquellen-Verbindungsinformationen.  
  
 Sie können auch mit einer Datenquelle mit Verbinden der [Verbindungszeichenfolge](../../odbc/microsoft/connection-string-format-and-attributes.md).  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>Für die Verbindung mit einer Datenquelle mithilfe des Dialogfelds  
  
1.  Wenn das Dialogfeld Datenquelle angezeigt wird, wählen Sie eine Oracle-Datenquelle, und klicken Sie dann auf OK. Das Dialogfeld Verbinden wird angezeigt.  
  
2.  Füllen Sie die entsprechenden Informationen für die Verbindung herstellen (Dialogfeld), und klicken Sie dann auf OK.  
  
 Nachdem die Verbindung Informationen bestätigt wurde, Ihre Anwendung den ODBC-Treiber für Oracle verwenden können, auf die Informationen zugreifen, die die Datenquelle enthält.
