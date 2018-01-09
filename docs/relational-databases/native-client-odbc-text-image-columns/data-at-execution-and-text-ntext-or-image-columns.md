---
title: Data-at-Execution und Text-, ntext- oder Image-Spalten | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-text-image-columns
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- data-at-execution
- ODBC data-at-execution
- image columns [ODBC]
ms.assetid: 67ffb1a6-f38d-4712-ba64-96bdd41ec2b2
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b162fe3fe43cd50b35de1ff5f63eefec68d8108f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>Data-at-Execution und Text-, ntext- oder Imagespalten
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC verfügt über eine Funktion namens Data-at-Execution (Daten bei Ausführung), die es Anwendungen ermöglicht, sehr große Datenmengen in gebundenen Spalten oder Parametern zu verarbeiten. Beim Abrufen sehr großer **Text**, **Ntext**, oder **Image** Spalten, eine Anwendung möglicherweise nicht einfach einen sehr umfangreichen Puffer zuzuordnen, binden Sie die Spalte im Puffer und Abrufen die Zeile. Beim Aktualisieren sehr großer **Text**, **Ntext**, oder **Image** Spalten, die Anwendung möglicherweise nicht einfach einen sehr umfangreichen Puffer zuzuordnen, binden es an eine parametermarkierung in einem SQL Anweisung, und führen Sie die Anweisung. In diesen Fällen muss die Anwendung verwenden [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) oder [SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md) mit ihrer Data-at-Execution-Optionen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verwalten von Text und Imagespalten](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
