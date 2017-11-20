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
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d1ecc435a6b62d75527292ab8dc098e8cb121627
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="bound-descriptor-records"></a>Gebundene Deskriptordatensätze
Wenn die Anwendung das SQL_DESC_DATA_PTR-Feld der anwendungsparameterdeskriptor-Datensatz legt fest, sodass sie nicht mehr auf einen null-Wert enthält, der Datensatz gilt als *gebunden*.  
  
 Ist der Deskriptor ein APD, bildet jeder gebundenen Datensatz gebundenen Parameter an. Bei Eingabeparametern muss die Anwendung einen Parameter für jeden Marker dynamischer Parameter in der SQL-Anweisung vor der Ausführung der Anweisung binden. Für Output-Parameter muss die Anwendung den Parameter nicht binden.  
  
 Ist der Deskriptor ein ARD, die eine Zeile mit Datenbankdaten beschreibt, stellt jeder gebundenen Datensatz eine gebundene Spalte dar.

