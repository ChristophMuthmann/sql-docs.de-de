---
title: SQL-Abschnitt der Anpassung | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: e65c2871-9986-44ff-b8b7-7f5eda91b3fa
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6294ab601f527527cf69ca017e3643dfe98a1336
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="customization-file-sql-section"></a>SQL-Abschnitt der Anpassung
Die **Sql** Abschnitt kann eine neue SQL-Zeichenfolge, die die Client-Befehl angegebene Zeichenfolge ersetzt enthalten. Wenn Sie keine SQL-Zeichenfolge im Abschnitt vorhanden ist, wird der Abschnitt ignoriert.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Die neue SQL-Zeichenfolge möglicherweise *parametrisierten*. D. h. ein Parameter in der **Sql** Abschnitt der SQL-Zeichenfolge (bezeichnete der "?" Zeichen) können ersetzt werden, durch die entsprechenden Argumente in eine *Bezeichner* in der Clientbefehlszeichenfolge (bezeichnete ein durch Trennzeichen getrennte Liste in Klammern). Der Bezeichner und dieselbe Argumentliste Verhalten sich wie ein Funktionsaufruf.  
  
 Nehmen wir beispielsweise an den Client-Befehlszeichenfolge ist `"CustomerByID(4)"`, ist der Überschrift des Abschnitts SQL `[SQL CustomerByID]`, und die neue Zeichenfolge der SQL-Abschnitt ist `"SELECT * FROM Customers WHERE CustomerID = ?".` der Handler generiert `"SELECT * FROM Customers WHERE CustomerID = 4"` und diese Zeichenfolge für die Datenquelle verwenden.  
  
 Wenn die neue SQL-Anweisung, die null-Zeichenfolge ist (""), und klicken Sie dann im Abschnitt ignoriert wird.  
  
 Wenn die neue Zeichenfolge der SQL-Anweisung nicht gültig ist, schlägt die Ausführung der Anweisung fehl. Der Clientparameter wird effektiv ignoriert. Sie erreichen dies absichtlich "alle Client-SQL-Befehle durch Angabe deaktivieren":  
  
```  
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>Syntax  
 Ersatz der Eintrag der SQL-Zeichenfolge weist das Format:  
  
 **SQL=**   
 ***sqlString***  
  
|Teil|Description|  
|----------|-----------------|  
|**SQL**|Eine literale Zeichenfolge, die Hiermit ist ein SQL-Abschnitt-Eintrag.|  
|***sqlString***|Eine SQL-Zeichenfolge, die die Clientzeichenfolge ersetzt.|  
  
## <a name="see-also"></a>Siehe auch  
 [Connect-Abschnitt der Anpassungsdatei](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Anpassung Dateiabschnitt-Protokolle](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Anpassung UserList Dateiabschnitt](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory-Anpassung](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Erforderlichen Clienteinstellungen](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Grundlegendes zu der Anpassungsdatei](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Schreiben Ihres eigenen benutzerdefinierten Handlers](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


