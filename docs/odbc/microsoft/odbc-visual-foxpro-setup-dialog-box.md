---
title: Visual FoxPro-Setupdialogfeld ODBC | Microsoft Docs
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
- installing Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], installing
- FoxPro ODBC driver [ODBC], installing
ms.assetid: de020197-7f53-4643-9cbf-b7887ba88de9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e891cbbdfdf77c49262ca21263a7f5b248a70c27
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>ODBC-Visual FoxPro einrichten (Dialogfeld)
Die **ODBC Visual FoxPro-Setup** Dialogfeld können Sie zum Hinzufügen oder Ändern einer Visual FoxPro-Datenquelle.  
  
 Informationen zum Herunterladen des Treibers finden Sie unter [der Visual FoxPro-ODBC-Treiber-Download-Website](http://go.microsoft.com/fwlink/?LinkId=121318).  
  
## <a name="dialog-box-options"></a>Dialogfeldoptionen  
 **Datenquellenname**  
 Geben Sie den Namen, die, den Sie für die Datenquelle verwenden möchten.  
  
 **Beschreibung**  
 Geben Sie eine Beschreibung für die Datenquelle an.  
  
 **Datenbanktyp**  
 Sie können den Typ der Datenbank auswählen die Datenquelle zum Herstellen von Verbindungen verwendet werden soll.  
  
 **Visual FoxPro-Datenbank (. EINER DATENBANK)**  
 Gibt an, dass die Datenquelle zu einer Visual FoxPro hergestellt [Datenbank](../../odbc/microsoft/visual-foxpro-terminology.md) (.dbc-Datei) und für alle Tabellen und lokalen Ansichten in der Datenbank.  
  
 **Kostenloses Tabelle directory**  
 Gibt an, dass die Verbindung in einem Verzeichnis mit der Datenquelle [frei Tabellen](../../odbc/microsoft/visual-foxpro-terminology.md). Alle [Datenbank](../../odbc/microsoft/visual-foxpro-terminology.md) werden Tabellen im selben Verzeichnis wie z. B. durch ODBC-Katalogfunktionen ignoriert [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) oder [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md). Datenbanktabellen können zugegriffen werden, indem SQL SELECT-Anweisungen, die durch gesendeten [SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md) und [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 **Pfad**  
 Zeigt den Pfad und Namen für die Datenbank oder das Verzeichnis der freien Tabellen, die mit denen die Datenquelle verbunden.  
  
 **Durchsuchen**  
 Ermöglicht das Suchen der System- und für die Datenbank oder das Verzeichnis mit der Datenquelle hergestellt werden soll.  
  
 **Optionen**  
 Erweitert das Dialogfeld, sodass Visual FoxPro-ODBC-Treiber-Optionen festgelegt werden können.  
  
## <a name="driver"></a>Treiber  
 **Sortierreihenfolge**  
 Die Reihenfolge, in der Felder sortiert werden. Die Standard-Sequenzen wider, die Sequenzen, die von Ihrer Sprachversion des Betriebssystems unterstützt wird. Eine Liste der unterstützten Sortierreihenfolge Sequenzen, finden Sie unter [festgelegt COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
 **Exclusive**  
 Wenn dieses Kontrollkästchen aktiviert ist, wird der Treiber Visual FoxPro-Datenbank geöffnet, exklusiv, wenn Sie Daten mit der Datenquelle zugreifen. Andere Benutzer können nicht die Datenbank oder den Tabellen in der Datenbank zugreifen, während die Datenbank exklusiv genutzt wird. Tabellen innerhalb der exklusiv geöffnete Datenbank werden als SHARED geöffnet. Um eine Tabelle ausschließlich zu öffnen, verwenden die [exklusive festgelegt](../../odbc/microsoft/set-exclusive-command.md) Befehl. Ist dieses Kontrollkästchen deaktiviert, wenn **Datenbanktyp** festgelegt ist, um **freies**.  
  
 **NULL**  
 Bestimmt, ob mit der ALTER TABLE und CREATE TABLE erstellte Spalten null-Werte zulassen. Wenn Sie Null ON festlegen, fügt INSERT-SQL einen null-Wert in jede Spalte in einer INSERT-SQL nicht enthalten... VALUE-Klausel. Ein Leerzeichen wird eingefügt, wenn Null auf OFF festgelegt ist. Sie können auch diese Option aus, über eine übergebene Verbindungszeichenfolge wie im folgenden Code steuern:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **gelöscht**  
 Bestimmt, ob als gelöscht markierte Zeilen zurückgegeben werden. Sie können auch diese Option aus, über eine übergebene Verbindungszeichenfolge wie im folgenden Code steuern:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **Abrufen von Daten im Hintergrund**  
 Bestimmt, ob die Datensätze werden im Hintergrund (progressiven abrufen) abgerufen werden, oder die Anwendung wird gewartet, bis alle Datensätze im Resultset abgerufen werden.
