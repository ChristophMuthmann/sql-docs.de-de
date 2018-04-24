---
title: Read (Datenbank-Engine) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Read_TSQL
- Read
dev_langs:
- TSQL
helpviewer_keywords:
- Read [Database Engine]
ms.assetid: f2b8207c-b69f-4327-a874-100b3a1f27d8
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 433a83375e2ae256963c5f304d9c6921086e41f9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="read-database-engine"></a>Read (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Read liest binäre Darstellung von **SqlHierarchyId** aus dem übergebenen **BinaryReader** und legt das **SqlHierarchyId**-Objekt auf diesen Wert fest. Read kann nicht mit [!INCLUDE[tsql](../../includes/tsql-md.md)] aufgerufen werden. Verwenden Sie stattdessen CAST oder CONVERT.
  
## <a name="syntax"></a>Syntax  
  
```sql
void Read( BinaryReader r )   
```  
  
## <a name="arguments"></a>Argumente  
*r*  
 Das **BinaryReader**-Objekt, das einen binären Datenstrom erzeugt, der einer binären Darstellung eines **hierarchyid**-Knotens entspricht.  
  
## <a name="return-types"></a>Rückgabetypen
 **CLR-Rückgabetyp: void**  
  
## <a name="remarks"></a>Remarks  
 Read überprüft seine Eingabe nicht. Wenn eine ungültige binäre Eingabe gegeben wird, löst Read möglicherweise eine Ausnahme aus. Oder der Vorgang ist erfolgreich und erzeugt ein ungültiges **SqlHierarchyId**-Objekt, dessen Methoden zu unvorhersagbaren Ergebnissen führen oder eine Ausnahme auslösen können.  
  
 Read kann nur für ein neu erstelltes **SqlHierarchyId**-Objekt aufgerufen werden.  
  
 Read wird wenn nötig intern von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet, z.B. beim Schreiben von Daten in die **hierarchyid**-Spalte. Read wird auch intern aufgerufen, wenn eine Konvertierung zwischen **varbinary** und **hierarchyid** ausgeführt wird.  
  
## <a name="examples"></a>Beispiele  
  
```sql
Byte[] encoding = new byte[] { 0x58 };  
MemoryStream stream = new MemoryStream(encoding, false /*not writable*/);  
BinaryReader br = new BinaryReader(stream);  
SqlHierarchyId hid = new SqlHierarchyId();  
hid.Read(br);   
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Write &#40;Datenbank-Engine&#41;](../../t-sql/data-types/write-database-engine.md)  
[ToString &#40;Datenbank-Engine&#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[hierarchyid-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
