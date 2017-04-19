---
title: "How to: Verify the Digital Signatures of XML Documents | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "System.Security.Cryptography.SignedXml class"
  - "signatures, cryptographic"
  - "System.Security.Cryptography.RSACryptoServiceProvider class"
  - "verifying signatures"
  - "checking signatures"
  - "XML digital signatures"
  - "digital signatures, verifying"
ms.assetid: a4d5ceb1-b9f5-47e8-9e4a-a2b39110002f
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# How to: Verify the Digital Signatures of XML Documents
Um XML\-Daten zu überprüfen, die mit einer digitalen Signatur signiert sind, können Sie die Klassen im <xref:System.Security.Cryptography.Xml>\-Namespace verwenden.  Über digitale XML\-Signaturen \(XMLDSIG\) können Sie sich vergewissern, dass Daten nicht mehr geändert wurden, nachdem sie signiert wurden.  Weitere Informationen über den XMLDSIG\-Standard finden Sie in der W3C\-Spezifikation \(World Wide Web Consortium\) unter "http:\/\/www.w3.org\/TR\/xmldsig\-core\/" \(nur auf Englisch verfügbar\).  
  
 Das Codebeispiel in dieser Vorgehensweise veranschaulicht, wie eine digitale XML\-Signatur überprüft wird, die in einem \<`Signature`\>\-Element enthalten ist.   Im Beispiel wird ein öffentlicher RSA\-Schlüssel aus einem Schlüsselcontainer abgerufen und anschließend zum Überprüfen der Signatur verwendet.  
  
 Informationen dazu, wie eine digitale Signatur erstellt wird, die mithilfe dieser Technik überprüft werden kann, finden Sie unter [How to: Sign XML Documents with Digital Signatures](../../../docs/standard/security/how-to-sign-xml-documents-with-digital-signatures.md).  
  
### So überprüfen Sie die digitale Signatur eines XML\-Dokuments  
  
1.  Um das Dokument zu überprüfen, müssen Sie denselben asymmetrischen Schlüssel wie für die Signierung verwenden.  Erstellen Sie ein <xref:System.Security.Cryptography.CspParameters>\-Objekt, und geben Sie den Namen des Schlüsselcontainers an, der zum Signieren verwendet wurde.  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#2)]
     [!code-vb[HowToVerifyXMLDocumentRSA#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#2)]  
  
2.  Rufen Sie den öffentlichen Schlüssel mit der <xref:System.Security.Cryptography.RSACryptoServiceProvider>\-Klasse ab.  Der Schlüssel wird automatisch nach Name aus dem Schlüsselcontainer geladen, wenn Sie das <xref:System.Security.Cryptography.CspParameters>\-Objekt an den Konstruktor der <xref:System.Security.Cryptography.RSACryptoServiceProvider>\-Klasse übergeben.  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#3)]
     [!code-vb[HowToVerifyXMLDocumentRSA#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#3)]  
  
3.  Erstellen Sie ein <xref:System.Xml.XmlDocument>\-Objekt, indem Sie eine XML\-Datei von einem Datenträger laden.  Das <xref:System.Xml.XmlDocument>\-Objekt enthält das signierte XML\-Dokument, das überprüft werden soll.  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#4)]
     [!code-vb[HowToVerifyXMLDocumentRSA#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#4)]  
  
4.  Erstellen Sie ein neues <xref:System.Security.Cryptography.Xml.SignedXml>\-Objekt, und übergeben Sie diesem das <xref:System.Xml.XmlDocument>\-Objekt.  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#5)]
     [!code-vb[HowToVerifyXMLDocumentRSA#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#5)]  
  
5.  Suchen Sie nach dem \<`signature`\>\-Element, und erstellen Sie ein neues <xref:System.Xml.XmlNodeList>\-Objekt.  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#6)]
     [!code-vb[HowToVerifyXMLDocumentRSA#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#6)]  
  
6.  Laden Sie den XML\-Code des ersten \<`signature`\>\-Elements in das <xref:System.Security.Cryptography.Xml.SignedXml>\-Objekt.  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#7)]
     [!code-vb[HowToVerifyXMLDocumentRSA#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#7)]  
  
7.  Überprüfen Sie die Signatur mit der <xref:System.Security.Cryptography.Xml.SignedXml.CheckSignature%2A>\-Methode und dem öffentlichen RSA\-Schlüssel.  Diese Methode gibt einen booleschen Wert zurück, mit dem Erfolg oder Fehlschlagen des Vorgangs angegeben wird.  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#8)]
     [!code-vb[HowToVerifyXMLDocumentRSA#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#8)]  
  
## Beispiel  
 Für dieses Beispiel wird angenommen, dass eine Datei namens `"test.xml"` im selben Verzeichnis wie das kompilierte Programm vorhanden ist.  Die Datei `"test.xml"` muss mit den Vorgehensweisen signiert worden sein, die unter [How to: Sign XML Documents with Digital Signatures](../../../docs/standard/security/how-to-sign-xml-documents-with-digital-signatures.md) beschrieben sind.  
  
 [!code-csharp[HowToVerifyXMLDocumentRSA#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#1)]
 [!code-vb[HowToVerifyXMLDocumentRSA#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#1)]  
  
## Kompilieren des Codes  
  
-   Um dieses Beispiel zu kompilieren, müssen Sie einen Verweis auf `System.Security.dll` einfügen.  
  
-   Fügen Sie die folgenden Namespaces hinzu: <xref:System.Xml>, <xref:System.Security.Cryptography> und <xref:System.Security.Cryptography.Xml>.  
  
## .NET Framework-Sicherheit  
 Sie sollten den privaten Schlüssel eines asymmetrischen Schlüsselpaars niemals in Klartext speichern oder übertragen.  Weitere Informationen über symmetrische und asymmetrische kryptografische Schlüssel finden Sie unter [Generating Keys for Encryption and Decryption](../../../docs/standard/security/generating-keys-for-encryption-and-decryption.md).  
  
 Sie sollten einen privaten Schlüssel niemals direkt in Ihren Quellcode einbetten.  Eingebettete Schlüssel können problemlos aus einer Assembly gelesen werden, indem [Ildasm.exe \(IL Disassembler\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) verwendet oder die Assembly in einem Texteditor wie Editor geöffnet wird.  
  
## Siehe auch  
 <xref:System.Security.Cryptography.Xml>   
 [How to: Sign XML Documents with Digital Signatures](../../../docs/standard/security/how-to-sign-xml-documents-with-digital-signatures.md)