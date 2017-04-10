---
title: "Konvertieren von Typen ohne Konvertierungspr&#252;fung (SQL Server-Import/Export-Assistent) | Microsoft Docs"
ms.custom: ""
ms.date: "01/11/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.nomappingfile.f1"
ms.assetid: 87d9d3e5-477f-4117-a37f-bff53ea3e14d
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# Konvertieren von Typen ohne Konvertierungspr&#252;fung (SQL Server-Import/Export-Assistent)
  Nachdem Sie die vorhandenen Tabellen und Ansichten ausgewählt haben, um die von Ihnen angegebene Abfrage zu kopieren oder zu überprüfen, wird im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Import/Export-Assistent ggf. **Typen ohne Konvertierungsprüfung konvertieren** angezeigt. Der Assistent zeigt diese Seite an, wenn er mindestens eine der Datentypkonvertierungs- und Zuordnungsdateien nicht finden kann, die er benötigt, um Datentypen zwischen Ihrer Quelle und dem Ziel zuzuordnen. Die Seite enthält Informationen, die Ihnen hilft zu verstehen, was fehlt.
  
 Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen, ohne zu wissen, ob Datentypkonvertierungen erfolgreich sein werden. Klicken Sie andernfalls auf **Zurück**, um Ihre Auswahl zu ändern, oder auf **Abbrechen**, um den Assistenten zu beenden.
  
 Informationen dazu, wie der Assistent Datentypen aus den Quellspalten den Zielspalten zuordnet und Zuordnungsdateien für Datentypen verwendet, finden Sie unter [Wie ordnet der Assistent Datentypen zwischen Quelle und Ziel zu?](Import%20and%20Export%20Data%20with%20the%20SQL%20Server%20Import%20and%20Export%20Wizard.md\#wizardMapping).  

## <a name="screen-shot-of-the-convert-types-page"></a>Screenshot der Seite „Konvertieren von Typen“  
  
Die folgende Abbildung zeigt ein Beispiel der Seite **Typen ohne Konvertierungsprüfung konvertieren** des Assistenten.

![Konvertieren von Typen](../../integration-services/import-export-data/media/convert-types.png)

Das Problem hier ist, dass der Assistent keine Zuordnungsdatei finden kann, die Datentypen für das von Ihnen ausgewählte Ziel zuordnet.

Die Informationen auf dieser Seite enthalten nicht den Namen der fehlenden Zuordnungsdatei. Da der Assistent nicht weiß, ob eine Datei für den angegebenen Datenanbieter vorhanden ist, kann er keinen Namen für die fehlende Datei bereitstellen.

## <a name="whats-next"></a>Wie geht es weiter?  
 Nachdem Sie auf **Weiter** geklickt haben, um dem Fortsetzen des Vorgangs zuzustimmen, ohne zu wissen, ob Datentypkonvertierungen erfolgreich sind, lautet die nächste Seite **Paket speichern und ausführen**. Auf dieser Seite geben Sie an, ob der Kopiervorgang sofort ausgeführt werden soll. Abhängig von Ihrer Konfiguration können Sie möglicherweise auch das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paket speichern, das der Assistent erstellt hat, um es anzupassen und später wiederzuverwenden. Weitere Informationen finden Sie unter [Paket speichern und ausführen](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).  
