---
title: "Installieren von Updates an der Eingabeaufforderung | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bc98ba2b-aae9-4d01-aa85-d4c36428cb0b
caps.latest.revision: 18
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 18
---
# Installieren von Updates an der Eingabeaufforderung
  Testen und ändern Sie die Installationsskripts, um die Anforderungen Ihrer Organisation zu erfüllen.  
  
## Beispielsyntax zur Installation  
 Der Name des Updatepakets kann variieren und enthält möglicherweise Komponenten zu Sprache, Version und Prozessor. Anwenden eines Updates über eine Eingabeaufforderung. Dabei wird <Paketname> mit dem Namen des Updatepakets ersetzt:  
  
-   Aktualisieren Sie eine einzelne Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und aller freigegebenen Komponenten wie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] und Verwaltungstools: Sie können entweder die Instanz mit dem InstanceName-Parameter oder dem InstanceID-Parameter angeben. Um eine vorbereitete Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu aktualisieren, müssen Sie den InstanceID-Parameter <Paketname>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceName=MyInstance oder <Paketname>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceID=\<Instanz-ID> angeben.  
  
-   Setup ist in der Lage, die neuesten Produktupdates in die Installation des Hauptprodukts zu integrieren, sodass das Hauptprodukt und geeignete Updates gleichzeitig installiert werden. Sie können die Installation von Instanzen eines Datenbankmoduls so einrichten, dass Produktupdates eingeschlossen werden: setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=PrepareImage /UpdateEnabled=True /UpdateEnabled=True /UpdateSource=\<Downloadpfad des Updates> /INSTANCEID=\<Instanz-ID> /FEATURES=SQLEngine.  
  
-   Aktualisierung nur von freigegebenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Komponenten, wie z. B. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] und Verwaltungstools: <Paketname>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch  
  
-   Aktualisieren aller Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem Computer und aller freigegebenen Komponenten, wie z. B. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] und Verwaltungstools: <Paketname>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances.  
  
 Entfernen eines Updates über eine Eingabeaufforderung. Dabei wird <Paketname> mit dem Namen des Updatepakets ersetzt:  
  
-   Entfernen eines Updates aus einer einzelnen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und aus allen freigegebenen Komponenten, z. B. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] und Verwaltungstools: <Paketname>.exe /qs /Action=RemovePatch /InstanceName=MyInstance.  
  
-   Ausschließliches Entfernen eines Updates aus freigegebenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Komponenten, z. B. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] und Verwaltungstools: <Paketname>.exe /qs /Action=RemovePatch  
  
    > [!NOTE]  
    >  Mit dem Updateinstallationsprogramm wird sichergestellt, dass die freigegebenen Komponenten stets mindestens die Version der Instanz auf höchster Ebene aufweisen.  
  
## Unterstützte Befehlszeilenparameter  
  
> [!IMPORTANT]  
>  Anmeldeinformationen sollten nach Möglichkeit zur Laufzeit angegeben werden. Wenn Sie Anmeldeinformationen in einer Skriptdatei speichern müssen, sollten Sie die Datei schützen, um nicht autorisierten Zugriff zu verhindern.  
  
|Schalter|Beschreibung|  
|------------|-----------------|  
|**/?**|Zeigt Hilfe zur unbeaufsichtigten Installation an der Eingabeaufforderung an.|  
|**/action=Patch oder /action=RemovePatch**|Gibt die Installationsaktion an: Patch oder RemovePatch.|  
|**/allinstances**|Wendet das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Update auf alle Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und auf alle freigegebenen, nicht instanzabhängigen Komponenten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an.|  
|**/instancename=Instanzname***|Wendet das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Update auf eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit dem Namen InstanceName und auf alle freigegebenen, nicht instanzabhängigen Komponenten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an.|  
|**/InstanceID=Inst1**|Wendet das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Update auf eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Inst1 und auf alle freigegebenen, nicht instanzabhängigen Komponenten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an.|  
|**/quiet**|Führt Setup für das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Update im unbeaufsichtigten Modus aus.|  
|**/qs**|Zeigt nur das Statusdialogfeld in der Benutzeroberfläche an.|  
|**/UpdateEnabled**|Gibt an, ob Produktupdates von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup ermittelt und eingeschlossen werden sollen. Gültige Werte sind True und False oder 1 und 0. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup schließt standardmäßig alle gefundenen Updates ein.|  
|**/IAcceptSQLServerLicenseTerms**|Nur erforderlich, wenn der /Q-Parameter oder der /QS-Parameter für die unbeaufsichtigte Installation angegeben wird.|  
  
 *Sie können diesen Parameter nicht angeben, um ein Update auf eine vorbereitete Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anzuwenden. Sie müssen stattdessen den /instanceID-Parameter angeben.  
  
## Siehe auch  
 [Übersicht über die SQL Server-Wartungsinstallation](../Topic/Overview%20of%20SQL%20Server%20Servicing%20Installation.md)  
  
  