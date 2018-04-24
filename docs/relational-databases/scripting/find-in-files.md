---
title: In Dateien suchen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.findreplace.findinfiles
- vs.findinfiles
helpviewer_keywords:
- Find in Files dialog box
ms.assetid: bf92770a-33df-43ef-85ad-5a9223649b98
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ae2a6f71c1c8423e550883b6ca82f2f03eff0261
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="find-in-files"></a>In Dateien suchen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Die Registerkarte **In Dateien suchen** des Fensters zum Suchen und Ersetzen ermöglicht es Ihnen, den Code eines angegebenen Satzes von Dateien nach einer Zeichenfolge oder einem Ausdruck zu durchsuchen. Die gefundenen Übereinstimmungen und ausgeführten Aktionen werden in dem unter **Ergebnisoptionen**ausgewählten Suchergebnisfenster aufgelistet.  
  
 Das Dialogfeld **Suchen und Ersetzen** kann auch über Symbolleistenschaltflächen und Tastenkombinationen geöffnet werden.  
  
 In den folgenden Abschnitten werden die auf der Registerkarte **In Dateien suchen** verfügbaren Steuerelemente aufgelistet.  
  
## <a name="find-what"></a>Suchen nach  
 Die folgenden Steuerelemente auf der Registerkarte **In Dateien suchen** ermöglichen es Ihnen, die Zeichenfolge oder den Ausdruck anzugeben, für die/den nach Übereinstimmungen gesucht werden soll.  
  
 **Find what**  
 Geben Sie den Suchtext ein. Im Dialogfeld wird ein wahrscheinlicher Suchtext eingetragen. Dabei wird entweder auf den Text zurückgegriffen, der vor dem Öffnen des Dialogfelds mit dem Cursor markiert wurde, oder auf in der Nähe befindlichen Text oder auf zuvor verwendeten Suchtext. Sie können aus der Dropdownliste eine der letzten 20 Suchzeichenfolgen zur Wiederverwendung auswählen.  
  
 **[Zeichenfolge mit Platzhaltern]**  
 Wenn Sie Platzhalter wie Sternchen (`*`) und Fragezeichen (`?`) in den Suchzeichenfolgen verwenden möchten, aktivieren Sie unter **Suchoptionen** das Kontrollkästchen **Mit** , und klicken Sie dann auf **Platzhalter**.  
  
 **[regulärer Ausdruck]**  
 Wenn das Suchmodul die Suchzeichenfolge als regulären Ausdruck interpretieren soll, aktivieren Sie unter **Suchoptionen** das Kontrollkästchen **Mit** , und klicken Sie anschließend auf **Reguläre Ausdrücke**.  
  
 **Ausdrucks-Generator**  
 Die dreieckige Schaltfläche neben dem Feld **Suchen nach** steht zur Verfügung, nachdem das Kontrollkästchen **Mit** in den **Suchoptionen**aktiviert wurde. Klicken Sie auf diese Schaltfläche, um in Abhängigkeit von der für **Mit** gewählten Option eine Liste von Platzhaltern oder regulären Ausdrücken anzuzeigen. Ein aus dieser Liste ausgewähltes Element wird zur Zeichenfolge **Suchen nach** hinzugefügt.  
  
## <a name="look-in"></a>Suchen in  
 Über die aus der Dropdownliste **Suchen in** ausgewählte Option legen Sie fest, ob die Funktion **In Dateien suchen** nur in den zurzeit aktiven Dateien oder in allen in bestimmten Ordnern gespeicherten Dateien sucht. Wählen Sie einen Suchbereich aus der Liste aus, geben Sie einen Ordnerpfad ein, oder klicken Sie auf die Schaltfläche **Durchsuchen** , um das Dialogfeld **Suchordner auswählen** anzuzeigen und einen Satz zu durchsuchender Ordner auszuwählen.  
  
> [!NOTE]  
>  Wenn die für **Suchen in** ausgewählte Option eine aus der Quellcodeverwaltung ausgecheckte Datei durchsuchen soll, wird nur die Version der Datei durchsucht, die auf den lokalen Computer heruntergeladen wurde.  
  
 **Look in**  
 Wählen Sie aus dieser Liste einen vordefinierten Suchbereich, oder geben Sie über das Dialogfeld **Suchordner auswählen** eine Gruppe von Verzeichnissen an.  
  
 **Aktuelles Dokument**  
 Diese Option steht zur Verfügung, wenn ein Dokument in einem Editor geöffnet ist. Dabei wird nur das aktive Dokument nach der unter **Suchen nach**angegebenen Zeichenfolge durchsucht.  
  
 **Alle offenen Dokumente**  
 Durchsucht alle zurzeit zum Bearbeiten geöffneten Dokumente.  
  
 **Aktuelles Projekt**  
 Durchsucht alle Dateien im aktuellen Projekt.  
  
 **Gesamte Projektmappe**  
 Durchsucht alle Dateien in der aktiven Projektmappe.  
  
 **Unterordner einbeziehen**  
 Gibt an, dass die Unterordner des unter **Suchen in** angegebenen Ordners durchsucht werden. Dazu ist ein benutzerdefinierter Verzeichnissatz erforderlich.  
  
 **Durchsuchen**  
 Klicken Sie auf diese Schaltfläche, um das Dialogfeld **Benutzerdefinierter Verzeichnissatz** anzuzeigen. In diesem Dialogfeld können Sie benannte Verzeichnissätze zusammenstellen, bearbeiten, speichern und auswählen, die Sie dann im Feld **Suchen in** eingeben können.  
  
## <a name="find-options"></a>Mit  
 Sie können den Abschnitt **Suchoptionen** reduzieren oder erweitern. Die folgenden Optionen können aktiviert oder deaktiviert werden.  
  
 **Groß-/Kleinschreibung beachten**  
 Wenn dieses Kontrollkästchen aktiviert ist, werden im Suchergebnisfenster nur Instanzen der unter **Suchen nach** angegebenen Zeichenfolge angezeigt, bei denen neben der inhaltlichen Übereinstimmung auch die Groß-/Kleinschreibung identisch ist. Eine Suche nach **MyObject** bei aktiviertem Kontrollkästchen **Groß-/Kleinschreibung beachten** gibt "MyObject", nicht aber "myobject" oder "MYOBJECT" zurück.  
  
 **Nur ganzes Wort suchen**  
 Wenn dieses Kontrollkästchen aktiviert ist, werden im Suchergebnisfenster nur Instanzen der unter **Suchen nach** angegebenen Zeichenfolge angezeigt, bei denen jeweils das ganze Wort übereinstimmt. Eine Suche nach **MyObject** gibt beispielsweise "MyObject", nicht aber "CMyObject" oder "MyObjectC" zurück.  
  
 **Suchoptionen**  
 Gibt an, wie in den Textfeldern **Suchen nach** oder **Ersetzen durch** eingegebene Sonderzeichen interpretiert werden sollen. Zur Auswahl stehen **Platzhalter** und **Reguläre Ausdrücke**.  
  
 **Regular Expressions**  
 Mithilfe spezieller Notationen werden zu suchende Textmuster definiert. Eine Liste finden Sie unter [Suchen von Text mit regulären Ausdrücken](../../relational-databases/scripting/search-text-with-regular-expressions.md).  
  
 **Platzhalter**  
 Sonderzeichen, wie Sternchen (`*`) und Fragezeichen (`?`), stellen ein oder mehrere Zeichen dar. Eine Liste finden Sie unter [Suchen von Text mit Platzhaltern](../../relational-databases/scripting/search-text-with-wildcards.md).  
  
 **Nach diesen Dateitypen suchen**  
 Diese Liste gibt die Dateitypen an, die in den unter **Suchen in**angegebenen Verzeichnissen durchsucht werden sollen. Wird dieses Feld leer gelassen, werden alle Dateien in den unter **Suchen in** angegebenen Verzeichnissen durchsucht.  
  
```  
*.[ext]; *.[ext] (manual)  
```  
  
 Um nach Dateien eines bestimmten Typs zu suchen, geben Sie ein Sternchen-Platzhalter (`*`) für den Dateinamen, gefolgt von einem Punkt (`.`) und der Dateierweiterung ein. Wenn Sie nach mehreren Dateitypen suchen möchten, geben Sie mehrere Suchzeichenfolgen getrennt durch Semikolons (`;`) ein.  
  
```  
*.[ext]; *.[ext] (from list)  
```  
  
 Wählen Sie ein beliebiges Element in der Liste aus, um eine vorkonfigurierte Suchzeichenfolge einzugeben, die nach Dateien eines bestimmten Typs sucht.  
  
## <a name="result-options"></a>Ergebnisoptionen  
 Bestimmt den Speicherort, an dem die Ergebnisse abgelegt werden, wenn Sie auf **Alle suchen**klicken. Sie können den Abschnitt **Ergebnisoptionen** reduzieren oder erweitern. Die folgenden Optionen können aktiviert oder deaktiviert werden.  
  
 **Fenster "Suchergebnisse 1"**  
 Wenn dieses Kontrollkästchen aktiviert ist, werden die Ergebnisse der aktuellen Suche an den Inhalt im Fenster "Suchergebnisse 1" angehängt. Dieses Fenster wird automatisch geöffnet, um die Suchergebnisse anzuzeigen. Zum manuellen Öffnen des Fensters klicken Sie im Menü **Ansicht** auf **Weitere Fenster** und dann auf **Suchergebnisse 1**.  
  
 **Ergebnisse suchen: 2**  
 Wenn dieses Kontrollkästchen aktiviert ist, werden die Ergebnisse der aktuellen Suche an den Inhalt im Fenster Suchergebnisse 2 angehängt. Dieses Fenster wird automatisch geöffnet, um die Suchergebnisse anzuzeigen. Zum manuellen Öffnen des Fensters klicken Sie im Menü **Ansicht** auf **Weitere Fenster** und dann auf **Suchergebnisse 2**.  
  
 **Nur Dateinamen anzeigen**  
 Zeigt einen Eintrag je Datei an, die eine Übereinstimmung für die Suchbedingung enthält, statt einen Eintrag je Treffer entweder im Fenster Suchergebnisse 1 oder Suchergebnisse 2. Diese Option steht in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]nicht zur Verfügung.  
  
 **Geänderte Dateien offen lassen, nachdem alles ersetzt wurde**  
 Wenn diese Option aktiviert ist, bleiben alle Dateien geöffnet, in denen Ersetzungen vorgenommen wurden. Auf diese Weise können Sie die Änderungen rückgängig machen oder speichern. Speichereinschränkungen können eine Begrenzung der Anzahl der Dateien, die nach einem Ersetzungsvorgang geöffnet bleiben, zur Folge haben.  
  
> [!CAUTION]  
>  Sie können die Funktion **Rückgängig** nur bei Dateien verwenden, die zum Bearbeiten geöffnet bleiben. Wenn diese Option nicht aktiviert ist, bleiben Dateien, die nicht bereits zum Bearbeiten geöffnet waren, geschlossen, und die Option **Rückgängig** steht für diese Dateien nicht zur Verfügung.  
  
## <a name="find-and-replace-views"></a>Sichten beim Suchen und Ersetzen  
 Die Registerkarten oben im Fenster Suchen und Ersetzen beinhalten Menüs, die als **Sichten** bezeichnet werden. Mithilfe dieser Menüs können Sie eine Gruppe von Feldern auswählen, die im aktiven Bereich angezeigt werden. Sie können das Fenster Suchen und Ersetzen an einem für Sie geeigneten Platz angedockt lassen und dann zwischen den Registerkarten und Sichten wechseln, um einen beliebigen Typ eines Such- oder Ersetzungsvorgangs auszuführen.  
  
 **Zur Schnellsuche wechseln**  
 Über diese Symbolleisten-Registerkarte wechseln Sie zum Dialogfeld **Schnellsuche** .  
  
 **Zur Suche in Dateien wechseln**  
 Über diese Symbolleisten-Registerkarte wechseln Sie zum Dialogfeld **In Dateien suchen** .  
  
 **Zur Symbolsuche wechseln**  
 Über diese Symbolleisten-Registerkarte wechseln Sie zum Dialogfeld **Symbol suchen** .  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Tastenkombinationen für SQL Server Management Studio](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md)  
  
  
