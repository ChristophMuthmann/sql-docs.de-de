---
title: Herstellen einer Verbindung mit SQLBrowseConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLBrowseConnect
- SQLBrowseConnect function [ODBC], connecting
- connecting to data source [ODBC], SQLBrowseConnect
ms.assetid: 6c2e9f76-b766-48df-b109-246bb05ae45d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0078c9cf3d7d9ba23cade5ff6d53815e1300ba7a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-with-sqlbrowseconnect"></a>Herstellen einer Verbindung mit SQLBrowseConnect
**SQLBrowseConnect**, z. B. **SQLDriverConnect**, verwendet eine Verbindungszeichenfolge. Indem jedoch **SQLBrowseConnect**, eine Anwendung kann eine vollständige Verbindungszeichenfolge zur Laufzeit erstellen. Dadurch kann die Anwendung zwei Funktionen erfüllen:  
  
-   Erstellen Sie eigener Dialogfelder, der Eingabe dieser Informationen, wodurch beibehalten der Kontrolle über seine "Erscheinungsbild."  
  
-   Durchsuchen des Systems nach Datenquellen, die von einem bestimmten Treiber verwendet werden können. Dies sollte nach Möglichkeit in mehreren Schritten erfolgen. Beispielsweise kann der Benutzer zunächst das Netzwerk nach Servern durchsuchen und, sobald er einen Server ausgewählt hat, diesen nach Datenbanken durchsuchen, auf die der Treiber zugreifen kann.  
  
 Ruft die Anwendung **SQLBrowseConnect** und übergibt eine Verbindungszeichenfolge, bekannt als die *durchsuchen Anforderung Verbindungszeichenfolge* , einen Treiber oder eine Datenquelle angibt. Gibt eine Verbindungszeichenfolge, bekannt als der Treiber die *durchsuchen Ergebnis-Verbindungszeichenfolge,* enthält Schlüsselwörter, die möglichen Werte (wenn das Schlüsselwort einen diskreten Satz von Werten akzeptiert), und benutzerfreundliche Namen. Die Anwendung erstellt ein Dialogfeld mit den benutzerfreundlichen Namen und fordert den Benutzer für Werte. Klicken Sie dann eine neue durchsuchen Anforderung Verbindungszeichenfolge aus der folgenden Werte sind anlegen und gibt diese zurück an den Treiber mit einem weiteren Aufruf von **SQLBrowseConnect**.  
  
 Da Verbindungszeichenfolgen hin und her übergeben werden, kann der Treiber bereit, auf mehreren Ebenen aus durchsuchen, indem Sie eine neue Verbindungszeichenfolge zurückgeben, wenn die Anwendung die alte Pläne zurückgegeben. Beispielsweise die ersten Mal eine Anwendung ruft **SQLBrowseConnect**, der Treiber möglicherweise Schlüsselwörter, um den Benutzer für einen Servernamen aufzufordern zurück. Wenn die Anwendung den Namen des Servers zurückgegeben wird, kann der Treiber Schlüsselwörter, um den Benutzer für eine Datenbank aufzufordern zurück. Die Suche nach Prozess würde abgeschlossen werden, nachdem die Anwendung den Datenbanknamen zurückgegeben.  
  
 Jedes Mal **SQLBrowseConnect** neue durchsuchen Verbindung gibt eine Ergebniszeichenfolge zurück, der als Rückgabecode SQL_NEED_DATA zurückgegeben. Dies weist der Anwendung an, dass der Verbindungsprozess nicht abgeschlossen ist. Bis **SQLBrowseConnect** gibt SQL_SUCCESS zurück, die Verbindung befindet sich in einem Zustand erforderlich und kann nicht verwendet werden für andere Zwecke, z. B. ein Verbindungsattribut festlegen. Die Anwendung kann die Verbindung mit dem Durchsuchen der Prozess durch den Aufruf beendet **SQLDisconnect**.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [SQL Server-Suchbeispiel](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
