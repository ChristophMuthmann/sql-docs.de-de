---
title: "Gebunden Deskriptordatensätze | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e50c4819177a0154d4c739215724763535c84aac
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="bound-descriptor-records"></a>Gebundene Deskriptordatensätze
Wenn die Anwendung das SQL_DESC_DATA_PTR-Feld der anwendungsparameterdeskriptor-Datensatz legt fest, sodass sie nicht mehr auf einen null-Wert enthält, der Datensatz gilt als *gebunden*.  
  
 Ist der Deskriptor ein APD, bildet jeder gebundenen Datensatz gebundenen Parameter an. Bei Eingabeparametern muss die Anwendung einen Parameter für jeden Marker dynamischer Parameter in der SQL-Anweisung vor der Ausführung der Anweisung binden. Für Output-Parameter muss die Anwendung den Parameter nicht binden.  
  
 Ist der Deskriptor ein ARD, die eine Zeile mit Datenbankdaten beschreibt, stellt jeder gebundenen Datensatz eine gebundene Spalte dar.
