---
title: Verbindungsattribute | Microsoft Docs
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
- data sources [ODBC], connection attributes
- ODBC drivers [ODBC], connection attributes
- connecting to data source [ODBC], connection attributes
- connection attributes [ODBC]
- connecting to driver [ODBC], connection attributes
ms.assetid: e6d03089-30a3-4627-a642-591ba0980894
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d62657134276621442c58639d1ef1c7f2a4b63e0
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="connection-attributes"></a>Verbindungsattribute
Verbindungsattribute sind die Merkmale der Verbindung. Da Transaktionen auf Verbindungsebene auftreten, handelt es sich bei der Transaktionsisolationsstufe beispielsweise um ein Verbindungsattribut. Ebenso ist die Anmeldungstimeout bzw. die Anzahl von Sekunden warten, bevor ein Timeout auftritt, eine Verbindung herstellen möchten, ein Verbindungsattribut.  
  
 Weitere Verbindungsattribute gesetzt werden, mit **SQLSetConnectAttr** und mit ihren aktuellen Einstellungen abgerufen **SQLGetConnectAttr**. Wenn **SQLSetConnectAttr** wird aufgerufen, bevor der Treiber geladen ist, wird der Treiber-Manager speichert die Attribute in seiner Verbindungsstruktur und im Rahmen des Verbindungsprozesses im Treiber festgelegt. Es ist nicht erforderlich, dass eine Anwendung weitere Verbindungsattribute gesetzt. Alle Verbindungsattribute haben Standardwerte, von die einige Treiber-spezifisch sind.  
  
 Ein Verbindungsattribut kann vor oder nach der Verbindung oder entweder abhängig von dem Attribut und der Treiber festgelegt werden. Das Anmeldungstimeout (SQL_ATTR_LOGIN_TIMEOUT) gilt, um den Verbindungsprozess und wird nur wirksam, wenn vor dem Herstellen einer Verbindung festgelegt. Die Attribute, die angeben, ob die ODBC-Cursorbibliothek (SQL_ATTR_ODBC_CURSORS) und die Netzwerk-Paketgröße (SQL_ATTR_PACKET_SIZE) verwenden, müssen vor dem Herstellen einer Verbindung festgelegt werden, da zwischen der Treiber-Manager und der Treiber die ODBC-Cursorbibliothek befindet und aus diesem Grund muss vor der Treiber geladen werden.  
  
 Die Attribute, die angeben, ob eine Datenquelle schreibgeschützt ist oder Lese-/ Schreibzugriff (SQL_ATTR_ACCESS_MODE) und den aktuellen Katalog (SQL_ATTR_CURRENT_CATALOG) festgelegt werden, können vor oder nach dem Herstellen einer Verbindung, je nach den Treiber. Allerdings festgelegt interoperable Anwendungen ausführen können sie vor dem Herstellen einer Verbindung, da einige Treiber nicht unterstützen, ändern diese nach dem Herstellen einer Verbindung.  
  
 Einige Verbindungsattribute aufweisen einen Standardwert, bevor die Verbindung hergestellt wird, andere nicht. Führen Sie die sind SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE und SQL_ATTR_TRACEFILE.  
  
 Die Übersetzung Verbindungsattribute (SQL_ATTR_TRANSLATE_DLL und SQL_ATTR_TRANSLATE_OPTION) müssen nach dem Herstellen einer Verbindung festgelegt werden.  
  
 Alle weiteren Verbindungsattributen können zu einem beliebigen Zeitpunkt festgelegt werden. Weitere Informationen finden Sie unter der [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) funktionsbeschreibung. (Verbindungsattribute können nicht auf die Umgebung Ebene festgelegt werden, durch den Aufruf von **SQLSetEnvAttr**.)
