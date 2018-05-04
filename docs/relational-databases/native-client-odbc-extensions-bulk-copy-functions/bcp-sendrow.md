---
title: Bcp_sendrow | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- bcp_sendrow
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: baf75dd4d0c9c040573a54dd102f38ef3ecd4f21
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="bcpsendrow"></a>'bcp_sendrow'
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Sendet eine Datenzeile aus Programmvariablen nach [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC hdbc);  
```  
  
## <a name="arguments"></a>Argumente  
 *HDBC*  
 Das für den Massenkopiervorgang aktivierte ODBC-Verbindungshandle.  
  
## <a name="returns"></a>Rückgabewert  
 SUCCEED oder FAIL.  
  
## <a name="remarks"></a>Hinweise  
 Die **Bcp_sendrow** Funktion erstellt eine Zeile aus Programmvariablen und sendet sie an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Vor dem Aufruf **Bcp_sendrow**, müssen Aufrufe an [Bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) um die Programmvariablen mit den Zeilendaten anzugeben.  
  
 Wenn **Bcp_bind** aufgerufen wird, Angeben eines langen Daten variabler Länge-Typs, z. B. ein *eDataType* -Parameter von SQLTEXT und ein Wert ungleich NULL *pData* Parameter, **Bcp_sendrow** sendet den gesamten Datenwert, ebenso wie bei einem beliebigen anderen Datentyp dar. IF, allerdings **Bcp_bind** enthält eine NULL *pData* Parameter **Bcp_sendrow** Steuerelement an die Anwendung zurückgegeben werden, sofort, nachdem alle Spalten mit den angegebenen Daten an gesendet werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die Anwendung kann dann aufrufen [Bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) wiederholt, um die langen, variabler Länge, die Daten senden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ein Segment zu einem Zeitpunkt. Weitere Informationen finden Sie unter [Bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md).  
  
 Wenn **Bcp_sendrow** wird verwendet, um Zeilen aus Programmvariablen in Massenimport [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabellen, Zeilen sind ein Commit ausgeführt wurde, nur, wenn der Benutzer ruft [Bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md) oder [Bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md) . Der Benutzer kann **bcp_batch** wahlweise einmal für alle *n* Zeilen aufrufen oder dann, wenn bei den eingehenden Daten eine Pause auftritt. Wird **bcp_batch** nie aufgerufen, wird ein Commit für die Zeilen ausgeführt, wenn **bcp_done** aufgerufen wird.  
  
 Informationen über eine wichtige Änderung, in Massenkopieren ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], finden Sie unter [Durchführen von Massenkopiervorgängen &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen zum Massenkopieren](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
