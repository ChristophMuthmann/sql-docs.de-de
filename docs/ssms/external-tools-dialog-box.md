---
title: Externe Tools (Dialogfeld) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- adding external tools
- external tools [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], external tools
ms.assetid: ba797203-24d0-4922-9b97-8ab483f1db14
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 96e4b3799c478e219308a121bb31713ac171ddcb
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="external-tools-dialog-box"></a>Externe Tools (Dialogfeld)
Mit dem Dialogfeld **Externe Tools** können Sie dem Menü **Extras** externe Tools hinzufügen, z. B. SQLCMD oder den Editor. Durch das Hinzufügen von externen Tools können Sie auf einfache Weise andere Anwendungen starten, während Sie in der [!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] -Umgebung arbeiten. Sie können beim Starten des Tools Argumente und ein Arbeitsverzeichnis angeben. Darüber hinaus kann im **Ausgabefenster** die Ausgabe einiger Tools angezeigt werden. Das Dialogfeld **Externe Tools** wird über das Menü **Extras** aufgerufen.  
  
## <a name="options"></a>enthalten  
**Inhalt des Menüs**  
Führt die Titel der Elemente auf, die aktuell dem Menü **Extras** hinzugefügt sind. Verwenden Sie die Schaltflächen **Nach oben** und **Nach unten** , um die Reihenfolge zu ändern, in der die Elemente im Menü angezeigt werden. Verwenden Sie die Schaltfläche **Löschen** , um ein Element aus dem Menü zu entfernen.  
  
**Nach oben**  
Verschiebt das ausgewählte Tool innerhalb der Liste der Tools im Menü **Extras** nach oben.  
  
**Nach unten**  
Verschiebt das ausgewählte Tool innerhalb der Liste der Tools im Menü **Extras** nach unten.  
  
**Hinzufügen**  
Löscht die Textfelder, sodass Sie ein neues Tool angeben können.  
  
**Löschen**  
Entfernt das Tool oder den Befehl aus der Liste **Menüinhalt** und aus dem Menü **Extras** .  
  
**Titel**  
Geben Sie den Namen des Tools oder Befehls ein, der im Untermenü **Externe Tools** des Menüs **Extras** angezeigt wird. Fügen Sie vor einem Buchstaben im Namen des Tools ein kaufmännisches Und-Zeichen (&) ein, um diesen Buchstaben als Tastenkombination anzugeben. Mit „&SQLCMD“ wird z. B. SQLCMD im Menü **Extras** angezeigt.  
  
**Befehl**  
Gibt den Pfad zu der Datei an, die gestartet werden soll.  
  
**Argumente**  
Gibt die Variablen an, die an das Tool übergeben werden, wenn es im Menü aufgerufen wird. Argumente können Werte festlegen, die beim Starten an das Tool oder den Befehl übergeben werden. Ein Wert kann beispielsweise einen Dateinamen oder ein Verzeichnis angeben. Mit der Schaltfläche mit dem Pfeil können Sie aus einer Liste mit vordefinierten Argumenten auswählen. Sie können mehrere Argumente hinzufügen. Eine vollständige Liste vordefinierter Argumente und ihrer Definitionen finden Sie unter [Arguments for External Tools](../ssms/use-of-sql-server-features-and-capabilities-wwi-oltp.md). Abhängig vom verwendeten Befehl oder Tool können Sie auch benutzerdefinierte Argumente eingeben, (wie z. B. Befehlszeilenoptionen).  
  
**Ausgabefenster verwenden**  
Öffnet das Ausgabefenster in [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] , in dem die Ausgabe des derzeit ausgeführten Befehls angezeigt wird. Nicht alle Tools zeigen ihre Ausgabe in einem Format an, das im Ausgabefenster dargestellt werden kann. Weitere Informationen finden Sie unter [Ausgabefenster](http://msdn.microsoft.com/en-us/9808e00c-c8f6-45cc-896e-192b8420f747).  
  
**Ausgabe als Unicode behandeln**  
Interpretiert die Ausgabe als Unicode.  
  
**Ausgangsverzeichnis**  
Gibt das Arbeitsverzeichnis für das Tool an. Mit der Schaltfläche mit dem Pfeil können Sie Verzeichnisse auswählen. Sie können mehrere Verzeichnisse auswählen.  
  
**Zur Argumenteingabe auffordern**  
Zeigt das Dialogfeld **Argumente** an, in dem Sie bei jedem Start des externen Tools Werte für die Argumente eingeben oder bearbeiten können.  
  
**Beim Beenden schließen**  
Schließt das vom Fenster geöffnete Tool, wenn das Tool geschlossen wird.  
  
## <a name="example"></a>Beispiel  
Durch die Eingabe der folgenden Werte im Dialogfeld **Externe Tools** wird ein Menüelement mit der Bezeichnung "DAC" erstellt. Durch Auswählen des Elements wird eine Eingabeaufforderung geöffnet und das Hilfsprogramm **sqlcmd** mithilfe der dedizierten Administratorverbindung (Dedicated Administrator Connection, DAC) ausgeführt.  
  
|Feld|Wert|  
|-------|---------|  
|**Titel**|DAC|  
|**Befehl**|[!INCLUDE[ssInstallPath](../includes/ssinstallpath_md.md)]Tools\Binn\SQLCMD.exe|  
|**Argumente**|-A|  
  
## <a name="see-also"></a>Siehe auch  
[Arguments for External Tools](../ssms/use-of-sql-server-features-and-capabilities-wwi-oltp.md)  
[Allgemeine Benutzeroberflächenelemente](../ssms/general-user-interface-elements.md)  
  

