---
title: APP_NAME (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- APP_NAME_TSQL
- APP_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- name checking for current session [SQL Server]
- sessions [SQL Server], application names
- applications [SQL Server], names
- current session application names
- APP_NAME function
ms.assetid: e491e192-9b30-4243-bc19-33c133fe08a8
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aaea21b68fe0e7a9b0e57bf18d9e9907371dc9b6
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="appname-transact-sql"></a>APP_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Eine Funktion, die den Anwendungsnamen der aktuellen Sitzung zurückgibt, falls die Anwendung diesem Name-Wert festlegt.
  
> [!IMPORTANT]  
>  Der Client stellt den Anwendungsnamen zur Verfügung. Der Wert des Anwendungsnamens wird nicht überprüft. Verwenden Sie **APP_NAME** nicht als Teil einer Sicherheitsprüfung.  
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
  
APP_NAME  ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
**nvarchar(128)**
  
## <a name="remarks"></a>Remarks  
Verwenden Sie **APP_NAME**, um zwischen den verschiedenen Anwendungen zu unterscheiden, damit Sie verschiedene Aktionen für diese Anwendung durchführen können. **APP_NAME** kann beispielsweise zwischen verschiedenen Anwendungen unterscheiden, damit für jede Anwendung ein anderes Datumsformat verwendet werden kann. Außerdem kann durch diese Funktion eine Nachricht mit Informationen an bestimmte Anwendungen zurückgegeben werden.
  
Klicken Sie zum Festlegen eines Anwendungsnamens in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] im Dialogfeld **Verbindung mit Datenbank-Engine** herstellen auf **Optionen**. Geben Sie auf der Registerkarte **Zusätzliche Verbindungsparameter** das Attribut **app** im Format `;app='application_name'` an.
  
## <a name="example"></a>Beispiel  
In diesem Beispiel wird überprüft, ob die Clientanwendung, die diesen Prozess initiiert hat, eine `SQL Server Management Studio`-Sitzung ist und ein Datum im US- oder ANSI-Format bereitstellt.
  
```sql
USE AdventureWorks2012;  
GO  
IF APP_NAME() = 'Microsoft SQL Server Management Studio - Query'  
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( varchar(100) , GETDATE(), 101) + '.';  
ELSE   
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( varchar(100) , GETDATE(), 102) + '.';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch
[Systemfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
[Funktionen](../../t-sql/functions/functions.md)
  
  
