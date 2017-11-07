---
title: Erstellen von gespeicherten Prozeduren | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- registering assemblies
- database assemblies [Analysis Services]
- server assemblies [Analysis Services]
- stored procedures [Analysis Services], creating
- assemblies [Analysis Services]
ms.assetid: a12ff02f-6d0b-4488-9846-3609fc0d0554
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1212037722863a4dc72ddb99387308cf2e33fc33
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="creating-stored-procedures"></a>Erstellen von gespeicherten Prozeduren
  Alle gespeicherten Prozeduren müssen mit einer CLR-Klasse (Common Language Runtime) oder einer COM-Klasse (Component Object Model) verknüpft sein, damit sie verwendet werden können. Die Klasse muss auf dem Server installiert werden – in der Regel in Form von einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX® dynamic Link Library (DLL) – und registrierten als Assembly auf dem Server oder in einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank.  
  
 Gespeicherte Prozeduren sind auf einem Server oder in einer Datenbank registriert. Gespeicherte Serverprozeduren können aus einem beliebigen Abfragekontext aufgerufen werden. Der Zugriff auf gespeicherte Datenbankprozeduren ist nur möglich, wenn der Datenbankkontext die Datenbank ist, unter der die gespeicherte Prozedur definiert ist. Wenn Funktionen in einer Assembly die Funktionen in einer anderen Assembly aufrufen, müssen Sie beide Assemblys in demselben Kontext registrieren (Server oder Datenbank). Für einen Server oder eine bereitgestellte [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank auf einem Server können Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] um eine Assembly zu registrieren. Für ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Projekt können Sie eine Assembly mithilfe von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Designer im Projekt registrieren.  
  
> [!IMPORTANT]  
>  COM-Assemblys können ein Sicherheitsrisiko darstellen. Aufgrund dieses Risikos und anderer Überlegungen wurden COM-Assemblys in [!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)]als veraltet markiert. COM-Assemblys werden in zukünftigen Versionen möglicherweise nicht mehr unterstützt.  
  
## <a name="registering-a-server-assembly"></a>Registrieren einer Serverassembly  
 Im Objekt-Explorer von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] werden Serverassemblys im Ordner Assemblys unter einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] aufgelistet. Serverassemblys können sowohl .NET-Assemblys (CLR) als auch COM-Bibliotheken enthalten.  
  
### <a name="to-create-a-server-assembly"></a>So erstellen Sie eine Serverassembly  
  
1.  Erweitern Sie die Instanz [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] im Objekt-Explorer mit der Maustaste die **Assemblys** Ordner, und klicken Sie dann auf **neue Assembly**. Dadurch wird die **Serverassembly** (Dialogfeld).  
  
2.  Für **Typ** Geben Sie die Assembly:  
  
    -   Für eine DLL mit verwaltetem Code (CLR) geben Sie .NET-Assembly an.  
  
    -   Geben Sie für einen nativen Code (COM-DLL) COM-DLL.  
  
3.  Für **Dateiname**, geben Sie die DLL, die die gespeicherten Prozeduren enthält.  
  
4.  Für **Assemblyname**, geben Sie einen Namen für die Assembly.  
  
5.  Ist dies ein Debugbuild der Bibliothek, dass Sie beabsichtigen, zum Debuggen gespeicherte Prozeduren, wählen Sie die **Debuginformationen einschließen** Kontrollkästchen. Weitere Informationen zum Debuggen von gespeicherter Prozeduren finden Sie unter [Debuggen von gespeicherten Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/debugging-stored-procedures.md).  
  
6.  Klicken Sie auf **OK** zum Registrieren der Assemblys sofort oder auf der Symbolleiste des Dialogfelds können Sie einen Befehl klicken, auf die **Skript** -Menü, um das Skript für der Registrierungsaktion ein Abfragefenster, einer Datei oder die Zwischenablage.  
  
 Nachdem Sie eine Serverassembly registrieren, können Sie diese konfigurieren, indem Sie die Assembly im Objekt-Explorer mit der rechten Maustaste, und klicken Sie dann auf **Eigenschaften**.  
  
## <a name="registering-a-database-assembly-on-the-server"></a>Registrieren einer Datenbankassembly auf dem Server  
 Im Objekt-Explorer von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] werden Datenbankassemblys im Ordner Assemblys unter einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Datenbank aufgelistet. Datenbankassemblys können sowohl .NET-Assemblys (CLR) als auch COM-Bibliotheken enthalten.  
  
### <a name="to-create-a-database-assembly-on-a-server"></a>So erstellen Sie eine Datenbankassembly auf einem Server  
  
1.  Erweitern Sie die Instanz die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank im Objekt-Explorer der rechten Maustaste auf die **Assemblys** Ordner, und klicken Sie dann auf **neue Assembly**. Dadurch wird die **Datenbankassembly registrieren** (Dialogfeld).  
  
2.  Für **Typ** Geben Sie die Assembly:  
  
    -   Für eine DLL mit verwaltetem Code (CLR) geben Sie .NET-Assembly an.  
  
    -   Für eine DLL mit systemeigenem Code (COM) geben Sie COM-DLL an.  
  
3.  Für **Dateiname**, geben Sie die DLL, die die gespeicherten Prozeduren enthält.  
  
4.  Für **Assemblyname**, geben Sie einen Namen für die Assembly.  
  
5.  Ist dies ein Debugbuild der Bibliothek, dass Sie beabsichtigen, zum Debuggen gespeicherte Prozeduren, wählen Sie die **Debuginformationen einschließen** Kontrollkästchen. Weitere Informationen zum Debuggen von gespeicherter Prozeduren finden Sie unter [Debuggen von gespeicherten Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/debugging-stored-procedures.md).  
  
6.  Klicken Sie auf **OK** zum Registrieren der Assemblys sofort oder auf der Symbolleiste des Dialogfelds können Sie einen Befehl klicken, auf die **Skript** -Menü, um das Skript für der Registrierungsaktion ein Abfragefenster, einer Datei oder die Zwischenablage.  
  
 Nachdem Sie eine Datenbankassembly registrieren, können Sie diese konfigurieren, indem Sie die Assembly im Objekt-Explorer mit der rechten Maustaste, und klicken Sie dann auf **Eigenschaften**.  
  
## <a name="registering-a-database-assembly-in-a-project"></a>Registrieren einer Datenbankassembly in einem Projekt  
 Im Projektmappen-Explorer von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] werden Datenbankassemblys im Ordner Assemblys unter einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Projekt aufgelistet. Datenbankassemblys können sowohl .NET-Assemblys (CLR) als auch COM-Bibliotheken enthalten.  
  
### <a name="to-create-a-database-assembly-in-an-analysis-service-project"></a>So erstellen Sie eine Datenbankassembly in einem Analysis Services-Projekt  
  
1.  Erweitern Sie die Instanz die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank im Objekt-Explorer der rechten Maustaste auf die **Assemblys** Ordner, und klicken Sie dann auf **neuer Assemblyverweis**. Dadurch wird die **Verweis hinzufügen** (Dialogfeld). Die **.NET** auf der Registerkarte die **Verweis hinzufügen** Dialogfeld Listet vorhandene Assemblys für .NET (CLR), während die **Projekte** Registerkarte listet Projekte.  
  
2.  Sie können eine vorhandene Komponente oder ein Projekt klicken und dann auf **hinzufügen** zum Hinzufügen der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Projekt. Um einen Verweis auf eine COM-DLL hinzuzufügen, klicken Sie auf die **Durchsuchen** Tab, um die Datei nicht finden. Die **ausgewählte Projekte und Komponenten** Liste zeigt den Namen, Typ, Version und Speicherort für die einzelnen Komponenten, die Sie dem Projekt hinzufügen.  
  
3.  Wenn Sie nach Auswahl der Komponenten hinzuzufügen, klicken Sie auf **OK** zum Hinzufügen der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Projekt.  
  
## <a name="script-format-for-an-assembly"></a>Skriptformat für eine Assembly  
 Das Registrieren einer .NET-Assembly ist ein relativ einfacher Vorgang. Eine .NET-Assembly wird im Binärformat einer Datenbank mithilfe des folgenden Formats hinzugefügt:  
  
```  
<Create>  
   <ObjectDefinition>  
      <Assembly>  
         <Files>  
            <File>  
               <Name>filename</Name>  
               <Type>filetype</Type>  
               <Data>  
                  <Block>binarydatablock</Block>  
                  <Block>binarydatablock</Block>  
                  ...  
               </Data>  
            </File>  
         </Files>  
         <PermissionSet>PermissionSet</PermissionSet>  
      </Assembly>  
   <ObjectDefinition>  
</Create>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Mehrdimensionales Modell Assemblys-Verwaltung](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definieren von gespeicherten Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  

