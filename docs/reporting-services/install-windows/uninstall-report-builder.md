---
title: "Deinstallieren des Berichts-Generators | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
  - "reporting-services-sharepoint"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 009538c6-4941-4393-b14b-9144cffdbdaf
caps.latest.revision: 10
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 10
---
# Deinstallieren des Berichts-Generators
  Sie können die eigenständige Version des Berichts-Generators über die Systemsteuerung oder die Befehlszeile deinstallieren.  
  
 Zum Deinstallieren des Berichts-Generators über die Befehlszeile wird die gleiche Syntax verwendet wie zum Installieren des Berichts-Generators. Sie geben lediglich die /x-Option anstelle der /i-Option an. In den Befehlszeilen zur Deinstallation können auch die /quiet-Option und andere Standardoptionen verwendet werden. Wenn das Windows Installer Package für den Berichts-Generator (ReportBuilder3_x86.msi) entfernt wurde, ist das Entfernen des Berichts-Generators über die Befehlszeile nicht ohne Weiteres möglich. In der Dokumentation für das msiexec-Programm unter [Befehlszeilenoptionen](https://msdn.microsoft.com/library/windows/desktop/aa367988.aspx) wird beschrieben, wie Sie den Berichts-Generator möglicherweise dennoch mit der GUID entfernen können.  
  
 Enthalten vom Berichts-Generator verwendete Ordner benutzerdefinierte Dateien, werden die Ordner und Dateien beim Entfernen des Berichts-Generators beibehalten. Nur die Berichts-Generator-Dateien werden entfernt.  
  
### So deinstallieren Sie den Berichts-Generator über die Systemsteuerung  
  
1.  Klicken Sie im Menü **Start** auf **Systemsteuerung**.  
  
2.  Klicken Sie in der Systemsteuerung auf **Programme und Funktionen**.  
  
3.  Suchen Sie [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Berichts-Generator in der Liste **Name** , und klicken Sie darauf.  
  
4.  Klicken Sie auf **Deinstallieren**.  
  
5.  Klicken Sie auf **Ja**, wenn Sie aufgefordert werden, das Deinstallieren des Berichts-Generators zu bestätigen.  
  
### So deinstallieren Sie den Berichts-Generator über die Befehlszeile  
  
1.  Klicken Sie im Menü **Start** auf **Ausführen**.  
  
2.  Geben Sie im Textfeld **Öffnen** den Befehl **cmd.**ein.  
  
3.  Navigieren Sie im Eingabeaufforderungsfenster zum Ordner mit der Datei "ReportBuilder3_x86.msi".  
  
4.  Geben Sie eine Standardbefehlszeile wie im folgenden Beispiel ein:  
  
 `msiexec /x ReportBuilder3_x86.msi /quiet /l*v install.log`  
  
 Wenn Sie die Protokollierung einschließen möchten, verwenden Sie z. B. folgende Befehlszeile:  
  
 `msiexec /x ReportBuilder3_x86.msi /quiet /l*v c:\junk\install.log`  
  
1.  Drücken Sie die EINGABETASTE ****.  
  
## Siehe auch  
 [Installieren des Berichts-Generators](../../reporting-services/install-windows/install-report-builder.md)  
  
  