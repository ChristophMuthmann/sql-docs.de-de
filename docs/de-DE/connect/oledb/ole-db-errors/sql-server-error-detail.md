---
title: SQL Server-Fehlerdetail | Microsoft Docs
description: SQL Server-Fehlerdetail
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], error details
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error details
- ISQLServerErrorInfo interface
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: d606e6e33e71100c4be512b454138483dd74c6dc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-error-detail"></a>SQL Server-Fehlerdetail
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Der OLE DB-Treiber für SQL Server definiert die Schnittstelle anbieterspezifischer Fehler [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1). Diese Schnittstelle stellt Details zu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Fehlern bereit und ist daher eine nützliche Informationsquelle, wenn Fehler bei der Ausführung von Befehlen oder Rowsetvorgängen auftreten.  
  
 Es gibt zwei Möglichkeiten, erhalten Zugriff auf **ISQLServerErrorInfo** Schnittstelle.  
  
 Der Consumer kann aufgerufen werden **IErrorRecords:: Getcustomererrorobject** zum Abrufen einer **ISQLServerErrorInfo** -Zeiger ist, wie im folgenden Codebeispiel gezeigt. (Besteht keine Notwendigkeit zum Abrufen **ISQLErrorInfo.**) Beide **ISQLErrorInfo** und **ISQLServerErrorInfo** sind benutzerdefinierte OLE DB-Fehlerobjekte mit **ISQLServerErrorInfo** wird die Schnittstelle zum Abrufen von Informationen zu Serverfehlern einschließlich Details wie Prozedurname und Zeilennummern Zeilennummern.  
  
```  
// Get the SQL Server custom error object.  
if(FAILED(hr=pIErrorRecords->GetCustomErrorObject(  
   nRec, IID_ISQLServerErrorInfo,  
   (IUnknown**)&pISQLServerErrorErrorInfo)))  
```  
  
 Eine weitere Möglichkeit zum Abrufen einer **ISQLServerErrorInfo** Zeiger besteht im Aufrufen der **QueryInterface** Methode für einen bereits erhaltenen **ISQLErrorInfo** Zeiger. Beachten Sie, dass, weil **ISQLServerErrorInfo** enthält eine Obermenge der verfügbaren Informationen von **ISQLErrorInfo**, es ist sinnvoll, direkt **ISQLServerErrorInfo** über **ISQLServerErrorInfo**.  
  
 Die **ISQLServerErrorInfo** Schnittstelle macht eine Memberfunktion, [ISQLServerErrorInfo:: GetErrorInfo](../../oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md). Die Funktion gibt einen Zeiger auf eine SSERRORINFO-Struktur und einen Zeiger auf einen Zeichenfolgenpuffer zurück. Beide Zeiger verweisen auf den Arbeitsspeicher, die der Consumer muss Aufheben der Zuordnung mithilfe der **IMalloc:: Free** Methode.  
  
 SSERRORINFO-Strukturmember werden vom Consumer interpretiert wie folgt.  
  
|Member|Description|  
|------------|-----------------|  
|*pwszMessage*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Fehlermeldung. Identisch mit der Zeichenfolge zurückgegeben, die **IErrorInfo:: GetDescription**.|  
|*pwszServer*|Name der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] für diese Sitzung.|  
|*pwszProcedure*|Falls zutreffend, der Name der Prozedur, in der der Fehler aufgetreten ist. Andernfalls eine leere Zeichenfolge.|  
|*lNative*|Systemeigene [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Fehlernummer. Identisch mit den zurückgegebenen Wert der *PlNativeError* Parameter **ISQLErrorInfo:: GetSQLInfo**.|  
|*bState*|Der Status einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Fehlermeldung.|  
|*bClass*|Schweregrad einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Fehlermeldung.|  
|*wLineNumber*|Falls zutreffend, die Zeilennummer einer gespeicherten Prozedur, in der der Fehler aufgetreten ist.|  
  
## <a name="see-also"></a>Siehe auch  
 [Fehler](../../oledb/ole-db-errors/errors.md)   
 [RAISERROR & #40; Transact-SQL & #41;](../../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
