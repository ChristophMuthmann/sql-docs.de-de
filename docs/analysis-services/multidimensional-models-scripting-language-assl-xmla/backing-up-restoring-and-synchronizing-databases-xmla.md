---
title: Sichern, wiederherstellen und Synchronisieren von Datenbanken (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- restoring databases [XML for Analysis]
- backing up databases [XML for Analysis]
- database backups [XML for Analysis]
- synchronization [XML for Analysis]
- database restores [XML for Analysis]
ms.assetid: 6c021b2e-6ad0-444e-b23f-4b5f72ce084b
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7155763db87be5c44ae9e5718d3d72939380038b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="backing-up-restoring-and-synchronizing-databases-xmla"></a>Sichern, Wiederherstellen und Synchronisieren von Datenbanken (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]In XML for Analysis gibt es drei Befehle für die sichern, wiederherstellen und Synchronisieren von Datenbanken:  
  
-   Die [Backup](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) Befehl sichert eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank mithilfe einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Sicherungsdatei (.abf), wie beschrieben im Abschnitt [Sichern von Datenbanken](#backing_up_databases).  
  
-   Die [wiederherstellen](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) -Befehl wird eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank aus einer ABF-Datei, wie beschrieben im Abschnitt [Wiederherstellen von Datenbanken](#restoring_databases).  
  
-   Die [Synchronize](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) -Befehl synchronisiert eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank mit den Daten und Metadaten von einer anderen Datenbank, wie beschrieben im Abschnitt [Synchronisieren von Datenbanken](#synchronizing_databases).  
  
##  <a name="backing_up_databases"></a>Sichern von Datenbanken  
 Wie oben erwähnt: die **Backup** Befehl sichert eine angegebene [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank in einer Sicherungsdatei. Die **Backup** Befehl verfügt über verschiedene Eigenschaften, mit denen Sie, die angeben zu sichernde Datenbank die Sicherungsdatei zu verwenden, wie Sie von sicherheitsdefinitionen sowie die zu sichernden Remotepartitionen sichern.  
  
> [!IMPORTANT]  
>  Das Analysis Services-Dienstkonto muss über die Berechtigung zum Schreiben von Daten in den für jede Datei angegebenen Sicherungsspeicherort verfügen. Dem Benutzer muss zudem eine der folgenden Rollen zugewiesen worden sein: Administratorrolle für die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz oder Mitglied einer Datenbankrolle mit der Berechtigung Vollzugriff (Administrator) für die wiederherzustellende Datenbank.  
  
### <a name="specifying-the-database-and-backup-file"></a>Angeben der Datenbank und der Sicherungsdatei  
 Die Datenbank gesichert werden soll, Sie legen die [Objekt](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) Eigenschaft von der **Sicherung** Befehl. Die **Objekt** Eigenschaft muss einen Objektbezeichner für eine Datenbank enthalten, oder ein Fehler auftritt.  
  
 Um die Datei anzugeben, die erstellt und der im Sicherungsprozess verwendet werden, legen Sie die [Datei](../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md) Eigenschaft von der **Backup** Befehl. Die **Datei** Eigenschaft sollte festgelegt werden, auf einen UNC-Pfad und Dateinamen für die Sicherungsdatei erstellt werden soll.  
  
 Sie können nicht nur angeben, welche Datei für die Sicherung verwendet werden soll, sondern Sie können auch die folgenden Optionen für die angegebene Sicherungsdatei festlegen:  
  
-   Wenn Sie festlegen, die [AllowOverwrite](../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md) Eigenschaft auf "true", die **Backup** Befehl überschreibt die Sicherungsdatei aus, wenn die angegebene Datei bereits vorhanden ist. Wenn Sie festlegen, die **AllowOverwrite** -Eigenschaft auf "false", ein Fehler auftritt, wenn die angegebene Sicherungsdatei bereits vorhanden ist.  
  
-   Wenn Sie festlegen, die [ApplyCompression](../../analysis-services/xmla/xml-elements-properties/applycompression-element-xmla.md) Eigenschaft auf "true", die Sicherungsdatei komprimiert wird, nachdem die Datei erstellt wurde.  
  
-   Wenn Sie festlegen, die [Kennwort](../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md) Eigenschaft auf einen nicht leeren Wert, die Sicherungsdatei mithilfe des angegebenen Kennworts verschlüsselt.  
  
    > [!IMPORTANT]  
    >  Wenn **ApplyCompression** und **Kennwort** Eigenschaften sind nicht angegeben ist, speichert die Sicherungsdatei Benutzernamen und Kennwörter, die enthalten sind, in Verbindungszeichenfolgen in Klartext. Daten, die in Klartext gespeichert werden, können abgerufen werden. Verwenden Sie zur Erhöhung der Sicherheit der **ApplyCompression** und **Kennwort** für beide Einstellungen komprimieren und verschlüsseln die Sicherungsdatei.  
  
### <a name="backing-up-security-settings"></a>Sichern von Sicherheitseinstellungen  
 Die [Sicherheit](../../analysis-services/xmla/xml-elements-properties/security-element-xmla.md) Eigenschaft bestimmt, ob die **Sicherung** Befehl sichert die sicherheitsdefinitionen wie Rollen und Berechtigungen definiert werden, auf ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank. Die **Sicherheit** -Eigenschaft bestimmt auch, ob die Sicherungsdatei enthält, die Windows-Benutzerkonten und Gruppen als Mitglieder der sicherheitsdefinitionen definiert.  
  
 Der Wert, der die **Sicherheit** Eigenschaft ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*SkipMembership*|Einbeziehen von Sicherheitsdefinitionen und Ausschließen von Informationen zur Mitgliedschaft in der Sicherungsdatei.|  
|*CopyAll*|Einbeziehen von Sicherheitsdefinitionen und Informationen zur Mitgliedschaft in der Sicherungsdatei.|  
|*IgnoreSecurity*|Ausschließen von Sicherheitsdefinitionen aus der Sicherungsdatei.|  
  
### <a name="backing-up-remote-partitions"></a>Sichern von Remotepartitionen  
 Zum Sichern von Remotepartitionen in der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank Festlegen der [BackupRemotePartitions](../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md) Eigenschaft von der **Sicherung** -Befehls auf "true". Diese Einstellung bewirkt, dass die **Backup** Befehl aus, um eine remotesicherungsdatei für jede Remotedatenquelle zu erstellen, die zum Speichern von Remotepartitionen für die Datenbank verwendet wird.  
  
 Für jede Remotedatenquelle gesichert werden soll, können Sie eine entsprechende Sicherungsdatei angeben, indem Sie z. B. eine [Speicherort](../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) Element in der [Speicherorte](../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md) Eigenschaft von der **Backup** -Befehl. Die **Speicherort** -Element seine **Datei** -Eigenschaft auf den UNC-Pfad und Dateinamen der remotesicherungsdatei, festgelegt und die zugehörige [DataSourceID](../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md) -Eigenschaft auf den Bezeichner des die Remotedatenquelle, die in der Datenbank definiert.  
  
##  <a name="restoring_databases"></a>Wiederherstellen von Datenbanken  
 Die **wiederherstellen** Befehl wird ein angegebenes wiederhergestellt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank aus einer Sicherungsdatei. Die **wiederherstellen** Befehl verfügt über verschiedene Eigenschaften, mit denen Sie angeben, dass die Datenbank wiederhergestellt, die Sicherungsdatei zu verwendende Vorgehensweise beim Wiederherstellen von sicherheitsdefinitionen, die zu speichernden Remotepartitionen und das Verschieben relationaler OLAP (ROLAP) -Objekte.  
  
> [!IMPORTANT]  
>  Für jede Sicherungsdatei muss der Benutzer, der den Wiederherstellungsbefehl ausführt, über die Berechtigung zum Lesen von dem für jede Datei angegebenen Sicherungsspeicherort verfügen. Zum Wiederherstellen einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank, die nicht auf dem Server installiert ist, muss der Benutzer zusätzlich Mitglied der Serverrolle für die betreffende [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz sein. Zum Überschreiben einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Datenbank muss der Benutzer entweder Mitglied der Serverrolle für die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz oder Mitglied einer Datenbankrolle mit den Berechtigungen Vollzugriff (Administrator) für die wiederherzustellende Datenbank sein.  
  
> [!NOTE]  
>  Nach dem Wiederherstellen einer vorhandenen Datenbank verliert der Benutzer, der die Datenbank wiederhergestellt hat, möglicherweise den Zugriff auf diese Datenbank. Dies ist u. U. der Fall, wenn der Benutzer zum Zeitpunkt der Sicherung kein Mitglied der Serverrolle oder der Datenbankrolle mit der Berechtigung "Vollzugriff (Administrator)" war.  
  
### <a name="specifying-the-database-and-backup-file"></a>Angeben der Datenbank und der Sicherungsdatei  
 Die **DatabaseName** Eigenschaft von der **wiederherstellen** -Befehls muss einen Objektbezeichner für eine Datenbank enthalten, oder ein Fehler auftritt. Wenn die angegebene Datenbank bereits vorhanden ist, die **AllowOverwrite** -Eigenschaft bestimmt, ob die vorhandene Datenbank überschrieben wird. Wenn die **AllowOverwrite** Eigenschaft auf "false" festgelegt ist und die angegebene Datenbank bereits vorhanden ist, ein Fehler auftritt.  
  
 Sollten Sie festlegen, die **Datei** Eigenschaft von der **wiederherstellen** Befehls auf einen UNC-Pfad und Dateinamen der Sicherungsdatei in der angegebenen Datenbank wiederhergestellt werden. Sie können auch Festlegen der **Kennwort** -Eigenschaft für die angegebene Sicherungsdatei. Wenn die **Kennwort** Eigenschaft auf einen nicht leeren Wert festgelegt ist, wird die Sicherungsdatei mithilfe des angegebenen Kennworts entschlüsselt. Wenn die Sicherungsdatei nicht verschlüsselt ist oder wenn das angegebene Kennwort nicht mit dem für die Entschlüsselung der Sicherungsdatei verwendeten Kennwort übereinstimmt, tritt ein Fehler auf.  
  
### <a name="restoring-security-settings"></a>Wiederherstellen von Sicherheitseinstellungen  
 Die **Sicherheit** Eigenschaft bestimmt, ob die **wiederherstellen** Befehl stellt die sicherheitsdefinitionen wie Rollen und Berechtigungen, die auf definierten ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank. Die **Sicherheit** -Eigenschaft bestimmt auch, ob die **wiederherstellen** Befehl enthält, die Windows-Benutzerkonten und Gruppen als Mitglieder der sicherheitsdefinitionen definiert sind, im Rahmen des Wiederherstellungsvorgangs.  
  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*SkipMembership*|Einbeziehen von Sicherheitsdefinitionen und Ausschließen von Informationen zur Mitgliedschaft in der Datenbank.|  
|*CopyAll*|Einbeziehen von Sicherheitsdefinitionen und Informationen zur Mitgliedschaft in der Datenbank.|  
|*IgnoreSecurity*|Ausschließen von Sicherheitsdefinitionen aus der Datenbank.|  
  
### <a name="restoring-remote-partitions"></a>Wiederherstellen von Remotepartitionen  
 Für jede remotesicherungsdatei erstellt, die während eines zuvor ausgeführten **Backup** Befehl, Sie können die zugeordnete Remotepartition wiederherstellen, indem Sie z. B. eine **Speicherort** Element in der **Speicherorte**Eigenschaft von der **wiederherstellen** Befehl. Die [DataSourceType](../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md) Eigenschaft für die einzelnen **Speicherort** -Element muss ausgeschlossen oder explizit auf festgelegt *Remote*.  
  
 Für jedes angegebene **Speicherort** Element, das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Instanz kontaktiert der Remotedatenquelle, die im angegebenen der **DataSourceID** Eigenschaft zum Wiederherstellen der Partitionen in der remotesicherungsdatei definiert im angegebenen der **Datei** Eigenschaft. Neben den **DataSourceID** und **Datei** Eigenschaften, die folgenden Eigenschaften stehen für die einzelnen **Speicherort** Element verwendet, um eine Remotepartition wiederherstellen:  
  
-   Überschreiben Sie die Verbindungszeichenfolge für die Remotedatenquelle im angegebenen **DataSourceID**, können Sie festlegen der **"ConnectionString"** Eigenschaft von der **Speicherort** Element ein andere Verbindungszeichenfolge. Die **wiederherstellen** Befehl verwendet die Verbindungszeichenfolge, die in enthalten ist dann die **"ConnectionString"** Eigenschaft. Wenn **"ConnectionString"** nicht angegeben wird, die **wiederherstellen** Befehl verwendet die Verbindungszeichenfolge, die in der Sicherungsdatei für die angegebene Remotedatenquelle gespeichert. Sie können die **"ConnectionString"** Einstellung aus, um eine Remotepartition auf eine andere Remoteinstanz zu verschieben. Allerdings können keine der **"ConnectionString"** Einstellung aus, um eine Remotepartition auf der gleichen Instanz wiederherzustellen, die die wiederhergestellte Datenbank enthält. Das heißt, Sie können keine der **"ConnectionString"** Eigenschaft, um eine Remotepartition in eine lokale Partition umzuwandeln.  
  
-   Für jeden ursprünglichen Ordner zum Speichern von Remotepartitionen in der Remotedatenquelle verwendet wird, geben Sie einen [Ordner](../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md) Element an den neuen Ordner, in dem alle im ursprünglichen Ordner gespeicherte Remotepartitionen wiederherzustellen. Wenn eine **Ordner** Element nicht angegeben wird, die **wiederherstellen** Befehl verwendet die ursprünglichen Ordner für die, die in der remotesicherungsdatei enthaltenen Remotepartitionen angegeben.  
  
### <a name="relocating-rolap-objects"></a>Verschieben von ROLAP-Objekten  
 Die **wiederherstellen** Befehl kann nicht wiederhergestellt, Aggregationen oder Daten für Objekte, die ROLAP-Speichermodus verwenden, da solche Informationen in Tabellen in einer zugrunde liegenden relationalen Datenquelle gespeichert ist. Jedoch können die Metadaten für ROLAP-Objekte wiederhergestellt werden. Zum Wiederherstellen der Metadaten für ROLAP-Objekte, die **wiederherstellen** Befehl wird die Tabellenstruktur in einer relationalen Datenquelle neu erstellt.  
  
 Können Sie die **Speicherort** Element in einem **wiederherstellen** Befehl aus, um die ROLAP-Objekte zu verschieben. Für jede **Speicherort** Element zum Verschieben einer Datenquelle verwendet den **DataSourceType** Eigenschaft muss explizit festgelegt werden, um *lokale*. Außerdem müssen Sie festlegen der **"ConnectionString"** Eigenschaft der **Speicherort** Element an der Verbindungszeichenfolge für den neuen Speicherort. Während der Wiederherstellung der **wiederherstellen** Befehl wird die Verbindungszeichenfolge für die Datenquelle identifiziert durch Ersetzen der **DataSourceID** Eigenschaft von der **Speicherort** Element mit dem Wert der **"ConnectionString"** Eigenschaft von der **Speicherort** Element.  
  
##  <a name="synchronizing_databases"></a>Synchronisieren von Datenbanken  
 Die **Synchronize** -Befehl synchronisiert die Daten und Metadaten eines angegebenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank mit einer anderen Datenbank. Die **Synchronize** Befehl verfügt über verschiedene Eigenschaften, mit denen Sie die Quelldatenbank angeben, wie sicherheitsdefinitionen, die zu synchronisierenden Remotepartitionen und die Synchronisierung von ROLAP-Objekte synchronisiert.  
  
> [!NOTE]  
>  Die **Synchronize** Befehl kann nur von Serveradministratoren und Datenbankadministratoren ausgeführt werden. Sowohl die Quell- als auch die Zieldatenbank müssen den gleichen Datenbank-Kompatibilitätsgrad besitzen.  
  
### <a name="specifying-the-source-database"></a>Angeben der Quelldatenbank  
 Die [Quelle](../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md) Eigenschaft von der **Synchronize** -Befehl enthält zwei Eigenschaften **"ConnectionString"** und **Objekt**. Die **"ConnectionString"** Eigenschaft enthält die Verbindungszeichenfolge der Instanz, die die Quelldatenbank enthält und die **Objekt** Eigenschaft enthält die Objekt-ID für die Quelldatenbank.  
  
 Die Zieldatenbank ist die aktuelle Datenbank für die Sitzung, in dem die **Synchronize** -Befehl ausgeführt wird.  
  
 Wenn die **ApplyCompression** Eigenschaft von der **synchronisieren** Befehlssatz ist auf "true", die aus der Quelle gesendete Informationen wird die Datenbank in die Zieldatenbank vor dem Senden komprimiert.  
  
### <a name="synchronizing-security-settings"></a>Synchronisieren von Sicherheitseinstellungen  
 Die [SynchronizeSecurity](../../analysis-services/xmla/xml-elements-properties/synchronizesecurity-element-xmla.md) Eigenschaft bestimmt, ob die **Synchronize** -Befehl synchronisiert die sicherheitsdefinitionen wie Rollen und Berechtigungen, die für die Quelldatenbank definiert. Die **SynchronizeSecurity** -Eigenschaft bestimmt auch, ob die **synchronisieren** Befehl enthält, die Windows-Benutzerkonten und Gruppen als Mitglieder der sicherheitsdefinitionen definiert.  
  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*SkipMembership*|Einbeziehen von Sicherheitsdefinitionen und Ausschließen von Informationen zur Mitgliedschaft in der Zieldatenbank.|  
|*CopyAll*|Einbeziehen von Sicherheitsdefinitionen und Informationen zur Mitgliedschaft in der Zieldatenbank.|  
|*IgnoreSecurity*|Ausschließen von Sicherheitsdefinitionen aus der Zieldatenbank.|  
  
### <a name="synchronizing-remote-partitions"></a>Synchronisieren von Remotepartitionen  
 Für jede Remotedatenquelle, die in der Quelldatenbank vorhanden ist, können Sie jede zugeordnete Remotepartition synchronisieren, indem Sie z. B. eine **Speicherort** Element in der **Speicherorte** Eigenschaft von der  **Synchronisieren** Befehl. Für jede **Speicherort** Element, das **DataSourceType** Eigenschaft muss ausgeschlossen oder explizit auf festgelegt *Remote*.  
  
 Definieren und Herstellen einer Verbindung mit einer Remotedatenquelle in der Zieldatenbank die **synchronisieren** Befehl verwendet die Verbindungszeichenfolge, die definiert, der **"ConnectionString"** Eigenschaft von der **Speicherort**  Element. Die **Synchronize** -Befehl verwendet dann die **DataSourceID** Eigenschaft von der **Speicherort** Element, um die zu synchronisierenden Remotepartitionen zu identifizieren. Die **Synchronize**-Befehl synchronisiert die Remotepartitionen für die Remotedatenquelle im angegebenen der **DataSourceID** Eigenschaft für die Quelldatenbank mit der in der angegebeneRemotedatenquelle **DataSourceID** Eigenschaft in der Zieldatenbank.  
  
 Sie können auch angeben, für die einzelnen ursprünglichen Ordner zum Speichern von Remotepartitionen in der Remotedatenquelle der Quelldatenbank verwendet, eine **Ordner** Element in der **Speicherort** Element. Die **Ordner** Element gibt den neuen Ordner für die Zieldatenbank, in dem alle im ursprünglichen Ordner in der Remotedatenquelle gespeicherten Remotepartitionen synchronisiert. Wenn eine **Ordner** Element nicht angegeben ist, der Synchronize-Befehl verwendet die ursprünglichen Ordner angegeben für Remotepartitionen, die in der Quelldatenbank enthalten sind.  
  
### <a name="synchronizing-rolap-objects"></a>Synchronisieren von ROLAP-Objekten  
 Die **Synchronize** Befehl kann nicht synchronisiert, Aggregationen oder Daten für Objekte, die ROLAP-Speichermodus verwenden, da solche Informationen in Tabellen in einer zugrunde liegenden relationalen Datenquelle gespeichert ist. Jedoch können die Metadaten für ROLAP-Objekte synchronisiert werden. Beim Synchronisieren der Metadaten der **Synchronize** Befehl erstellt die Tabellenstruktur in einer relationalen Datenquelle.  
  
 Sie können die **Speicherort** Element in einem Synchronize-Befehl zum Synchronisieren von ROLAP-Objekten. Für jede **Speicherort** Element zum Verschieben einer Datenquelle verwendet den **DataSourceType** Eigenschaft muss explizit festgelegt werden, um *lokale*. zugreifen. Außerdem müssen Sie festlegen der **"ConnectionString"** Eigenschaft der **Speicherort** Element an der Verbindungszeichenfolge für den neuen Speicherort. Während der Synchronisierung der **Synchronize** Befehl wird die Verbindungszeichenfolge für die Datenquelle identifiziert durch Ersetzen der **DataSourceID** Eigenschaft von der **Speicherort** Element mit dem Wert, der die **"ConnectionString"** Eigenschaft von der **Speicherort** Element.  
  
## <a name="see-also"></a>Siehe auch  
 [Backup-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)   
 [Restore-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [Synchronize-Element &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [Sichern und Wiederherstellen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
