---
title: 'HelloData: Eine einfache ADO-Anwendung | Microsoft Docs'
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- HelloData sample application [ADO]
- ADO, samples
ms.assetid: de4bcd56-dac2-45e6-95ab-9fd7f25878fc
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d5ade478a37ed8810934d7c3c9fd08200c7d54b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="hellodata-a-simple-ado-application"></a>HelloData: Eine einfache ADO-Anwendung
Diese einfache Anwendung schrittweise jeden der vier wichtigsten ADO-Vorgänge: Abrufen, untersuchen, bearbeiten und Aktualisieren von Daten. Diese Vorgänge werden für die Beispieldatenbank Northwind, die Sie mit Microsoft® SQL Server ausgeführt. Im Beispiel für die Fehlerbehandlung ist minimal, auf die Grundlagen von ADO konzentrieren und Code übersichtliche zu verhindern.  
  
### <a name="to-run-hellodata"></a>Ausführen von HelloData  
  
1.  Erstellen Sie ein neues Standard EXE Visual Basic-Projekt, das die ADO-Bibliothek verweist. Weitere Informationen finden Sie unter [verweisen auf die ADO-Bibliotheken](../../../ado/guide/referencing-the-ado-libraries.md).  
  
2.  Erstellen Sie vier Schaltflächen am oberen Rand des Formulars, das Festlegen der **Namen** und **Beschriftung** Eigenschaften mit den Werten in der Tabelle am Ende dieses Themas aufgeführt.  
  
3.  Fügen Sie unterhalb der Schaltflächen eine **Microsoft DataGrid Control** (Msdatgrd.ocx). Die Msdatgrd.ocx-Datei ist im Lieferumfang von Visual Basic und befindet sich im Verzeichnis \windows\system32 oder \winnt\system32. Um Ihrem Visual Basic-Bereich "Toolbox" DataGrid-Steuerelement hinzugefügt haben, wählen Sie **Komponenten...**  aus der **Projekt** Menü. Aktivieren Sie das Kontrollkästchen neben "Microsoft DataGrid Control 6.0 (SP3) (OLEDB)", und klicken Sie dann auf **OK**. Ziehen Sie zum Hinzufügen des Steuerelements zum Projekt das DataGrid-Steuerelement aus der Toolbox in das Visual Basic-Formular.  
  
4.  Erstellen einer **Textfeld** auf das Formular unten im Raster und seine Eigenschaften festlegen, wie in der Tabelle dargestellt. Das Formular sollte die folgende Abbildung entsprechen, wenn Sie fertig sind.  
  
5.  Schließlich kopieren Sie den Code weiter in [HelloData Code](../../../ado/guide/data/hellodata-code.md), und fügen Sie ihn in das Fenster des Code-Editor des Formulars. Drücken Sie **F5** Ausführen des Codes.  
  
> [!NOTE]
>  Im folgenden Beispiel und in diesem Handbuch wird die Benutzer-Id "MyId" mit dem Kennwort "123aBc" zum Authentifizieren beim Server verwendet. Sie sollten diese Werte mit gültigen Anmeldeinformationen für den Server ersetzen. Ersetzen Sie außerdem den Wert "MySQLServer" durch den Namen Ihres Servers.  
  
 Eine ausführliche Beschreibung des Codes, finden Sie unter [Kommentare zu HelloData](../../../ado/guide/data/comments-on-hellodata.md).  
  
 ![Zeigt Form1 für die HelloData VB-Anwendung](../../../ado/guide/data/media/hellodata.gif "HelloData")  
  
|Steuerelementtyp|Eigenschaft|Wert|  
|------------------|--------------|-----------|  
|Form|Name|Form1|  
||Höhe|6500|  
||Breite|6500|  
|MS-DataGrid|Name|grdDisplay1|  
|Textfeld|Name|txtDisplay1|  
||Mehrzeilige|true|  
|Befehlsschaltfläche|Name|cmdGetData|  
||Beschriftung|Get Data|  
|Befehlsschaltfläche|Name|cmdExamineData|  
||Beschriftung|Überprüfen von Daten|  
|Befehlsschaltfläche|Name|cmdEditData|  
||Beschriftung|Bearbeiten von Daten|  
|Befehlsschaltfläche|Name|cmdUpdateData|  
||Beschriftung|Aktualisierungsdaten|
