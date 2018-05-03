---
title: Datenquellen-Assistentenbildschirm 1 (Odbcdriver for SQLServer) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
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
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4dc34a7239f931b09f36365ce2dfb595c0c6e9ee
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-wizard-screen-1"></a>Data Source-Assistentenbildschirm 1

Geben Sie den Namen und die Beschreibung der Datenquelle und den Namen des Servers mit SQL Server, der der Datenquelle hergestellt wird. 
    
## <a name="options"></a>enthalten

### <a name="name"></a>Name

Der von einer ODBC-Anwendung verwendete Datenquellenname, wenn sie eine Verbindung mit der Datenquelle anfordert. Beispielsweise „Personal“. Der Name der Datenquelle wird im Dialogfeld ODBC-Datenquellen-Administrator angezeigt.

### <a name="description"></a>Description

(Optional) Eine Beschreibung der Datenquelle. Zum Beispiel „Einstellungsdatum, Gehaltsverlauf und aktuelle Überprüfung aller Mitarbeiter“.

### <a name="select-or-enter-a-server-name"></a>Wählen Sie einen Servernamen aus, oder geben Sie ihn ein.

Der Name einer Instanz von SQL Server in Ihrem Netzwerk. Sie müssen im nächsten Eingabefeld einen Server angeben.

In den meisten Fällen kann der ODBC-Treiber mit der Standardprotokollreihenfolge und den in diesem Feld bereitgestellten Servernamen herstellen. Verwenden Sie SQL Server-Konfigurations-Manager, wenn Sie einen Alias für den Server erstellen oder Clientnetzwerkbibliotheken konfigurieren möchten.

Sie können eingeben "(local)" in das Feld bei Verwendung von dem gleichen Computer wie SQL Server. Der Benutzer kann dann Verbindung mit der lokalen Instanz von SQL Server, selbst wenn eine nicht vernetzte Version von SQL Server ausgeführt. Es können mehrere Instanzen von SQL Server auf demselben Computer ausgeführt. Um eine benannte Instanz von SQL Server angeben, wird der Servername als angegeben _ServerName_\\_InstanceName_.

Weitere Informationen über Servernamen für verschiedene Typen von Netzwerken finden Sie in der Dokumentation der SQL Server-Installation in der SQL Server-Onlinedokumentation.

### <a name="finish"></a>Fertig stellen

Wenn die auf diesem Bildschirm angegebene Informationen erforderlich ist, für die Verbindung mit SQL Server sind, können Sie klicken **Fertig stellen**. Für alle auf anderen Bildschirmen des Assistenten angegebenen Attribute werden Standardwerte verwendet.

### <a name="next"></a>Weiter

Um zum nächsten Bildschirm des Assistenten fortzufahren, klicken Sie auf **Weiter**.

## <a name="next-steps"></a>Nächste Schritte

[Data Source-Assistent (Bildschirm 2)](../../../connect/odbc/windows/dsn-wizard-2.md)
