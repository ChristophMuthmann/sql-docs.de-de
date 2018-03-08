---
title: Bcp_getcolfmt | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: bcp_getcolfmt
apilocation: sqlncli11.dll
apitype: DLLExport
helpviewer_keywords: bcp_getcolfmt function
ms.assetid: f8bdada5-7b2d-4475-8c98-f93e9d77b130
caps.latest.revision: "36"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 642290f1093c1f0730417e4bcbed259322c3e630
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/24/2018
---
# <a name="bcpgetcolfmt"></a>bcp_getcolfmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Zum Suchen des Spaltenformat-Eigenschaftswerts.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RETCODE bcp_getcolfmt (  
        HDBC hdbc,  
        INT field,  
        INT property,  
        void* pValue,  
        INT cbvalue,  
        INT* pcbLen);  
```  
  
## <a name="arguments"></a>Argumente  
 *HDBC*  
 Das für den Massenkopiervorgang aktivierte ODBC-Verbindungshandle.  
  
 *field*  
 Die Spaltenzahl, für die die Eigenschaft abgerufen wird.  
  
 *Eigenschaft*  
 Eine der Eigenschaftskonstanten.  
  
 *pValue*  
 Der Verweis auf den Puffer, von dem der Eigenschaftswert abgerufen werden soll.  
  
 *cbValue*  
 Die Länge des Puffers der Eigenschaft in Bytes.  
  
 *pcbLen*  
 Verweis auf Länge der Daten, die im Eigenschaftspuffer zurückgegeben werden.  
  
## <a name="returns"></a>Rückgabewert  
 SUCCEED oder FAIL.  
  
## <a name="remarks"></a>Hinweise  
 Spaltenformat-Eigenschaftswerte werden aufgeführt, der [Bcp_setcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md) Thema. Die Spaltenformat-Eigenschaftswerte werden festgelegt werden, indem die **Bcp_setcolfmt** -Funktion und die **Bcp_getcolfmt** Funktion wird verwendet, um das Spaltenformat-Eigenschaftswert suchen.  
  
 Das Verhalten ändert sich möglicherweise beobachtet werden, beim Herstellen einer Verbindung mit einem [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (oder höher)-Servercomputer im Vergleich zu früheren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Versionen. Weitere Informationen finden Sie unter [Metadatenermittlung](../../relational-databases/native-client/features/metadata-discovery.md).  
  
## <a name="bcpgetcolfmt-support-for-enhanced-date-and-time-features"></a>bcp_getcolfmt-Unterstützung für erweiterte Funktionen für Datum und Uhrzeit  
 Die Typen, die verwendet wird, mit der **BCP_FMT_TYPE** -Eigenschaft für Datum/Uhrzeit-Typen sind nach den Angaben in [Massenkopieränderungen für erweiterte Datums- und Uhrzeittypen &#40; OLE DB und ODBC &#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Weitere Informationen finden Sie unter [Datum und Uhrzeit-Verbesserungen &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen zum Massenkopieren](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
