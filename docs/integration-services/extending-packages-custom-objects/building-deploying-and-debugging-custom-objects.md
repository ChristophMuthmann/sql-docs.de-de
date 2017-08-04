---
title: Erstellen, bereitstellen und Debuggen von benutzerdefinierten Objekten | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom objects [Integration Services]
ms.assetid: b03685bc-5398-4c3f-901a-1219c1098fbe
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 99fdd71403b12cee8ba9f207890268cde2e1d450
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="building-deploying-and-debugging-custom-objects"></a>Erstellen, Bereitstellen und Debuggen von benutzerdefinierten Objekten
  Nachdem Sie den Code für ein benutzerdefiniertes Objekt zur verfasst haben [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], müssen Sie erstellen Sie die Assembly, bereitstellen und integrieren Sie ihn in [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers können Sie Pakete, für die Verwendung zur Verfügung stellen und testen und Debuggen.  
  
##  <a name="top"></a>Schritte zum Erstellen, bereitstellen und Debuggen eines benutzerdefinierten Objekts für Integrationsservices  
 Sie haben bereits die benutzerdefinierte Funktionalität für das Objekt geschrieben. Jetzt müssen Sie es testen und Benutzern zur Verfügung stellen. Die Schritte sind für alle Typen benutzerdefinierter Objekte, die Sie für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] erstellen können, ähnlich.  
  
 Hier werden die Schritte zum Erstellen, bereitstellen und testen.  
  
1.  [Anmeldung](#signing) die Assembly mit einem starken Namen generiert werden soll.  
  
2.  [Erstellen Sie](#building) der Assembly.  
  
3.  [Bereitstellen von](#deploying) verschieben oder kopieren es an die entsprechende Assembly [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Ordner.  
  
4.  [Installieren Sie](#installing) die Assembly im globalen Assemblycache (GAC).  
  
     Das Objekt wird der Toolbox automatisch hinzugefügt.  
  
5.  [Problembehandlung bei](#troubleshooting) der Bereitstellung, bei Bedarf.  
  
6.  [Test](#testing) und Debuggen Ihres Codes.  
  
 Jetzt können Sie SSIS-Designer in SQL Server Data Tools (SSDT) zu erstellen, verwalten und Ausführen von Paketen, die verschiedene von Versionen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere Informationen zu den Auswirkungen dieser Verbesserung auf Ihre benutzerdefinierten Erweiterungen finden Sie unter [erste Ihre benutzerdefinierten SSIS-Erweiterungen, die von der Unterstützung mehrerer Versionen von SSDT 2015 für SQL Server 2016 unterstützt werden](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)  
  
##  <a name="signing"></a>Signieren der Assembly  
 Wenn eine Assembly freigegeben werden soll, muss sie im GAC installiert sein. Nachdem die Assembly dem globalen Assemblycache hinzugefügt wurden, kann die Assembly von Anwendungen wie [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] genutzt werden. Für den globalen Assemblycache muss die Assembly mit einem starken Namen signiert werden, um sicherzustellen, dass eine Assembly global eindeutig ist. Eine Assembly mit starkem Namen verfügt über einen vollqualifizierten Namen, der den Namen, öffentlichen Schlüssel und die Versionsnummer der Assembly umfasst. Anhand dieser Informationen wird die Assembly von der Laufzeit gefunden und von anderen Assemblys mit demselben Namen unterschieden.  
  
 Um eine Assembly mit einem starken Namen zu signieren, müssen Sie zuerst über ein Schlüsselpaar verfügen oder eines erstellen, das aus einem öffentlichen und einem privaten Schlüssel besteht. Dieses kryptografische Schlüsselpaar wird während der Erstellung zum Generieren einer Assembly mit starkem Namen verwendet.  
  
 Weitere Informationen zu starken Namen und zu den Schritten zum Signieren einer Assembly finden Sie in den folgenden Themen in der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK-Dokumentation:  
  
-   Assemblys mit starkem Namen  
  
-   Erstellen eines Schlüsselpaars  
  
-   Signieren einer Assembly mit einem starken Namen  
  
 Sie können die Assembly mühelos in [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] beim Erstellen mit einem starken Namen signieren. In der **Projekteigenschaften** wählen Sie im Dialogfeld die **Signierung** Registerkarte. Wählen Sie die Option **zum Signieren der Assembly** , und geben Sie den Pfad der Schlüsseldatei (.snk).  
  
##  <a name="building"></a>Beim Erstellen der Assembly  
 Nach der Signierung des Projekts müssen Sie erstellen oder neu erstellen des Projekts oder der Projektmappe mithilfe der Befehle zur Verfügung, auf die **erstellen** Menü [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Die Lösung enthält möglicherweise ein separates Projekt für eine benutzerdefinierte Benutzeroberfläche, die ebenfalls mit einem starken Namen signiert sein muss und zur gleichen Zeit erstellt werden kann.  
  
 Der einfachste Weg, um die nächsten zwei Schritte (Bereitstellen der Assembly und Installieren im globalen Assemblycache) auszuführen, besteht darin, für diese Schritte als Postbuildereignis in [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ein Skript zu erstellen. Buildereignisse stehen über die **Kompilieren** Seite der Projekteigenschaften für ein [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] Projekt, und von der **Buildereignisse** Seite für ein C#-Projekt. Der vollständige Pfad ist erforderlich, damit die eingabeaufforderungs-Hilfsprogramme, z. B. **gacutil.exe**. Pfade mit Leerzeichen und Makros wie $(TargetPath), mit denen Pfade mit Leerzeichen erweitert werden, müssen von Anführungszeichen umschlossen werden.  
  
 Nachfolgend finden Sie ein Beispiel einer Postbuildereignis-Befehlszeile für einen benutzerdefinierten Protokollanbieter:  
  
```  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -u $(TargetName)  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -i $(TargetFileName)  
copy $(TargetFileName) "C:\Program Files\Microsoft SQL Server\130\DTS\LogProviders "  
```  
  
##  <a name="deploying"></a>Bereitstellen der Assembly  
 Die [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer sucht die benutzerdefinierten Objekte, die zur Verwendung in Paketen durch das Auflisten der Dateien in eine Reihe von Ordnern, die erstellt werden, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installiert ist. Wenn die Standardeinstellung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installationseinstellungen verwendet werden, befindet sich dieser Satz von Ordnern unter **C:\Program Files\Microsoft SQL Server\130\DTS**. Jedoch wenn Sie ein Setupprogramm für das benutzerdefinierte Objekt erstellen, Sie den Wert der überprüfen sollten die **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS\Setup\DtsPath** Registrierungsschlüssel auf den Speicherort dieses Ordners zu überprüfen.  
  
> [!NOTE]  
>  Informationen zum Bereitstellen von benutzerdefinierter Komponenten auch bei der Unterstützung mehrerer Versionen in SQL Server Data Tools ordnungsgemäß funktionieren, finden Sie unter [erste Ihre benutzerdefinierten SSIS-Erweiterungen, die von der Unterstützung mehrerer Versionen von SSDT 2015 für SQL Server 2016 unterstützt werden](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/).  
  
 Sie können die Assembly auf zwei Arten im Ordner platzieren:  
  
-   Verschieben oder kopieren Sie die kompilierte Assembly nach der Erstellung in den entsprechenden Ordner. (Sie können auch einfach den Kopierbefehl in ein Postbuildereignis einschließen.)  
  
-   Erstellen Sie die Assembly direkt im entsprechenden Ordner.  
  
 Die folgenden Bereitstellungsordner unter **C:\Program Files\Microsoft SQL Server\130\DTS** werden für die unterschiedlichen Typen benutzerdefinierter Objekte verwendet:  
  
|Benutzerdefiniertes Objekt|Bereitstellungsordner|  
|-------------------|-----------------------|  
|Task|Aufgaben|  
|Verbindungs-Manager|Verbindungen|  
|Protokollanbieter|LogProviders|  
|Datenflusskomponente|PipelineComponents|  
  
> [!NOTE]  
>  Assemblys werden in diese Ordner kopiert, um die Aufzählung der verfügbaren Tasks, Verbindungs-Manager usw. zu unterstützen. Sie müssen daher keine Assemblys, die nur die benutzerdefinierte Benutzeroberfläche für benutzerdefinierte Objekte enthalten, in diesen Ordnern bereitstellen.  
  
##  <a name="installing"></a>Installieren der Assembly im globalen Assemblycache  
 Um die taskassembly im globalen Assemblycache (GAC) zu installieren, verwenden Sie das Befehlszeilentool **gacutil.exe**, oder ziehen Sie die Assemblys, die `%system%\assembly` Verzeichnis. Der Einfachheit halber können Sie auch den Aufruf von einschließen **gacutil.exe** in ein Postbuildereignis.  
  
 Der folgende Befehl installiert eine Komponente mit dem Namen *Datei MyTask.dll* im globalen Assemblycache mithilfe **gacutil.exe**.  
  
 `gacutil /iF MyTask.dll`  
  
 Sie müssen [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer nach der Installation einer neuer Version des benutzerdefinierten Objekts schließen und erneut öffnen. Wenn Sie frühere Versionen des benutzerdefinierten Objekts im globalen Assemblycache installiert haben, müssen Sie sie vor der Installation der neuen Version entfernen. Führen Sie zum Deinstallieren einer Assemblys **gacutil.exe** und geben Sie den Assemblynamen mit dem `/u` Option.  
  
 Weitere Informationen zum globalen Assemblycache finden Sie unter Globales Assemblycache-Tool (Gactutil.exe) in den [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Tools.  
  
##  <a name="troubleshooting"></a>Problembehandlung bei der Bereitstellung  
 Wenn das benutzerdefinierte Objekt wird, in angezeigt der **Toolbox** oder die Liste der verfügbaren Objekte, aber Sie können nicht zu einem Paket hinzugefügt haben, versuchen Folgendes:  
  
1.  Suchen Sie im globalen Assemblycache nach mehreren Versionen der Komponente. Wenn im globalen Assemblycache mehrere Versionen der Komponente vorliegen, kann der Designer u. U. die Komponente nicht laden. Löschen Sie alle Instanzen der Assembly aus dem globalen Assemblycache, und fügen Sie die Assembly wieder hinzu.  
  
2.  Stellen Sie sicher, dass nur eine einzelne Instanz der Assembly im Bereitstellungsordner existiert.  
  
3.  Aktualisieren Sie die Toolbox.  
  
4.  Fügen Sie [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] auf **devenv.exe** und legen Sie einen Haltepunkt, durchlaufen den Initialisierungscode, um sicherzustellen, dass keine Ausnahmen auftreten.  
  
##  <a name="testing"></a>Testen und Debuggen von Code  
 Die einfachste Vorgehensweise zum Debuggen die Laufzeitmethoden eines benutzerdefinierten Objekts gestartet ist **dtexec.exe** aus [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] nach dem Erstellen des benutzerdefinierten Objekts, und führen Sie ein Paket, das die Komponente verwendet.  
  
 Wenn Sie die Komponente zur Entwurfszeit-Methoden, wie z. B. debuggen möchten die **überprüfen** -Methode, öffnen Sie ein Paket, das die Komponente in einer zweiten Instanz von verwendet [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], und fügen Sie an seine **devenv.exe** Prozess.  
  
 Wenn Sie möchten auch die Laufzeitmethoden der Komponente zu debuggen, wenn ein Paket offen ist und ausgeführt wird, [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, Sie müssen erzwingen, halten Sie die Ausführung des Pakets, damit Sie auch an anfügen können die **DtsDebugHost.exe** Prozess.  
  
#### <a name="to-debug-an-objects-run-time-methods-by-attaching-to-dtexecexe"></a>So debuggen Sie die Laufzeitmethoden eines Objekts durch das Anfügen an dtexec.exe  
  
1.  Signieren und erstellen Sie Ihr Projekt in der Debug-Konfiguration, stellen Sie es bereit, und installieren Sie es im globalen Assemblycache wie in diesem Thema beschrieben.  
  
2.  Auf der **Debuggen** Registerkarte **Projekteigenschaften**Option **externes Programm starten** als der **Startaktion**, und suchen Sie **dtexec.exe**, das standardmäßig in c:\Programme\Microsoft c:\Programme\Microsoft SQL Server\130\DTS\Binn installiert wird.  
  
3.  In der **Befehlszeilenoptionen** Textfeld unter **Startoptionen**, geben Sie die Befehlszeilenargumente erforderlich, um ein Paket auszuführen, die Ihre Komponente verwendet. Oftmals besteht das Befehlszeilenargument aus dem /F[ILE]-Schalter gefolgt vom Pfad und dem Namen der .dtsx-Datei. Weitere Informationen finden Sie unter [dtexec Utility](../../integration-services/packages/dtexec-utility.md).  
  
4.  Legen Sie sofern erforderlich im Quellcode Breakpoints in den Laufzeitmethoden der Komponente fest.  
  
5.  Das Projekt auszuführen.  
  
#### <a name="to-debug-a-custom-objects-design-time-methods-by-attaching-to-sql-server-data-tools"></a>So debuggen Sie die Entwurfszeitmethoden eines benutzerdefinierten Objekts durch das Anfügen zu SQL Server-Datentools  
  
1.  Signieren und erstellen Sie Ihr Projekt in der Debug-Konfiguration, stellen Sie es bereit, und installieren Sie es im globalen Assemblycache wie in diesem Thema beschrieben.  
  
2.  Legen Sie sofern erforderlich im Quellcode Breakpoints in den Entwurfszeitmethoden des benutzerdefinierten Objekts fest.  
  
3.  Öffnen Sie eine zweite Instanz von [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], und laden Sie ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projekt, das ein Paket enthält, das das benutzerdefinierte Objekt verwendet.  
  
4.  Von der ersten Instanz des [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], Anfügen an die zweite Instanz von **devenv.exe** in das Laden des Pakets dazu **an den Prozess anhängen** aus der **Debuggen** Menü der ersten Instanz.  
  
5.  Führen Sie das Paket aus der zweiten Instanz von [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] aus.  
  
#### <a name="to-debug-a-custom-objects-run-time-methods-by-attaching-to-sql-server-data-tools"></a>So debuggen Sie die Laufzeitmethoden eines benutzerdefinierten Objekts durch das Anfügen zu SQL Server-Datentools  
  
1.  Nachdem Sie die in der vorherigen Prozedur aufgeführten Schritte abgeschlossen haben, erzwingt eine Pause in der Ausführung des Pakets auf, sodass Sie anfügen können **DtsDebugHost.exe**. Sie können diese Pause erzwingen, indem Sie einen Breakpoint Hinzufügen der **OnPreExecute** Ereignis, oder indem Sie einen Skripttask zum Projekt hinzufügen und das Skript eingeben, das ein modales Meldungsfeld anzeigt.  
  
2.  Führen Sie das Paket aus. Wechseln Sie nach dem Anhalten, mit der Instanz von [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] in dem Codeprojekt geöffnet ist, und wählen Sie **an den Prozess anhängen** aus der **Debuggen** Menü. Stellen Sie sicher, dass für die Verbindung mit der Instanz von **DtsDebugHost.exe** als **verwaltet, X86** in der **Typ** Spalte nicht mit der Instanz, die als **X86** nur.  
  
3.  Kehren Sie zum angehaltenen Paket zurück und über den Breakpoint hinaus fortgesetzt, oder klicken Sie auf **OK** schließen das Meldungsfeld, die vom Skripttask ausgelöst und Ausführung des Pakets und das Debuggen fortsetzen.  
  
## <a name="see-also"></a>Siehe auch  
 [Entwickeln benutzerdefinierter Objekte für Integrationsservices](../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)   
 [Beibehalten von benutzerdefinierten Objekten](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)   
 [Tools zur Problembehandlung für die Paketentwicklung](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
  
  
