---
title: Befehl "SET" | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SET PATH command [ODBC]
ms.assetid: db488d1e-0963-4f45-8c76-a23b9bde9e9d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 553c3f464b5a14d578aa05bece939126f7251974
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="set-path-command"></a>Befehl "SET"
Gibt einen Pfad für die Datei sucht. Treiberspezifische Informationen finden Sie unter den Hinweisen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>Argumente  
 AUF [ *Pfad*]  
 Gibt die Verzeichnisse Visual FoxPro gesucht werden soll. Verwenden Sie Kommas oder Semikolons, um die Verzeichnisse zu trennen.  
  
## <a name="remarks"></a>Hinweise  
 Legen Sie Pfad können Sie Suchpfade für andere Programme Visual FoxPro angeben, die innerhalb von gespeicherten Prozeduren aufgerufen werden können. SET PATH ändert sich nicht auf den Pfad der Datenquelle aus, die Sie für die Verbindung angegeben haben.  
  
 Geben Sie Pfad festlegen auf, ohne *Pfad* auf den Pfad zu dem Standardverzeichnis oder Ordner wiederherzustellen.  
  
## <a name="driver-remarks"></a>Treiber "Hinweise".  
 Wenn Sie in einer gespeicherten Prozedur festgelegt Pfad ausgeben, wird sie durch die folgenden Funktionen und Befehle ignoriert:  
  
-   Katalogfunktionen z. B. [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md) und [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) ignoriert den neuen Pfad und den von der Datenquelle im angegebenen Pfad verweisen weiterhin auf [SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md) oder [ SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
-   Befehle wie z. B. SELECT, INSERT, UPDATE, DELETE und CREATE TABLE ignoriert den neuen Pfad und den von der Datenquelle im angegebenen Pfad verweisen weiterhin auf **SQLPrepare** oder **SQLExecDirect**.  
  
 Wenn Sie SET PATH in einer gespeicherten Prozedur aus und der Pfad nicht anschließend wieder in seinen ursprünglichen Zustand festgelegt werden, werden anderen Verbindungen zur Datenbank den neuen Pfad verwenden (da es sich um eine SET PATH nicht auf Daten Sitzungen begrenzt ist).  
  
 Wenn erstellen, wählen, oder Aktualisieren von Tabellen in einem Verzeichnis als dem von der Datenquelle angegeben werden sollen, geben Sie den vollständigen Pfad der Datei mit dem Befehl.  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-Visual FoxPro einrichten (Dialogfeld)](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns (Visual FoxPro-ODBC-Treiber)](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect (Visual FoxPro-ODBC-Treiber)](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables (Visual FoxPro-ODBC-Treiber)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
