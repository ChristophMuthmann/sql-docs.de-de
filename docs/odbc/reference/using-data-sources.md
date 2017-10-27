---
title: Verwenden von Datenquellen | Microsoft Docs
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
- data sources [ODBC], about data sources
ms.assetid: d5550619-22b2-4b16-bd08-fbabb6554c40
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eb3e6adb6f563e49429c2e04239ce3170d96b9a4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-data-sources"></a>Verwenden von Datenquellen
Datenquellen werden in der Regel vom Benutzer erstellt oder ein Techniker mit einem Programm aufgerufen der *ODBC-Administrator*. Der ODBC-Administrator fordert den Benutzer für den Treiber verwenden, und ruft dann diesen Treiber. Der Treiber zeigt ein Dialogfeld, das die Informationen zu Anforderungen für die Verbindung mit der Datenquelle benötigten. Nachdem der Benutzer die Informationen eingegeben hat, werden Sie von der Treiber auf dem System gespeichert.  
  
 Später wird die Anwendung ruft der Treiber-Manager und übergibt den Namen einer Datenquelle für den Computer oder den Pfad einer Datei mit einer Datenquelle. Wenn Computer Datenquellenname übergeben wird, sucht der Treiber-Manager das System, um die von der Datenquelle verwendeten Treiber suchen. Anschließend wird der Treiber geladen und der Name der Datenquelle an diese übergibt. Der Treiber verwendet die Namen der Datenquelle für die Verbindung mit der Datenquelle benötigten Informationen zu finden. Zum Schluss wird eine Verbindung mit der Datenquelle, die in der Regel den Benutzer aufzufordern, Benutzer-ID und Kennwort, die in der Regel nicht gespeichert werden.  
  
 Wenn eine Datei als Datenquelle zu übergeben, wird der Treiber-Manager öffnet die Datei und lädt die angegebenen Treiber. Wenn die Datei auch eine Verbindungszeichenfolge enthält, übergibt sie dies an den Treiber. Verbindet mit den Informationen in der Verbindungszeichenfolge der Treiber mit der Datenquelle. Wenn keine Verbindungszeichenfolge übergeben wurde, fordert der Treiber in der Regel der Benutzer die erforderlichen Informationen.

