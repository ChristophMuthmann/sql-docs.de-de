---
title: Synchronisieren von Analysis Services-Datenbanken | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Analysis Services deployments, Synchronize Database Wizard
- deploying [Analysis Services], Synchronize Database Wizard
- Synchronize Database Wizard
- synchronization [Analysis Services]
ms.assetid: 6aeff68d-8470-43fb-a3ed-a4b9685332c2
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 3bb86dbcb264f7073847cce62dc9c3e200208821
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="synchronize-analysis-services-databases"></a>Synchronisieren von Analysis Services-Datenbanken
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] umfasst eine Funktion für die Datenbanksynchronisierung, mit der zwei [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbanken auf den gleichen Stand gebracht werden, indem die Daten und Metadaten aus einer Datenbank auf einem Quellserver in eine Datenbank auf einem Zielserver kopiert werden. Die Funktion für die Datenbanksynchronisierung kann für folgende Aufgaben verwendet werden:  
  
-   Bereitstellen einer Datenbank von einem Stagingserver auf einem Produktionsserver  
  
-   Aktualisieren einer Datenbank auf einem Produktionsserver mit den Änderungen, die an den Daten und Metadaten in einer Datenbank auf einem Stagingserver vorgenommen wurden  
  
-   Generieren eines XMLA-Skripts, das zukünftig zum Synchronisieren der Datenbanken ausgeführt werden kann  
  
-   In verteilten Arbeitsauslastungen, in denen Cubes und Dimensionen auf mehreren Servern verarbeitet werden, verwenden Sie die Datenbanksynchronisierung, um die Änderungen in einer einzigen Datenbank zusammenzuführen.  
  
 Die Datenbanksynchronisierung wird auf dem Zielserver initiiert und überträgt Daten und Metadaten per Pull in eine Datenbankkopie auf dem Quellserver. Falls die Datenbank nicht vorhanden ist, wird sie erstellt. Die Synchronisierung ist ein unidirektionaler, einmaliger Vorgang, der abgeschlossen ist, nachdem die Datenbank kopiert wurde. Er gewährleistet nicht, dass zwischen den Datenbanken Parität in Echtzeit herrscht.  
  
 Sie können bereits auf einem Quell- und Zielserver enthaltene Datenbanken erneut synchronisieren, um die neuesten Änderungen von einem Stagingserver in eine Produktionsdatenbank zu übertragen. Die Dateien auf den beiden Servern werden auf Änderungen verglichen, und abweichende Dateien werden aktualisiert. Eine vorhandene Datenbank auf einem Zielserver bleibt verfügbar, während die Synchronisierung im Hintergrund ausgeführt wird. Benutzer können während einer laufenden Synchronisierung weiterhin Abfragen an die Zieldatenbank senden. Nach Beendigung der Synchronisierung werden die Benutzer von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] automatisch auf die neu kopierten Daten und Metadaten umgestellt, und die alten Daten werden aus der Zieldatenbank gelöscht.  
  
 Zum Synchronisieren von Datenbanken führen Sie den Assistenten zum Synchronisieren einer Datenbank aus, um die Datenbanken sofort zu synchronisieren, oder Sie generieren mit dem Assistenten ein Synchronisierungsskript, das Sie später ausführen können. Die Verfügbarkeit und Skalierbarkeit der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbanken und des Cubes können mit beiden Verfahren gesteigert werden.  
  
> [!NOTE]  
>  Die folgenden Whitepapers beziehen sich zwar auf frühere Versionen von Analysis Services, gelten aber weiterhin für skalierbare mehrdimensionale Lösungen, die mit SQL Server 2012 erstellt wurden. Weitere Informationen finden Sie unter [Horizontale Skalierung bei Abfragen für Analysis Services](http://go.microsoft.com/fwlink/?LinkId=253136) und [Horizontale Skalierung bei Abfragen für Analysis Services mit schreibgeschützten Datenbanken](http://go.microsoft.com/fwlink/?LinkId=253137.)  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 Auf dem Zielserver, auf dem die Datenbanksynchronisierung initiiert wird, müssen Sie Mitglied der Serveradministratorrolle von Analysis Services sein. Auf dem Quellserver muss das Windows-Benutzerkonto über Vollzugriff auf die Quelldatenbank verfügen. Wenn Sie die Datenbank interaktiv synchronisieren, sollten Sie beachten, dass die Synchronisierung im Sicherheitskontext der Windows-Benutzeridentität ausgeführt wird. Wenn dem Konto der Zugriff auf bestimmte Objekte verweigert wurde, werden diese Objekte aus dem Vorgang ausgeschlossen. Weitere Informationen zu Serveradministratorrollen und Datenbankberechtigungen finden Sie unter [Erteilen von serverweiten Administratorrechten für eine Analysis Services-Instanz](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md) und [Erteilen von Datenbankberechtigungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md).  
  
 TCP-Port 2383 muss auf beiden Servern geöffnet sein, damit Remoteverbindungen zwischen den Standardinstanzen unterstützt werden. Weitere Informationen zum Erstellen einer Ausnahme in der Windows-Firewall finden Sie unter [Configure the Windows Firewall to Allow Analysis Services Access](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
 Sowohl die Quell-und Zielservern muss die gleiche Version und Servicepack. Da die darin enthaltenen Modellmetadaten auch synchronisiert wird, sollte um Kompatibilität sicherzustellen, dass den Build Anzahl für beide Server identisch sein. Die Editionen der einzelnen Installationen müssen die Datenbanksynchronisierung unterstützen. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]wird die Datenbanksynchronisierung in der Enterprise, Developer und Business Intelligence Edition unterstützt. Weitere Informationen zu Funktionen in den einzelnen Editionen finden Sie unter [Editionen und unterstützte Funktionen für SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Der Serverbereitstellungsmodus muss auf beiden Servern identisch sein. Wenn die synchronisierte Datenbank mehrdimensional ist, müssen sowohl der Quell- als auch der Zielserver für den mehrdimensionalen Servermodus konfiguriert sein. Weitere Informationen zu Bereitstellungsmodi finden Sie unter [Determine the Server Mode of an Analysis Services Instance](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
 Deaktivieren Sie die verzögerte Aggregationsverarbeitung, falls sie auf dem Quellserver verwendet wird. Im Hintergrund verarbeitete Aggregationen können die Datenbanksynchronisierung beeinträchtigen. Weitere Informationen zum Festlegen dieser Servereigenschaft finden Sie unter [OLAP Properties](../../analysis-services/server-properties/olap-properties.md).  
  
> [!NOTE]  
>  Die Datenbankgröße trägt maßgeblich zur Entscheidung bei, ob die Synchronisierung ein geeigneter Ansatz ist. Es gibt keine festen Anforderungen, wenn die Synchronisierung jedoch zu langsam verläuft, sollten Sie die parallele Synchronisierung mehrerer Server in Betracht ziehen, die im technischen Artikel [Bewährte Methoden für die Synchronisierung in Analysis Services](http://go.microsoft.com/fwlink/?LinkID=253136)beschrieben wird.  
  
## <a name="synchronize-database-wizard"></a>Assistent zum Synchronisieren einer Datenbank  
 Verwenden Sie den Assistenten zum Synchronisieren einer Datenbank, um eine unidirektionale Synchronisierung von einer Quell- zu einer Zieldatenbank auszuführen oder um ein Skript zu generieren, in dem ein Datenbanksynchronisierungsvorgang angegeben ist. Während des Synchronisierungsvorgangs können Sie sowohl lokale als auch Remotepartitionen synchronisieren und auswählen, ob Rollen eingeschlossen werden sollen.  
  
 Mit dem Assistenten zum Synchronisieren einer Datenbank werden Sie durch die folgenden Schritte geführt:  
  
-   Wählen Sie die Quellinstanz und die Datenbank aus, von der aus synchronisiert werden soll.  
  
-   Wählen Sie Speicherorte für lokale Partitionen auf der Zielinstanz aus.  
  
-   Wählen Sie Speicherorte für Remotepartitionen auf anderen Zielinstanzen aus.  
  
-   Wählen Sie die Sicherheitsstufe und die Informationen zur Mitgliedschaft aus, die aus der Quellinstanz und der Datenbank in die Zielinstanz kopiert werden sollen.  
  
-   Wählen Sie aus, ob die Synchronisierung sofort ausgeführt werden soll oder ob der XMLA-Befehl (XML for Analysis) **Synchronize** , der vom Assistenten zum Synchronisieren einer Datenbank generiert wurde, zwecks späterer Synchronisierung in einer Skriptdatei gespeichert werden soll.  
  
 Standardmäßig synchronisiert der Assistent alle Daten und Metadaten außer der Mitgliedschaft in bestehenden Sicherheitsgruppen. Sie können beim Synchronisieren der Daten und Metadaten auch alle Sicherheitseinstellungen kopieren oder alle Sicherheitseinstellungen ignorieren.  
  
#### <a name="run-the-wizard"></a>Ausführen des Assistenten  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz her, auf der die Zieldatenbank ausgeführt wird. Wenn Sie beispielsweise eine Datenbank auf einem Produktionsserver bereitstellen, würden Sie den Assistenten auf dem Produktionsserver ausführen.  
  
2.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Ordner **Datenbanken** , und klicken Sie anschließend auf **Synchronisieren**.  
  
3.  Geben Sie den Quellserver und die Quelldatenbank an. Geben Sie auf der Seite Datenbank für die Synchronisierung auswählen unter **Quellserver** und **Quelldatenbank**den Namen des Quellservers und der Quelldatenbank ein. Wenn eine Bereitstellung beispielsweise von einer Testumgebung auf einem Produktionsserver erfolgt, entspricht die Quelle der Datenbank auf dem Stagingserver.  
  
     Unter**Zielserver** wird der Name der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz angezeigt, mit der die Daten und Metadaten aus der in **Quelldatenbank** ausgewählten Datenbank synchronisiert werden.  
  
     Die Synchronisierung wird für Quell- und Zieldatenbanken mit dem gleichen Namen ausgeführt. Wenn der Zielserver bereits über eine Datenbank mit dem gleichen Namen wie die Quelldatenbank verfügt, wird die Zieldatenbank mit den Metadaten und Daten der Quelldatenbank aktualisiert. Wenn die Datenbank nicht vorhanden ist, wird sie auf dem Zielserver erstellt.  
  
4.  Ändern Sie ggf. den Speicherort für die lokale Partition. Auf der Seite **Speicherorte für lokale Partitionen angeben** können Sie angeben, wo die lokalen Partitionen auf dem Zielserver gespeichert werden sollen.  
  
    > [!NOTE]  
    >  Diese Seite wird nur angezeigt, wenn in der angegebenen Datenbank mindestens eine lokale Partition vorhanden ist.  
  
     Wenn auf Laufwerk C: des Quellservers eine Gruppe von Partitionen installiert ist, können Sie mithilfe des Assistenten diese Partitionen an einen anderen Speicherort auf dem Zielserver kopieren. Wenn Sie die Standardspeicherorte nicht ändern, stellt der Assistent die Partitionen der Measuregruppe innerhalb eines jeden Cubes auf dem Quellserver auf denselben Speicherorten auf dem Zielserver bereit. Auf ähnliche Weise werden, wenn der Quellserver Remotepartitionen verwendet, auf dem Zielserver dieselben Remotepartitionen verwendet.  
  
     Unter der Option **Speicherorte** wird ein Raster mit dem Quellordner, dem Zielordner und der geschätzten Größe der lokalen Partitionen angezeigt, die auf der Zielinstanz gespeichert werden sollen. Das Raster enthält die folgenden Spalten:  
  
     **Quellordner**  
     Zeigt den Ordnernamen auf der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz an, die die lokale Partition enthält. Wenn die Spalte den Wert "(Standard)" enthält, muss der Standardspeicherort für die Quellinstanz die lokale Partition enthalten.  
  
     **Zielordner**  
     Zeigt den Namen des Ordners an der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Zielinstanz an, in die die lokale Partition synchronisiert werden soll. Wenn die Spalte den Wert "(Standard)" enthält, muss der Standardspeicherort für die Zielinstanz die lokale Partition enthalten.  
  
     Klicken Sie auf die Schaltfläche zum Durchsuchen (**...**), um das Dialogfeld **Nach Remoteordner suchen** aufzurufen, und geben Sie einen Ordner auf der Zielinstanz an, in die die am ausgewählten Speicherort gespeicherten lokalen Partitionen synchronisiert werden sollen.  
  
    > [!NOTE]  
    >  Diese Spalte kann für lokale Partitionen, die am Standardspeicherort für die Quellinstanz gespeichert sind, nicht geändert werden.  
  
     **Schriftgrad**  
     Zeigt die geschätzte Größe der lokalen Partition an.  
  
     Unter der Option **Partitionen am ausgewählten Speicherort** wird ein Raster angezeigt, in dem die lokalen Partitionen beschrieben werden, die am Speicherort auf der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Quellinstanz gespeichert sind, die in der Spalte **Quellordner** der ausgewählten Zeile in **Speicherorte**angegeben ist.  
  
     **Cube**  
     Zeigt den Namen des Cubes an, der die Partition enthält.  
  
     **Measuregruppe**  
     Zeigt den Namen der Measuregruppe in dem Cube an, der die Partition enthält.  
  
     **Partitionsname**  
     Zeigt den Namen der Partition an.  
  
     **Größe (MB)**  
     Zeigt die Größe der Partition in Megabytes (MB) an.  
  
5.  Ändern Sie ggf. den Speicherort für Remotepartitionen. Verwenden Sie die Seite **Speicherorte für Remotepartitionen angeben** , um anzugeben, ob Remotepartitionen, die von der angegebenen Datenbank auf dem Quellserver verwaltet werden, synchronisiert werden sollen, und um eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Zielinstanz und -Zieldatenbank festzulegen, in der die ausgewählten Remotepartitionen gespeichert werden sollen.  
  
    > [!NOTE]  
    >  Diese Seite wird nur angezeigt, wenn mindestens eine Remotepartition von der angegebenen Datenbank auf der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Quellinstanz verwaltet wird.  
  
     Unter der Option **Speicherorte** wird ein Raster mit Informationen zu Speicherorten angezeigt, an denen Remotepartitionen für die Quelldatenbank gespeichert sind. Dazu zählen Informationen zu Quelle und Ziel sowie die von den einzelnen Speicherorten verwendete Speichergröße, die in der ausgewählten Datenbank verfügbar ist. Das Raster enthält die folgenden Spalten:  
  
     **Sync**  
     Aktivieren Sie diese Option, um bei der Synchronisierung einen Speicherort hinzuzufügen, der Remotepartitionen enthält.  
  
    > [!NOTE]  
    >  Wenn diese Option nicht aktiviert ist, werden Remotepartitionen an diesem Speicherort nicht synchronisiert.  
  
     **Quellserver**  
     Zeigt den Namen der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz an, die Remotepartitionen enthält.  
  
     **Quellordner**  
     Zeigt den Ordnernamen auf der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz an, die Remotepartitionen enthält. Wenn die Spalte den Wert „(Standard)“ enthält, enthält der Standardspeicherort für die in **Quellserver** angezeigte Instanz Remotepartitionen.  
  
     **Zielserver**  
     Zeigt den Namen der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz an, in die die Remotepartitionen synchronisiert werden sollen, die an dem in **Quellserver** und **Quellordner** angegebenen Speicherort gespeichert sind.  
  
     Klicken Sie auf die Schaltfläche zum Durchsuchen (**...**), um das Dialogfeld **Verbindungs-Manager** aufzurufen, und geben Sie eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz an, in die die am ausgewählten Speicherort gespeicherten Remotepartitionen synchronisiert werden sollen.  
  
     **Zielordner**  
     Zeigt den Namen des Ordners auf der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Zielinstanz an, in die die Remotepartition synchronisiert werden soll. Wenn die Spalte den Wert "(Standard)" enthält, muss der Standardspeicherort für die Zielinstanz die Remotepartition enthalten.  
  
     Klicken Sie auf die Schaltfläche zum Durchsuchen (**...**), um das Dialogfeld **Nach Remoteordner suchen** aufzurufen, und geben Sie einen Ordner auf der Zielinstanz an, in die die am ausgewählten Speicherort gespeicherten Remotepartitionen synchronisiert werden sollen.  
  
     **Größe**  
     Zeigt die geschätzte Größe von den am Speicherort gespeicherten Remotepartitionen an.  
  
     Unter **Partitionen am ausgewählten Speicherort** wird ein Raster angezeigt, in dem die Remotepartitionen beschrieben werden, die am Speicherort auf der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Quellinstanz gespeichert sind, die in der Spalte **Quellordner** der ausgewählten Zeile in **Speicherorte**angegeben ist. Das Raster enthält die folgenden Spalten:  
  
     **Cube**  
     Zeigt den Namen des Cubes an, der die Partition enthält.  
  
     **Measuregruppe**  
     Zeigt den Namen der Measuregruppe in dem Cube an, der die Partition enthält.  
  
     **Partitionsname**  
     Zeigt den Namen der Partition an.  
  
     **Größe (MB)**  
     Zeigt die Größe der Partition in Megabytes (MB) an.  
  
6.  Geben Sie an, ob Informationen zu Benutzerberechtigungen eingeschlossen werden sollen und ob eine Komprimierung verwendet werden soll. Der Assistent komprimiert standardmäßig alle Daten und Metadaten, bevor die Dateien auf den Zielserver kopiert werden. Diese Option bewirkt eine schnellere Dateiübertragung. Sobald sie den Zielserver erreichen, werden die Dateien dekomprimiert.  
  
     **Alle kopieren**  
     Wählen Sie diese Option aus, um während der Synchronisierung Sicherheitsdefinitionen und Informationen zur Mitgliedschaft hinzuzufügen.  
  
     **Mitgliedschaft auslassen**  
     Wählen Sie diese Option aus, um während der Synchronisierung Sicherheitsdefinitionen hinzuzufügen, Informationen zur Mitgliedschaft jedoch auszuschließen.  
  
     **Alle ignorieren**  
     Wählen Sie diese Option aus, um die derzeit in der Quelldatenbank geltende Sicherheitsdefinition und Mitgliedschaftsinformationen zu ignorieren. Wenn während der Synchronisierung eine Zieldatenbank erstellt wird, werden keine Sicherheitsdefinitionen oder Mitgliedschaftsinformationen kopiert. Wenn die Zieldatenbank bereits vorhanden ist und Rollen und Mitgliedschaften aufweist, werden diese Sicherheitsinformationen beibehalten.  
  
7.  Wählen Sie die Synchronisierungsmethode aus. Sie können sofort synchronisieren oder ein Skript generieren, das in einer Datei gespeichert wird. Standardmäßig wird die Datei mit der Erweiterung .xmla im Ordner Dokumente gespeichert.  
  
8.  Klicken Sie auf **Fertig stellen** , um die Synchronisierung zu starten. Klicken Sie erneut auf **Fertig stellen** , nachdem Sie die Optionen auf der Seite **Assistenten abschließen** überprüft haben.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Wenn Sie keine Rollen oder Mitgliedschaften synchronisiert haben, achten Sie darauf, jetzt Zugriffsberechtigungen für Benutzer in der Zieldatenbank festzulegen.  
  
## <a name="see-also"></a>Siehe auch  
 [Synchronize-Element &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [Bereitstellen von Modelllösungen mit XMLA](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)   
 [Bereitstellen von Modelllösungen mithilfe des Bereitstellungs-Assistenten](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)  
  
  
