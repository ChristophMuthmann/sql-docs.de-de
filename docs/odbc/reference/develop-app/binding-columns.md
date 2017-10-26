---
title: Binden von Spalten | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: c4407694-c8e1-4b0b-a39d-b007e6c3b54d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5903070b8918baa9734e5d188d90861322b57986
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="binding-columns"></a>Binden von Spalten
Aus der Datenquelle abgerufene Daten werden in der Variablen an die Anwendung zurückgegeben, die die Anwendung für diesen Zweck reserviert wurde. Bevor Sie dies tun kann, muss die Anwendung zuzuordnen, oder *binden*, dieser Variablen auf die Spalten des Resultsets festgelegt; grundsätzlich dieser Prozess das Binden von Anwendungsvariablen an Anweisungsparametern identisch. Wenn die Anwendung eine Variable bindet eine Resultsetspalte, es wird beschrieben, mit dieser Variable – Adresse, Datentyp und So weiter – an den Treiber. Der Treiber speichert diese Informationen in der Struktur, die sie für diese Anweisung verwaltet und verwendet die Informationen, um den Wert aus der Spalte zurück, wenn die Zeile abgerufen wird.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Binden von Ergebnis Resultsetspalten](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [SQLBindCol verwenden](../../../odbc/reference/develop-app/using-sqlbindcol.md)

