---
title: Objekthierarchiesyntax (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], hierarchy syntax
ms.assetid: 7ed8df86-9fd2-4e09-96bc-5381fec85f65
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b217fa48f2bbaad1b8c2423dd701f0f839f8786b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="object-hierarchy-syntax-transact-sql"></a>Objekthierarchiesyntax (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Die *Propertyname* -Parameter von Sp_OAGetProperty und Sp_OASetProperty und *Methodname* -Parameter von Sp_OAMethod unterstützen eine Objekthierarchiesyntax, die ähnlich dem Konzept ist [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. Bei Verwendung dieser speziellen Syntax haben diese Parameter das folgende allgemeine Format.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
'TraversedObject.PropertyOrMethod'  
```  
  
## <a name="arguments"></a>Argumente  
 *TraversedObject*  
 Ist ein OLE-Objekt in der Hierarchie unterhalb der *Objecttoken* in der gespeicherten Prozedur angegeben. Mithilfe der [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]-Syntax geben Sie eine Folge von Auflistungen, Objekteigenschaften und Methoden an, die Objekte zurückgeben. Alle Objektbezeichner in dieser Folge müssen durch Punkte (.) getrennt werden.  
  
 Ein Element der Folge kann der Name einer Auflistung sein. Mit der folgenden Syntax geben Sie eine Auflistung an:  
  
 Sammlung ("*Element*")  
  
 Die doppelten Anführungszeichen (") sind erforderlich. Das [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]-Ausrufezeichen (!) der Syntax für Auflistungen wird nicht unterstützt.  
  
 *PropertyOrMethod*  
 Ist der Name einer Eigenschaft oder Methode von der *TraversedObject*.  
  
 Um alle Index- oder Methodenparameter mit den Parametern sp_OAGetProperty, sp_OASetProperty oder sp_OAMethod (einschließlich der Unterstützung für Ausgabeparameter von sp_OAMethod) anzugeben, verwenden Sie die folgende Syntax:  
  
 *PropertyOrMethod*  
  
 Um alle Index- oder Methodenparameter innerhalb der Klammern anzugeben (dadurch werden alle Index- oder Methodenparameter von sp_OAGetProperty, sp_OASetProperty und sp_OAMethod ignoriert), verwenden Sie die folgende Syntax:  
  
 *PropertyOrMethod*([ *ParameterName*: =] "*Parameter*" [,...])  
  
 Die doppelten Anführungszeichen (") sind erforderlich. Alle benannten Parameter müssen nach den Positionsparametern angegeben werden.  
  
## <a name="remarks"></a>Hinweise  
 Wenn *TraversedObject* nicht angegeben ist, *PropertyOrMethod* ist erforderlich.  
  
 Wenn *PropertyOrMethod* nicht angegeben wird, die *TraversedObject* als Objekttoken-Ausgabeparameter von der gespeicherten OLE-Automatisierungsprozedur zurückgegeben. Wenn *PropertyOrMethod* angegeben wird, die Eigenschaft oder Methode von der *TraversedObject* aufgerufen wird, und der Eigenschaftswert oder Rückgabewert der Methode wird als Output-Parameter zurückgegeben, aus der OLE-Automatisierung gespeicherte Prozedur.  
  
 Wenn ein Element der *TraversedObject* Liste keinen OLE-Objekt zurückgibt, wird ein Fehler ausgelöst.  
  
 Weitere Informationen zur [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]-OLE-Objektsyntax finden Sie in der [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]-Dokumentation.  
  
 Weitere Informationen zu HRESULT-Rückgabecodes finden Sie unter [Sp_OACreate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oacreate-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
 Es folgen Beispiele für die Objekthierarchiesyntax, die ein SQL-DMO SQLServer-Objekt verwendet wird.  
  
```  
-- Get the AdventureWorks2012 Person.Address Table object.  
EXEC @hr = sp_OAGetProperty @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address")',  
   @table OUT  
  
-- Get the Rows property of the AdventureWorks2012 Person.Address table.  
EXEC @hr = sp_OAGetProperty @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address").Rows',  
   @rows OUT  
  
-- Call the CheckTable method to validate the   
-- AdventureWorks2012 Person.Address table.  
EXEC @hr = sp_OAMethod @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address").CheckTable',  
   @checkoutput OUT  
```  
  
## <a name="see-also"></a>Siehe auch  
 [OLE-Automatisierungsbeispielskript](../../relational-databases/stored-procedures/ole-automation-sample-script.md)   
 [Gespeicherte OLE-Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
  
  
