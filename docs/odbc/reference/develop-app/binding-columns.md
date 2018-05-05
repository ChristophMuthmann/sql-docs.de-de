---
title: Binden von Spalten | Microsoft Docs
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
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: c4407694-c8e1-4b0b-a39d-b007e6c3b54d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b78a87884e075e4cbe3dcb914335994aba2e4159
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="binding-columns"></a>Binden von Spalten
Aus der Datenquelle abgerufene Daten werden in der Variablen an die Anwendung zurückgegeben, die die Anwendung für diesen Zweck reserviert wurde. Bevor Sie dies tun kann, muss die Anwendung zuzuordnen, oder *binden*, dieser Variablen auf die Spalten des Resultsets festgelegt; grundsätzlich dieser Prozess das Binden von Anwendungsvariablen an Anweisungsparametern identisch. Wenn die Anwendung eine Variable bindet eine Resultsetspalte, es wird beschrieben, mit dieser Variable – Adresse, Datentyp und So weiter – an den Treiber. Der Treiber speichert diese Informationen in der Struktur, die sie für diese Anweisung verwaltet und verwendet die Informationen, um den Wert aus der Spalte zurück, wenn die Zeile abgerufen wird.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Binden von Resultsetspalten](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [Verwenden von SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
