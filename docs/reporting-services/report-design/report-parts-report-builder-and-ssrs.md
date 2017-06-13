---
title: Berichtsteile (Berichts-Generator und SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10543"
ms.assetid: 957f664c-8a7a-4532-b5a6-5f859c5840bd
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 817f519ef87ae764f41634f467a554cbae04baed
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="report-parts-report-builder-and-ssrs"></a>Berichtsteile (Berichts-Generator und SSRS)
  Berichtselemente wie Tabellen, Matrizen, Diagramme und Bilder können als *Berichtsteile*veröffentlicht werden. Berichtsteile sind Elemente paginierter Berichte, die separat auf einem Berichtsserver veröffentlicht wurden und in anderen paginierten Berichten wieder verwendet werden können. Berichtsteile besitzen die Dateierweiterung ".rsc".  
  
 Dank Berichtsteilen können Arbeitsgruppen jetzt die verschiedenen Stärken und Rollen ihrer Teammitglieder optimal nutzen. Wenn Sie z. B. für das Erstellen von Diagrammen zuständig sind, können Sie die Diagramme als separate Teile speichern, die Sie und Ihre Kollegen in anderen Berichten erneut verwenden können. Sie können Berichtsteile auf einem Berichtsserver oder auf einer in einen Berichtsserver integrierten SharePoint-Website veröffentlichen. Die Berichtsteile können Sie in mehreren Berichten verwenden und auf dem Server aktualisieren.  
  
 Die Beziehung zwischen dem Berichtsteil, den Sie einem Bericht hinzufügen, und der Instanz des Berichtsteils auf der Website oder dem Server bleibt durch die Verwendung einer eindeutigen ID erhalten. Nachdem Sie einem Bericht Berichtsteile von einer Website oder einem Server hinzugefügt haben, können Sie diese unabhängig vom ursprünglichen Berichtsteil auf der Website oder dem Server ändern. Sie können Updates annehmen, die andere Personen am Berichtsteil auf der Website oder dem Server vorgenommen haben, und den geänderten Berichtsteil auf der Website oder dem Server neu speichern, indem Sie entweder einen neuen Berichtsteil hinzufügen oder die ursprüngliche Datei überschreiben, sofern Sie über entsprechende Berechtigungen dafür verfügen.  
  
##  <a name="ComponentWorkflow"></a> Lebenszyklus eines Berichtsteils  
 ![Rs_ComponentCreation](../../reporting-services/report-design/media/rs-componentcreation.gif "Rs_ComponentCreation")  
  
1.  Person A erstellt einen Bericht mit einem Diagramm, das von einem eingebetteten Dataset abhängig ist.  
  
2.  Person A entscheidet sich dafür, das Diagramm auf dem Berichtsserver zu veröffentlichen. Berichts-Generator weist dem veröffentlichten Diagramm eine eindeutige ID zu. Person A gibt das Dataset nicht frei, sodass es weiterhin in das Diagramm eingebettet ist.  
  
3.  Person B erstellt einen leeren Bericht, durchsucht den Berichtsteilkatalog, findet das Diagramm und fügt es dem Bericht hinzu. Das Diagramm ist jetzt zusammen mit dem eingebetteten Dataset Teil des Berichts von Person B. Person B kann die im Bericht enthaltenen Diagramm- und Datasetinstanzen ändern. Dies hat weder Auswirkungen auf die Diagramm- und Datasetinstanzen auf dem Berichtsserver, noch wird die Beziehung zwischen den Instanzen im Bericht und auf dem Berichtsserver unterbrochen.  
  
     ![Rs_componentupdate](../../reporting-services/report-design/media/rs-componentupdate.gif "Rs_componentupdate")  
  
4.  Person C fügt das Diagramm einem Bericht hinzu und ändert dieses Diagramm im Bericht von einem Balkendiagramm zu einem Kreisdiagramm.  
  
5.  Person C verfügt über die Berechtigung, das Diagramm auf dem Server zu überschreiben, und macht dies auch, wobei das Diagramm erneut auf dem Server veröffentlicht wird. Dadurch wird die veröffentlichte Kopie des Diagramms auf dem Server aktualisiert. Person C gibt das Dataset ebenfalls nicht frei, sodass es weiterhin in das Diagramm eingebettet ist.  
  
6.  Person B akzeptiert das aktualisierte Diagramm vom Server. Dadurch werden die Änderungen, die Person B am Diagramm im Bericht von Person B vorgenommen hatte, überschrieben.  
  
  
##  <a name="PublishingComponents"></a> Veröffentlichen von Berichtsteilen  
 Wenn Sie einen Berichtsteil veröffentlichen, weist Berichts-Generator ihm eine eindeutige ID zu, die sich vom Berichtsteilnamen unterscheidet. Berichts-Generator behält diese ID bei, unabhängig davon, welche anderen Änderungen Sie an dem Berichtsteil vornehmen. Durch die ID wird das ursprüngliche Berichtselement im Bericht mit dem Berichtsteil verknüpft. Wird der Berichtsteil von anderen Berichtsautoren wiederverwendet, wird auch der Berichtsteil in deren Berichten durch die ID mit dem Berichtsteil auf dem Berichtsserver verknüpft.  
  
 Die folgenden Berichtselemente können als Berichtsteile veröffentlicht werden:  
  
-   Diagramme  
  
-   Messgeräte  
  
-   Bilder  
  
-   Karten  
  
-   Parameter  
  
-   Rechtecke  
  
-   Tabellen  
  
-   Matrizen  
  
-   Listen  
  
 Wenn Sie ein Berichtselement veröffentlichen, in dem Daten angezeigt werden, z. B. eine Tabelle, eine Matrix oder ein Diagramm, wird das Dataset, von dem das Berichtselement abhängig ist, zusammen damit als ein darin eingebettetes Dataset gespeichert. Sie können das Dataset auch separat als freigegebenes Dataset speichern, das Sie und andere Personen als Grundlage für andere Berichtsteile verwenden können. Weitere Informationen finden Sie unter [Berichtsteile und Datasets in Berichts-Generator](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md).  
  
 Einige Berichtsteile können auch andere Berichtselemente enthalten. Eine Tabelle kann z. B. ein Diagramm enthalten, während ein Rechteck eine Matrix und ein Diagramm enthalten kann. Wenn Sie ein Berichtselement veröffentlichen, das andere Berichtselemente enthält, werden diese als Einheit gespeichert. Die anderen Berichtselemente werden in den Containerberichtsteil eingebettet gespeichert. Sie können sie weder getrennt voneinander aktualisieren noch die Elemente im Container als separate Berichtsteile speichern.  
  
 Weitere Informationen zur Veröffentlichung von Berichtsteilen finden Sie unter [Veröffentlichen und erneutes Veröffentlichen von Berichtsteilen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/publish-and-republish-report-parts-report-builder-and-ssrs.md)veröffentlicht werden.  
  
### <a name="modifying-report-part-metadata"></a>Ändern der Metadaten von Berichtsteilen  
 Sie können Berichtsteile mit den Standardeinstellungen an einem Standardspeicherort veröffentlichen oder die einzelnen Berichtsteile an einem anderen Speicherort speichern und die Metadaten (z. B. Titel und Beschreibung) ändern.  
  
 Es empfiehlt sich, einen aussagekräftigen Namen und eine klare Beschreibung für den Berichtsteil zu erstellen, wenn Sie ihn veröffentlichen, damit er bei einer Suche von anderen Personen leichter gefunden werden kann. Möglicherweise erhalten Sie viele Berichtsteile mit ähnlichen Namen auf der Website oder dem Server. Legen Sie Benennungskonventionen fest, um Beziehungen zwischen Berichtsteilen und den davon abhängigen Elementen darzustellen.  
  
 Denken Sie auch darüber nach, freigegebene Datenquellen, freigegebene Datasets und die Berichtsteile, die davon abhängig sind, im gleichen Ordner zu speichern.  
  
 Sie können auch die Beschreibung im Eigenschaftenbereich bearbeiten.  
  
  
##  <a name="ReusingComponents"></a> Wiederverwenden von Berichtsteilen  
 Die einfachste Möglichkeit zum Erstellen eines Berichts besteht darin, einen vorhandenen Berichtsteil zum Bericht im Berichtsteilkatalog hinzuzufügen, beispielsweise eine Tabelle oder ein Diagramm. Nachdem Sie dem Bericht den Berichtsteil hinzugefügt haben, können Sie diesen nach Bedarf ändern oder Updates vom Server akzeptieren. Eine Änderung des Berichtselements in Ihrem Bericht wirkt sich nicht auf die Instanz des Berichtsteils aus, die auf der Website oder dem Server veröffentlicht wurde. Auch die Beziehung zwischen der Instanz im Bericht und der Instanz auf der Website oder dem Server bleibt bestehen. Wenn Sie über ausreichende Berechtigungen verfügen, können Sie die aktualisierte Kopie auf der Website oder auf dem Server erneut speichern. Wenn eine andere Person die Kopie auf der Website oder dem Server ändert, können Sie Ihre Kopie in ihrem momentanen Zustand beibehalten oder sie aktualisieren, damit sie der Kopie auf der Website oder dem Server entspricht.  
  
### <a name="searching-for-report-parts"></a>Suchen nach Berichtsteilen  
 Im Berichtsteilkatalog können Sie nach Berichtsteilen suchen, die Sie Ihrem Bericht hinzufügen möchten. Sie können die Berichtsteile nach dem gesamten Namen oder einem Teil des Namens, nach der Person, die sie erstellt oder zuletzt geändert hat, nach dem letzten Änderungsdatum, dem Speicherort oder dem Typ des Berichtsteils filtern. Sie konnten z. B. nach allen Diagrammen suchen, die in der vorhergehenden Woche von einem oder mehreren Ihrer Kollegen erstellt wurden.  
  
 Sie können die Suchergebnisse als Miniaturansichten oder in Listenform anzeigen und nach Name, Erstellungs- und Änderungsdatum und dem Ersteller sortieren. Weitere Informationen finden Sie unter [Suchen nach Berichtsteilen und Festlegen eines Standardordners &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)veröffentlicht werden.  
  
### <a name="what-comes-with-a-report-part"></a>Zugehörige Elemente zu einem Berichtsteil  
 Wenn Sie dem Bericht einen Berichtsteil hinzufügen, werden damit auch alle für die Verarbeitung erforderlichen Elemente hinzugefügt. Beispielsweise ist jedes angezeigte Objekt von einem Dataset (d. h., einer Abfrage und einer Verbindung zu einer Datenquelle) abhängig. Möglicherweise verfügt es auch über einen oder mehrere Parameter. Alle Elemente, von denen es abhängig ist, werden als *Abhängigkeiten*bezeichnet. Diese Elemente und Verweise auf diese Elemente sind im Berichtsteil enthalten, wenn Sie ihn dem Bericht hinzufügen. Das Dataset und die Parameter werden im Berichtsdatenbereich des Berichts aufgeführt.  
  
 Das Dataset für den Berichtsteil kann in den Berichtsteil eingebettet oder ein separates freigegebenes Dataset sein, auf den der Berichtsteil verweist. Wenn es in den Berichtsteil eingebettet ist, können Sie es möglicherweise ändern. Wenn es ein freigegebenes Dataset ist, ist es ein separates Objekt, für das Sie die entsprechenden Berechtigungen benötigen. Weitere Informationen zu freigegebenen und eingebetteten Datasets finden Sie unter [Berichtsdatasets &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md).  
  
### <a name="resolving-naming-conflicts"></a>Lösen von Namenskonflikten  
 Wenn Sie einen Berichtsteil hinzufügen, löst Berichts-Generator alle Namenskonflikte. Wenn beispielsweise bereits ein Diagramm1 in Ihrem Bericht vorhanden ist und Sie einen Berichtsteil namens Diagramm1 hinzufügen, benennt Berichts-Generator den neuen Berichtsteil automatisch in Diagramm2 um. Wenn der Bericht bereits ein Dataset1 enthält und Sie einen Berichtsteil hinzufügen, der auf ein anderes Dataset mit dem Namen Dataset1 verweist, benennt Berichts-Generator das neue Dataset in Dataset2 um und aktualisiert die Verweise.  
  
### <a name="adding-more-than-one-report-part"></a>Hinzufügen von mehreren Berichtsteilen  
 Sie können dem Bericht eine unbegrenzte Anzahl von Berichtsteilen hinzufügen. Sie können jedoch immer nur jeweils einen Berichtsteil hinzufügen. Sie können dem gleichen Bericht sogar mehrere Instanzen desselben Berichtsteils hinzufügen. Diese verfügen alle über eindeutige Namen, sind jedoch Instanzen des gleichen Berichtsteils auf dem Server und haben die gleiche eindeutige ID.  
  
 Wenn Sie einen anderen Berichtsteil hinzufügen, der ein mit einem bereits im Bericht verwendeten Dataset identisch ist, fügt der Assistent dem Bericht keine andere Version dieses Datasets hinzu. Es leitet die Verweise im Berichtsteil um, sodass Sie auf das vorhandene Dataset verweisen. Weitere Informationen finden Sie unter [Berichtsteile und Datasets in Berichts-Generator](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md).  
  
  
##  <a name="UpdatingComponents"></a> Aktualisieren von Berichtsteilen mit Änderungen vom Server  
 Jedes Mal, wenn Sie einen Bericht öffnen, überprüft der Berichts-Generator, ob die Serverinstanzen der Berichtsteile in diesem Bericht auf dem Server aktualisiert wurden. Er überprüft auch Änderungen in den abhängigen Elementen des Berichtsteils, z. B. im Dataset und den Parametern. Wenn veröffentlichte Berichtsteile oder ihre Abhängigkeiten auf dem Server aktualisiert wurden, zeigt eine Informationsleiste im Bericht die Anzahl der aktualisierten Berichtsteile an. Sie können die Updates anzeigen und akzeptieren oder ablehnen oder die Informationsleiste schließen. Wenn Sie die Updates anzeigen, wird Ihnen eine Miniaturansicht des Berichtsteils mit den Angaben zur Person, die die letzten Änderungen daran vorgenommen hat, und das Änderungsdatum angezeigt. Danach können Sie beliebige oder alle aktualisierten Elemente akzeptieren.  
  
> [!NOTE]  
>  Sie können die Informationsleiste deaktivieren, wenn Sie nicht über Änderungen eines Berichtsteils informiert werden möchten. Diese Option wird beim Hinzufügen des Berichtsteils zum Bericht festgelegt. Auch wenn Sie die Informationsleiste deaktiviert haben, können Sie weiterhin nach Updates suchen. Weitere Informationen finden Sie unter [Suchen nach Updates oder Deaktivieren von Updates (Berichts-Generator und SSRS)](http://msdn.microsoft.com/en-us/9c69792d-d7c4-453b-ae2f-6d2d071d8606).  
  
 Der Berichts-Generator überprüft, ob Unterschiede zwischen dem Datum des letzten Updates des Berichtsteils auf dem Server und dem Datum der letzten Synchronisierung des Berichtsteils mit dem Server bestehen. Er überprüft nicht das Datum, an dem Sie den Berichtsteil im Bericht geändert haben. So kann es sein, dass der Berichtsteil im Bericht und der Berichtsteil auf dem Server sich erheblich unterscheiden, Berichts-Generator jedoch keine Änderungen findet, wenn er nach Updates sucht.  
  
### <a name="accepting-updates"></a>Akzeptieren von Updates  
 Wenn Sie ein Update für einen Berichtsteil annehmen, ersetzt dieses die Kopie des bereits im Bericht befindlichen Berichtsteils vollständig. Sie können Funktionen des Berichtsteils im Bericht nicht mit Funktionen des veröffentlichten Berichtsteils auf dem Server kombinieren. Wenn Sie jedoch eine der Abhängigkeiten des Berichtsteils (z. B. ein eingebettetes Dataset) geändert haben, überschreibt Berichts-Generator die bereits im Bericht befindliche Abhängigkeit im Bericht nicht. Er lädt eine neue Kopie der Abhängigkeit herunter und aktualisiert den Berichtsteil, sodass er auf die neue Kopie verweist.  
  
### <a name="reverting-to-a-previous-version-of-a-report-part"></a>Wiederherstellen der früheren Version eines Berichtsteils  
 Wenn Sie eine Version eines Berichtsteils im Bericht geändert haben und es durch die Version ersetzen möchten, die sich auf dem Server befindet, können Sie dazu nicht das Dialogfeld **Aktualisieren** verwenden. Updates sind nur für Berichtsteile möglich, die sich auf dem Server geändert haben, seit Sie sie heruntergeladen haben.  
  
 Um die Version auf dem Server wiederherzustellen, löschen Sie einfach die Version im Bericht, und fügen Sie sie erneut hinzu.  
  
  
##  <a name="RepublishingComponents"></a> Aktualisieren von Berichtsteilen, die sich bereits auf dem Server befinden  
 Sie können einen vorhandenen Berichtsteil auf dem Server aktualisieren oder ihn als neuen Berichtsteil veröffentlichen, ohne den vorhandenen Berichtsteil zu ersetzen. Wenn Sie den Berichtsteil auf dem Server aktualisieren, werden Kopien des Berichtsteils in anderen Berichten nicht automatisch ebenfalls geändert. Wenn andere Berichtsautoren diesen Berichtsteil einem Bericht hinzugefügt haben, werden Sie über die Änderung informiert, wenn sie diesen Bericht das nächste Mal öffnen. Sie können die Änderungen annehmen oder ablehnen.  
  
 Wenn Sie den Berichtsteil als neuen Berichtsteil veröffentlichen möchten, gibt Berichts-Generator ihm eine neue eindeutige ID, und es besteht kein Link zum ursprünglichen Berichtsteil mehr.  
  
 Wenn das Dataset in den Berichtsteil eingebettet wird, wird das Dataset jedes Mal, wenn Sie den Berichtsteil veröffentlichen, im Dialogfeld **Berichtselemente veröffentlichen** angezeigt. Freigegebene Datasets werden nicht im Dialogfeld **Berichtselemente veröffentlichen** angezeigt.  
  
  
##  <a name="RptPartsRptDesigner"></a> Arbeiten mit Berichtsteilen in Berichts-Designer  
 Die Funktion von Berichtsteilen unterscheidet sich in Berichts-Designer in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. In Berichts-Designer verläuft die Veröffentlichung in einer Richtung: Sie können zwar einen Berichtsteil aus Berichts-Designer veröffentlichen, jedoch keinen vorhandenen Berichtsteil in Berichts-Designer wiederverwenden. Weitere Informationen finden Sie unter [Berichtsteile im Berichts-Designer &#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md).  
  
##  <a name="HowTo"></a> Themen zur Vorgehensweise  
 [Veröffentlichen und erneutes Veröffentlichen von Berichtsteilen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/publish-and-republish-report-parts-report-builder-and-ssrs.md)  
  
 [Suchen nach Berichtsteilen und Festlegen eines Standardordners &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)  
  
 [Suchen nach Updates oder Deaktivieren von Updates (Berichts-Generator und SSRS)](http://msdn.microsoft.com/en-us/9c69792d-d7c4-453b-ae2f-6d2d071d8606)  
  
## <a name="see-also"></a>Siehe auch  
 [Berichtsteile und Datasets in Berichts-Generator](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [Problembehandlung bei Berichtsteilen (Berichts-Generator und SSRS)](http://msdn.microsoft.com/en-us/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [Verwalten von Berichtsteilen](../../reporting-services/report-design/managing-report-parts.md)  
  
  
