---
title: Mehrdimensionales Modell Assemblys-Verwaltung | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 89678cac9febb3adbed049e859876d646b3ddf82
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="multidimensional-model-assemblies-management"></a>Verwaltung von mehrdimensionalen Modellassemblys
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] stellt viele systeminterne Funktionen bereit, mit den Sprachen Multidimensional Expressions (MDX) und Data Mining Extensions (DMX), die entwickelt, um die standardmäßige statistische Berechnungen wie zum durchlaufenden der Elemente in einer Hierarchie zu erreichen. Wie bei jedem komplexen und robusten Produkt gibt es jedoch immer die Bestrebung, die Funktionalität des Produkts zu erweitern.  
  
 Deshalb bietet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die Möglichkeit, einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz oder -Datenbank Assemblys hinzuzufügen. Mithilfe von Assemblys können Sie mit einer beliebigen CLR-Sprache (Common Language Runtime), z. B. Microsoft Visual Basic .NET oder Microsoft Visual C#, externe benutzerdefinierte Funktionen erstellen. Darüber hinaus können Sie COM-Automatisierungssprachen (Component Object Model) wie Microsoft Visual Basic oder Microsoft Visual C++ verwenden.  
  
> [!IMPORTANT]  
>  COM-Assemblys können ein Sicherheitsrisiko darstellen. Aufgrund dieses Risikos und anderer Überlegungen wurden COM-Assemblys in [!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)]als veraltet markiert. COM-Assemblys werden in zukünftigen Versionen möglicherweise nicht mehr unterstützt.  
  
 Mit Assemblys können Sie die Geschäftsfunktionalität von MDX und DMX erweitern. Sie integrieren die gewünschte Funktionalität in eine Bibliothek, z. B. eine DLL (Dynamic Link Library), und fügen die Bibliothek als Assembly einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz oder einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank hinzu. Die öffentlichen Methoden in der Bibliothek werden dann als benutzerdefinierte Funktionen für MDX- und DMX-Ausdrücke, Prozeduren, Berechnungen, Aktionen und Clientanwendungen verfügbar gemacht.  
  
 Dem Server kann eine Assembly mit neuen Prozeduren und Funktionen hinzugefügt werden. Sie können Assemblys verwenden, um benutzerdefinierte Funktionen zu verbessern oder hinzuzufügen, die nicht vom Server bereitgestellt werden. Mithilfe von Assemblys können Sie mehrdimensionalen Ausdrücken (MDX), Data Mining-Erweiterungen oder gespeicherten Prozeduren neue Funktionen hinzufügen. Assemblys werden von der Position geladen, auf der die benutzerdefinierte Anwendung ausgeführt wird. Eine Kopie der Binärdateien der Assembly wird zusammen mit den Datenbankdaten auf dem Server gespeichert. Wenn eine Assembly entfernt wird, wird die kopierte Assembly ebenfalls vom Server entfernt.  
  
 Assemblys können von zwei verschiedenen Typen sein: COM und CLR. CLR-Assemblys sind Assemblys, die in .NET Framework-Programmiersprachen wie C#, Visual Basic .NET und Managed C++ entwickelt wurden. COM-Assemblys sind COM-Bibliotheken, die auf dem Server registriert werden müssen.  
  
 Assemblys können <xref:Microsoft.AnalysisServices.Server> - oder <xref:Microsoft.AnalysisServices.Database> -Objekten hinzugefügt werden. Serverassemblys können von allen mit dem Server verbundenen Benutzern und allen Objekten auf dem Server aufgerufen werden. Datenbankassemblys können nur von <xref:Microsoft.AnalysisServices.Database> -Objekten aufgerufen werden oder von Benutzern, die mit der Datenbank verbunden sind.  
  
 Ein einfaches <xref:Microsoft.AnalysisServices.Assembly> -Objekt besteht aus grundlegenden Informationen (Name und ID), der Dateisammlung und Sicherheitsinformationen.  
  
 Die Dateiauflistung verweist auf die geladenen Assemblydateien und ihre zugehörigen Debuggingdateien (.pdb), wenn die Debuggingdateien mit den Assemblydateien geladen wurden. Assemblydateien werden von der Position geladen, die von der Anwendung definiert wurde. Eine Kopie wird zusammen mit den Daten auf dem Server gespeichert. Die Kopie der Assemblydatei wird verwendet, um die Assembly bei jedem Start des Diensts zu laden.  
  
 Die Sicherheitsinformationen beinhalten den Berechtigungssatz und den für die Ausführung der Assembly verwendeten Identitätswechsel.  
  
## <a name="calling-user-defined-functions"></a>Aufrufen von benutzerdefinierten Funktionen  
 Das Aufrufen einer benutzerdefinierten Funktion in einer Assembly erfolgt auf dieselbe Art wie das Aufrufen einer systeminternen Funktion, abgesehen davon, dass Sie einen vollqualifizierten Namen verwenden müssen. Beispielsweise ist eine benutzerdefinierte Funktion, die einen von MDX erwarteten Typ zurückgibt, in einer MDX-Abfrage enthalten, wie das folgende Beispiel zeigt:  
  
```  
Select MyAssembly.MyClass.MyStoredProcedure(a, b, c) on 0 from Sales  
```  
  
 Benutzerdefinierte Funktionen können außerdem mithilfe des CALL-Schlüsselworts aufgerufen werden. Sie müssen das CALL-Schlüsselwort für benutzerdefinierte Funktionen verwenden, die Recordsets oder 'void' zurückgeben. Dagegen können Sie das CALL-Schlüsselwort nicht verwenden, wenn die benutzerdefinierte Funktion von einem Objekt im Kontext der MDX- oder DMX-Anweisung bzw. des -Skripts, z. B. dem aktuellen Cube oder dem Data Mining-Modell, abhängt. Eine außerhalb einer MDX- oder DMX-Abfrage aufgerufene Funktion wird häufig verwendet, um das AMO-Objektmodell für die Ausführung administrativer Funktionen einzusetzen. Beispielsweise wird die `MyVoidProcedure(a, b, c)` -Funktion in einer MDX-Anweisung mit der folgenden Syntax verwendet:  
  
```  
Call MyAssembly.MyClass.MyVoidProcedure(a, b, c)  
```  
  
 Assemblys vereinfachen die Datenbankentwicklung, da gemeinsamer Code nur einmal entwickelt zu werden braucht und an einem einzigen Ort gespeichert werden kann. Entwickler von Clientsoftware können Bibliotheken mit Funktionen für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] erstellen und diese mit ihren Anwendungen verteilen.  
  
 Es kann vorkommen, dass Assemblys und benutzerdefinierte Funktionen die Funktionsnamen aus der Funktionsbibliothek von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oder von anderen Assemblys duplizieren. Solange Sie die benutzerdefinierte Funktion mit ihrem vollqualifizierten Namen aufrufen, verwendet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die richtige Prozedur. Aus Sicherheitsgründen und damit nicht ein doppelter Name aus einer anderen Klassenbibliothek aufgerufen wird, müssen Sie in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vollqualifizierte Namen für gespeicherte Prozeduren verwenden.  
  
 Um eine benutzerdefinierte Funktion von einer bestimmten CLR-Assembly aus aufzurufen, wird der benutzerdefinierten Funktion der Assemblyname, der vollständige Klassenname und der Prozedurname vorangestellt, wie im Folgenden dargestellt:  
  
 *Assemblyname*.*VollständigerKlassenname*.*Prozedurname*(*Argument1*, *Argument2*, ...)  
  
 Um die Abwärtskompatibilität mit früheren Versionen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]sicherzustellen, ist die folgende Syntax ebenfalls zulässig:  
  
 *Assemblyname*!*VollständigerKlassenname*!*Prozedurname*(*Argument1*, *Argument2*, ...)  
  
 Unterstützt eine COM-Bibliothek mehrere Schnittstellen, kann der Prozedurname auch mithilfe der Schnittstellen-ID aufgelöst werden, wie im Folgenden dargestellt:  
  
 *Assemblyname*!*Schnittstellen-ID*!*Prozedurname*(*Argument1*, *Argument2*, ...)  
  
## <a name="security"></a>Security  
 Die Sicherheit für Assemblys basiert auf dem .NET Framework-Sicherheitsmodell, bei dem es sich um ein Codezugriffs-Sicherheitsmodell handelt. .NET Framework unterstützt einen Codezugriffs-Sicherheitsmechanismus, der annimmt, dass die Laufzeit sowohl vollständig vertrauenswürdigen als auch teilweise vertrauenswürdigen Code hosten kann. Die durch die .NET Framework-Codezugriffssicherheit geschützten Ressourcen sind üblicherweise von verwaltetem Code umgeben, der die entsprechenden Berechtigungen anfordert, bevor er den Zugriff auf die Ressource ermöglicht. Die Anforderung der Berechtigung ist nur dann erfüllt, wenn alle aufrufenden Prozesse (auf Assemblyebene) in der Aufrufliste über die entsprechende Ressourcenberechtigung verfügen.  
  
 Für Assemblys wird die Ausführungsberechtigung mit der **PermissionSet** -Eigenschaft des **Assembly** -Objekts erteilt. Die Berechtigungen, die der verwaltete Code erhält, hängen von der gültigen Sicherheitsrichtlinie ab. In einer nicht von[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gehosteten Umgebung werden drei Richtlinienebenen unterschieden: Unternehmen, Computer und Benutzer. Die gültige Berechtigungsliste, die der Code erhält, hängt von der Schnittmenge der Berechtigungen auf diesen drei Ebenen ab.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] stellt für die gehostete CLR eine Sicherheitsrichtlinie auf Hostebene bereit; diese Richtlinie stellt eine zusätzliche Richtlinienebene unterhalb der drei Richtlinienebenen dar, die immer gültig sind. Die Richtlinie wird für jede Anwendungsdomäne festgelegt, die von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]erstellt wird.  
  
 Die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Richtlinie auf Hostebene ist eine Kombination der festen Richtlinie von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] für Systemassemblys und der benutzerdefinierten Richtlinie für Benutzerassemblys. Der benutzerdefinierte Teil der Hostrichtlinie von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] basiert darauf, dass der Assemblybesitzer einen von drei Berechtigungsbuckets für jede Assembly angibt:  
  
|Berechtigungseinstellung|Description|  
|------------------------|-----------------|  
|**Safe**|Stellt eine interne Berechnungsberechtigung bereit. Dieser Berechtigungsbucket weist keine Berechtigungen für den Zugriff auf die geschützten Ressourcen in .NET Framework zu. Es handelt es hierbei um den Standard-Berechtigungsbucket für eine Assembly, sofern nicht mithilfe der **PermissionSet** -Eigenschaft ein anderer Bucket angegeben wurde.|  
|**ExternalAccess**|Bietet den gleichen Zugriff wie die **Safe** -Einstellung, zusätzlich jedoch die Möglichkeit, auf externe Systemressourcen zuzugreifen. Dieser Berechtigungsbucket leistet keine Gewähr für Sicherheit (obwohl dieses Szenario gesichert werden kann), wohl aber für Zuverlässigkeit.|  
|**Unsafe**|Es gelten keine Einschränkungen. Für verwalteten Code, der unter diesem Berechtigungssatz ausgeführt wird, kann keine Gewähr für Sicherheit oder Zuverlässigkeit geleistet werden. Für Code, der auf dieser Vertrauensebene ausgeführt wird, wird jede Berechtigung gewährt, selbst eine vom Administrator hinzugefügte benutzerdefinierte Berechtigung.|  
  
 Wenn die CLR von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]gehostet wird, hält die stackwalkbasierte Berechtigungsüberprüfung an der Grenze mit dem systemeigenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Code an. Sämtlicher verwalteter Code in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Assemblys fällt in eine der drei oben aufgelisteten Berechtigungskategorien.  
  
 COM- (oder nicht verwaltete) Assemblyroutinen unterstützen das CLR-Sicherheitsmodell nicht.  
  
### <a name="impersonation"></a>Identitätswechsel  
 Wenn verwalteter Code auf eine Ressource außerhalb von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]zugreift, hält [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sich an die der **ImpersonationMode** -Eigenschaftseinstellung zugeordneten Regeln, um sicherzustellen, dass der Zugriff innerhalb des entsprechenden Windows-Sicherheitskontexts erfolgt. Da Assemblys mit der **Safe** -Berechtigungseinstellung nicht auf Ressourcen außerhalb von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]zugreifen können, gelten diese Regeln nur für Assemblys mit den Berechtigungseinstellungen **ExternalAccess** und **Unsafe** .  
  
-   Wenn der aktuelle Ausführungskontext einem von Windows authentifizierten Benutzernamen entspricht und mit dem Kontext des ursprünglichen aufrufenden Prozesses übereinstimmt (wenn sich also nicht EXECUTE AS in der Mitte befindet), nimmt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die Identität des von Windows authentifizierten Benutzernamens an, bevor der Zugriff auf die Ressource erfolgt.  
  
-   Wird der Kontext des ursprünglichen aufrufenden Prozesses durch EXECUTE AS geändert, erzeugt der Zugriff auf die externe Ressource einen Fehler.  
  
 Für die **ImpersonationMode** -Eigenschaft kann **ImpersonateCurrentUser** oder **ImpersonateAnonymous**festgelegt werden. Mit der Standardeinstellung, **ImpersonateCurrentUser**, wird eine Assembly unter dem Netzwerk-Anmeldekonto des aktuellen Benutzers ausgeführt. Wird die **ImpersonateAnonymous** -Einstellung verwendet, entspricht der Ausführungskontext dem Benutzerkonto IUSER_*Servername* für die Windows-Anmeldung auf dem Server. Hierbei handelt es sich um ein Internet-Gastkonto, das nur über eingeschränkte Rechte auf dem Server verfügt. Eine Assembly, die in diesem Kontext ausgeführt wird, kann nur beschränkt auf Ressourcen auf dem lokalen Server zugreifen.  
  
### <a name="application-domains"></a>Anwendungsdomänen  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] macht Anwendungsdomänen nicht direkt verfügbar. Aufgrund eines Assemblysatzes, der in der gleichen Anwendungsdomäne ausgeführt wird, können Anwendungsdomänen während der Ausführung einander erkennen, indem sie den **System.Reflection** -Namespace in .NET Framework oder ein anderes Verfahren anwenden, und sie können einander auf spät gebundene Weise aufrufen. Solche Aufrufe werden der Berechtigungsüberprüfung unterzogen, die im Rahmen der autorisierungsbasierten Sicherheit von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] durchgeführt wird.  
  
 Sie sollten sich nicht darauf verlassen, Assemblys in der gleichen Anwendungsdomäne zu finden, da die Grenze der Anwendungsdomäne und die Assemblys, die sich in jeder Domäne befinden, durch die Implementierung definiert werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Festlegen der Sicherheit für gespeicherte Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/setting-security-for-stored-procedures.md)   
 [Definieren von gespeicherten Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
