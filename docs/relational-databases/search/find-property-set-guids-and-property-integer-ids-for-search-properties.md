---
title: "Suchen von Eigenschaftensatz-GUIDS und ganzzahligen Eigenschaft-IDs für Sucheigenschaften | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search property lists [SQL Server], configuring
ms.assetid: 7db79165-8bcc-4be6-8d40-12d44deda79f
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d234dc5d1d44c11c50483505898586ab5e845a77
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="find-property-set-guids-and-property-integer-ids-for-search-properties"></a>Suchen von Eigenschaftensatz-GUIDS und ganzzahligen Eigenschaft-IDs für Sucheigenschaften
  In diesem Thema wird erläutert, wie Sie die Werte, die Sie vor dem Hinzufügen einer Eigenschaft zu einer Sucheigenschaftenliste benötigen, abrufen und für die Volltextsuche durchsuchbar machen. Zu diesen Werten zählen die Eigenschaftensatz-GUID und der ganzzahlige Eigenschaftsbezeichner einer Dokumenteigenschaft.  
  
 Dokumenteigenschaften, die von IFilters aus Binärdaten extrahiert werden, d. h. aus Daten, die in einer Spalte vom Datentyp **varbinary**, **varbinary(max)** (einschließlich **FILESTREAM**) oder **image** gespeichert sind, können für die Volltextsuche verfügbar gemacht werden. Um eine extrahierte Eigenschaft durchsuchbar zu machen, muss sie manuell einer Sucheigenschaftenliste hinzugefügt werden. Darüber hinaus muss der Sucheigenschaftenliste mindestens ein Volltextindex zugeordnet werden. Weitere Informationen finden Sie unter [Suchen von Dokumenteigenschaften mithilfe von Sucheigenschaftenlisten](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
 Bevor Sie eine verfügbare Eigenschaft einer Eigenschaftenliste hinzufügen können, müssen Sie die folgenden zwei Informationen zur Eigenschaft ermitteln:  
  
-   Die Eigenschaftensatz-GUID der Eigenschaft.  
  
-   Die ganzzahlige ID der Eigenschaft.  
  
 (Beim Hinzufügen einer Eigenschaft zu einer Eigenschaftenliste müssen Sie auch einen Namen und eine Beschreibung angeben. Es ist jedoch nicht erforderlich, den kanonischen Namen und die kanonische Beschreibung der Eigenschaft zu verwenden.)  
  
 In diesem Thema werden die am häufigsten verwendeten Methoden für die Suche nach Informationen zu verfügbaren, von Microsoft definierten Eigenschaften beschrieben. Informationen zu Eigenschaften, die von einem Drittanbieter definiert wurden, finden Sie in der Dokumentation des Drittanbieters, oder wenden Sie sich an den Anbieter.  
  
##  <a name="wellknown"></a> Suchen von Informationen zu häufig verwendeten, bekannten Microsoft-Eigenschaften  
 Microsoft definiert Hunderte von Dokumenteigenschaften, die in vielen Kontexten verwendet werden können. Es wird jedoch nur eine kleine Teilmenge der verfügbaren Eigenschaften für jedes Dateiformat verwendet. Zu den häufig verwendeten Windows-Eigenschaften zählen auch einige wenige generische Eigenschaften. Einige Beispiele für bekannte generische Eigenschaften werden in der folgenden Tabelle aufgelistet. In der Tabelle werden der bekannte Name, der kanonische Windows-Name (aus der von Microsoft veröffentlichten Eigenschaftenbeschreibung), die Eigenschaftensatz-GUID, der ganzzahlige Eigenschaftsbezeichner und eine kurze Beschreibung aufgelistet.  
  
|Bekannter Name|Kanonischer Windows-Name|Eigenschaftensatz-GUID|Ganzzahlige ID|Beschreibung|  
|----------------------|----------------------------|-----------------------|----------------|-----------------|  
|Authors|**System.Author**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|4|Autor oder Autoren eines angegebenen Elements.|  
|Tags|**System.Keywords**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|5|Satz von Schlüsselwörtern (die auch als Tags bezeichnet werden), die dem Element zugewiesen sind.|  
|Typ|**System.PerceivedType**|28636AA6-953D-11D2-B5D6-00C04FD918D0|9|Auf der Grundlage des zugehörigen kanonischen Typs erkannter Dateityp.|  
|Titel|**System.Title**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|2|Titel des Elements. Dabei kann es sich z. B. um den Titel eines Dokuments, den Betreff einer Nachricht, die Beschriftung eines Fotos oder den Namen eines Musiktitels handeln.|  
  
 Um die Einheitlichkeit unter den Dateiformaten zu fördern, hat Microsoft Teilmengen von häufig verwendeten Dokumenteigenschaften mit hoher Priorität für verschiedene Kategorien von Dokumenten angegeben. Hierzu zählen Nachrichten, Kontakte, Dokumente, Musikdateien, Bilder und Videos. Weitere Informationen zu den wichtigsten Eigenschaften für die einzelnen Kategorien finden Sie unter [Systemdefinierte Eigenschaften für benutzerdefinierte Dateiformate](http://go.microsoft.com/fwlink/?LinkId=144336) in der Windows Search-Dokumentation.  
  
 Ein Dateiformat kann Eigenschaften der folgenden drei Typen implementieren:  
  
-   Von [!INCLUDE[msCoName](../../includes/msconame-md.md)]definierte generische Eigenschaften  
  
-   Von [!INCLUDE[msCoName](../../includes/msconame-md.md)]definierte kategoriespezifische Eigenschaften  
  
-   Vom Softwareanbieter definierte benutzerdefinierte, anwendungsspezifische Eigenschaften  
  
##  <a name="filtdump"></a> Suchen von Informationen zu verfügbaren Eigenschaften mit FILTDUMP.EXE  
 Wenn Sie feststellen möchten, welche Eigenschaften von einem installierten IFilter erkannt und extrahiert werden, können Sie das Hilfsprogramm **filtdump.exe** , das Teil des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows SDK ist, installieren und ausführen.  
  
 **filtdump.exe** wird über die Eingabeaufforderung mit nur einem Argument ausgeführt. Dieses Argument ist der Name einer einzelnen Datei mit einem Dateityp, für den ein IFilter installiert ist. Das Hilfsprogramm zeigt eine Liste aller vom IFilter im Dokument erkannten Eigenschaften mit ihren Eigenschaftensatz-GUIDs, ganzzahligen IDs und weiteren Informationen an.  
  
 Informationen zum Installieren dieser Software finden Sie unter [Microsoft Windows SDK für Windows 7 und .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=212980). Nachdem Sie das SDK heruntergeladen und installiert haben, suchen Sie in den folgenden Ordnern nach dem Hilfsprogramm "filtdump.exe".  
  
-   Informationen zur 64-Bit-Version finden Sie unter `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin\x64`.  
  
-   Informationen zur 32-Bit-Version finden Sie unter `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin`.  
  
##  <a name="propdesc"></a> Suchen von Werten für eine Sucheigenschaft mithilfe einer Windows-Eigenschaftenbeschreibung  
 Bei einer bekannten Windows-Sucheigenschaft können Sie die erforderlichen Informationen aus den **formatID** - und **propID** -Attributen der Eigenschaftenbeschreibung (**propertyDescription**) abrufen.  
  
 Im folgenden Beispiel wird der relevante Teil einer typischen Microsoft-Eigenschaftenbeschreibung veranschaulicht. Hier wird die `System.Author` -Eigenschaft dargestellt. Das `formatID` -Attribut gibt die Eigenschaftensatz-GUID ( `F29F85E0-4FF9-1068-AB91-08002B27B3D9`) an und das `propID` -Attribut die ganzzahlige Eigenschaften-ID ( `4.` ). Beachten Sie, dass das `name` -Attribut den kanonischen Windows-Eigenschaftennamen ( `System.Author`) angibt. (In diesem Beispiel wurden nicht relevante Teile der Eigenschaftenbeschreibung weggelassen.)  
  
```  
.  
propertyDescription  
name = System.Author  
…  
formatID = F29F85E0-4FF9-1068-AB91-08002B27B3D9  
propID = 4  
…  
```  
  
 Eine vollständige Beschreibung dieser Eigenschaft finden Sie unter [System.Author](http://go.microsoft.com/fwlink/?LinkId=144337) in der Windows Search-Dokumentation.  
  
 Eine vollständige Liste der Windows-Eigenschaften finden Sie ebenfalls in der Windows Search-Dokumentation unter [Windows-Eigenschaften](http://go.microsoft.com/fwlink/?LinkId=215013).  
  
##  <a name="examples"></a> Hinzufügen einer Eigenschaft zu einer Sucheigenschaftenliste  
 Das folgende Beispiel zeigt, wie einer Sucheigenschaftenliste eine Eigenschaft hinzugefügt wird. Im Beispiel wird einer Sucheigenschaftenliste mit dem Namen [mithilfe einer](../../t-sql/statements/alter-search-property-list-transact-sql.md) ALTER SEARCH PROPERTY LIST `System.Author` -Anweisung die `PropertyList1`-Eigenschaft hinzugefügt und für die Eigenschaft der Anzeigename `Author`angegeben.  
  
```  
ALTER SEARCH PROPERTY LIST PropertyList1   
  ADD 'Author'  
    WITH (  
          PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9',  
          PROPERTY_INT_ID = 4,   
          PROPERTY_DESCRIPTION = 'System.Author - the author or authors of the item'   
         )  
GO  
```  
  
 Weitere Informationen zum Erstellen einer Sucheigenschaftenliste und Zuordnen eines Volltextindexes finden Sie unter [Suchen von Dokumenteigenschaften mithilfe von Sucheigenschaftenlisten](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Suchen von Dokumenteigenschaften mithilfe von Sucheigenschaftenlisten](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [Konfigurieren und Verwalten von Filtern für die Suche](../../relational-databases/search/configure-and-manage-filters-for-search.md)  
  
  
