---
title: DiagnoseDatensätze | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- handles [ODBC], diagnostic records
- header records [ODBC]
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 92c73f9b-3ed7-410d-9cec-2771004aae60
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d6395d87e5691dc33b5a08267ef83c459f94c0d1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="diagnostic-records"></a>DiagnoseDatensätze
Jede Umgebung zugeordnet, Verbindung, der Anweisung und Deskriptorhandles sind *DiagnoseDatensätze*. Dieser Datensatz enthält Diagnoseinformationen über die letzte Funktion aufgerufen, die ein bestimmtes Handle verwendet. Nur, wenn eine andere Funktion mit diesem Handle aufgerufen wird, werden die Datensätze ersetzt. Es gibt keine Beschränkung der Anzahl der DiagnoseDatensätze, die jeweils gespeichert werden können.  
  
 Es gibt zwei Arten von Diagnosedatensätzen: eine *Headerdatensatz* und NULL oder mehr *Statusdatensätze*. Der Headerdatensatz ist Datensatz 0; die Statusdatensätze werden Datensätze 1 und höher. DiagnoseDatensätze bestehen aus einer Reihe von separate Felder, die für den Headerdatensatz und die Statusdatensätze unterschiedlich sind. ODBC-Komponenten können außerdem eigene diagnosedatensatzfelder definieren.  
  
 Obwohl DiagnoseDatensätze als Strukturen betrachtet werden können, ist es nicht notwendig damit Strukturen tatsächlich werden; wie ein Treiber für die Diagnoseinformationen speichert ist treiberspezifische.  
  
 Feldern in Diagnosedatensätzen werden abgerufen, mit **SQLGetDiagField**. In einem einzigen Aufruf mit SQLSTATE, systemeigener Fehlernummer und diagnosemeldung Felder der Statusdatensätze abgerufen werden **SQLGetDiagRec**.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Headerdatensatz](../../../odbc/reference/develop-app/header-record.md)  
  
-   [Statusdatensätze](../../../odbc/reference/develop-app/status-records.md)
