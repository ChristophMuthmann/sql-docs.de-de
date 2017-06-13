---
title: Aktivieren und Deaktivieren von RDL-Sandkasten | Microsoft Docs
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d5619e9f-ec5b-4376-9b34-1f74de6fade7
caps.latest.revision: 9
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2a435c6f6b5dc2d9df676f504837393d448820a4
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="enable-and-disable-rdl-sandboxing"></a>Aktivieren und Deaktivieren von RDL-Sandkasten
  Mithilfe der Sandkastenfunktion der RDL (Report Definition Language, Berichtsdefinitionssprache) können Sie die Verwendung bestimmter Ressourcentypen durch einzelne Mandanten in einer Umgebung erkennen und einschränken, in der mehrere Mandanten eine einzelne Webfarm von Berichtsservern verwenden. Ein Beispiel hierfür ist ein Szenario mit einem Hostingdienst, in dem eine einzelne Webfarm mit Berichtsservern verwaltet wird, die von mehreren Mandanten und möglicherweise auch unterschiedlichen Firmen verwendet werden. Als Berichtsserveradministrator können Sie diese Funktion aktivieren, um die folgenden Zielsetzungen zu erreichen:  
  
-   Beschränken der Größen externer Ressourcen. Externe Ressourcen sind Bilder, XSLT-Dateien und Kartendaten.  
  
-   Beschränken der Typen und Elemente, die in Ausdruckstext verwendet werden, zum Veröffentlichungszeitpunkt des Berichts.  
  
-   Beschränken der Länge des Texts und der Größe des Rückgabewerts für Ausdrücke zur Berichtsverarbeitungszeit.  
  
 Bei Aktivierung des RDL-Sandboxing werden die folgenden Funktionen deaktiviert:  
  
-   Benutzerdefinierter Code in der  **\<Code >** -Element einer Berichtsdefinition.  
  
-   RDL-Abwärtskompatibilitätsmodus für benutzerdefinierte Berichtselemente von [!INCLUDE[ssRSversion2005](../../includes/ssrsversion2005-md.md)] .  
  
-   Benannte Parameter in Ausdrücken.  
  
 In diesem Thema wird beschrieben, jedes Element in der \< **RDLSandboxing**>-Element in der Datei "rsreportserver.config". Weitere Informationen zum Ändern dieser Datei finden Sie unter [Ändern einer Reporting Services-Konfigurationsdatei &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md). In einem Server-Ablaufverfolgungsprotokoll werden Aktivitäten aufgezeichnet, die sich auf die RDL-Sandboxingfunktion beziehen. Weitere Informationen zu Ablaufverfolgungsprotokollen finden Sie unter [Berichtsserverdienst-Ablaufverfolgungsprotokoll](../../reporting-services/report-server/report-server-service-trace-log.md).  
  
## <a name="example-configuration"></a>Beispielkonfiguration  
 Das folgende Beispiel zeigt die Einstellungen und Beispielwerte für die \< **RDLSandboxing**>-Element in der Datei "rsreportserver.config".  
  
```  
<RDLSandboxing>  
   <MaxExpressionLength>5000</MaxExpressionLength>  
   <MaxResourceSize>5000</MaxResourceSize>  
   <MaxStringResultLength>3000</MaxStringResultLength>  
   <MaxArrayResultLength>250</MaxArrayResultLength>  
   <Types>  
      <Allow Namespace=”System.Drawing” AllowNew=”True”>Bitmap</Allow>  
      <Allow Namespace=”TypeConverters.Custom” AllowNew=”True”>*</Allow>  
   </Types>  
   <Members>  
      <Deny>Format</Deny>  
      <Deny>StrDup</Deny>  
   </Members>  
</RDLSandboxing>  
```  
  
## <a name="configuration-settings"></a>Konfigurationseinstellungen  
 Die folgende Tabelle enthält Informationen zu Konfigurationseinstellungen. Diese Einstellungen werden in der Reihenfolge aufgeführt, in der sie in der Konfigurationsdatei angezeigt werden.  
  
|Einstellung|Description|  
|-------------|-----------------|  
|**MaxExpressionLength**|Maximale Anzahl von Zeichen, die in RDL-Ausdrücken zugelassen sind.<br /><br /> Standard: 1000|  
|**MaxResourceSize**|Maximale Anzahl von KB, die für eine externe Ressource zugelassen sind.<br /><br /> Standard: 100|  
|**MaxStringResultLength**|Maximale Anzahl von Zeichen, die für einen Rückgabewert für einen RDL-Ausdruck zugelassen sind.<br /><br /> Standard: 1000|  
|**MaxArrayResultLength**|Maximale Anzahl von Elementen, die für einen Rückgabewert vom Typ "Array" für einen RDL-Ausdruck zugelassen sind.<br /><br /> Standard: 100|  
|**Typen**|Die Liste der Elemente, die innerhalb von RDL-Ausdrücken zugelassen sind.|  
|**Allow**|Ein Typ oder ein Satz von Typen, die in RDL-Ausdrücken zugelassen sind.|  
|**Namespace**|Attribut für **Erlauben** , das den Namespace darstellt, der mindestens einen gültigen Typ für Value enthält. Bei dieser Eigenschaft wird die Groß-/Kleinschreibung nicht beachtet.|  
|**AllowNew**|Boolesches Attribut für **zulassen** , die steuert, ob neue Instanzen des Typs in RDL-Ausdrücken oder einem RDL erstellt werden dürfen  **\<Klasse >** Element.<br /><br /> Hinweis: Wenn **RDLSandboxing** aktiviert ist, können in RDL-Ausdrücken keine neuen Arrays erstellt werden, unabhängig von der Einstellung von **AllowNew**.|  
|**Wert**|Wert für **Allow** , der den Namen des in RDL-Ausdrücken zuzulassenden Typs angibt. Der Wert **\*** gibt an, dass alle Typen im Namespace zugelassen werden. Bei dieser Eigenschaft wird die Groß-/Kleinschreibung nicht beachtet.|  
|**Element**|Die Liste der Typen, die in eingeschlossen werden sollen, werden die  **\<Typen >** -Element, das die Liste der Elementnamen, die in RDL-Ausdrücken nicht zulässig sind.|  
|**Verweigern**|Der Name eines Elements, das nicht in RDL-Ausdrücken zugelassen wird. Bei dieser Eigenschaft wird die Groß-/Kleinschreibung nicht beachtet.<br /><br /> Hinweis: Wenn **Deny** für ein Element angegeben wird, werden alle Elemente mit diesem Namen für alle Typen nicht zugelassen.|  
  
## <a name="working-with-expressions-when-rdl-sandboxing-is-enabled"></a>Arbeiten mit Ausdrücken bei aktiviertem RDL-Sandboxing  
 Sie können die RDL-Sandboxingfunktion auf die folgenden Weisen ändern, um die von einem Ausdruck verwendeten Ressourcen zu verwalten:  
  
-   Schränken Sie die Anzahl von Zeichen ein, die für einen Ausdruck verwendet werden.  
  
-   Schränken Sie die Größe des Ergebnisses ein, das von einem Ausdruck zurückgegeben wird.  
  
-   Lassen Sie eine bestimmte Liste von Typen zu, die in einem Ausdruck verwendet werden können.  
  
-   Schränken Sie die Liste der Elemente anhand ihrer Namen für die Liste von zulässigen Typen ein, die in einem Ausdruck verwendet werden können.  
  
-   Mithilfe der RDL-Sandboxingfunktion können Sie eine Liste genehmigter Typen und eine Liste verweigerter Elemente erstellen. Die Liste der genehmigten Typen wird als Zulassungsliste bezeichnet. Die Liste der verweigerten Elemente wird als Sperrliste bezeichnet.  
  
> [!NOTE]  
>  In der Berichtsdefinition ist der Typ der einzelnen Instanzen eines Ausdrucksverweises nicht angegeben. Wenn Sie der Sperrliste ein Element hinzufügen, verweigern Sie alle Elemente dieses Namens für alle Typen in der Zulassungsliste.  
  
 Ergebnisse von RDL-Ausdrücken werden zur Laufzeit überprüft. RDL-Ausdrücke werden in die Berichtsdefinition überprüft, wenn der Bericht veröffentlicht wird. Überwachen Sie das Ablaufverfolgungsprotokoll des Berichtsservers auf Verstöße. Weitere Informationen finden Sie unter [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md).  
  
### <a name="working-with-types"></a>Arbeiten mit Typen  
 Wenn Sie der Zulassungsliste einen Typ hinzufügen, steuern Sie die folgenden Einstiegspunkte, um auf RDL-Ausdrücke zuzugreifen:  
  
-   Statische Elemente eines Typs.  
  
-   Die [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] **New** method.  
  
-   Die  **\<Klassen >** Element in der Berichtsdefinition.  
  
-   Elemente, die Sie der Sperrliste für einen Typ in der Zulassungsliste hinzugefügt haben.  
  
 Die Zulassungsliste steuert die folgenden Einstiegspunkte nicht:  
  
-   Berichtsdatasets. Felder in Berichtsdatasets, die von Abfragen zurückgegeben werden, können jeden gültigen RDL-Typ enthalten.  
  
-   Berichtsparameter. Vom Benutzer bereitgestellte Parameterwerte könnten jeden gültigen RDL-Typ enthalten.  
  
-   Elemente eines aktivierten Typs, die nicht in der Sperrliste enthalten sind. Standardmäßig werden alle Elemente aller Typen in der Zulassungsliste aktiviert. Wenn Sie der Sperrliste einen Elementnamen hinzufügen, verweigern Sie alle Elemente dieses Namens für alle Typen in der Zulassungsliste.  
  
 Um ein Element eines Typs zu aktivieren, aber ein Element mit dem gleichen Namen für einen anderen Typ zu verweigern, gehen Sie wie folgt vor:  
  
-   Hinzufügen einer  **\<Deny >** Element für den Elementnamen.  
  
-   Erstellen Sie ein Proxyelement mit einem anderen Namen für eine Klasse in einer benutzerdefinierten Assembly für das Element, das Sie aktivieren möchten.  
  
-   Fügen Sie der Zulassungsliste diese neue Klasse hinzu.  
  
 Um der Zulassungsliste [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Funktionen für .NET Framework hinzuzufügen, fügen Sie die entsprechenden Typen aus dem Namespace „Microsoft.VisualBasic“ zur Zulassungsliste hinzu.  
  
 Um der Zulassungsliste [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Typschlüsselwörter für .NET Framework hinzuzufügen, fügen Sie der Zulassungsliste den entsprechenden CLR-Typ hinzu. Beispielsweise verwenden die [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework-Schlüsselwort **Ganzzahl**, fügen Sie die folgenden XML-Fragment in der  **\<RDLSandboxing >** Element:  
  
```  
<Allow Namespace="System">Int32</Allow>  
```  
  
 Um der Zulassungsliste einen generischen Typ oder einen [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Typ für .NET Framework hinzuzufügen, der NULL-Werte zulässt, führen Sie folgende Aktionen aus.  
  
-   Erstellen Sie einen Proxytyp für den generischen Typ oder den [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Typ für .NET Framework, der NULL-Werte zulässt.  
  
-   Fügen Sie der Zulassungsliste den Proxytyp hinzu.  
  
 Indem Sie einen Typ aus einer benutzerdefinierten Assembly der Zulassungsliste hinzufügen, gewähren Sie nicht implizit die Ausführungsberechtigung für die Assembly. Sie müssen die Codezugriffs-Sicherheitsdatei spezifisch ändern und die  Ausführungsberechtigung für die Assembly bereitstellen. Weitere Informationen finden Sie unter [Code Access Security in Reporting Services](../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md).  
  
#### <a name="maintaining-the-deny-list-of-members"></a>Verwalten der \<verweigern > Liste von Elementen  
 Wenn Sie der Zulassungsliste einen neuen Typ hinzufügen, verwenden Sie die folgende Liste, um zu bestimmen, wann Sie die Sperrliste von Elementen möglicherweise aktualisieren müssen:  
  
-   Wenn Sie eine benutzerdefinierte Assembly mit einer Version aktualisieren, in der neue Typen eingeführt werden.  
  
-   Wenn Sie den Typen in der Zulassungsliste Elemente hinzufügen.  
  
-   Wenn Sie den [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] auf dem Berichtsserver aktualisieren.  
  
-   Wenn Sie den Berichtsserver auf eine höhere Version von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]aktualisieren.  
  
-   Wenn Sie einen Berichtsserver aktualisieren, um ein späteres RDL-Schema verarbeiten zu können, da RDL-Typen möglicherweise neue Elemente hinzugefügt wurden.  
  
### <a name="working-with-operators-and-new"></a>Arbeiten mit Operatoren und "New"  
 Standardmäßig werden [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Sprachoperatoren für .NET Framework außer **New**immer zugelassen. Die **neu** Operator wird gesteuert, indem die **AllowNew** -Attribut auf die  **\<zulassen >** Element. Andere Sprachoperatoren, wie z. B. der standardmäßige Auflistungsungsaccessoroperator **!** und [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Umwandlungsmakros von .NET Framework wie **CInt**sind immer zulässig.  
  
 Das Hinzufügen von Operatoren, einschließlich benutzerdefinierter Operatoren, zu einer Sperrliste wird nicht unterstützt. Um Operatoren für einen Typ auszuschließen, gehen Sie wie folgt vor:  
  
-   Erstellen Sie einen Proxytyp, der die auszuschließenden Operatoren nicht implementiert.  
  
-   Fügen Sie der Zulassungsliste den Proxytyp hinzu.  
  
 Um in einem RDL-Ausdruck ein neues Array zu erstellen, erstellen Sie das Array in einer Methode für eine Klasse, die Sie definieren, und fügen Sie der Zulassungsliste diese Klasse hinzu.  
  
 Um in einem RDL-Ausdruck ein neues Array zu erstellen, gehen Sie wie folgt vor:  
  
-   Definieren Sie eine neue Klasse, und erstellen Sie das Array in einer Methode für diese Klasse.  
  
-   Fügen Sie der Zulassungsliste die Klasse hinzu.  
  
## <a name="see-also"></a>Siehe auch  
 [RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Berichtsserverdienst-Ablaufverfolgungsprotokoll](../../reporting-services/report-server/report-server-service-trace-log.md)  
  
  
