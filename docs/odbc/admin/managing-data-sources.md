---
title: Verwalten von Datenquellen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- deleting data sources [ODBC], ODBC data source administrator
- data sources [ODBC], ODBC data source administrator
- adding data sources [ODBC], ODBC data source administrator
- removing data sources [ODBC], ODBC data source administrator
- ODBC data source administrator [ODBC], data source management
ms.assetid: 67cc4945-4850-4eb4-8da6-b835ddaeca4c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6be8fba37a93e2fda66e96d1334ee4ddcb15d9e5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="managing-data-sources"></a>Verwalten von Datenquellen
Nachdem Sie einen ODBC-Treiber vom Setupprogramm der Treiber installiert haben, können Sie eine oder mehrere Datenquellen dafür definieren. Der Datenquellenname (DSN) sollte eine eindeutige Beschreibung des ausgewählten angeben; beispielsweise *Payroll* oder *"Accounts Payable"*. Die Benutzer und System-Datenquellen, die für alle Treiber installierten definiert sind, werden aufgeführt, der **Benutzer-DSN** oder **System-DSN** Registerkarten der **ODBC-Datenquellen-Administrator**(Dialogfeld). Die Datei-Datenquellen in einem bestimmten Verzeichnis sind aufgeführt, der **Datei-DSN** Registerkarte; in das Verzeichnis angezeigt werden eingegeben wird die **Suchen in** im Feld der **Datei-DSN** Registerkarte.  
  
> [!NOTE]  
>  Verwenden Sie zum Verwalten von einer Datenquelle, die mit einer 32-Bit-Treiber unter 64-Bit-Plattform verbindet c:\windows\sysWOW64\odbcad32.exe. Verwenden Sie zum Verwalten von einer Datenquelle, die mit einer 64-Bit-Treiber verbindet c:\windows\system32\odbcad32.exe. In **Verwaltung** auf einem 64-Bit-Windows 8-Betriebssystem, es sind Symbole für die 32-Bit- und 64-Bit- **ODBC-Datenquellenadministrator** (Dialogfeld).  
  
 Bei Verwendung der 64-Bit-odbcad32.exe zum Konfigurieren oder Entfernen von einem DSN, der mit einer 32-Bit-Treiber, z. B. verbindet **Treiber führen Microsoft Access (\*.mdb)**, erhalten Sie die folgende Fehlermeldung angezeigt:  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 Um diesen Fehler zu beheben, verwenden Sie die 32-Bit-odbcad32.exe zum Konfigurieren oder entfernen den DSN.  
  
 Eine Datenquelle ordnet einen bestimmten ODBC-Treiber die Daten, die Sie über diesen Treiber zugreifen möchten. Beispielsweise können Sie eine Datenquelle aus, um den ODBC-Treiber dBASE zu verwenden, um eine oder mehrere dBASE-Dateien gefunden, die in einem bestimmten Verzeichnis auf der Festplatte oder einem Netzlaufwerk zuzugreifen erstellen. Verwenden die ODBC-Datenquellen-Administrator, können Sie hinzufügen, ändern und Löschen von Datenquellen, wie in der folgenden Tabelle beschrieben.  
  
|Aktion|Description|  
|------------|-----------------|  
|Hinzufügen von Datenquellen|Es ist möglich, mehrere Datenquellen hinzuzufügen, jeweils einige Daten, die Sie mit diesen Treiber zugreifen möchten, einen Treiber zuordnen. Benennen Sie jede Datenquelle, die diese Datenquelle eindeutig identifiziert. Z. B. Wenn Sie eine Datenquelle für einen Satz von dBASE-Dateien, die Kundendaten enthalten erstellen, können Sie die Datenquelle "Customers". Namen Anwendungen in der Regel die Datenquellennamen für Benutzer zur Auswahl anzeigen<br /><br /> Hinzufügen einer Datei als Datenquelle ist etwas anders als Benutzer oder System-Datenquellen hinzufügen. Weitere Informationen finden Sie in der Hilfedatei ODBC-Datenquellen-Administrator.|  
|Ändern von Datenquellen|Je nach Ihren Anforderungen möglicherweise finden Sie es zum Konfigurieren von Datenquellen. Sie können die Optionen zurücksetzen, indem Sie auf **konfigurieren** in alle Treiber einrichten (Dialogfeld).|  
|Löschen von Datenquellen|Klicken Sie auf **entfernen** nach der Auswahl einer Datenquelle.|  
  
 Weitere Informationen zu Datenquellen finden Sie unter [Herstellen einer Verbindung mithilfe von Dateidatenquellen](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) oder [SQLDriverConnect-Funktion](../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-Datenquellen-Administrator](../../odbc/admin/odbc-data-source-administrator.md)
