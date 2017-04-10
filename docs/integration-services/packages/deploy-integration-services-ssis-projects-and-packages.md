---
title: "Bereitstellen von SQL Server Integration Services-Projekten und Paketen (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bea8ce8d-cf63-4257-840a-fc9adceade8c
caps.latest.revision: 21
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 21
---
# Bereitstellen von SQL Server Integration Services-Projekten und Paketen (SSIS)
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] unterstützt zwei Bereitstellungsmodelle: das Projektbereitstellungsmodell und das Legacy-Paketbereitstellungsmodell. Mithilfe des Projektbereitstellungsmodells können Sie Projekte auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitstellen.  
  
 Weitere Informationen zum Bereitstellen eines Projekts auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Server finden Sie unter [Bereitstellen von Projekten auf dem Integration Services-Server](../../integration-services/packages/deploy-projects-to-integration-services-server.md).  
  
 Weitere Informationen zum Legacy-Paketbereitstellungsmodell finden Sie unter [Legacy-Paketbereitstellung &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md).  
  
> [!NOTE]  
>  Das Projektbereitstellungsmodell wurde in [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]eingeführt. Wenn Sie dieses Modell verwendet haben, konnten Sie keine Pakete bereitstellen, ohne das gesamte Projekt bereitzustellen. In [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] wurde die Funktion für inkrementelle Paketbereitstellung eingeführt, mit der Sie Pakete in einem vorhandenen oder neuen Projekt bereitstellen können, ohne das gesamte Projekt bereitzustellen. Weitere Informationen zu diesem Feature finden Sie unter [Deploy Packages to Integration Services Server](../../integration-services/packages/deploy-packages-to-integration-services-server.md) .  
  
## Vergleich von Projektbereitstellungsmodell und Legacy-Paketbereitstellungsmodells  
 Der Typ von Bereitstellungsmodell, den Sie für ein Projekt auswählen, bestimmt, welche Entwicklungs- und Verwaltungsoptionen für dieses Projekt verfügbar sind. In der folgenden Tabelle werden Unterschiede und Ähnlichkeiten der Verwendung des Projektbereitstellungsmodells und des Paketbereitstellungsmodells dargestellt.  
  
|Bei Verwendung des Projektbereitstellungsmodells|Bei Verwendung des Legacy-Paketbereitstellungsmodells|  
|---------------------------------------------|----------------------------------------------------|  
|Ein Projekt stellt die Entwicklungseinheit dar.|Ein Paket ist die Bereitstellungseinheit.|  
|Parameter werden verwendet, um Paketeigenschaften Werte zuzuweisen.|Konfigurationen werden verwendet, um Paketeigenschaften Werte zuzuweisen.|  
|Aus einem Projekt, das Pakete und Parameter enthält, wird eine Projektbereitstellungsdatei (Erweiterung .ISPAC) erstellt.|Pakete (Erweiterung .DTSX) und Konfigurationen (Erweiterung .DTSCONFIG) werden einzeln im Dateisystem gespeichert.|  
|Ein Projekt, das Pakete und Parameter enthält, wird im SSISDB-Katalog auf einer Instanz von SQL Server bereitgestellt.|Pakete und Konfigurationen werden in das Dateisystem auf einem anderen Computer kopiert. Pakete können auch in der MSDB-Datenbank auf einer Instanz von SQL Server gespeichert werden.|  
|Auf dem Datenbankmodul ist die CLR-Integration erforderlich.|Auf dem Datenbankmodul ist die CLR-Integration nicht erforderlich.|  
|Umgebungsspezifische Parameterwerte werden in Umgebungsvariablen gespeichert.|Umgebungsspezifische Konfigurationswerte werden in Konfigurationsdateien gespeichert.|  
|Im Katalog enthaltene Projekte und Pakete können vor der Ausführung auf dem Server überprüft werden. Sie können die Überprüfung mithilfe von SQL Server Management Studio, gespeicherten Prozeduren oder verwaltetem Code ausführen.|Pakete werden unmittelbar vor der Ausführung überprüft. Ein Paket kann auch mit dtExec oder verwaltetem Code überprüft werden.|  
|Pakete werden ausgeführt, indem mit dem Datenbankmodul eine Ausführung gestartet wird. Einer Ausführung werden vor dem Start ein Projektbezeichner, explizite Parameterwerte (optional) und Umgebungsverweise (optional) zugewiesen.<br /><br /> Sie können Pakete mit **dtExec**ausführen.|Pakete werden mit den Ausführungshilfsprogrammen **dtExec** und **DTExecUI** ausgeführt. Anwendbare Konfigurationen werden durch Eingabeaufforderungsargumente (optional) identifiziert.|  
|Während der Ausführung werden Ereignisse, die vom Paket erzeugt werden, automatisch aufgezeichnet und im Katalog gespeichert. Sie können diese Ereignisse mit Transact-SQL-Sichten abfragen.|Während der Ausführung werden Ereignisse, die von einem Paket erzeugt werden, nicht automatisch aufgezeichnet. Dem Paket muss ein Protokollanbieter zum Aufzeichnen von Ereignissen hinzugefügt werden.|  
|Pakete werden in einem separaten Windows-Prozess ausgeführt.|Pakete werden in einem separaten Windows-Prozess ausgeführt.|  
|SQL Server-Agent wird verwendet, um die Paketausführung zu planen.|SQL Server-Agent wird verwendet, um die Paketausführung zu planen.|  
  
 Das Projektbereitstellungsmodell wurde in [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]eingeführt. Wenn Sie dieses Modell verwendet haben, konnten Sie keine Pakete bereitstellen, ohne das gesamte Projekt bereitzustellen. In [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] wurde die Funktion für inkrementelle Paketbereitstellung eingeführt, mit der Sie Pakete in einem vorhandenen oder neuen Projekt bereitstellen können, ohne das gesamte Projekt bereitzustellen. Weitere Informationen zu diesem Feature finden Sie unter [Deploy Packages to Integration Services Server](../../integration-services/packages/deploy-packages-to-integration-services-server.md) .  
  
## Funktionen des Projektbereitstellungsmodells  
 In der folgenden Tabelle sind die Funktionen aufgeführt, die für Projekte, die nur für das Projektbereitstellungsmodell entwickelt wurden, verfügbar sind.  
  
|Funktion|Description|  
|-------------|-----------------|  
|Parameter|Ein Parameter gibt die Daten an, die von einem Paket verwendet werden. Sie können die Gültigkeit von Parametern Paketparametern und Projektparametern auf die Paketebene bzw. Projektebene beschränken. Parameter können in Ausdrücken oder Tasks verwendet werden. Wenn das Projekt im Katalog bereitgestellt wird, können Sie einen Literalwert für jeden Parameter zuweisen oder den Standardwert verwenden, der zur Entwurfszeit zugewiesen wurde. Statt eines Literalwerts kann auch auf eine Umgebungsvariable verwiesen werden. Umgebungsvariablenwerte werden zur Laufzeit der Paketausführung aufgelöst.|  
|Umgebungen|Eine Umgebung ist ein Container für Variablen, auf die von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekten verwiesen werden kann. Jedes Projekt kann über mehrere Umgebungsverweise verfügen, aber eine einzelne Instanz der Paketausführung kann nur auf Variablen von einer einzelnen Umgebung verweisen. Umgebungen ermöglichen es Ihnen, die Werte zu organisieren, die Sie einem Paket zuweisen. Sie könnten z. B. Umgebungen mit den Namen "Entwicklung", "Test" und "Produktion" definieren.|  
|Umgebungsvariablen|Eine Umgebungsvariable definiert einen Literalwert, der einem Parameter während der Paketausführung zugewiesen werden kann. Um eine Umgebungsvariable zu verwenden, erstellen Sie einen Umgebungsverweis (im Projekt, das der Umgebung entspricht, die über den Parameter verfügt), weisen Sie dem Namen der Umgebungsvariablen einen Parameterwert zu, und geben Sie während der Konfiguration einer Ausführungsinstanz den entsprechenden Umgebungsverweis an.|  
|SSISDB-Katalog|Alle [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Objekte für eine Instanz von SQL Server werden in einer Datenbank, die als SSISDB-Katalog bezeichnet wird, gespeichert und verwaltet. Der Katalog ermöglicht es Ihnen, Projekte und Umgebungen mithilfe von Ordnern zu organisieren. Jede Instanz von SQL Server kann nur einen Katalog besitzen. Jeder Katalog kann 0 (Null) oder mehr Ordner aufweisen. Jeder Ordner kann 0 (Null) oder mehr Projekte und 0 (Null) oder mehr Umgebungen haben. Ein Katalogordner kann auch als Begrenzung für Berechtigungen für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Objekte verwendet werden.|  
|Im Katalog gespeicherte Prozeduren und Sichten|Eine große Anzahl von gespeicherten Prozeduren und Sichten kann zum Verwalten von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Objekten im Katalog verwendet werden. Zum Beispiel können Sie Werte für Parameter und Umgebungsvariablen angeben, Ausführungen erstellen und starten und Katalogvorgänge überwachen. Sie können sogar vor dem Start der Ausführung genau sehen, welche Werte von einem Paket verwendet werden.|  
  
## Projektbereitstellung  
 Den Mittelpunkt des Projektbereitstellungsmodells bildet die Projektbereitstellungsdatei (Erweiterung .ISPAC). Die Projektbereitstellungsdatei ist eine in sich geschlossene Bereitstellungseinheit, die nur die wesentlichen Informationen zu den Paketen und Parametern des Projekts umfasst. Die Projektbereitstellungsdatei enthält nicht sämtliche Informationen, die in der Projektdatei von Integration Services (Erweiterung .DTPROJ) enthalten sind. Beispielsweise werden zusätzliche Textdateien, die Sie zum Schreiben von Hinweisen verwenden, nicht in der Projektbereitstellungsdatei gespeichert und daher nicht im Katalog bereitgestellt.  
  
## Erforderliche Tasks  
  
-   [Bereitstellen von Projekten auf dem Integration Services-Server](../../integration-services/packages/deploy-projects-to-integration-services-server.md)  
  
## Verwandte Inhalte  
 Blogeintrag zu [Überlegungen zu Verzweigungsstrategien für SSIS-Projekte](http://go.microsoft.com/fwlink/?LinkId=245739)auf mattmasson.com.  
  
## Siehe auch  
 [dtexec (Hilfsprogramm)](../../integration-services/packages/dtexec-utility.md)  
  
  