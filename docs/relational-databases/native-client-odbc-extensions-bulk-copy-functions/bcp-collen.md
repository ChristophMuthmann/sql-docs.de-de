---
title: Bcp_collen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- bcp_collen
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_collen function
ms.assetid: faaf1f7a-81f2-4852-a178-56602c33673a
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 45bd90619619a18d818898cce5b29d48e79bfb4c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="bcpcollen"></a>bcp_collen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Legt die Datenlänge in der Programmvariable für das aktuelle Massenkopieren nach [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RETCODE bcp_collen (  
        HDBC hdbc,  
        DBINT cbData,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>Argumente  
 *HDBC*  
 Das für den Massenkopiervorgang aktivierte ODBC-Verbindungshandle.  
  
 *cbData*  
 Die Länge der Daten in der Programmvariable ohne die Länge eines Längenindikators oder Längenabschlusszeichens. Wenn Sie *cbData* auf SQL_NULL_DATA setzen, wird angegeben, dass alle zum Server kopierten Zeilen einen NULL-Wert für die Spalte enthalten. Wenn Sie es auf SQL_VARLEN_DATA setzen, geben Sie damit an, dass ein Zeichenfolgenabschlusszeichen oder eine andere Methode verwendet wird, um die Länge der kopierten Daten zu bestimmen. Wenn sowohl ein Längenindikator als auch ein Abschlusszeichen vorliegen, bestimmt das System, was verwendet werden soll, daran, bei welchem Vorgang weniger Daten kopiert werden.  
  
 *idxServerCol*  
 Die Ordnungsposition der Spalte in der Tabelle, in die die Daten kopiert werden. Die erste Spalte ist 1. Die Ordnungsposition einer Spalte wird von [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)ausgegeben.  
  
## <a name="returns"></a>Rückgabewert  
 SUCCEED oder FAIL.  
  
## <a name="remarks"></a>Hinweise  
 Mit der **bcp_collen** -Funktion können Sie die Datenlänge in der Programmvariable für eine bestimmte Spalte ändern, wenn Sie Daten mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bcp_sendrow [nach](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)kopieren.  
  
 Anfänglich wird die Datenlänge beim Aufrufen von [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) bestimmt. Wenn sich die Datenlänge zwischen den Aufrufen von **bcp_sendrow** ändert und kein Längenpräfix oder -abschlusszeichen verwendet wird, können Sie **bcp_collen** aufrufen, um die Länge zurückzusetzen. Mit dem nächsten Aufruf von **bcp_sendrow** wird der Längensatz vom Aufruf von **bcp_collen**verwendet.  
  
 Für jede Spalte in der Tabelle, deren Datenlänge Sie ändern möchten, muss **bcp_collen** einmal aufgerufen werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen zum Massenkopieren](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
