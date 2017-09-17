---
title: "Die Länge der Pufferlänge und Abschneiden | Microsoft Docs"
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
- data buffers [ODBC], length
- data length [ODBC]
- truncating data [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 2825c6e7-b9ff-42fe-84fc-7fb39728ac5d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 616dc403fdd23f3233bde4a5db19dd58b6d94cf1
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="data-length-buffer-length-and-truncation"></a>Die Länge der Pufferlänge und Abschneiden
Die *Datenlänge* ist die Bytelänge der Daten, die in der Anwendung Datenpuffers gespeichert werden würde, nicht verwendet werden, wie er in der Datenquelle gespeichert wird. Diese Unterscheidung ist wichtig, da die Daten häufig in unterschiedlichen Typen im Datenpuffer als in der Datenquelle gespeichert werden. Daher ist dies für Daten, die an die Datenquelle gesendet werden, die Bytelänge der Daten vor der Konvertierung in den Typ der Datenquelle. Für Daten aus der Datenquelle abgerufen wird ist dies die Bytelänge der Daten nach der Konvertierung in den Datenpuffer Typ und bevor jedes Abschneiden erfolgt.  
  
 Für Daten mit fester Länge, z. B. eine ganze Zahl oder eine Datumsstruktur ist die Bytelänge der Daten immer die Größe des Datentyps. Im Allgemeinen weisen Sie Anwendungen einen Daten--Puffer mit der Größe des Datentyps. Wenn die Anwendung einen kleineren Puffer belegt wird, sind die möglichen Konsequenzen nicht definiert, da der Treiber geht davon aus, der Datenpuffer ist die Größe des Datentyps und die Daten in eine kleinere Puffer zu passen nicht abschneidet. Wenn die Anwendung einen größeren Puffer belegt wird, wird der zusätzliche Leerraum nie verwendet.  
  
 Für Daten mit variabler Länge, z. B. Zeichen- oder Binärdaten ist es wichtig zu wissen, dass die Bytelänge der Daten getrennt von und häufig anders als die Bytelänge des Puffers ist. Die Beziehung zwischen diesen zwei Längen wird beschrieben, der [Puffer](../../../odbc/reference/develop-app/buffers.md) Abschnitt. Wenn die Bytelänge der Daten größer als die Bytelänge des Puffers ist, wird der Treiber schneidet die abgerufenen Daten auf die Bytelänge des Puffers ab und gibt SQL_SUCCESS_WITH_INFO mit SQLSTATE 01004 (Daten abgeschnitten) zurück. Die zurückgegebene Bytelänge ist jedoch die Länge der ungekürzten Daten.  
  
 Nehmen Sie beispielsweise an, dass eine Anwendung für einen Puffer von Binärdaten 50 Bytes belegt. Wenn der Treiber 10 Bytes aus Binärdaten zurückgegeben hat, gibt diese 10 Bytes im Puffer zurück. Die Bytelänge der Daten ist 10, und die Länge in Byte des Puffers ist 50. Wenn der Treiber 60 Bytes aus Binärdaten zurückgegeben wurde, kürzt die Daten auf 50 Bytes, gibt diese Bytes im Puffer und gibt SQL_SUCCESS_WITH_INFO zurück. Die Bytelänge der Daten ist 60 (die Länge vor dem abschneiden), und die Bytelänge des Puffers ist weiterhin 50.  
  
 Für jede Spalte, die abgeschnitten wird, wird ein Diagnosedatensatz erstellt. Da es Zeit für den Treiber, um diese Datensätze zu erstellen und für die Anwendung für die Verarbeitung akzeptiert, kann Abschneiden Leistung beeinträchtigt werden. In der Regel kann eine Anwendung dieses Problem vermeiden, indem groß genug Puffer reservieren, obwohl dies nicht möglich, kann bei der Arbeit mit long-Daten. Wenn Daten abgeschnitten, wird die Anwendung kann in einigen Fällen einen größeren Puffer reservieren und müssen Sie die Daten; Dies gilt nicht in allen Fällen. Wenn eine Kürzung auftritt, beim Abrufen der Daten durch Aufrufe von **SQLGetData**, die Anwendung nicht aufrufen muss **SQLGetData** für Daten, die bereits zurückgegeben wurde; Weitere Informationen finden Sie unter [erste Long-Daten](../../../odbc/reference/develop-app/getting-long-data.md).
