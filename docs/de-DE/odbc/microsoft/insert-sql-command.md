---
title: INSERT - SQL-Befehl | Microsoft Docs
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
- INSERT [ODBC]
ms.assetid: 9b648198-349f-46f6-b869-13d129945971
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2ea4fe39e46e34495f7a672e3974b51d61b6088a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="insert---sql-command"></a>INSERT - SQL-Befehl
Fügt einen Datensatz an das Ende einer Tabelle, die die angegebenen Werte enthält.  
  
 Der Visual FoxPro-ODBC-Treiber unterstützt die systemeigene Visual FoxPro-Sprachsyntax für diesen Befehl an. Treiberspezifische Informationen finden Sie unter den Hinweisen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>Argumente  
 INSERT INTO *Dbf_name*  
 Gibt den Namen der Tabelle, zu der der neue Datensatz angefügt wurde. *Dbf_name* kann einen Pfad enthalten und kann ein Namensausdruck sein.  
  
 Wenn die Tabelle, die Sie angeben, nicht geöffnet ist, es ausschließlich in einen neuen Arbeitsbereich geöffnet ist und der neue Datensatz wird auf die Tabelle angefügt. Der neue Arbeitsbereich wird nicht ausgewählt. der aktuelle Arbeitsbereich bleibt so lange ausgewählt.  
  
 Wenn die Tabelle, die Sie angeben, geöffnet ist, fügt Einfügen des neuen Datensatzes zur Tabelle an. Wenn die Tabelle als der aktuelle Arbeitsbereich in einem Arbeitsbereich geöffnet ist, ist nicht es ausgewählt, nachdem der Datensatz angefügt wurde; der aktuelle Arbeitsbereich bleibt so lange ausgewählt.  
  
 [( *fname1*[, *fname2*[,...]])]  
 Gibt an, die Namen der Felder im neuen Datensatz in die die Werte eingefügt werden.  
  
 Werte ( *eExpression1*[, *eExpression2*[,...]])  
 Gibt die Feldwerte in den neuen Eintrag eingefügt. Wenn Sie die Feldnamen weglassen, müssen Sie die Feldwerte in der Reihenfolge, die durch die Tabellenstruktur definierten angeben.  
  
## <a name="remarks"></a>Hinweise  
 Der neue Datensatz enthält die Daten in der VALUES-Klausel aufgeführt.  
  
## <a name="driver-remarks"></a>Treiber "Hinweise".  
 Wenn Ihre Anwendung die ODBC-SQL-Anweisung INSERT an die Datenquelle gesendet wird, konvertiert der Visual FoxPro-ODBC-Treiber den Befehl in den Visual FoxProINSERT-Befehl ohne Übersetzung an.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen der Tabelle - SQL-Befehl](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT (SQL-Befehl)](../../odbc/microsoft/select-sql-command.md)
