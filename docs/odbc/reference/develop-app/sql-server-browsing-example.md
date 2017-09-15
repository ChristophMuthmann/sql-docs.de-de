---
title: SQLServer-Beispiel durchsuchen | Microsoft Docs
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
- SQLBrowseConnect function [ODBC], example
- connecting to data source [ODBC], SqlBrowseConnect
- connecting to driver [ODBC], SQLBrowseConnect
ms.assetid: 6e0d5fd1-ec93-4348-a77a-08f5ba738bc6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6f344ce0a3830bbd79d6674cfd4d5961b973939e
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sql-server-browsing-example"></a>Durchsuchen von SQL Server-Beispiel
Das folgende Beispiel zeigt wie **SQLBrowseConnect** kann verwendet werden, um die Verbindungen mit einem Treiber verfügbar für SQL Server zu durchsuchen. Zuerst, fordert die Anwendung ein Verbindungshandle:  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 Anschließend wird die Anwendung ruft **SQLBrowseConnect** und gibt den SQL Server-Treiber mithilfe der treiberbeschreibung zurückgegebenes **SQLDrivers**:  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Da dies der erste Aufruf ist **SQLBrowseConnect**, der Treiber-Manager wird der SQL Server-Treiber geladen und des Treibers ruft **SQLBrowseConnect** -Funktion mit den gleichen Argumenten, die vom erhalten die die Anwendung.  
  
> [!NOTE]  
>  Wenn Sie ein Datenquellenanbieter, die Windows-Authentifizierung unterstützt Verbindung, müssen Sie angeben `Trusted_Connection=yes` anstelle von Benutzerinformationen-ID und Kennwort in der Verbindungszeichenfolge angegeben.  
  
 Der Treiber feststellt, dass dies der erste Aufruf von **SQLBrowseConnect** und gibt die zweite Ebene der Verbindungsattribute: Server, Benutzername, Kennwort, Anwendungsname und Workstation-ID. Für das Serverattribut gibt es eine Liste der gültigen Servernamen zurück. Der Rückgabecode von **SQLBrowseConnect** wird SQL_NEED_DATA zurück. Hier wird die Ergebniszeichenfolge durchsuchen:  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 Jedes Schlüsselwort in der Ergebniszeichenfolge durchsuchen wird von einem Doppelpunkt und eine oder mehrere Wörter vor dem Gleichheitszeichen folgen. Diese Wörter werden den benutzerfreundlichen Namen, den eine Anwendung verwenden können, um ein Dialogfeld zu erstellen. Die **APP** und **WSID** Schlüsselwörter sind Präfix ein Sternchen, d. h., sie sind optional. Die **SERVER**, **UID**, und **PWD** Schlüsselwörter sind nicht mit dem Präfix ein Sternchen; Werte müssen für sie auf die nächste Anforderung durchsuchen Zeichenfolge angegeben werden. Der Wert für die **SERVER** Schlüsselwort möglicherweise einen der Server zurückgegebenes **SQLBrowseConnect** oder einen vom Benutzer angegebenen Namen.  
  
 Ruft die Anwendung **SQLBrowseConnect** erneut, den grünen Server anzugeben und das Auslassen der **APP** und **WSID** -Schlüsselwörter und den Anzeigenamen nach jedes Schlüsselwort:  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Der Treiber versucht, mit dem grünen Server herzustellen. Wenn nicht schwerwiegende Fehler, z. B. eine fehlende Schlüsselwort-Wert-Paars auftreten **SQLBrowseConnect** wird SQL_NEED_DATA zurückgegeben und bleibt im gleichen Zustand wie vor dem Fehler. Die Anwendung kann Aufrufen **SQLGetDiagField** oder **SQLGetDiagRec** um den Fehler zu ermitteln. Wenn die Verbindung erfolgreich ist, wird der Treiber gibt SQL_NEED_DATA zurück und gibt die Ergebniszeichenfolge durchsuchen:  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 Da die Attribute in dieser Zeichenfolge optional sind, kann die Anwendung und obligatorisch. Allerdings muss die Anwendung aufrufen **SQLBrowseConnect** erneut aus. Wenn die Anwendung entscheidet, lassen Sie den Datenbanknamen und die Sprache, gibt es eine leere durchsuchen Anforderungszeichenfolge an. In diesem Beispiel wählt die Anwendung die Pubs-Datenbank und ruft **SQLBrowseConnect** ein letztes Mal Auslassen der **Sprache** -Schlüsselwort und das Sternchen vor der **Datenbank**Schlüsselwort:  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Da die **Datenbank** -Attribut ist das letzte Verbindungsattribut vom Treiber erforderlich sind, die beim Durchsuchen Prozess abgeschlossen ist, die Anwendung mit der Datenquelle verbunden ist und **SQLBrowseConnect** Gibt SQL_SUCCESS zurück. **SQLBrowseConnect** gibt auch die vollständige Verbindungszeichenfolge als die Ergebniszeichenfolge durchsuchen:  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 Die vom Treiber zurückgegebene endgültige Verbindungszeichenfolge enthält keine benutzerfreundlichen Namen nach jedes Schlüsselwort noch enthält optionale Schlüsselwörtern, die nicht von der Anwendung angegeben. Die Anwendung kann diese Zeichenfolge mit verwenden **SQLDriverConnect** (nach dem Trennen) eine Verbindung mit der Datenquelle auf dem aktuellen Verbindungshandle bzw. zum Verbinden mit der Datenquelle auf einem anderen Verbindungshandle. Beispiel:  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
