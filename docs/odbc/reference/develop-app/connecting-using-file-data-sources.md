---
title: Herstellen einer Verbindung mithilfe von Dateidatenquellen | Microsoft Docs
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
- connecting to driver [ODBC], file data sources
- SQLDriverConnect function [ODBC], connecting using file data sources
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], file data sources
- file data sources [ODBC]
ms.assetid: 3003f8c2-8be6-41cc-8d9c-612e9bd0f3ae
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5f8a5d949127e7ad87866a0272fbd285fe12ceed
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-using-file-data-sources"></a>Herstellen einer Verbindung mit Datenquellen
Die Verbindungsinformationen für eine Datei als Datenquelle wird in einer DSN-Datei gespeichert. Daher kann die Verbindungszeichenfolge wiederholt verwendet werden, indem ein einzelner Benutzer oder für mehrere Benutzer freigegeben werden, wenn sie den entsprechenden Treiber installiert haben. Die Datei enthält einen Treibernamen (oder einen anderen Datenquellennamen im Falle einer Dateidatenquelle) und optional eine Verbindungszeichenfolge, die von verwendet werden kann **SQLDriverConnect**. Der Treiber-Manager erstellt die Verbindungszeichenfolge für den Aufruf von **SQLDriverConnect** aus der Schlüsselwörter in der DSN-Datei.  
  
 Eine Dateidatenquelle ermöglicht einer Anwendung Verbindungsoptionen angeben, ohne dass zum Erstellen einer Verbindungszeichenfolge für die Verwendung mit **SQLDriverConnect**. Die Datei als Datenquelle in der Regel wird erstellt, indem die **SAVEFILE** Schlüsselwort, das bewirkt, dass der Treiber-Manager zum Speichern der Ausgabe-Verbindungszeichenfolge erstellt, die durch einen Aufruf von **SQLDriverConnect** auf die DSN-Datei. Dass die Verbindungszeichenfolge wiederholt verwendet werden kann, können Sie durch Aufrufen von **SQLDriverConnect** mit der **FILEDSN** Schlüsselwort. Dies optimiert das Verbindung und eine permanente Datenquelle der Verbindungszeichenfolge.  
  
 Dateidatenquellen auch können erstellt werden, durch den Aufruf **SQLCreateDataSource** im DLL-Installer. Informationen in den DSN-Datei geschrieben werden kann, durch den Aufruf **SQLWriteFileDSN**, und die DSN-Datei auslesen, durch den Aufruf **SQLReadFileDSN**; beide Funktionen werden auch in der DLL-Installer. Informationen zu den Installer DLL finden Sie unter [Konfigurieren von Datenquellen](../../../odbc/reference/install/configuring-data-sources.md).  
  
 Schlüsselwörter für Verbindungsinformationen sind im Abschnitt [ODBC] DSN-Datei. Die minimale Informationen, die eine freigegebenes DSN-Datei im Abschnitt [ODBC] ist das DRIVER-Schlüsselwort:  
  
```  
DRIVER = SQL Server  
```  
  
 Die freigebbare DSN-Datei enthält eine Verbindungszeichenfolge in der Regel wie folgt aus:  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 Wenn die Datei als Datenquelle Dateidatenquelle ist, sind nur die DSN-Datei enthält eine **DSN** Schlüsselwort. Wenn der Treiber-Manager die Informationen in eine Dateidatenquelle gesendet wird, verbindet nach Bedarf mit der Datenquelle, angegeben durch die **DSN** Schlüsselwort. Eine Dateidatenquelle DSN-Datei würde die folgenden-Schlüsselwort enthalten:  
  
```  
DSN = MyDataSource  
```  
  
 Für eine Datei als Datenquelle verwendete Verbindungszeichenfolge ist die Kombination der Schlüsselwörter in der DSN-Datei angegeben und die Schlüsselwörter in der Verbindungszeichenfolge im Aufruf angegebenen **SQLDriverConnect**. Wenn keines der Schlüsselwörter in der DSN-Datei mit Schlüsselwörtern in der Verbindungszeichenfolge einen Konflikt verursacht, entscheidet der Treiber-Manager an, welche Schlüsselwortwert verwendet werden soll. Weitere Informationen finden Sie unter [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Siehe auch  
 [http://support.Microsoft.com/kb/165866](http://support.microsoft.com/kb/165866)

