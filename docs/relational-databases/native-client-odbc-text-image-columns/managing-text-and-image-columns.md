---
title: Verwalten von Text- und Image-Spalten | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-text-image-columns
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- data types [ODBC], mapping
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 7b543556-ff36-4d35-ac08-de96223d92cd
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e21dcb6e30fa85a235443b9dcb5d12786882ad78
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="managing-text-and-image-columns"></a>Verwalten von Text und Imagespalten
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Text**, **Ntext**, und **Image** Daten (auch als long-Daten bezeichnet) sind Zeichen- oder binären Zeichenfolgen-Datentypen, die Datenwerte zu groß für aufnehmenkönnen**Char**, **Varchar**, **binäre**, oder **Varbinary** Spalten. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Text** -Datentyp mit der ODBC SQL_LONGVARCHAR-Datentyp; **Ntext** ordnet SQL_WLONGVARCHAR und **Image** -Datentyp SQL_LONGVARBINARY. Einige Datenelemente, wie z. B. lange Dokumente oder große Bitmaps, sind möglicherweise zu groß, um im Speicher gespeichert zu werden. Zum Abrufen von long-Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in teilsequenzen, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber ermöglicht einer Anwendung aufrufen [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md). Um lange Daten in teilsequenzen zu senden, kann die Anwendung aufrufen [SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md). Parameter, für die Daten zur Ausführungszeit gesendet werden, werden als Data-at-Execution-Parameter bezeichnet.  
  
 Tatsächlich eine Anwendung schreiben bzw. jeden Datentyp (nicht nur long-Daten) mit abrufen **SQLPutData** oder **SQLGetData**, obwohl nur **Zeichen** und  **binäre** Daten gesendet oder in Teilen abgerufen werden können. Wenn die Daten klein genug, um einen einzelnen Puffer zu groß ist, besteht jedoch im Allgemeinen kein Grund zur Verwendung **SQLPutData** oder **SQLGetData**. Es ist viel leichter, den einzelnen Puffer an den Parameter oder die Spalte zu binden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Gebundene im Vergleich zu ungebundenen Text- und Image-Spalten](../../relational-databases/native-client-odbc-text-image-columns/bound-vs-unbound-text-and-image-columns.md)  
  
-   [Protokollierte im Vergleich zu nicht protokollierten Änderungen](../../relational-databases/native-client-odbc-text-image-columns/logged-vs-unlogged-modifications.md)  
  
-   [Data-at-Execution und Text-, ntext- oder Imagespalten](../../relational-databases/native-client-odbc-text-image-columns/data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
