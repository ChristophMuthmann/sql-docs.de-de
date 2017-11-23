---
title: Fehler | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-errors
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
ms.assetid: bd0612f4-96ef-4919-b0f9-b5447210fe93
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ee71ffa155401cd25bcc0254364733d6c72412fd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="errors"></a>Fehler
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  OLE/COM-Objekte melden Fehler durch den HRESULT-Rückgabecode von Objektelementfunktionen. Ein OLE/COM HRESULT ist eine Bitgepackte Struktur. OLE stellt Makros bereit, die Strukturmember dereferenzieren.  
  
 OLE/COM gibt die **IErrorInfo** Schnittstelle. Die Schnittstelle macht Methoden verfügbar, z. B. **GetDescription**. Dies ermöglicht es Clients, Fehlerdetails aus OLE/COM-Servern zu extrahieren. OLE DB erweitert **IErrorInfo** um die Rückgabe von mehreren fehlerinformationspaketen auf die Ausführung einer einzelmemberfunktion zu unterstützen.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann mehrere Fehler zurückgeben. Eine Anwendung kann Serverfehler zu einem Zeitpunkt abrufen, durch den Aufruf [IMultipleResults:: GetResult](http://go.microsoft.com/fwlink/?LinkId=129630) mit ISQLErrorInfo und IErrorRecords kombiniert.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter stellt der OLE DB-Datensätze erweiterte **IErrorInfo**, die benutzerdefinierte **ISQLErrorInfo**, und die anbieterspezifische [ISQLServerErrorInfo ](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) Schnittstellen für Error-Objekt.  
  
 Informationen zur Ablaufverfolgung von Fehlern finden Sie unter [Datenzugriffsablaufverfolgung](http://go.microsoft.com/fwlink/?LinkId=125805). Informationen zu Verbesserungen hinzugefügten fehlerablaufverfolgung [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], finden Sie unter [Zugriff auf Diagnoseinformationen im Protokoll für erweiterte Ereignisse](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Rückgabecodes](../../relational-databases/native-client-ole-db-errors/return-codes.md)  
  
-   [Informationen in Fehlerschnittstellen](../../relational-databases/native-client-ole-db-errors/information-in-error-interfaces.md)  
  
-   [SQL Server-Fehlerdetail](../../relational-databases/native-client-ole-db-errors/sql-server-error-detail.md)  
  
-   [Abrufen von Fehlerinformationen](../../relational-databases/native-client-ole-db-errors/retrieving-error-information.md)  
  
-   [SQL Server-Meldungsergebnisse](../../relational-databases/native-client-ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
