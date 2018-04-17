---
title: Diagnosemeldungen | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic messages messages
- error messages [ODBC], diagnostic messages
- diagnostic messages [ODBC]
ms.assetid: 98027871-9901-476e-a722-ee58b7723c1f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d8820ce1c437d4bb5012a84ced5db6040cd1b552
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="diagnostic-messages"></a>Diagnosemeldungen
Eine diagnosemeldung wird mit jeder SQLSTATE zurückgegeben. Die gleiche SQLSTATE wird häufig mit einer Anzahl verschiedener Nachrichten zurückgegeben. Beispielsweise ist SQLSTATE 42000 (Syntaxfehler oder zugriffsverletzung) für die meisten Fehler in SQL-Syntax zurückgegeben. Jede Syntaxfehler ist jedoch wahrscheinlich durch eine andere Meldung beschrieben werden.  
  
 Diagnosemeldungen Beispiel sind in der Error-Spalte in der Tabelle der SQLSTATEs in Anhang A und in jeder Funktion aufgeführt. Obwohl Treiber diese Meldungen zurückgegeben werden können, sind sie eher die Nachricht an sie übergeben wird, von der Datenquelle zurückzugeben.  
  
 Anwendungen anzeigen diagnosemeldungen in der Regel dem Benutzer zusammen mit den SQLSTATE und der systemeigene Fehlercode. Dies hilft dem Benutzer und Support in Verbindung zu den Grund mittels Ursachenanalyse ermitteln. Die Komponenteninformationen in der Meldung eingebettete ist besonders hilfreich, auf diese Weise.  
  
 Diagnosemeldungen stammen aus Datenquellen und Komponenten in einer ODBC-Verbindung, z. B. Treiber, Gateways und der Treiber-Manager. In der Regel unterstützt Datenquellen nicht direkt ODBC. Daher, wenn eine Komponente in einer ODBC-Verbindung aus einer Datenquelle eine Nachricht empfängt, muss die Datenquelle als Quelle der Nachricht identifiziert werden. Sie müssen auch selbst als die Komponente kennzeichnen, die die Nachricht empfangen.  
  
 Wenn die Quelle der Warnung oder ein Fehler einer Komponente selbst ist, muss die diagnosemeldung dies erläutern. Daher muss der Text der Fehlermeldungen zwei verschiedene Formaten. Für Fehler und Warnungen, die nicht in eine Datenquelle auftreten, muss die diagnosemeldung dieses Format verwenden:  
  
 **[** *Hersteller-ID* **] [** *ODBC komponentenbezeichners* **]** *Komponente bereitgestellten Text*  
  
 Für Fehler und Warnungen, die in einer Datenquelle auftreten, muss die diagnosemeldung dieses Format verwenden:  
  
 **[** *Hersteller-ID* **] [** *ODBC komponentenbezeichners* **] [** *datenquellenbezeichner*  **]** *Data Source bereitgestellten Text*  
  
 Die folgende Tabelle zeigt die Bedeutung der einzelnen Elemente an.  
  
|Element|Bedeutung|  
|-------------|-------------|  
|*Hersteller-ID*|Gibt den Hersteller der Komponente in der der Fehler oder die Warnung aufgetreten ist, oder, die den Fehler oder die Warnung, direkt aus der Datenquelle empfangen an.|  
|*ODBC-Komponenten-ID*|Identifiziert die Komponente in der der Fehler oder die Warnung aufgetreten ist, oder, die den Fehler oder die Warnung, direkt aus der Datenquelle empfangen.|  
|*datenquellenbezeichner*|Identifiziert die Datenquelle an. Für den dateibasierten Treibern, dies ist normalerweise ein Dateiformat, z. B. Xbase [1] für DBMS-basierten Treibern, ist dies das DBMS-Produkt.|  
|*Komponente bereitgestellten text*|Von der ODBC-Komponente generiert werden.|  
|*Data Source bereitgestellten text*|Von der Datenquelle generiert.|  
  
 [1] In diesem Fall wird der Treiber als der Treiber und der Datenquelle fungiert.  
  
 Klammern (**[]**) in der Nachricht enthalten sein müssen, und zeigen optionale Elemente.
