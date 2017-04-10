---
title: "SSIS-Paket speichern (SQL Server-Import/Export-Assistent) | Microsoft Docs"
ms.custom: ""
ms.date: "02/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.savedtspackage.f1"
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
caps.latest.revision: 64
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 61
---
# SSIS-Paket speichern (SQL Server-Import/Export-Assistent)
  Wenn Sie auf der Seite **Paket speichern und ausführen** angegeben haben, dass das vom Assistenten erstellte SSIS-Paket gespeichert werden soll, zeigt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Import/Export-Assistent **SSIS-Paket speichern** an. Auf dieser Seite geben Sie zusätzliche Optionen für das Speichern des Pakets an.  

Die auf der Seite **SSIS-Paket speichern** angezeigten Optionen hängen von Ihrer Auswahl auf der Seite **Paket speichern und ausführen** ab, ob das Paket in SQL Server oder im Dateisystem gespeichert werden soll. Weitere Informationen zur Seite **Paket speichern und ausführen** finden Sie unter [Paket speichern und ausführen](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).
 
**Was ist ein Paket?** Der Assistent verwendet SQL Server Integration Services (SSIS) zum Kopieren von Daten. In SSIS stellt das Paket die Basiseinheit dar. Der Assistent erstellt ein SSIS-Paket im Arbeitsspeicher, während Sie die Seiten des Assistenten durchlaufen und Optionen festlegen.
 
## <a name="screen-shot---save-the-package-in-the-file-system"></a>Screenshot: Speichern des Pakets im Dateisystem
 
Der folgende Screenshot zeigt die Seite **SSIS-Paket speichern** des Assistenten nach der Auswahl der Option **Dateisystem** auf der Seite **Paket speichern und ausführen**. 
  
![Save SSIS Package page of the Import and Export Wizard](../../integration-services/import-export-data/media/save-package1.png "Save SSIS Package page of the Import and Export Wizard")  

## <a name="screen-shot---save-the-package-in-sql-server"></a>Screenshot: Speichern des Pakets in SQL Server

 Der folgende Screenshot zeigt die Seite **SSIS-Paket speichern** des Assistenten nach der Auswahl der Option **SQL Server** auf der Seite **Paket speichern und ausführen**. 
  
![Save SSIS Package page of the Import and Export Wizard](../../integration-services/import-export-data/media/save-package2.png "Save SSIS Package page of the Import and Export Wizard")  
  
## <a name="provide-a-name-and-description-for-the-package"></a>Bereitstellen eines Namens und einer Beschreibung für das Paket  
 **Name**  
 Geben Sie einen eindeutigen Namen für das Paket an.  
  
 **Beschreibung**  
 Geben Sie eine Beschreibung für das Paket an. Es wird hierbei empfohlen, das Paket zweckbezogen zu beschreiben, sodass Pakete selbsterklärend und einfacher zu verwalten sind.  
  
 **Target**  
 Das Ziel ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder Dateisystem), das Sie zuvor für das Paket angegeben haben. Wenn Sie das Paket an einem anderen Ziel speichern möchten, navigieren Sie zurück zur Seite **Paket speichern und ausführen**.
  
## <a name="save-the-package-in-the-file-system"></a>Speichern des Pakets im Dateisystem 
Wenn Sie ein Dateisystemziel ausgewählt haben, füllen Sie die folgenden Felder aus.

 **Dateiname**  
 Geben Sie den Pfad und den Dateinamen für die Zieldatei ein, oder verwenden Sie die Schaltfläche **Durchsuchen**, um ein Ziel auszuwählen.  
  
> [!TIP] Achten Sie darauf, einen Zielordner anzugeben – entweder durch Eingabe oder durch eine Suche. Wenn Sie nur den Dateinamen ohne Pfad eingeben, wissen Sie nicht, wo der Assistent das Paket speichert. Außerdem versucht der Assistent möglicherweise, das Paket an einem Speicherort zu speichern, an dem Sie nicht über die Berechtigung zum Speichern einer Datei verfügen, und löst einen Fehler aus.  
>   
>  Notieren Sie sich, wo Sie die Paketdatei speichern.  
  
 **Durchsuchen**  
 Sie können den Pfad zur Zieldatei auch im Dialogfeld **Paket speichern** durch eine Suche auswählen.  

## <a name="save-the-package-in-sql-server"></a>Speichern des Pakets in SQL Server 
Wenn Sie ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ziel ausgewählt haben, füllen Sie die folgenden Felder aus.

Der Assistent speichert das Paket in der Datenbank **msdb** in der Tabelle **sysssispackages**.
 
 > [!NOTE] Mit dieser Option wird das Paket nicht in der SSIS-Katalogdatenbank (SSISDB) gespeichert.  
 
 **Servername**  
 Geben Sie den Namen des Zielservers ein, oder wählen Sie ihn aus.  
   
 **Windows-Authentifizierung verwenden**  
Stellen Sie eine Verbindung mit dem Server mithilfe der integrierten Windows-Authentifizierung her. Dies ist die bevorzugte Authentifizierungsmethode.  
  
 **SQL Server-Authentifizierung verwenden**  
Stellen Sie eine Verbindung mit dem Server mithilfe der SQL Server-Authentifizierung her.  
  
 **Benutzername**  
Wenn Sie die SQL-Authentifizierung angegeben haben, geben Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Benutzernamen ein.  
  
 **Kennwort**  
Wenn Sie die SQL-Authentifizierung angegeben haben, geben Sie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Kennwort ein.  
  
## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>Informationen zu den beiden Seiten der Optionen für das Speichern des Pakets  
 Die Seite **SSIS-Paket speichern** ist eine der beiden Seiten, auf denen Sie Optionen für das Speichern des SSIS-Pakets auswählen.  
  
-   Auf der vorherigen Seite (**Paket speichern und ausführen**) haben Sie ausgewählt, ob das Paket in SQL Server oder als Datei gespeichert werden soll. Sie können auch Sicherheitseinstellungen für das gespeicherte Paket auswählen. Weitere Informationen zur Seite **Paket speichern und ausführen** finden Sie unter [Paket speichern und ausführen](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).  
  
-   Auf der aktuellen Seite geben Sie einen Namen für das Paket und weitere Informationen dazu an, wo Sie es speichern möchten.  
 
## <a name="run-the-saved-package-again-later"></a>Erneutes Ausführen des gespeicherten Pakets zu einem späteren Zeitpunkt  
 Weitere Informationen dazu, wie Sie das gespeicherte Paket später erneut ausführen, finden Sie in den folgenden Themen.  
  
-   Weitere Informationen dazu, wie Sie ein Paket über eine benutzerfreundliche Oberfläche eines Hilfsprogramms ausführen, finden Sie unter [Paketausführungshilfsprogramm &#40;DtExecUI&#41; – Referenz zur Benutzeroberfläche](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md).  
  
-   Weitere Informationen dazu, wie Sie ein Paket über die Eingabeaufforderung oder über eine Batchdatei ausführen, finden Sie unter [dtexec (Hilfsprogramm)](../../integration-services/packages/dtexec-utility.md).  
  
-   Wenn Sie das Paket im Dateisystem gespeichert haben, finden Sie unter [Ausführen eines Pakets in SQL Server Data Tools](../../integration-services/packages/run-a-package-in-sql-server-data-tools.md) Informationen zum Ausführen des Pakets in der Entwicklungsumgebung. Sie müssen das Paket einem Integration Services-Projekt hinzufügen, bevor Sie es öffnen und ausführen können.  
 
-   Wenn Sie das Paket in SQL Server in der Datenbank **msdb** gespeichert haben, stellen Sie eine Verbindung mit dem Integration Services-Dienst her. Navigieren Sie dann in SQL Server Management Studio im Objekt-Explorer zu **Gespeicherte Pakete | MSDB**, klicken Sie mit der rechten Maustaste auf das Paket, und wählen Sie **Paket ausführen** aus.

## <a name="customize-the-saved-package"></a>Anpassen des gespeicherten Pakets  
 Weitere Informationen zum Anpassen des gespeicherten Pakets finden Sie unter [Integration Services-Pakete &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md).  
  
## <a name="whats-next"></a>Wie geht es weiter?  
 Nachdem Sie zusätzliche Optionen für das Speichern des Pakets angegeben haben, ist die nächste Seite **Abschließen des Assistenten**. Auf dieser Seite überprüfen Sie die im Assistenten ausgewählten Optionen und starten dann den Vorgang. Weitere Informationen finden Sie unter [Assistenten abschließen](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).  
 
## <a name="see-also"></a>Siehe auch  
[Speichern von Paketen](../../integration-services/save-packages.md)  
[Ausführen von Integration Services-Paketen (SSIS)](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)
 
 