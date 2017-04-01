---
title: "Bereitstellen von Paketen mithilfe des Bereitstellungshilfsprogramms | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Pakete [Integration Services], installieren"
  - "Installieren von Paketen"
  - "Abhängigkeiten [Integration Services]"
  - "Bereitstellen von Paketen [Integration Services], Installieren"
ms.assetid: eaf4b56e-2023-4d17-971c-703031da758c
caps.latest.revision: 57
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 57
---
# Bereitstellen von Paketen mithilfe des Bereitstellungshilfsprogramms
  Wenn Sie ein Bereitstellungshilfsprogramm erstellt haben, um Pakete aus einem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt auf einem anderen Computer zu installieren als dem Computer, auf dem das Bereitstellungshilfsprogramm erstellt wurde, müssen Sie zuerst den Bereitstellungsordner auf den Zielcomputer kopieren.  
  
 Der Pfad des Bereitstellungsordners wird in der DeploymentOutputPath-Eigenschaft des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projekts angegeben, für das Sie das Bereitstellungshilfsprogramm erstellt haben. Der Standardpfad ist bin\Deployment, relativ zum [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projekt. Weitere Informationen finden Sie unter [Create a Deployment Utility](../../integration-services/packages/create-a-deployment-utility.md).  
  
 Sie können zum Installieren der Pakete den Paketinstallations-Assistenten verwenden. Doppelklicken Sie zum Starten des Assistenten auf die Datei des Bereitstellungshilfsprogramms, nachdem Sie den Bereitstellungsordner auf den Server kopiert haben. Die Datei hat den Namen „\<Projektname>.SSISDeploymentManifest“ und befindet sich im Bereitstellungsordner des Zielcomputers.  
  
> [!NOTE]  
>  Abhängig von der Version des Pakets, das Sie bereitstellen, könnte ein Fehler auftreten, wenn Sie verschiedene Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parallel installiert haben. Dieser Fehler kann auftreten, da die Dateinamenerweiterung ".SSISDeploymentManifest" für alle Versionen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]identisch ist. Durch Doppelklicken auf die Datei wird das Installationsprogramm („dtsinstall.exe“) für die zuletzt installierte Version von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] aufgerufen, die möglicherweise nicht der Version der Datei des Bereitstellungs-Hilfsprogramms entspricht. Um dieses Problem zu umgehen, führen Sie die richtige Version von "dtsinstall.exe" in der Befehlszeile aus, und stellen Sie den Pfad der Datei des BereitstellungsHilfsprogramms bereit.  
  
 Der Paketinstallations-Assistent führt Sie schrittweise durch das Installieren der Pakete im Dateisystem oder in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Es gibt folgende Möglichkeiten, um die Installation zu konfigurieren:  
  
-   Auswählen des Speichertyps und des Speicherorts zum Installieren der Pakete.  
  
-   Auswählen des Speicherorts zum Installieren von Paketabhängigkeiten.  
  
-   Überprüfen der Pakete nach dem Installieren der Pakete auf dem Zielserver.  
  
 Die dateibasierten Abhängigkeiten für Pakete werden immer im Dateisystem installiert. Wenn Sie ein Paket im Dateisystem installieren, werden die Abhängigkeiten im selben Ordner installiert, den Sie für das Paket angeben. Wenn Sie ein Paket in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installieren, können Sie den Ordner angeben, in dem die dateibasierten Abhängigkeiten gespeichert werden sollen.  
  
 Wenn das Paket Konfigurationen enthält, die zum Verwenden auf dem Zielcomputer geändert werden sollen, können Sie die Werte der Eigenschaften mit diesem Assistenten aktualisieren.  
  
 Außer der Installation von Paketen mit dem Paketinstallations-Assistenten können Sie Pakete mit dem Eingabeaufforderungs-Hilfsprogramm **dtutil** kopieren und verschieben. Weitere Informationen finden Sie unter [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
### So stellen Sie Pakete in einer Instanz von SQL Server bereit  
  
1.  Öffnen Sie den Bereitstellungsordner auf dem Zielcomputer.  
  
2.  Doppelklicken Sie auf die Manifestdatei „\<Projektname>.SSISDeploymentManifest“, um den Paketinstallations-Assistenten zu starten.  
  
3.  Wählen Sie auf der Seite **SSIS-Pakete bereitstellen** die Option **Bereitstellung in SQL Server** .  
  
4.  Wählen Sie optional **Pakete nach der Installation überprüfen** , wenn Sie die Pakete nach der Installation auf dem Zielserver überprüfen lassen möchten.  
  
5.  Geben Sie auf der Seite **Zielserver mit SQL Server angeben** die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an, in der die Pakete installiert werden sollen, und wählen Sie einen Authentifizierungsmodus aus. Wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung auswählen, müssen Sie einen Benutzernamen und ein Kennwort bereitstellen.  
  
6.  Geben Sie auf der Seite **Installationsordner auswählen** den Dateisystemordner für die zu installierenden Paketabhängigkeiten an.  
  
7.  Wenn das Paket Konfigurationen enthält, können Sie diese bearbeiten, indem Sie die Werte der **Wert** -Liste auf der Seite Pakete konfigurieren aktualisieren.  
  
8.  Wenn Sie ausgewählt haben, dass Pakete nach der Installation überprüft werden sollen, zeigen Sie nun die Überprüfungsergebnisse der bereitgestellten Pakete an.  
  
## Siehe auch  
 [Legacy-Paketbereitstellung &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)  
  
  