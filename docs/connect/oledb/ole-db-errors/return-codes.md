---
title: Rückgabecodes | Microsoft Docs
description: Rückgabecodes
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
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
- OLE DB error handling, return codes
- OLE DB Driver for SQL Server, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 37efa9ce4a80cb9d90b3cddccefab243ef3a90ea
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="return-codes"></a>Rückgabecodes
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Auf der grundlegenden Ebene wird eine Elementfunktion entweder erfolgreich ausgeführt, oder sie schlägt fehl. Auf einer genaueren Ebene kann eine Funktion erfolgreich ausgeführt werden, ohne dass das Ergebnis dem entspricht, was vom Anwendungsentwickler beabsichtigt war.  
  
 Weitere Informationen zu OLE DB-Rückgabecodes finden Sie unter [Rückgabecodes (OLE DB)](http://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Wenn ein OLE DB-Treiber für SQL Server-Memberfunktion S_OK zurückgibt, war die Funktion erfolgreich.  
  
 Wenn ein OLE DB-Treiber für SQL Server-Memberfunktion S_OK zurückgibt, können die Entpacken von OLE/COM HRESULT fehlgeschlagen, und IS_ERROR-Makros den Erfolg oder das Fehlschlagen einer Funktion bestimmen.  
  
 Wenn FAILED oder IS_ERROR "true" zurückgibt, wird der OLE DB-Treiber für SQL Server-Consumer sicher, dass die Ausführung der Elementfunktion fehlgeschlagen. Wenn FAILED oder IS_ERROR zurückgeben entspricht "false" und das HRESULT nicht S_OK, der OLE DB-Treiber für SQL Server-Consumer die Funktion erfolgreich ausgeführt, in gewisser Hinsicht gewährleistet ist. Der Consumer kann ausführliche Informationen zu dieser Rückgabewert "Success mit Informationen" aus der OLE DB-Treiber für SQL Server-Schnittstellen für Error abgerufen werden. In Fällen, in denen eine Funktion eindeutig (das FAILED-Makro gibt "true") fehlschlägt, ist auch, erweiterte Fehlerinformationen der OLE DB-Treiber für SQL Server-Schnittstellen für Error verfügbar.  
  
 OLE DB-Treiber für SQL Server-Consumer treten häufig auf den HRESULT-erfolgsrückgabe mit Informationen DB_S_ERRORSOCCURRED "Success". In der Regel definieren Elementfunktionen, die DB_S_ERRORSOCCURRED zurückgeben, einen oder mehrere Parameter, die Statuswerte an den Consumer übermitteln. Keine Fehlerinformationen kann an den Consumer, die in statuswertparametern, zurückgegeben werden, damit Consumer Anwendungslogik, um Statuswerte abzurufen, wenn sie verfügbar sind implementieren soll als verfügbar sein.  
  
 Der OLE DB-Treiber für SQL Server-Memberfunktionen zurück nicht den Erfolgscode S_FALSE. Alle OLE DB-Treiber für SQL Server-Memberfunktionen stets S_OK zurück, um einen Erfolg zu melden.  
  
## <a name="see-also"></a>Siehe auch  
 [Fehler](../../oledb/ole-db-errors/errors.md)  
  
  
