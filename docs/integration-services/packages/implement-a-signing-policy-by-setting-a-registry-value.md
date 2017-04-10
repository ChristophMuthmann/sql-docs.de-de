---
title: "Implementieren einer Signaturrichtlinie durch Festlegen eines Registrierungswerts | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Signaturrichtlinien [Integration Services]"
ms.assetid: 64f6966f-2292-401f-acb1-2ccb5aee484a
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# Implementieren einer Signaturrichtlinie durch Festlegen eines Registrierungswerts
  Sie können einen optionalen Registrierungswert zum Verwalten einer Organisationsrichtlinie verwenden, um signierte und nicht signierte Pakete zu laden. Wenn Sie diesen Registrierungswert verwenden, müssen Sie ihn auf jedem Computer erstellen, auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete ausgeführt werden und auf dem Sie die Richtlinie durchsetzen möchten. Nachdem der Registrierungswert festgelegt wurde, überprüft oder verifiziert [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] die Signaturen vor dem Laden der Pakete.  
  
 Die Prozedur in diesem Thema beschreibt, wie Sie den optionalen DWORD-Wert **BlockedSignatureStates** zum Registrierungsschlüssel HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS hinzufügen. Der Datenwert in **BlockedSignatureStates** bestimmt, ob ein Paket blockiert werden soll, wenn es eine nicht vertrauenswürdige Signatur, eine ungültige Signatur oder keine Signatur aufweist. Hinsichtlich des Status der zum Signieren von Paketen verwendeten Signaturen werden für den Registrierungswert **BlockedSignatureStates** folgende Definitionen verwendet:  
  
-   Eine *gültige Signatur* ist eine Signatur, die erfolgreich gelesen werden kann.  
  
-   Eine *ungültige Signatur* ist eine Signatur, bei der die entschlüsselte Prüfsumme (der mit einem privaten Schlüssel verschlüsselte unidirektionale Hash des Paketcodes) nicht der entschlüsselten Prüfsumme entspricht, die während des Ladevorgangs von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paketen berechnet wird.  
  
-   Eine *vertrauenswürdige Signatur* ist eine Signatur, die mithilfe eines von einer vertrauenswürdigen Stammzertifizierungsstelle signierten digitalen Zertifikats erstellt wird. Für diese Einstellung ist es nicht erforderlich, dass der Unterzeichner in der Liste vertrauenswürdiger Herausgeber des Benutzers vorhanden ist.  
  
-   Eine *nicht vertrauenswürdige Signatur* ist eine Signatur, bei der nicht überprüft werden kann, ob sie von einer vertrauenswürdigen Stammzertifizierungsstelle ausgestellt wurde, oder eine Signatur, die nicht aktuell ist.  
  
 In der folgenden Tabelle werden die gültigen Werte der DWORD-Daten und ihre verbundenen Richtlinien aufgelistet.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|0|Keine administrative Einschränkung.|  
|1|Blockieren von ungültigen Signaturen.<br /><br /> Bei dieser Einstellung werden nicht signierte Pakete nicht blockiert.|  
|2|Blockieren von ungültigen und nicht vertrauenswürdigen Signaturen.<br /><br /> Bei dieser Einstellung werden zwar nicht signierte Pakete nicht blockiert, selbst generierte Signaturen werden jedoch blockiert.|  
|3|Blockieren von ungültigen und nicht vertrauenswürdigen Signaturen und nicht signierten Paketen.<br /><br /> Bei dieser Einstellung werden auch selbst generierte Signaturen blockiert.|  
  
> [!NOTE]  
>  Die empfohlene Einstellung für **BlockedSignatureStates** ist 3. Diese Einstellung bietet den besten Schutz vor nicht signierten Paketen oder Signaturen, die entweder ungültig oder nicht vertrauenswürdig sind. Die empfohlene Einstellung eignet sich jedoch möglicherweise nicht in allen Fällen. Weitere Informationen zum Signieren von Digital Assets finden Sie im Thema "[Introduction to Code Signing](http://go.microsoft.com/fwlink/?LinkId=51414)" (in Englisch) in der MSDN Library.  
  
### So implementieren Sie eine Signaturrichtlinie für ein Paket  
  
1.  Klicken Sie im Menü **Start** auf **Ausführen**.  
  
2.  Geben Sie im Dialogfeld **Regedit**ein, und klicken Sie dann auf **OK**.  
  
3.  Suchen Sie den Schlüssel HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS.  
  
4.  Klicken Sie mit der rechten Maustaste auf **MSDTS**, zeigen Sie auf **Neu**, und klicken Sie anschließend auf **DWORD-Wert**.  
  
5.  Aktualisieren Sie den Namen des neuen Werts auf **BlockedSignatureStates**.  
  
6.  Klicken Sie mit der rechten Maustaste auf **BlockedSignatureStates**, und klicken Sie anschließend auf **Ändern**.  
  
7.  Geben Sie im Dialogfeld **DWORD-Wert bearbeiten** den Wert 0, 1, 2, oder 3 ein.  
  
8.  Klicken Sie auf **OK**.  
  
9. Klicken Sie im Menü **Datei** auf **Beenden**.  
  
## Siehe auch  
 [Sicherheitsübersicht &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md)   
 [Identifizieren der Quelle von Paketen mit digitalen Signaturen](../../integration-services/packages/identify-the-source-of-packages-with-digital-signatures.md)  
  
  