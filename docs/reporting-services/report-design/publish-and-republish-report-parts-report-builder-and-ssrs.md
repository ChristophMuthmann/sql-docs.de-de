---
title: "Veröffentlichen und erneutes Veröffentlichen von Berichtsteilen (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 92dce484-f39b-403c-9caf-d8772bc3aca3
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 03b06d981e4ff824fbdca3f598271fce666237af
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="publish-and-republish-report-parts-report-builder-and-ssrs"></a>Veröffentlichen und erneutes Veröffentlichen von Berichtsteilen (Berichts-Generator und SSRS)
  Berichtsteile sind Elemente paginierter Berichte, die separat auf einem Berichtsserver veröffentlicht wurden und in anderen paginierten Berichten wieder verwendet werden können. Sie können einen Berichtsteil mit den Standardeinstellungen an einem Standardspeicherplatz veröffentlichen oder Metadaten eines Berichtsteils wie Name und Beschreibung bearbeiten und danach an einem anderen Ort auf dem Berichtsserver speichern. Außerdem können Sie ihn auf einer SharePoint-Website speichern, die in einen Berichtsserver integriert ist, wenn Sie die erforderlichen Berechtigungen dafür haben.  
  
 Sie können nur den Berichtsteil oder den Berichtsteil mit dem davon abhängigen Dataset, das darin eingebettet wurde, veröffentlichen. Sie können jedoch auch das Dataset getrennt davon veröffentlichen. Wenn Sie das Dataset separat veröffentlichen, wird es zu einem freigegebenen Dataset, und der Berichtsteil wird damit verknüpft. Weitere Informationen finden Sie unter [Berichtsteile und Datasets](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md).  
  
 Sie können einen vorhandenen Berichtsteil erneut veröffentlichen. Wenn Sie über die entsprechenden Berechtigungen verfügen, können Sie die ursprüngliche Instanz des Berichtsteils auf dem Server überschreiben, auch wenn Sie diese nicht erstellt haben. Sie können ihn auch als neuen Berichtsteil veröffentlichen und am gleichen Speicherort oder einem anderen Speicherort speichern.  
  
## <a name="to-publish-a-report-part"></a>So veröffentlichen Sie einen Berichtsteil  
  
1.  Klicken Sie im Menü von Berichts-Generator auf **Berichtselemente veröffentlichen**.  
  
     Wenn Sie keine Verbindung mit einem Berichtsserver hergestellt haben, werden Sie dazu aufgefordert, eine Verbindung herzustellen. Wenn Sie keine Verbindung mit einem Berichtsserver herstellen können, können Sie auch keine Berichtsteile veröffentlichen.  
  
2.  Um die Berichtsteile mit den Standardeinstellungen am Standardspeicherort zu speichern, klicken Sie auf **Alle Berichtselemente mit Standardeinstellungen verwenden**.  
  
     Klicken Sie andernfalls auf **Überprüfen und ändern Sie Berichtselemente vor der Veröffentlichung**.  
  
3.  Bearbeiten Sie den Namen und die Beschreibung des Berichtsteils. Doppelklicken Sie dazu auf den Namen, um ihn zu bearbeiten, und klicken Sie in das Feld **Beschreibung** , um eine Beschreibung hinzuzufügen.  
  
    > [!NOTE]  
    >  Es empfiehlt sich, einen Namen und eine Beschreibung für den Berichtsteil zu erstellen, damit er bei einer Suche von anderen Personen leichter gefunden werden kann. Die maximale Länge des Namens eines Berichtsteils beträgt 260 Zeichen für den gesamten Pfad einschließlich der Namen der Ordner auf dem Server, gefolgt von dem tatsächlichen Namen des Berichtsteils.  
  
4.  Wenn Sie den Berichtsteil nicht im Standardordner speichern möchten, klicken Sie auf die Schaltfläche **Durchsuchen** .  
  
5.  Klicken Sie auf **Veröffentlichen**, nachdem Sie die Optionen für alle Berichtsteile im Bericht festgelegt haben.  
  
     Nach dem Veröffentlichen der Berichtsteile wird im Dialogfeld angezeigt, welche Berichtsteile erfolgreich veröffentlicht wurden und welche nicht. Details zu den Berichtsteilen, die nicht veröffentlicht werden konnten, können im Dialogfeld **Berichtsteile veröffentlichen** angezeigt werden.  
  
6.  Klicken Sie auf **Schließen**.  
  
## <a name="to-republish-a-report-part"></a>So veröffentlichen Sie einen Berichtsteil erneut  
  
1.  Gehen Sie wie im Folgenden beschrieben vor, um einen Berichtsteil erneut zu veröffentlichen.  
  
2.  Wenn Sie im Dialogfeld **Berichtselemente veröffentlichen** auf **Als neue Kopie des Berichtselements veröffentlichen**klicken, überschreibt Berichts-Generator beim Speichern den vorhandenen Berichtsteil auf dem Server nicht, sondern erstellt stattdessen einen anderen Berichtsteil.  
  
> [!NOTE]  
>  Wenn Sie diesen als neuen Berichtsteil veröffentlichen, verfügt er über eine neue eindeutige ID. Er wird nicht mehr aktualisiert, wenn sich der ursprüngliche Berichtsteil ändert.  
  
## <a name="see-also"></a>Siehe auch  
 [Berichtsteile &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)   
 [Berichtsteile und Datasets im Berichts-Generator](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [Problembehandlung bei Berichtsteilen (Berichts-Generator und SSRS)](http://msdn.microsoft.com/en-us/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [Suchen nach Updates oder Deaktivieren von Updates (Berichts-Generator und SSRS)](http://msdn.microsoft.com/en-us/9c69792d-d7c4-453b-ae2f-6d2d071d8606)   
 [Suchen nach Berichtsteilen und Festlegen eines Standardordners &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)  
  
  

