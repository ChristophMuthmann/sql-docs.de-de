---
title: "Richtlinien und Einschränkungen von DiffGrams für SQLXML | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 07f698a9bcd18566d4cca639e810056f79523684
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>Richtlinien und Einschränkungen von DiffGrams für SQLXML
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Beachten Sie Folgendes ein, bei Verwendung von DiffGrams mit SQLXML 4.0:  
  
-   Typen von Binary large Object (BLOB), z. B. **Text/Ntext** und Images sollten nicht verwendet werden, der  **\<Diffgr: vor dem >** Sperren im bei der Verwendung von DiffGrams, da auf diese Weise für die Verwendung in eingeschlossen werden parallelitätssteuerung. Dies kann wegen der Einschränkungen auf Vergleich für BLOB-Typen Probleme mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verursachen. Z. B. das LIKE-Schlüsselwort wird verwendet in der WHERE-Klausel für den Vergleich zwischen den Spalten von der **Text** -Datentyps; Vergleiche schlägt jedoch fehl, im Fall von BLOB-Typen, in denen die Größe der Daten größer als 8 KB ist.  
  
-   Sonderzeichen in **Ntext** Daten können Probleme mit SQLXML 4.0 verursachen, aufgrund der Einschränkungen auf Vergleich für BLOB-Typen. Beispielsweise die Verwendung von "[Serializable]" in der  **\<Diffgr: vor dem >** -Block eines Diffgrams bei Verwendung in der parallelitätsprüfung einer Spalte vom **Ntext** Typ mit der folgenden SQLOLEDB fehl fehlerbeschreibung:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
