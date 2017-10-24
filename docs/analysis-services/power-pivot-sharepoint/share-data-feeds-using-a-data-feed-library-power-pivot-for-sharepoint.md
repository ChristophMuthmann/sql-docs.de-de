---
title: "Freigeben von Datenfeeds mithilfe einer Datenfeedbibliothek (PowerPivot für SharePoint) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data feeds [Analysis Services with SharePoint]
ms.assetid: 4ec98dec-0cd2-4727-bb79-5bf6f8a865d6
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 31457f6abb88dff525bd19609b8dd552adadfeb8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="share-data-feeds-using-a-data-feed-library-power-pivot-for-sharepoint"></a>Freigeben von Datenfeeds mithilfe einer Datenfeedbibliothek (PowerPivot für SharePoint)
  Ein Datenfeed ist ein XML-Datenstrom, der von einem Dienst oder einer Anwendung generiert wird, der bzw. die Daten im Atom-Übertragungsformat verfügbar macht. Datenfeeds werden zunehmend verwendet, um Daten zwischen Anwendungen und zu clientseitigen Viewern zu transportieren. In einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Bereitstellung werden Datenfeeds verwendet, um eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenquelle mit Daten aus Atom-fähigen Anwendungen oder Diensten aufzufüllen.  
  
 Wenn Sie bereits eine Kombination Atom-fähiger Anwendungen verwenden, benötigen Sie u. U. gar keine Kenntnisse in der Generierung und Nutzung von Feeds, da die Daten nahtlos zwischen den Anwendungen übertragen werden. Organisationen, die benutzerdefinierte Lösungen zum Veröffentlichen von Atom-Feeds verwenden, benötigen jedoch oft eine Möglichkeit, Feeds für Information-Worker verfügbar zu machen. Eine Möglichkeit besteht im Erstellen und Freigeben von Datendienstdokumenten (ATOMSVC-Dateien), die Verbindungen mit den Onlinequellen bereitstellen, die Feeds erzeugen. Das Erstellen und Freigeben von Datendienstdokumenten in einer SharePoint-Webanwendung wir durch eine spezielle Bibliothek, die so genannte Datenfeedbibliothek, unterstützt.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [Erforderliche Komponenten](#prereq)  
  
 [Erstellen eines Datendienstdokuments](#createdsdoc)  
  
 [Sichern eines Datendienstdokuments](#securedsdoc)  
  
 [Ändern eines Datendienstdokuments](#modifydsdoc)  
  
 [Nächster Schritt: Verwenden eines Datendienstdokuments](#usedsdoc)  
  
> [!NOTE]  
>  Obwohl Datenfeeds zum Hinzufügen von Webdaten zu einer in einem [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] erstellten [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]-Datenquelle verwendet werden, kann jede Clientanwendung, die Atom-Feeds lesen kann, Datendienstdokumente verarbeiten.  
  
##  <a name="prereq"></a> Erforderliche Komponenten  
 Sie müssen über eine Bereitstellung von [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint verfügen, die einer SharePoint-Farm [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Abfrageverarbeitung hinzufügt. Datenfeedunterstützung wird durch das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Lösungspaket bereitgestellt.  
  
 Sie müssen über eine SharePoint-Bibliothek verfügen, die den Inhaltstyp von Datendienstdokumenten unterstützt. Zu diesem Zweck wird zwar eine Standard-Datenfeedbibliothek empfohlen, Sie können den Inhaltstyp jeder Bibliothek jedoch auch manuell hinzufügen. Weitere Informationen finden Sie unter [Erstellen oder Anpassen einer Datenfeedbibliothek &#40;Power Pivot für SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/create-or-customize-a-data-feed-library-power-pivot-for-sharepoint.md).  
  
 Sie benötigen einen Datendienst oder eine Onlinedatenquelle, der bzw. die XML-Tabellendaten im Atom 1.0-Format bereitstellt.  
  
 Sie müssen auf einer SharePoint-Website über Teilnahmeberechtigungen verfügen, um ein Datendienstdokument in einer SharePoint-Bibliothek zu erstellen oder zu verwalten.  
  
##  <a name="createdsdoc"></a> Erstellen eines Datendienstdokuments  
 Ein Datendienstdokument stellt eine permanente Anforderung dar, Daten von einer Onlinedatenquelle oder Onlineanwendung, die Daten in einem Feedformat bereitstellt, zu streamen. Beim Erstellen eines Datendienstdokuments geben Sie einen Zeiger auf mindestens einen via URL adressierbaren Datendienst an, der XML im tabellarischen Atom Syndication Format bereitstellt.  
  
 In einem einzelnen Dokument können mehrere Datenfeeds angegeben werden. Dies ist hilfreich, wenn Sie eine Reihe von Datennutzlasten vom gleichen Dienst oder sogar von unterschiedlichen Diensten in einem einzelnen Importvorgang abrufen möchten.  
  
1.  Öffnen Sie auf einer SharePoint-Website die Datenfeedbibliothek oder eine andere Dokumentbibliothek, in der Sie den Inhaltstyp für Datendienste hinzugefügt und konfiguriert haben. Klicken Sie auf der Schnellstartleiste auf **Alles anzeigen** , um eine zuvor erstellte Datenfeedbibliothek zu suchen.  
  
2.  Klicken Sie im Menüband am oberen Rand der Seite unter Dokumenttools auf **Dokumente**.  
  
3.  Klicken Sie auf **Neues Dokument** , und wählen Sie anschließend **Datendienstdokument**aus.  
  
4.  Geben Sie auf der Seite Neues Datendienstdokument die folgenden Informationen ein:  
  
    1.  Einen Namen und eine Beschreibung für das Datendienstdokument. Achten Sie darauf, genügend Informationen anzugeben, damit Benutzer entscheiden können, ob sie den Feed verwenden möchten.  
  
    2.  Geben Sie in Datenfeed eine URL zu einem Datendienst oder einer Webanwendung ein, der bzw. die Daten im Atom 1.0-Format bereitstellt.  
  
         Die URL muss in einen Dienst aufgelöst werden, der strukturierte oder semistrukturierte Daten in Zeilen und Spalten zurückgibt. Der Dienst sollte Daten anonym oder über die Sicherheitsanmeldeinformationen des aktuellen Benutzers zurückgeben.  
  
         Die URL muss in einen Dienst aufgelöst werden, der die Windows-Authentifizierung, die Standardauthentifizierung oder den anonymen Zugriff unterstützt. Der Benutzer, der den Feed importiert, gibt das zu verwendende Schema an. Standardmäßig ist die integrierte Sicherheit ausgewählt.  
  
         Eine Datenfeed-URL kann Parameter enthalten. Verschiedene Arten von Datendiensttechnologien unterstützen erweiterte URL-Adressierungsschemas, die es Ihnen ermöglichen, die zu verwendenden Daten genau auszuwählen. Ein ADO.NET-Datendienst stellt z. B. URL-Parameter zum Angeben von Entitäten, Zuordnungen und Navigationspfaden in den zugrunde liegenden Daten bereit. Sie können das zu verwendende Dataset genau angeben, indem Sie eine komplexe URL als Quelle für einen Datenfeed angeben.  
  
    3.  Geben Sie für den gleichen Datenfeed einen Tabellennamen ein, der das Dataset anschließend in einer Clientanwendung identifiziert. In [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]wird jeder Datenfeed, den Sie importieren, in ein eigenes Tabellensteuerelement in einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenquelle eingefügt. Sie müssen beim Einrichten des Datenfeeds den Namen der Tabelle angeben, in die die importierten Daten eingefügt werden.  
  
5.  Klicken Sie auf Weiteren Datenfeed hinzufügen, um die vorherigen Schritte zu wiederholen und zusätzliche Feeds desselben oder eines anderen Diensts anzugeben.  
  
     Jedes Datendienstdokument wird in einem einzelnen Vorgang verarbeitet. Alle Datenfeeds im Dokument werden asynchron generiert und im gleichen Vorgang an eine Clientanwendung zurückgegeben. Geben Sie deshalb nur die URL-Tabelle-Paare für Datenfeeds an, die Sie zusammen verwenden möchten.  
  
     Da Authentifizierungsschemas auf der Ebene des Datendienstdokuments festgelegt werden, muss jeder weitere Datenfeed aus einem Dienst oder einer Anwendung stammen, der bzw. die das gleiche Authentifizierungsschema wie der erste Feed unterstützt. Alle Feeds innerhalb des gleichen Datendienstdokuments werden zur Laufzeit mit der gleichen Methode authentifiziert.  
  
6.  Speichern Sie das Dokument. Das Datendienstdokument wird als physische Datei (.atomsvc) in einer Inhaltsbibliothek gespeichert, die für diesen Inhaltstyp konfiguriert wurde.  
  
 Zur Verwendung des Datendienstdokuments können Sie in [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] eine [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] -Arbeitsmappe öffnen und im Datenimport-Assistenten die Option **Aus Datenfeed** auswählen. Wenn er dazu aufgefordert wird, gibt ein Benutzer die SharePoint-URL des Datendienstdokuments an, um einen Datenimportvorgang zu starten. Weitere Informationen finden Sie unter [Verwenden von Datenfeeds &#40;Power Pivot für SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/use-data-feeds-power-pivot-for-sharepoint.md).  
  
##  <a name="securedsdoc"></a> Sichern eines Datendienstdokuments  
 Ein Datendienstdokument erbt die Berechtigungen der Bibliothek, in der es enthalten ist. Von den für das Element festgelegten Berechtigungen wird bestimmt, ob ein Datendienstdokument von einem Benutzer geöffnet, geändert oder gelöscht werden kann.  
  
 Für die Verwendung eines Datendienstdokuments in der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Clientanwendung als Datenfeedimport benötigt ein Benutzer lediglich Anzeigeberechtigungen für das Dokument. Anzeigeberechtigungen reichen aus, um die URL im Import-Assistenten aufzulösen.  
  
 Anzeigeberechtigungen für Datendienstdokumente werden nur zu Beginn eines Datenfeed-Importvorgangs überprüft. Nach dem Import werden Dokumentberechtigungen nicht laufend kontrolliert. Einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenquelle hinzugefügte Feeds sind statische Daten, die vom Datendienstdokument getrennt wurden, in dem die ursprünglichen Verbindungsinformationen enthalten waren.  
  
 Ebenso wird das Datendienstdokument aus allen Datenaktualisierungsvorgängen ausgeschlossen, die Sie anschließend planen. Während des Imports werden Verbindungsinformationen für jeden Feed zu Aktualisierungszwecken in die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenquelle kopiert. Das bedeutet, dass Berechtigungen für ein Datendienstdokument nicht auf Datenaktualisierungen überprüft werden, da in einem Aktualisierungsvorgang nie auf das Dokument selbst verwiesen wird.  
  
|Task|SharePoint-Berechtigungsanforderungen|  
|----------|----------------------------------------|  
|Importieren von Datenfeeds in eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-fähige Arbeitsmappe.|Anzeigeberechtigungen für das Datendienstdokument in einer Bibliothek.|  
|Aktualisieren von Daten, die zuvor über einen Feed abgerufen wurden, in der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Clientanwendung.|Nicht verfügbar. Die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Clientanwendung verwendet eingebettete HTTP-Verbindungsinformationen, um eine direkte Verbindung mit den Datendiensten und -anwendungen herzustellen, die den Feed bereitstellen. Das Datendienstdokument wird von der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Clientanwendung nicht verwendet.|  
|Aktualisieren von Daten als geplanter Task in einer SharePoint-Farm, ohne dass eine Benutzereingabe erforderlich ist.|Nicht verfügbar. Der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienst verwendet eingebettete HTTP-Verbindungsinformationen, um eine direkte Verbindung mit den Datendiensten und -anwendungen herzustellen, die den Feed bereitstellen. Das Datendienstdokument wird vom [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienst nicht verwendet.|  
|Löschen eines Datendienstdokuments in einer Bibliothek.|Teilnahmeberechtigungen für die Bibliothek.|  
  
##  <a name="modifydsdoc"></a> Ändern eines Datendienstdokuments  
 Sie können einzelne URL-Tabelle-Einträge in einem Datendienstdokument hinzufügen, bearbeiten oder entfernen. Nachdem Sie die Änderungen gespeichert haben, erhalten Benutzer, die das Dienstdokument in einem neuen Importvorgang auswählen, die von Ihnen angegebenen Datenfeeds.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Arbeitsmappen, von denen eine frühere Version des Dokuments verwendet wurde, sind von den Änderungen nicht betroffen. Das liegt daran, dass ein Datendienstdokument nur einmal während des ursprünglichen Importvorgangs gelesen wird. Während des Imports werden Dienst-URL und Tabellennamen kopiert und intern in der Arbeitsmappe gespeichert. Diese internen Werte werden dann in nachfolgenden Aktualisierungsvorgängen zum Abrufen aktualisierter Daten verwendet.  
  
 Da kein persistenter Link zwischen einem Datendienstdokument auf einer SharePoint-Website und der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe besteht, die den importierten Feed enthält, haben Änderungen an Teilen des Datendienstdokuments keine Auswirkungen auf vorhandene [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen.  
  
> [!IMPORTANT]  
>  Obwohl das Datendienstdokument lediglich einmal gelesen wird, kann auf Datendienste, die die tatsächlichen Daten bereitstellen, zum Abrufen neuerer Feeds regelmäßig zugegriffen werden. Weitere Informationen zum Aktualisieren von Daten finden Sie unter [PowerPivot-Datenaktualisierung](../../analysis-services/power-pivot-sharepoint/power-pivot-data-refresh.md).  
  
##  <a name="usedsdoc"></a> Nächster Schritt: Verwenden eines Datendienstdokuments  
 Zur Verwendung eines in einer SharePoint-Bibliothek erstellten Datendienstdokuments verwenden Sie die Importoption **Aus Datenfeeds** in einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenquelle. Anweisungen finden Sie unter [Verwenden von Datenfeeds &#40;Power Pivot für SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/use-data-feeds-power-pivot-for-sharepoint.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Power Pivot-Datenfeeds](../../analysis-services/power-pivot-sharepoint/power-pivot-data-feeds.md)  
  
  

