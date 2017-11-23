---
title: Massenkopieren von Text- und Image-Daten | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0e9e9a39634c28ea9948d2f34b08cd7401048b04
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="bulk-copying-text-and-image-data"></a>Massenkopieren von Text- und Bilddaten
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Große **Text**, **Ntext**, und **Image** Werte werden beim Massenkopieren mithilfe der [Bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) Funktion. Sie code [Bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) für die **Text**, **Ntext**, oder **Image** Spalte mit einem *pData* Zeiger festgelegt NULL, der angibt, die Daten mit bereitgestellt werden **Bcp_moretext**. Es ist wichtig, geben Sie die genaue Länge der bereitgestellten Daten für jede **Text**, **Ntext**, oder **Image** Spalte in jeder Zeile massenkopiert. Wenn die Länge der Daten für eine Spalte der Länge der Spalte im angegebenen unterscheidet [Bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md), verwenden Sie [Bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) auf die Länge auf den richtigen Wert festgelegt. Ein [Bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) sendet alle nicht-**Text**, nicht-**Ntext**, und nicht-**Image** Daten, sondern entwerfen die rufen dann **Bcp_moretext** zum Senden der **Text**, **Ntext**, oder **Image** Daten in separaten Einheiten. Massenkopierfunktionen erkennen, dass alle Daten für die aktuelle gesendet wurde **Text**, **Ntext**, oder **Image** Spalte, wenn die Summe der Längen der Daten das Versenden von **Bcp_moretext** entspricht der Länge, angegeben in der neuesten **Bcp_collen** oder **Bcp_bind**.  
  
 **Bcp_moretext** verfügt über keinen Parameter, um eine Spalte zu identifizieren. Wenn mehrere **Text**, **Ntext**, oder **Image** Spalten in einer Zeile **Bcp_moretext** arbeitet mit der **Text**, **Ntext**, oder **Image** Spalten, die mit der Spalte an, dass von der niedrigsten Ordnungszahl, und es wird auf die Spalte mit der höchsten Ordnungszahl ab. **Bcp_moretext** wechselt von einer Spalte zur nächsten, wenn die Summe der Längen der gesendeten Daten im aktuellen angegebene Länge ist gleich **Bcp_collen** oder **Bcp_bind** für die aktuelle Spalte.  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von Massenkopiervorgängen &#40; ODBC &#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
