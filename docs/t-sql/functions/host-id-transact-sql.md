---
title: HOST_ID (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- HOST_ID
- HOST_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IDs [SQL Server], workstations
- HOST_ID function
- workstation IDs [SQL Server]
- identification numbers [SQL Server], workstations
ms.assetid: 36ba56d4-20d7-4cd1-aa2a-e40a6c0a4e39
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fdfdc04297d89a970599b8977b631cb6e5a9fe08
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="hostid-transact-sql"></a>HOST_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Arbeitsstation-ID zurück. Die Arbeitsstation-ID ist die Prozess-ID (PID) der Anwendung auf dem Clientcomputer, die eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
HOST_ID ()  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **char(10)**  
  
## <a name="remarks"></a>Remarks  
 Wenn der Parameter für eine Systemfunktion optional ist, wird von der aktuellen Datenbank, dem aktuellen Hostcomputer, dem aktuellen Serverbenutzer oder dem aktuellen Datenbankbenutzer ausgegangen. Auf integrierte Funktionen müssen immer runde Klammern folgen.  
  
 Systemfunktionen können in der SELECT-Liste, in einer WHERE-Klausel und überall dort verwendet werden, wo ein Ausdruck zulässig ist.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Tabelle erstellt, bei der `HOST_ID()` in einer `DEFAULT`-Definition verwendet wird, um die Terminal-ID von Computern aufzuzeichnen, die Zeilen in eine Tabelle zur Auftragsaufzeichnung einfügen.  
  
```  
CREATE TABLE Orders  
   (OrderID     int       PRIMARY KEY,  
    CustomerID  nchar(5)  REFERENCES Customers(CustomerID),  
    TerminalID  char(8)   NOT NULL DEFAULT HOST_ID(),  
    OrderDate   datetime  NOT NULL,  
    ShipDate    datetime  NULL,  
    ShipperID   int       NULL REFERENCES Shippers(ShipperID));  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Systemfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
