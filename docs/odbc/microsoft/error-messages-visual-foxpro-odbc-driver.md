---
title: Fehlermeldungen (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
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
- error messages [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], error messages
- SQLSTATE [ODBC]
- FoxPro ODBC driver [ODBC], error messages
ms.assetid: 58ea9734-4edf-44da-ba80-938aa7b340e4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e561aab3359acb1f236aea38e76da33289e630ef
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>Fehlermeldungen (Visual FoxPro-ODBC-Treiber)
Wenn ein Fehler auftritt, gibt der Visual FoxPro-Treiber die folgende Informationen an:  
  
-   Die systemeigene Fehlernummer und der Text der Fehlermeldung  
  
-   Der SQLSTATE (ODBC-Fehlercode) und der Text der Fehlermeldung  
  
 Sie Zugriff auf diese Fehlerinformationen durch Aufrufen von [SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md).  
  
## <a name="native-errors"></a>Systemeigene Fehler  
 Für Fehler, die in der Datenquelle auftreten, gibt der Visual FoxPro-Treiber die systemeigene Fehlernummer und der Text der Fehlermeldung. Eine Liste mit systemeigenen Fehlernummern finden Sie [Visual FoxPro-ODBC-Treiber systemeigene Fehlermeldungen](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md).  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (ODBC-Fehlercodes)  
 Für Fehler, die erkannt und der Visual FoxPro-Treiber zurückgegebene, ordnet der Treiber die zurückgegebene systemeigene Fehlernummer dem entsprechenden SQLSTATE zu. Wenn eine systemeigene Fehlernummer keine ODBC-Fehlercode zum zuweisen, gibt der Visual FoxPro-Treiber SQLSTATE S1000 (Allgemeine Fehler).  
  
 Eine Liste der SQLSTATE-Werten, die von der Visual FoxPro-ODBC-Treiber für den entsprechenden Visual FoxPro-Fehler generiert, finden Sie unter [ODBC-Fehlercodes](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md).  
  
## <a name="syntax"></a>Syntax  
 Fehlermeldungen haben das folgende Format:  
  
 **[** *Hersteller* **] [** *ODBC_component* **]** *Error_message*  
  
 Die Präfixe in Klammern ([]) Identifizieren der Quelle des Fehlers, wie in der folgenden Tabelle definiert.  
  
|Datenquelle|Präfix|Wert|  
|-----------------|------------|-----------|  
|Treiber-Manager|[Hersteller]<br />[ODBC_component]<br />[Data_source]|[Microsoft]<br />[ODBC-Treiber-Manager]<br />–|  
|Visual FoxPro-Treiber|Hersteller]<br />[ODBC_component]<br />[Data_source]|[Microsoft]<br />[Visual FoxPro-ODBC-Treiber]<br />–|  
  
 Beispielsweise kann ein der Visual FoxPro-ODBC-Treiber nicht die Datei nützlich finden konnte, die folgende Fehlermeldung zurück:  
  
 "[*Microsoft*] [*ODBC-Treiber für Visual FoxPro*] Datei"nützlich"ist nicht vorhanden."
