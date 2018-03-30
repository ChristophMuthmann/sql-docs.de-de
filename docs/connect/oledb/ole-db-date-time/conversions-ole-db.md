---
title: Bindungen und Konvertierungen (OLE DB) | Microsoft Docs
description: Bindungen und Konvertierungen (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB]
- bindings [OLE DB]
- OLE DB, bindings and conversions
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e363464201a3d80c296ccd111e6708d5b3176501
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="conversions-ole-db"></a>Konvertierungen (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In diesem Abschnitt wird erläutert, wie zum Konvertieren zwischen **"DateTime"** und **"DateTimeOffset"** Werte. Die in diesem Abschnitt beschriebenen Konvertierungen werden entweder von OLE DB bereitgestellt oder sind eine konsistente Erweiterung von OLE DB.  
  
 Das Format für Literale und Zeichenfolgen für Datums- und Zeitangaben in OLE DB entspricht normalerweise ISO und hängt nicht von der Gebietsschemaeinstellung des Clients ab. Eine Ausnahme ist DBTYPE_DATE, wo der Standard OLE-Automatisierung ist. Da der OLE DB-Treiber für SQL Server nur zwischen Typen konvertiert, wenn Daten zum oder vom Client übertragen werden, besteht jedoch keine Möglichkeit für eine Anwendung auf die OLE DB-Treiber für SQL Server zum Konvertieren zwischen DBTYPE_DATE und Zeichenfolgenformaten zu erzwingen. Andernfalls verwenden Zeichenfolgen die folgenden Formate (Text in Klammern gibt ein optionales Element an):  
  
-   Das Format der **"DateTime"** und **"DateTimeOffset"** -Zeichenfolgen ist:  
  
     *JJJJ*-*mm*-*Dd*[ *"hh"*:*mm*:*ss*[. *9999999*] [± *"hh"*:*mm*]]  
  
-   Das Format der **Zeit** -Zeichenfolgen ist:  
  
     *hh*:*mm*:*ss*[.*9999999*]  
  
-   Das Format der **Datum** -Zeichenfolgen ist:  
  
     *JJJJ*-*mm*-*TT*  
  
> [!NOTE]  
>  Frühere Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client und SQLOLEDB haben OLE-Konvertierungen implementiert, falls Standardkonvertierungen fehlgeschlagen sind. Folglich unterscheiden sich einige Konvertierungen, die vom OLE DB-Treiber für SQL Server, von der OLE DB-Spezifikation.  
  
 Konvertierungen von Zeichenfolgen ermöglichen Flexibilität bei Leerstellen- und Feldbreite. Weitere Informationen finden Sie im Abschnitt "Datenformate: Zeichenfolgen und Literale" unter [Datentypunterstützung für OLE DB-Datum und Uhrzeit-Verbesserungen](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md).  
  
 Folgende sind allgemeine Konvertierungsregeln:  
  
-   Wenn eine Zeichenfolge in einen date/time-Typ konvertiert wird, wird die Zeichenfolge zuerst als ISO-Literal analysiert. Wenn dies fehlschlägt, wird die Zeichenfolge als OLE-Datumsliteral analysiert, das über Zeitkomponenten verfügt.  
  
-   Wenn keine Zeit vorhanden ist, der Empfänger aber Zeit speichern kann, wird die Zeit auf 0 (null) festgelegt. Wenn kein Datum vorhanden ist, der Empfänger aber ein Datum speichern kann, wird das Datum auf das aktuelle Datum festgelegt, wenn ISO-Konvertierungen verwendet werden, und auf den 30.12.1899, wenn OLE-Konvertierungen verwendet werden.  
  
-   Wenn im vom Client verwendeten Datentyp keine Zeitzone vorhanden ist, der Server aber eine Zeitzone speichern kann, wird angenommen, dass sich die Daten auf dem Client in der Clientzeitzone befinden.  
  
-   Wenn auf dem Server keine Zeitzone vorhanden ist, der Client aber über Zeitzoneninformationen verfügt, wird die UTC-Zeitzone angenommen. Dieses Verhalten unterscheidet sich vom Serververhalten.  
  
-   Wenn die Zeit vorhanden ist, der Empfänger aber keine Zeit speichern kann, wird die Zeitkomponente ignoriert.  
  
-   Wenn das Datum vorhanden ist, der Empfänger aber kein Datum speichern kann, wird die Datumskomponente ignoriert.  
  
-   Wenn beim Konvertieren vom Client zum Server ein Abschneiden der Sekunden oder Sekundenbruchteile auftritt, wird DB_E_ERRORSOCCURRED zurückgegeben, und als Status wird DBSTATUS_E_DATAOVERFLOW festgelegt.  
  
-   Wenn beim Konvertieren von Server zu Client ein Abschneiden der Sekunden oder Sekundenbruchteile auftritt, wird DBSTATUS_S_TRUNCATED festgelegt  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Client-/Server-Konvertierungen](../../oledb/ole-db-date-time/conversions-performed-from-client-to-server.md)  
 Beschreibt die Datum/Uhrzeit-Konvertierungen zwischen einer Clientanwendung, die mit OLE DB-Treiber für SQL Server geschrieben und [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (oder höher).  
  
 [Server/Client-Konvertierungen](../../oledb/ole-db-date-time/conversions-performed-from-server-to-client.md)  
 Beschreibt die Datum/Uhrzeit-Konvertierungen zwischen [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (oder höher) und einer Clientanwendung, die mit OLE DB-Treiber für SQL Server geschrieben.  
  
## <a name="see-also"></a>Siehe auch  
 [Datum und Uhrzeit-Verbesserungen &#40; OLE DB &#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
