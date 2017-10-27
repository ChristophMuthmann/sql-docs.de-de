---
title: Der Benutzer aufgefordert, Verbindungsinformationen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connecting to data source [ODBC], SqlConnect
- connecting to driver [ODBC], prompting user for information
- connecting to driver [ODBC], SQLConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLConnect function [ODBC], prompting user for connection information
- connecting to data source [ODBC], prompting user for information
- prompting user for connection information [ODBC]
- SQLDriverConnect function [ODBC], prompting user for connection information
ms.assetid: da98e9b9-a4ac-4a9d-bae6-e9252b1fe1e5
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3b1ee296ea292be7287c2cd4a8e93c9e33cb04bb
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="prompting-the-user-for-connection-information"></a>Der Benutzer aufgefordert, Verbindungsinformationen
Wenn die Anwendung verwendet **SQLConnect** und muss den Benutzer für alle Verbindungsinformationen aufzufordern wie Benutzername und Kennwort muss geschieht dies selbst. Obwohl dadurch die Anwendung die Steuerung des "Erscheinungsbilds" kann die Anwendung, die Treiber-spezifischen Code enthalten Internet Explorer erzwungen. Dies tritt auf, wenn die Anwendung den Benutzer zur treiberspezifische Verbindungsinformationen aufzufordern muss. Dies stellt eine unmöglich Situation für allgemeiner Anwendungen, die darauf ausgelegt sind, funktionieren alle Treiber, einschließlich der Treiber, die nicht vorhanden sind, wenn die Anwendung geschrieben wird.  
  
 **SQLDriverConnect** können zur auffordern Verbindungsinformationen. Z. B. die folgende Verbindungszeichenfolge, um das benutzerdefinierte Programm zuvor erwähnten übergeben **SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 Der Treiber kann dann ein Dialogfeld anzuzeigen, die Benutzer-IDs und Kennwörtern, ähnlich der folgenden Abbildung abfragt.  
  
 ![(Dialogfeld), die Benutzer-IDs und Kennwörtern abfragt](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 Dass der Treiber Verbindungsinformationen auffordern kann ist besonders nützlich, um generische und vertikale Anwendungen. Diese Anwendungen dürfen nicht treiberspezifische Informationen und dass der Treiber-Eingabeaufforderung für die benötigten Informationen hält diese Informationen nicht in der Anwendung. Dies wird von den vorherigen zwei Beispielen gezeigt. Wenn die Anwendung nur der Name der Datenquelle an den Treiber übergeben, wird die Anwendung enthielt nicht treiberspezifische Informationen und wurde daher nicht an einen bestimmten Treiber gebunden. Wenn die Anwendung eine vollständige Verbindungszeichenfolge für den Treiber übergeben wird, wurde es an den Treiber gebunden, die die Zeichenfolge interpretieren kann.  
  
 Eine allgemeine Anwendung möglicherweise nehmen einen Schritt weiter und auch nicht auf eine Datenquelle angeben. Wenn **SQLDriverConnect** empfängt einer leere Verbindungszeichenfolge der Treiber-Manager zeigt das Dialogfeld.  
  
 ![Wählen Sie im Dialogfeld der Datenquelle](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 Nachdem der Benutzer eine Datenquelle ausgewählt hat, wird der Treiber-Manager eine Verbindungszeichenfolge angeben, die Datenquelle erstellt und übergibt sie an den Treiber. Der Treiber kann dann die Benutzer für zusätzliche Informationen auffordern benötigten.  
  
 Die Bedingungen, unter dem der Treiber wird der Benutzer aufgefordert, die von gesteuert werden die *DriverCompletion* flag; es gibt Optionen, um immer eine Aufforderung, fordert bei Bedarf oder nie aufgefordert. Eine vollständige Beschreibung dieses Flags, finden Sie unter der [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) funktionsbeschreibung.

