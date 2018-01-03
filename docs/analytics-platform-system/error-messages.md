---
title: Fehlermeldungen (SQLServer PDW)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e6223cba-2dec-4b8a-bc10-e2ef6a821fe0
caps.latest.revision: "9"
ms.openlocfilehash: c9c0ebf9b452fdf2ec54ae84bec34288e73e88aa
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="error-messages"></a>Fehlermeldungen
SQL Server PDW-Fehlermeldungen zu melden Fehler und Probleme aufgetreten, durch die SQL Server PDW-Komponenten und können auch SQL Server-Fehlern, die Diagnoseinformationen werden über SQL Server PDW einschließen. Diese Fehlermeldungen verwenden eine einheitliche Syntax zum Darstellen von Informationen. Grundlegendes zu dieser Syntax können Sie identifizieren und Beheben von Problemen auf SQL Server PDW.  
  
## <a name="Basics"></a>Fehler-Nachricht-Grundlagen  
Fehlermeldungen, die zurückgegeben werden, führen Sie die gleiche Syntax.  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
Hierbei handelt es sich um die möglichen Werte für jedes Feld:  
  
|Feld|Description|Beispiel|  
|---------|---------------|-----------|  
|*Error_Indicator*|Das Wort "ERROR" oder anderem Text warnen der Benutzer auf ein Problem hin.|Fehler|  
|*SQL_State_Code*|Der Zustandscode SQL gemäß ODBC-Spezifikation. Der Treiber den entsprechenden Status des SQL-Code generiert jedes Mal, wenn er eine Nachricht an eine Anwendung zurückgibt. Der Text "Microsoft" zeigt die Quelle des Fehlers an.|42000|  
|*Driver_Details*|Treiber abhängiges Detailinformationen, beispielsweise den Typ des verwendeten Treiber.|ODBC SQL Server 2008 R2 Parallel Data Warehouse-Treiber|  
|*QueryID*|Der eindeutige Bezeichner für die Abfrage. Verwenden Sie diesen Wert zum Suchen zusätzlicher Informationen im Zusammenhang mit der Verarbeitung der Abfrage. Beispielsweise können die Abfragedetails für die Ausführung in der Verwaltungskonsole mit gefunden werden der Abfrage-ID. Weitere Informationen finden Sie unter [überwachen Sie die Anwendung mithilfe der Verwaltungskonsole](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />Wenn eine QueryID nicht anwendbar ist, wird der Text "Internal" für den Benutzer zurückgegeben.|QID2377|  
|*Message_String*|Eine lesbare Beschreibung des Fehlers oder Problem. Wenn SQL Server-Fehler zurückgegeben wird, ist dies der Text der SQL Server.|Equal-Zuweisung kann in der festgelegten Liste einer UPDATE-Anweisung angezeigt werden.|  
  
Diese Beispielwerte würde dem Benutzer wie folgt angezeigt werden:  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>Siehe auch  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Grundlegendes zu Warnungen-Verwaltungskonsole](understanding-admin-console-alerts.md)  
  
