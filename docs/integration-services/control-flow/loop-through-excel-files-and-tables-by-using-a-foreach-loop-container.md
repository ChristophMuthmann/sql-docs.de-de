---
title: Schleife durch Excel-Dateien und Tabellen mit einem Foreach-Schleifencontainer | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: a5393c1a-cc37-491a-a260-7aad84dbff68
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3a6bda13eb448dd8071908de58206b31fc003181
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="loop-through-excel-files-and-tables-by-using-a-foreach-loop-container"></a>Schleife durch Excel-Dateien und Tabellen mit einem Foreach-Schleifencontainer
  In diesem Thema wird beschrieben, wie mithilfe des Foreach-Schleifencontainers und dem entsprechenden Enumerator die Excel-Arbeitsmappen in einem Ordner oder die Tabellen in einer Excel-Arbeitsmappe durchlaufen werden.  

> [!IMPORTANT]
> Ausführliche Informationen über das Herstellen einer Verbindung mit Excel-Dateien sowie Einschränkungen und bekannte Probleme beim Laden von Daten aus oder in Excel-Dateien finden Sie unter [Load data from or to Excel with SQL Server Integration Services (SSIS) (Laden von Daten aus oder in Excel mit SQL Server Integration Services (SSIS))](../load-data-to-from-excel-with-ssis.md).
 
## <a name="to-loop-through-excel-files-by-using-the-foreach-file-enumerator"></a>So durchlaufen Sie Excel-Dateien mithilfe des Foreach-Dateienumerators  
  
1.  Erstellen Sie eine Zeichenfolgenvariable, die den aktuellen Excel-Pfad und -Dateinamen auf jeder Iteration der Schleife empfängt. Zur Vermeidung von Validierungsproblemen weisen Sie einen gültigen Excel-Pfad und einen Dateinamen als Anfangswert der Variablen zu. (Im weiter unten in dieser Prozedur gezeigten Beispielausdruck wird der Variablenname `ExcelFile`verwendet.)  
  
2.  Erstellen Sie optional eine weitere Zeichenfolgenvariable für den Wert des Arguments Erweiterte Eigenschaften der Excel-Verbindungszeichenfolge. Dieses Argument enthält eine Reihe von Werten, die die Excel-Version angeben und bestimmen, ob die erste Zeile Spaltennamen enthält und ob der Importmodus verwendet wird. (Der Beispielausdruck, der weiter unten in dieser Prozedur dargestellt wird, verwendet den Variablennamen `ExtProperties`und weist einen Anfangswert von "`Excel 8.0;HDR=Yes`" auf.)  
  
     Wenn Sie keine Variable für das Argument "Erweiterte Eigenschaften" verwenden, müssen Sie es dem Ausdruck, der die Verbindungszeichenfolge enthält, manuell hinzufügen.  
  
3.  Fügen Sie der Registerkarte **Ablaufsteuerung** einen Foreach-Schleifencontainer hinzu. Informationen zum Konfigurieren eines Foreach-Schleifencontainers finden Sie unter [Konfigurieren eines Foreach-Schleifencontainers](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25).  
  
4.  Wählen Sie auf der Seite **Auflistung** des **Foreach-Schleifen-Editors**den Foreach-Dateienumerator aus, geben Sie den Ordner an, in dem sich die Excel-Arbeitsmappen befinden, und geben Sie den Dateifilter an (normalerweise *.xls).  
  
5.  Ordnen Sie auf der Seite **Variablenzuordnungen** Index 0 einer benutzerdefinierten Zeichenfolgenvariablen zu, die bei jeder Iteration der Schleife den aktuellen Excel-Pfad und Dateinamen empfangen wird. (Im weiter unten in dieser Prozedur gezeigten Beispielausdruck wird der Variablenname `ExcelFile`verwendet.)  
  
6.  Schließen Sie den **Foreach-Schleifen-Editor**.  
  
7.  Fügen Sie dem Paket einen Excel-Verbindungs-Manager hinzu, wie unter [Hinzufügen, Löschen oder Freigeben eines Verbindungs-Managers in einem Paket](http://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655)beschrieben. Wählen Sie für die Verbindung eine vorhandene Excel-Arbeitsmappendatei aus, um Überprüfungsfehler zu vermeiden.  
  
    > [!IMPORTANT]  
    >  Wählen Sie im **Verbindungs-Manager-Editor für Excel**eine vorhandene Excel-Arbeitsmappe aus, um Überprüfungsfehler zu vermeiden, wenn Sie Tasks und Datenflusskomponenten konfigurieren, die diesen Excel-Verbindungs-Manager verwenden. Diese Arbeitsmappe wird vom Verbindungs-Manager zur Laufzeit nicht mehr verwendet, wenn Sie, wie in den folgenden Schritten beschrieben, einen Ausdruck für die **ConnectionString** -Eigenschaft konfigurieren. Nachdem Sie das Paket erstellt und konfiguriert haben, können Sie im Eigenschaftenfenster den Wert der **ConnectionString** -Eigenschaft löschen. Wenn Sie diesen Wert löschen, ist die Verbindungszeichenfolgen-Eigenschaft des Excel-Verbindungs-Managers allerdings erst dann wieder gültig, wenn die Foreach-Schleife ausgeführt wird. Daher müssen Sie für die Tasks, in denen der Verbindungs-Manager verwendet wird, oder für das Paket die **DelayValidation** -Eigenschaft auf **True** festlegen, um Überprüfungsfehler zu vermeiden.  
    >   
    >  Sie müssen auch den Standardwert von **False** für die **RetainSameConnection** -Eigenschaft des Excel-Verbindungs-Managers verwenden. Wenn Sie diesen Wert auf **True**ändern, wird jede Iteration der Schleife weiterhin die erste Excel-Arbeitsmappe öffnen.  
  
8.  Wählen Sie den neuen Excel-Verbindungs-Manager aus, klicken Sie im Eigenschaftenfenster auf die Eigenschaft **Ausdrücke** , und klicken Sie anschließend auf die Auslassungspunkte.  
  
9. Wählen Sie im **Eigenschaftsausdrucks-Editor** die **ConnectionString** -Eigenschaft aus, und klicken Sie anschließend auf die Auslassungspunkte.  
  
10. Geben Sie im Ausdrucks-Generator den folgenden Ausdruck ein:  
  
    ```  
    "Provider=Microsoft.Jet.OLEDB.4.0;Data Source=" +  @[User::ExcelFile] + ";Extended Properties=\"" + @[User::ExtProperties] + "\""  
    ```  
  
     Beachten Sie die Verwendung des Escapezeichens „\\“ bei den inneren Anführungszeichen, die um den Wert des Arguments für erweiterte Eigenschaften herum erforderlich sind.  
  
     Das Argument "Erweiterte Eigenschaften" ist nicht optional. Wenn Sie keine Variable zur Angabe des Werts verwenden, müssen Sie dem Ausdruck manuell einen Wert hinzufügen, wie im folgenden Beispiel einer Excel 2003-Datei gezeigt:  
  
    ```  
    "Provider=Microsoft.Jet.OLEDB.4.0;Data Source=" +  @[User::ExcelFile] + ";Extended Properties=Excel 8.0"  
    ```  
  
11. Erstellen Sie Tasks innerhalb des Foreach-Schleifencontainers, die den Excel-Verbindungs-Manager verwenden, um für alle Excel-Arbeitsmappen, die dem angegebenen Dateispeicherort und Dateimuster entsprechen, die gleichen Vorgänge auszuführen.  
  
## <a name="to-loop-through-excel-tables-by-using-the-foreach-adonet-schema-rowset-enumerator"></a>So durchlaufen Sie Excel-Tabellen mithilfe des Enumerators für Foreach-ADO.NET-Schemarowset  
  
1.  Erstellen Sie einen ADO.NET-Verbindungs-Manager, der den Microsoft Jet OLE DB-Anbieter zum Herstellen einer Verbindung mit einer Excel-Arbeitsmappe verwendet. Stellen Sie auf der Seite Alle des Dialogfelds **Verbindungs-Manager** sicher, dass Sie Excel 8.0 als Wert der Eigenschaft für erweiterte Eigenschaften eingeben. Weitere Informationen finden Sie unter [Add, Delete, or Share a Connection Manager in a Package](http://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655).  
  
2.  Erstellen Sie eine Zeichenfolgenvariable, die bei jeder Iteration der Schleife den Namen der aktuellen Tabelle empfangen wird.  
  
3.  Fügen Sie der Registerkarte **Ablaufsteuerung** einen Foreach-Schleifencontainer hinzu. Informationen zum Konfigurieren eines Foreach-Schleifencontainers finden Sie unter [Konfigurieren eines Foreach-Schleifencontainers](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25).  
  
4.  Wählen Sie auf der Seite **Auflistung** des **Foreach-Schleifen-Editors** den Enumerator für Foreach-ADO.NET-Schemarowset aus.  
  
5.  Wählen Sie als Wert für **Verbindung**den ADO.NET-Verbindungs-Manager aus, den Sie zuvor erstellt haben.  
  
6.  Wählen Sie als Wert für **Schema**die Option Tabellen aus.  
  
    > [!NOTE]  
    >  Die Liste der Tabellen in einer Excel-Arbeitsmappe schließt sowohl Arbeitsmappen (diese weisen das Suffix $ auf) als auch benannte Bereiche ein. Wenn Sie die Liste nach nur Arbeitsmappen oder nach nur benannten Bereichen filtern müssen, müssen Sie zu diesem Zweck möglicherweise benutzerdefinierten Code in einem Skripttask schreiben. Weitere Informationen finden Sie unter [Working with Excel Files with the Script Task](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md).  
  
7.  Ordnen Sie auf der Seite **Variablenzuordnung** den Index 2 der zuvor erstellten Zeichenfolgenvariablen zu, die den Namen der aktuellen Tabelle enthält.  
  
8.  Schließen Sie den **Foreach-Schleifen-Editor**.  
  
9. Erstellen Sie Tasks innerhalb des Foreach-Schleifencontainers, die den Excel-Verbindungs-Manager verwenden, um für alle Excel-Tabellen in der angegebenen Arbeitsmappe die gleichen Vorgänge auszuführen. Wenn Sie einen Skripttask zum Überprüfen der aufgezählten Tabellennamen oder zum Arbeiten mit den Tabellen verwenden, müssen Sie die Zeichenfolgenvariable der ReadOnlyVariables-Eigenschaft des Skripttasks hinzufügen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Load data from or to Excel with SQL Server Integration Services (SSIS) (Laden von Daten aus oder in Excel mit SQL Server Integration Services (SSIS))](../load-data-to-from-excel-with-ssis.md)  
 [Konfigurieren eines Foreach-Schleifencontainers](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)   
 [Hinzufügen oder Ändern eines Eigenschaftsausdrucks](../../integration-services/expressions/add-or-change-a-property-expression.md)   
 [Excel-Verbindungs-Manager](../../integration-services/connection-manager/excel-connection-manager.md)   
 [Excel-Quelle](../../integration-services/data-flow/excel-source.md)   
 [Excel-Ziel](../../integration-services/data-flow/excel-destination.md)   
 [Arbeiten mit Excel-Dateien mit dem Skripttask](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
  
  
