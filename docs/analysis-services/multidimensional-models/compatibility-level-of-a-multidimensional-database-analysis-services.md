---
title: "Kompatibilitätsgrad einer mehrdimensionalen Datenbank (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 978279e6-a581-4184-af9d-8701b9826a89
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0055b4c33a489d13ee7feac39f179505d76d50e9
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="compatibility-level-of-a-multidimensional-database-analysis-services"></a>Kompatibilitätsgrad einer mehrdimensionalen Datenbank (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], die Datenbank-kompatibilitätsgradeigenschaft bestimmt die Funktionsebene einer Datenbank. Kompatibilitätsgrade sind für jeden Modelltyp spezifisch. Abhängig davon, ob die Datenbank mehrdimensional oder tabellarisch ist, hat ein Kompatibilitätsgrad von **1100** beispielsweise eine unterschiedliche Bedeutung.  
  
 In diesem Thema wird nur der Kompatibilitätsgrad für mehrdimensionale Datenbanken beschrieben. Weitere Informationen zu tabellarischen Lösungen finden Sie unter [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).  
  
> [!NOTE]  
>  Tabellarische Modelle verfügen über zusätzliche Datenbank-Kompatibilitätsgrade, die für mehrdimensionale Modelle nicht gelten. Bei mehrdimensionalen Modellen gibt es keinen Kompatibilitätsgrad **1103** . Weitere Informationen zum Kompatibilitätsgrad [1103](http://go.microsoft.com/fwlink/?LinkId=301727) für tabellarische Lösungen finden Sie unter **Neuerungen beim tabellarischen Modell in SQL Server 2012 SP1 und dem Kompatibilitätsgrad** .  
  
 **Kompatibilitätsgrade für mehrdimensionale Datenbanken**  
  
 Das einzige Verhalten mehrdimensionaler Datenbanken, das derzeit im Hinblick auf die Funktionsebene abweicht, ist die Zeichenfolgenspeicherarchitektur. Wenn Sie den Kompatibilitätsgrad einer Datenbank erhöhen, können Sie den Höchstwert von 4 GB für den Zeichenfolgenspeicher überschreiben, in dem Measures und Dimensionen gespeichert sind.  
  
 Bei einer mehrdimensionalen Datenbank lauten die gültigen Werte für die **CompatibilityLevel** -Eigenschaft wie folgt:  
  
|Einstellung|Description|  
|-------------|-----------------|  
|**1050**|Dieser Wert ist in Skripts oder Tools nicht sichtbar, entspricht aber Datenbanken, die in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]oder [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]erstellt wurden. Alle Datenbanken, für die **CompatibilityLevel** nicht explizit festgelegt wurde, werden implizit mit Grad **1050** ausgeführt.|  
|**1100**|Dies ist der Standardwert für neue Datenbanken, die Sie in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] oder [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]erstellen. Sie können diesen auch für Datenbanken angeben, die in früheren Versionen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] erstellt wurden, um die Verwendung von Funktionen zu ermöglichen, die nur unter diesem Kompatibilitätsgrad unterstützt werden (d. h., größerer Zeichenfolgenspeicher für Dimensionsattribute oder Distinct Count Measures, die Zeichenfolgendaten enthalten).<br /><br /> Datenbanken mit einem **CompatibilityLevel** von **1100** erhalten zusätzlich die **StringStoresCompatibilityLevel**-Eigenschaft, über die Sie einen alternativen Zeichenfolgenspeicher für Partitionen und Dimensionen auswählen.|  
  
> [!WARNING]  
>  Das Festlegen der Datenbankkompatibilität auf einen höheren Grad ist nicht umkehrbar. Nach dem Erhöhen des Kompatibilitätsgrads auf **1100**müssen Sie die Datenbank auf neueren Servern ausführen. Sie können kein Rollback auf **1050**ausführen. Sie können eine Datenbank mit dem Kompatibilitätsgrad **1100** nicht auf einer früheren Serverversion als [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] oder [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]anfügen oder wiederherstellen.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 Datenbank-Kompatibilitätsgrade werden mit [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]eingeführt. Sie müssen über [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oder höher verfügen, um den Datenbank-Kompatibilitätsgrad anzuzeigen oder festzulegen.  
  
 Die Datenbank darf kein lokaler Cube sein. Lokale Cubes bieten keine Unterstützung der **CompatibilityLevel** -Eigenschaft.  
  
 Die Datenbank muss in einer früheren Version (SQL Server 2008 R2 oder früher) erstellt worden und dann an einen Server der Version [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oder höher angefügt oder dort wiederhergestellt worden sein. Für SQL Server 2012 bereitgestellte Datenbanken verfügen bereits über **1100** und können nicht zur Ausführung unter einem niedrigeren Grad herabgestuft werden.  
  
## <a name="determine-the-existing-database-compatibility-level-for-a-multidimensional-database"></a>Bestimmen des bestehenden Datenbank-Kompatibilitätsgrads für eine mehrdimensionale Datenbank  
 XMLA ist die einzige Möglichkeit, den Datenbank-Kompatibilitätsgrad anzuzeigen oder zu ändern. Das XMLA-Skript, durch das die Datenbank in SQL Server Management Studio angegeben wird, kann angezeigt oder geändert werden.  
  
 Wenn Sie die XMLA-Definition einer Datenbank nach der **CompatibilityLevel** -Eigenschaft durchsuchen, diese aber nicht vorhanden ist, verfügt die Datenbank höchstwahrscheinlich über den Kompatibilitätsgrad **1050** .  
  
 Anweisungen zum Anzeigen und Ändern des XMLA-Skripts finden Sie im nächsten Abschnitt.  
  
## <a name="set-the-database-compatibility-level-in-sql-server-management-studio"></a>Festlegen des Datenbank-Kompatibilitätsgrads in SQL Server Management Studio  
  
1.  Bevor Sie den Kompatibilitätsgrad erhöhen, sollten Sie die Datenbank sichern, damit Änderungen später bei Bedarf rückgängig gemacht werden können.  
  
2.  Stellen Sie mit SQL Server Management Studio eine Verbindung mit dem [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Server her, der die Datenbank hostet.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Datenbanknamen, zeigen Sie auf **Skript für Datenbank als**, zeigen Sie auf **ALTER in**, und wählen Sie dann **Neues Abfrage-Editor-Fenster**aus. Eine XMLA-Darstellung der Datenbank wird in einem neuen Fenster geöffnet.  
  
4.  Kopieren Sie das folgende XML-Element:  
  
    ```  
    <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
    ```  
  
5.  Fügen Sie es nach dem schließenden `</Annotations>` -Element und vor dem `<Language>` -Element ein. Die XML sollte ähnlich wie im folgenden Beispiel aussehen:  
  
    ```  
    </Annotations>  
    <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
    <Language>1033</Language>  
    ```  
  
6.  Speichern Sie die Datei.  
  
7.  Klicken Sie zum Ausführen des Skripts im Menü Abfrage auf **Ausführen** , oder drücken Sie F5.  
  
## <a name="supported-operations-that-require-the-same-compatibility-level"></a>Unterstützte Vorgänge, die denselben Kompatibilitätsgrad erfordern  
 Die folgenden Vorgänge erfordern, dass die Quelldatenbanken denselben Kompatibilitätsgrad verwenden.  
  
1.  Das Zusammenführen von Partitionen aus verschiedenen Datenbanken wird nur unterstützt, wenn beide Datenbanken denselben Kompatibilitätsgrad verwenden.  
  
2.  Für die Verwendung verknüpfter Dimensionen aus einer anderen Datenbank ist derselbe Kompatibilitätsgrad erforderlich. Wenn Sie z.B. eine verknüpfte Dimension aus einer [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] -Datenbank in einer [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] -Datenbank verwenden möchten, müssen Sie die [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] -Datenbank auf einen [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] -Server portieren und den Kompatibilitätsgrad auf **1100**festlegen.  
  
3.  Das Synchronisieren von Servern wird nur für Server unterstützt, die dieselbe Version und denselben Datenbank-Kompatibilitätsgrad verwenden.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Nachdem Sie den Datenbank-Kompatibilitätsgrad erhöht haben, können Sie die **StringStoresCompatibilityLevel** -Eigenschaft in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]festlegen. Dadurch wird der Zeichenfolgenspeicher für Measures und Dimensionen vergrößert. Weitere Informationen zu dieser Funktion finden Sie unter [Konfigurieren des Zeichenfolgenspeichers für Dimensionen und Partitionen](../../analysis-services/multidimensional-models/configure-string-storage-for-dimensions-and-partitions.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern, Wiederherstellen und Synchronisieren von Datenbanken &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
