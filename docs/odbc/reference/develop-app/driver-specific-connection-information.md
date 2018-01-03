---
title: Treiberspezifische Verbindungsinformationen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLConnect function [ODBC], driver-specific connection information
- connecting to driver [ODBC], SQLConnect
- SQLDriverConnect function [ODBC], driver specific connection information
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SQLConnect
- connecting to driver [ODBC], driver-specific information
ms.assetid: 3748758a-f16a-4f3b-9c40-06f2e300704e
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3352a0a31e6bb48be84d72a7da84eb3d7c6100c9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="driver-specific-connection-information"></a>Treiberspezifische Verbindungsinformationen
**SQLConnect** wird davon ausgegangen, dass Datenquellenname, Benutzer-ID und Kennwort sind ausreichend für die Verbindung mit einer Datenquelle und alle anderen Verbindungsinformationen auf das System gespeichert werden kann. Dies ist häufig nicht der Fall. Ein Treiber möglicherweise z. B. eine Benutzer-ID und Kennwort zum Anmelden bei einem Server und einen anderen Benutzer-ID und ein Kennwort zum Anmelden bei einem DBMS. Da **SQLConnect** akzeptiert einen einzelnen Benutzer-ID und ein Kennwort, das bedeutet, dass andere Benutzer-ID und Kennwort mit Informationen für die Datenquelle auf dem System Wenn gespeichert werden müssen **SQLConnect** verwendet werden soll. Dies ist eine potenzielle Verletzung der Sicherheit und sollte vermieden werden, es sei denn, das Kennwort verschlüsselt ist.  
  
 **SQLDriverConnect** ermöglicht es dem Treiber auf eine beliebige Anzahl von Verbindungsinformationen in der Schlüsselwort-Wert-Paare der Verbindungszeichenfolge zu definieren. Angenommen Sie, dass ein Treiber Datenquellenname, Benutzer-ID und Kennwort für den Server und eine Benutzer-ID und das Kennwort für das DBMS erforderlich ist. Ein benutzerdefiniertes Programm, das die XYZ Corp-Datenquelle immer verwendet möglicherweise auffordern den Benutzer-IDs und Kennwörtern und erstellen Sie die folgende Gruppe von Schlüsselwort-Wert-Paare oder *Verbindungszeichenfolge* Übergabe an **SQLDriverConnect**:  
  
> [!NOTE]  
>  Wenn Sie ein Datenquellenanbieter, die Windows-Authentifizierung unterstützt Verbindung, müssen Sie angeben `Trusted_Connection=yes` anstelle von Benutzerinformationen-ID und Kennwort in der Verbindungszeichenfolge angegeben.  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 Die **DSN** (Data Source Name)-Schlüsselwort den Namen der Datenquelle, die **UID** und **PWD** Schlüsselwörter angeben, die Benutzer-ID und Kennwort für den Server und die **UIDDBMS**  und **PWDDBMS** Schlüsselwörter geben Sie den Benutzer-ID und das Kennwort für das DBMS. Beachten Sie, dass das endgültige Semikolon optional ist. **SQLDriverConnect** analysiert diese Zeichenfolge; der XYZ Corp Datenquellenname abzurufenden werden zusätzliche Verbindungsinformationen aus dem System, z. B. die Serveradresse; verwendet und anmelden, um den Server und DBMS unter Verwendung des angegebenen Benutzer-IDs und Kennwörtern.  
  
 Schlüsselwort-Wert-Paare in **SQLDriverConnect** müssen bestimmte Syntaxregeln entsprechen. Die Schlüsselwörter und deren Werte dürfen nicht die **[] {} (),? \*=! @** Zeichen. Der Wert, der die **DSN** -Schlüsselwort darf nicht ausschließlich aus Leerzeichen bestehen und darf keine führende Leerzeichen enthalten. Aufgrund der Grammatik Registrierung Schlüsselwörter und Namen von Datenquellen können nicht den umgekehrten Schrägstrich enthalten (\\) Zeichen. Leerzeichen sind nach dem Gleichheitszeichen im Schlüsselwort-Wert-Paar nicht zulässig.  
  
 Die **FILEDSN** -Schlüsselwort kann verwendet werden, in einem Aufruf von **SQLDriverConnect** an den Namen einer Datei, die Informationen zur Datenquelle enthält (finden Sie unter [Herstellen einer Verbindung mithilfe von Dateidatenquellen](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)weiter unten in diesem Abschnitt). Die **SAVEFILE** -Schlüsselwort können Sie den Namen des DSN-Datei angeben, in dem die Schlüsselwort-Wert-Paare für eine erfolgreiche Verbindung verwendet werden, durch den Aufruf von **SQLDriverConnect** gespeichert werden sollen. Weitere Informationen zu Datenquellen finden Sie unter der [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) funktionsbeschreibung.
