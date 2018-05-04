---
title: Treiberfähiges Verbindungspooling | Microsoft Docs
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
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b88e45e4e2eeba13c974f818bf8ab45999772d45
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="driver-aware-connection-pooling"></a>Treiberfähiges Verbindungspooling
Treiber treiberfähiges Verbindungspooling ist eine neue Funktion des Treiber-Managers in Windows 8. Treiber treiberfähiges Verbindungspooling kann Treiber Writer zum Anpassen der Verbindungspooling-Verhalten in ihren ODBC-Treiber.  
  
> [!NOTE]  
>  Treiber treiberfähiges Verbindungspooling wird mit der Cursorbibliothek nicht unterstützt. Eine Anwendung wird die Fehlermeldung angezeigt, wenn es versucht, die Cursorbibliothek über SQLSetConnectAttr, aktivieren, wenn der Treiber Verbindungspooling aktiviert ist.  
  
 Treiberfähigen Verbindungspoolings Treiber Adressen werden die folgenden Probleme Treibermanager-Verbindungspooling beziehen:  
  
 **Fragmentierung Pool** der Treiber-Manager wird nur eine Verbindung aus dem Pool eine genaue Übereinstimmung mit der Verbindungszeichenfolge eine neue verbindungsanforderung wird zurückgegeben.  Ein Grund für den Treiber-Manager eine genaue Übereinstimmung erforderlich ist, dass der Treiber-Manager alle treiberspezifischen Verbindungszeichenfolgen-Schlüsselwort und dessen Wert nicht interpretieren kann.  Allerdings möglicherweise einige Werte der Verbindungszeichenfolge-Schlüsselwort (z. B. den Namen der Datenbank) eine genaue Übereinstimmung nicht erforderlich, da der Treiber, die Datenbank in weniger als die Zeit zum Öffnen einer neuen Verbindung ändern kann (die genauen Zeitunterschied hängt von der Datenquelle). Und Unterschiede in der einige Verbindungsattribute (z. B. SQL_ATTR_CURRENT_CATALOG) können dauert länger als Unterschiede in den anderen Attributen (z. B. SQL_ATTR_LOGIN_TIMEOUT) ändern. Hierzu kann ebenfalls verhindern, dass der Treiber-Manager mit der niedrigsten Kosten, wiederverwendbare-Verbindung aus dem Pool. Wenn ein Treiber verfügt über viele neue Verbindungen zu erstellen, beeinträchtigt möglicherweise die Leistung einer Anwendung, und die Datenquelle Skalierbarkeit verringern kann. Poolfragmentierung kann mit treiberfähiges Verbindungspooling, da ein Treiber die Kosten für die Wiederverwendung von eine Verbindung im Pool eine verbindungsanforderung besser einschätzen kann reduziert werden.  
  
 **Keine Aspekt der Anwendungsvoreinstellung** einige Datenquellen können effizient neue Verbindungen öffnen (im Vergleich zum Zurücksetzen von einige Attribute), also, eine Anwendung eine neue Verbindung herstellen, anstatt zu versuchen, eine etwas nicht übereinstimmende wiederverwenden möchten die Verbindung aus dem Pool und einige Werte (obwohl dies länger während der Verbindung Pool Initialisierung Ausdruck sein kann) zurücksetzen. Aber einige Anwendungen möglicherweise die Arbeitslast des Servers kleiner gehalten und kleinere Anzahl von Verbindungen zu öffnen, es kann jedoch auch eine größere Kosten, die Konflikte für das richtige Verhalten zu beheben. Ohne treiberfähiges Verbindungspooling, können Sie diese Art von Voreinstellung effektiv, angeben, da der Treiber-Manager alle treiberspezifische Verbindungsattribute nicht erkannt wird. Treiberfähiges Verbindungspooling ermöglicht einen Treiber für die benutzereinstellung (mit dem treiberspezifischen-Attribut SQLSetConnectAttr), damit es besser schätzen, die Kosten für die Wiederverwendung von eine Verbindung aus dem Pool, auf Grundlage der Einstellungen des Benutzers zu erhalten.  
  
 Weitere Informationen zum treiberfähiges Verbindungspooling finden Sie unter [entwickeln Verbindungspool wissen in eine ODBC-Treiber](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
## <a name="determining-driver-support"></a>Bestimmen der Treiberunterstützung  
 Treiberfähiges Verbindungspooling ist ein optionales Feature, das ein Treiber nicht unterstützt. Um festzustellen, ob ein Treiber unterstützt, verwenden Sie die SQL_DRIVER_AWARE_POOLING_SUPPORTED *Infotyp* von [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>Treiberfähiges Verbindungspooling aktivieren  
 Eine Anwendung kann einen Treiber Verbindungspooling Awareness verwenden, durch Festlegen der SQL_ATTR_CONNECTION_POOLING-Attributs auf SQL_CP_DRIVER_AWARE mit [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). Wenn ein Treiber Verbindungspool Erkennung nicht unterstützt, Treibermanager-Verbindungspooling verwendet werden (wie bei SQL_CP_ONE_PER_HENV wäre, statt SQL_CP_DRIVER_AWARE angegeben worden identisch). ODBC 2.x und 3.x-Anwendungen können diese Funktion aktivieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Developing an ODBC Driver (Entwickeln eines ODBC-Treibers)](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
