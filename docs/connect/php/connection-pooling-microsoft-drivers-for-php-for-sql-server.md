---
title: Verbindungspooling (Microsoft Drivers for PHP for SQLServer) | Microsoft Docs
ms.custom: ''
ms.date: 07/10/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connection pooling support
ms.assetid: 4d9a83d4-08de-43a1-975c-0a94005edc94
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 276944a1ab6c284aad0ca46fa7ed21f2d5acd592
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="connection-pooling-microsoft-drivers-for-php-for-sql-server"></a>Verbindungspooling (Microsoft Drivers for PHP for SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Folgende wichtige Punkte sollten Sie für das Verbindungspooling in [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]beachten:  
  
-   [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] verwendet ODBC-Verbindungspooling.  
  
-   Standardmäßig ist das Verbindungspooling in Windows aktiviert. Linux und Mac OS X sind Verbindungen "zusammengelegt" nur, wenn Verbindungspooling für ODBC aktiviert ist. Wenn Verbindungspooling aktiviert ist, und Sie mit einem Server verbinden, versucht der Treiber eine gepoolte Verbindung verwendet, bevor er ein neues Konto erstellt. Falls im Pool keine äquivalente Verbindung gefunden wird, wird eine neue Verbindung erstellt und dem Pool hinzugefügt. Basierend auf einem Vergleich der Verbindungszeichenfolgen, ermittelt der Treiber  ob die Verbindungen äquivalent sind.  
  
-   Wenn eine Verbindung aus dem Pool verwendet wird, wird der Verbindungsstatus zurückgesetzt.  
  
-   Das Schließen der Verbindung gibt die Verbindung an den Pool zurück.  
  
Weitere Informationen zum Verbindungspooling finden Sie unter [Treibermanager-Verbindungspooling](../../odbc/reference/develop-app/driver-manager-connection-pooling.md).  
  
## <a name="enablingdisabling-connection-pooling"></a>Aktivieren/Deaktivieren Verbindungspooling
### <a name="windows"></a>Windows
Sie können den Treiber zwingen, eine neue Verbindung (anstelle der Suche nach einer äquivalenten Verbindung im Verbindungspool) zu erstellen, durch Festlegen des Werts, der die *ConnectionPooling* Attribut in der Verbindungszeichenfolge auf **"false"**  (oder 0).  
  
Wenn die *ConnectionPooling* -Attribut wird aus der Verbindungszeichenfolge weggelassen oder wenn sie, um festgelegt ist **"true"** (oder 1) der Treiber erstellt eine neue Verbindung nur, wenn keine äquivalente Verbindung nicht, in vorhanden ist der Verbindungspool.  
  
Weitere Informationen zu weiteren Verbindungsattributen finden Sie unter [Connection Options](../../connect/php/connection-options.md).  
### <a name="linux-and-mac-os-x"></a>Linux und Mac OS X
*ConnectionPooling* Attribut kann nicht zum Aktivieren/Deaktivieren Sie die Verbindungs-pooling verwendet werden. 

Verbindungspooling kann aktiviert oder deaktiviert werden durch Bearbeiten der Konfigurationsdatei "Odbcinst.ini". Der Treiber sollte erneut geladen werden, damit die Änderungen wirksam werden.

Festlegen von `Pooling` auf `Yes` und eine Positive `CPTimeout`Wert in "Odbcinst.ini" wird die Verbindungspooling aktiviert. 
```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
CPTimeout=<int value>
```
Festlegen von `Pooling` auf `No` in "Odbcinst.ini" erzwingt, dass den Treiber erstellt eine neue Verbindung.
```
[ODBC]
Pooling=No
```
  
## <a name="see-also"></a>Siehe auch  
[Gewusst wie: Herstellen einer Verbindung mithilfe der Windows-Authentifizierung](../../connect/php/how-to-connect-using-windows-authentication.md)

[Gewusst wie: Herstellen einer Verbindung mithilfe der SQL Server-Authentifizierung](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
  
