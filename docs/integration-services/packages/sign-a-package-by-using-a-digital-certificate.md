---
title: "Signieren eines Pakets mit einem digitalen Zertifikat | Microsoft Docs"
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
  - "Digitale Signaturen [Integration Services]"
  - "Signieren von Paketen [Integration Services]"
  - "Signaturen [Integration Services]"
ms.assetid: 182b115e-0fe2-4717-8dff-183f9eb6e397
caps.latest.revision: 60
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 60
---
# Signieren eines Pakets mit einem digitalen Zertifikat
  In diesem Thema wird beschrieben, wie ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket mit einem digitalen Zertifikat signiert wird. Mit einer digitalen Signatur in Verbindung mit anderen Einstellungen können Sie verhindern, dass ein ungültiges Paket geladen und ausgeführt wird.  
  
 Bevor Sie ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket signieren können, müssen Sie folgende Schritte ausführen:  
  
-   Erstellen oder besorgen Sie sich einen privaten Schlüssel für die Zuordnung zum Zertifikat, und speichern Sie diesen Schlüssel auf dem lokalen Computer.  
  
-   Besorgen Sie sich ein Zertifikat zum Zwecke der Codesignierung von einer vertrauenswürdigen Zertifizierungsstelle. Sie können eine der folgenden Methoden verwenden, um ein Zertifikat zu erhalten oder zu erstellen:  
  
    -   Rufen Sie ein Zertifikat von einer öffentlichen, kommerziellen Zertifizierungsstelle ab, die Zertifikate ausgibt.  
  
    -   Rufen Sie ein Zertifikat von einem Zertifikatserver ab, mit dem eine Organisation Zertifikate intern ausstellen kann. Sie müssen das Stammzertifikat, mit dem das Zertifikat signiert wird, zum Speicher für **Vertrauenswürdige Stammzertifizierungsstellen** hinzufügen. Zum Hinzufügen des Stammzertifikats verwenden Sie das Zertifikate-Snap-In für die [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Verwaltungskonsole (MMC). Weitere Informationen finden Sie im Thema "[Certificate Services](http://go.microsoft.com/fwlink/?LinkId=100755)" (möglicherweise nur in englischer Sprache) in der MSDN Library.  
  
    -   Erstellen Sie ein eigenes Zertifikat nur für Testzwecke. Das Certificate Creation-Tool (Makecert.exe) generiert X.509-Zertifikate für Testzwecke. Weitere Informationen finden Sie im Thema „[Certificate Creation Tool (Makecert.exe)](http://go.microsoft.com/fwlink/?LinkId=100756)“ in der MSDN Library.  
  
     Weitere Informationen über Zertifikate finden Sie in der Onlinehilfe für das Zertifikate-Snap-In. Weitere Informationen zum Signieren von Digital Assets finden Sie im Thema "[Signing and Checking Code with Authenticode](http://go.microsoft.com/fwlink/?LinkId=78100)" (möglicherweise nur in englischer Sprache) in der MSDN Library.  
  
-   Stellen Sie sicher, dass das Zertifikat für Codesignaturen aktiviert wurde. Überprüfen Sie die Eigenschaften des Zertifikats im Zertifikate-Snap-In, um festzustellen, ob ein Zertifikat zum Signieren von Code aktiviert ist.  
  
-   Legen Sie das Zertifikat im Speicher Persönlich ab.  
  
 Nachdem Sie die vorherigen Schritte ausgeführt haben, können Sie das folgende Verfahren verwenden, um ein Paket zu signieren.  
  
### So signieren Sie ein Paket  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem Paket, das Sie signieren möchten.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie in [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer im Menü **SSIS** auf **Digitale Signatur**.  
  
4.  Klicken Sie im Dialogfeld **Digitale Signatur** auf **Signieren**.  
  
5.  Wählen Sie im Dialogfeld **Zertifikat auswählen** ein Zertifikat aus.  
  
6.  (Optional) Klicken Sie auf **Zertifikat anzeigen**, um Zertifikatinformationen anzuzeigen.  
  
7.  Klicken Sie auf **OK** , um das Dialogfeld **Zertifikat auswählen** zu schließen.  
  
8.  Klicken Sie auf **OK** , um das Dialogfeld **Digitale Signatur** zu schließen.  
  
9. Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
     Obwohl das Paket signiert wurde, müssen Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nun so konfigurieren, dass die digitale Signatur vor dem Laden des Pakets geprüft oder verifiziert wird. Weitere Informationen finden Sie unter [Identifizieren der Quelle von Paketen mit digitalen Signaturen](../../integration-services/packages/identify-the-source-of-packages-with-digital-signatures.md).  
  
## Siehe auch  
 [Sicherheitsübersicht &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md)  
  
  