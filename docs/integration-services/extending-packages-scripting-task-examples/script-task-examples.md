---
title: "Skript für Beispielaufgaben | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], examples
- examples [Integration Services]
- SSIS Script task, examples
ms.assetid: b0dd77ee-ee11-4cd9-87aa-61dd67f2fe1c
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f7732abe880aa5eeaab2030da423e18d1977d64a
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="script-task-examples"></a>Skripttask-Beispiele
  Bei Skripttask handelt es sich um ein Mehrzwecktool, das Sie in einem Paket verwenden können, um nahezu alle Anforderungen zu erfüllen, die von den Tasks nicht erfüllt werden, die in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enthalten sind. In diesem Thema werden Skripttaskcodebeispiele aufgeführt, in denen einige der verfügbaren Funktionen veranschaulicht werden.  
  
> [!NOTE]  
>  Wenn Sie Tasks erstellen möchten, die Sie einfacher in mehreren Paketen wiederverwenden können, empfiehlt es sich, den Code in diesen Skripttaskbeispielen als Ausgangspunkt für einen benutzerdefinierten Task zu verwenden. Weitere Informationen finden Sie unter [Entwickeln eines benutzerdefinierten Tasks](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
### <a name="example-topics"></a>Beispielthemen  
 Dieser Abschnitt enthält Codebeispiele, die verschiedene Einsatzbereiche der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Klassen veranschaulichen, die Sie in einen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Skripttask integrieren können:  
  
 [Erkennen einer leeren flachen Datei mit dem Skripttask](../../integration-services/extending-packages-scripting-task-examples/detecting-an-empty-flat-file-with-the-script-task.md)  
 Überprüft eine Flatfile auf vorhandene Datenzeilen, und speichert das Ergebnis in einer Variablen zur Verzweigung der Ablaufsteuerung.  
  
 [Erfassen einer Liste für die ForEach-Schleife mit dem Skripttask](../../integration-services/extending-packages-scripting-task-examples/gathering-a-list-for-the-foreach-loop-with-the-script-task.md)  
 Erstellt eine Liste mit Dateien, die benutzerspezifische Kriterien erfüllen, und füllt eine Variable für den späteren Gebrauch durch den Foreach from-Variablenenumerator.  
  
 [Abfragen des Active Directory mit dem Skripttask](../../integration-services/extending-packages-scripting-task-examples/querying-the-active-directory-with-the-script-task.md)  
 Ruft Benutzerinformationen aus Active Directory basierend auf den Wert des ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mithilfe von Klassen im Namespace System.DirectoryServices Variable.  
  
 [Überwachen von Leistungsindikatoren mit dem Skripttask](../../integration-services/extending-packages-scripting-task-examples/monitoring-performance-counters-with-the-script-task.md)  
 Erstellt einen benutzerdefinierten Leistungsindikator, der zum Nachverfolgen des Ausführungsstatus eines verwendet werden kann ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Paket mithilfe von Klassen im System.Diagnostics-Namespace.  
  
 [Arbeiten mit Bildern mithilfe des Skripttasks](../../integration-services/extending-packages-scripting-task-examples/working-with-images-with-the-script-task.md)  
 Komprimiert Bilder in das JPEG-Format und Miniaturbilder von ihnen, mithilfe der Klassen im Namespace "System.Drawing" erstellt.  
  
 [Suchen installierter Drucker mit dem Skripttask](../../integration-services/extending-packages-scripting-task-examples/finding-installed-printers-with-the-script-task.md)  
 Sucht installierte Drucker, die ein bestimmtes Papierformat unterstützen, mithilfe der Klassen im System.Drawing.Printing-Namespace an.  
  
 [Senden einer HTML-E-Mail mit dem Skripttask](../../integration-services/extending-packages-scripting-task-examples/sending-an-html-mail-message-with-the-script-task.md)  
 Sendet eine Mail-Nachricht im HTML-Format anstatt im Nur-Text-Format.  
  
 [Arbeiten mit Excel-Dateien mit dem Skripttask](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
 Listet die Arbeitsblätter in einer Excel-Datei auf und überprüft das Vorhandensein eines bestimmten Arbeitsblatts.  
  
 [Senden mit dem Skripttask an eine private Remotemeldungswarteschlange](../../integration-services/extending-packages-scripting-task-examples/sending-to-a-remote-private-message-queue-with-the-script-task.md)  
 Sendet eine Meldung an eine private Remotenachrichten-Warteschlange.  
  
### <a name="other-examples"></a>Andere Beispiele:  
 Die folgenden Themen enthalten ebenfalls Codebeispiele, die mit dem Skripttask verwendet werden können:  
  
 [Verwenden von Variablen im Skripttask](../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)  
 Fordert vom Benutzer eine Bestätigung an, ob das Paket weiterhin ausgeführt werden soll, basierend auf dem Wert einer Paketvariablen, der die in einer anderen Variablen festgelegte Begrenzung überschreiten kann.  
  
 [Herstellen einer Verbindung zu Datenquellen im Skripttask](../../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)  
 Ruft eine Verbindung oder Verbindungsinformationen von Verbindungs-Managern ab, die im Paket definiert sind.  
  
 [Auslösen von Ereignissen im Skripttask](../../integration-services/extending-packages-scripting/task/raising-events-in-the-script-task.md)  
 Gibt einen Fehler, eine Warnung oder eine Meldung basierend auf dem Status der Internetverbindung auf dem Server aus.  
  
 [Protokollieren im Skripttask](../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)  
 Protokolliert die Anzahl der Elemente, die vom Task zu aktivierten Protokollanbietern verarbeitet wird.  
  
  

