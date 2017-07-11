---
title: "&lt;netTcpBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "netTcpBinding-Element"
ms.assetid: 5c5104a7-8754-4335-8233-46a45322503e
caps.latest.revision: 33
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 33
---
# &lt;netTcpBinding&gt;
Gibt eine sichere, zuverlässige und optimierte Bindung an, die computerübergreifende Kommunikation unterstützt.  Diese Bindung generiert standardmäßig einen Laufzeitkommunikationsstapel mit Windows\-Sicherheit für die Nachrichtensicherheit und die Authentifizierung, TCP für die Nachrichtenübermittlung sowie binäre Nachrichtencodierung.  
  
## Syntax  
  
```  
  
<netTcpBinding>  
   <binding   
      closeTimeout="TimeSpan"  
      hostNameComparisonMode="StrongWildCard/Exact/WeakWildcard"  
      listenBacklog="Integer"  
      maxBufferPoolSize="integer"  
      maxBufferSize="Integer"  
      maxConnections="Integer"   
      maxReceivedMessageSize="Integer"  
      name="string"  
      openTimeout="TimeSpan"  
      portSharingEnabled="Boolean"  
      receiveTimeout="TimeSpan"  
      sendTimeout="TimeSpan"  
      transactionFlow="Boolean"   
      transactionProtocol="OleTransactions/WSAtomicTransactionOctober2004"   
            transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse"  
  
      <reliableSession ordered="Boolean"  
            inactivityTimeout="TimeSpan"  
            enabled="Boolean" />  
      <security mode="None/Transport/Message/Both">  
            <message clientCredentialType="None/Windows/UserName/Certificate/CardSpace"  
                defaultProtectionLevel="None/Sign/EncryptAndSign"   
algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15" />  
            <transport clientCredentialType="None/Windows/Certificate"  
                protectionLevel="None/Sign/EncryptAndSign" />  
      </security>  
       <readerQuotas   
            maxArrayLength="Integer"  
            maxBytesPerRead="Integer"  
            maxDepth="Integer"   
            maxNameTableCharCount="Integer"           
            maxStringContentLength="Integer" />  
   </binding>  
</netTcpBinding>  
```  
  
## Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### Attribute  
  
|Attribut|Beschreibung|  
|--------------|------------------|  
|closeTimeout|Ein <xref:System.TimeSpan>\-Wert, der das Zeitintervall für den Abschluss eines Schließvorgangs angibt.  Dieser Wert muss größer oder gleich <xref:System.TimeSpan.Zero> sein.  Der Standardwert ist 00:01:00.|  
|hostnameComparisonMode|Gibt den HTTP\-Hostnamen\-Vergleichsmodus an, der verwendet wird, um URIs zu analysieren.  Dieses Attribut ist vom Typ <xref:System.ServiceModel.HostnameComparisonMode> und gibt an, ob beim Abgleich des URI der Hostname zum Erreichen des Dienstes verwendet wird.  Der Standardwert lautet <xref:System.ServiceModel.HostnameComparisonMode.StrongWildcard>, wodurch der Hostname beim Abgleich ignoriert wird.|  
|listenBacklog|Eine positive ganze Zahl, die die maximale Anzahl an Kanälen angibt, die im Listener darauf warten, akzeptiert zu werden.  Verbindungen oberhalb des Limits werden in die Warteschlange gestellt, bis unterhalb des Limits Speicherplatz verfügbar wird.  Das `connectionTimeout`\-Attribut beschränkt die Zeit, die ein Client wartet, bevor eine Verbindungsausnahme ausgelöst wird.  Der Standard ist 10.|  
|maxBufferPoolSize|Eine ganze Zahl, die die maximale Pufferpoolgröße für diese Bindung angibt.  Der Standardwert ist 512 \* 1024 Bytes.  Viele Teile von Windows Communication Foundation \(WCF\) verwenden Puffer.  Das Erstellen und Zerstören von Puffern bei jeder Verwendung ist kostspielig. Dasselbe gilt für die Garbage Collection für Puffer.  Bei Pufferpools können Sie einen zu verwendenden Puffer aus dem Pool nehmen und ihn nach der Verwendung wieder dem Pool zuführen.  So wird der Aufwand beim Erstellen und Zerstören von Puffern vermieden.|  
|maxBufferSize|Eine positive ganze Zahl, die die maximale Größe des Puffers in Bytes angibt, der zum Speichern von Nachrichten verwendet wird.<br /><br /> Wenn das `transferMode`\-Attribut auf `Buffered` festgelegt ist, sollte dieses Attribut auf den `maxReceivedMessageSize`\-Attributwert festgelegt werden.<br /><br /> Wenn das `transferMode`\-Attribut auf `Streamed` festgelegt ist, darf dieses Attribut den `maxReceivedMessageSize`\-Attributwert nicht überschreiten und sollte mindestens auf die Größe des Headers festgelegt werden.<br /><br /> Der Standard ist 65536.  Weitere Informationen finden Sie unter <xref:System.ServiceModel.Configuration.NetNamedPipeBindingElement.MaxBufferSize%2A>.|  
|maxConnections|Eine ganze Zahl, die die maximale Anzahl ausgehender und eingehender Verbindungen angibt, die der Dienst erstellt bzw. akzeptiert.  Eingehende und ausgehende Verbindungen werden mit einem separaten, von diesem Attribut angegebenen Grenzwert verglichen.<br /><br /> Eingehende Verbindungen, die diesen Grenzwert überschreiten, werden in die Warteschlange gestellt, bis wieder Speicherplatz verfügbar wird.<br /><br /> Ausgehende Verbindungen, die diesen Grenzwert überschreiten, werden in die Warteschlange gestellt, bis wieder Speicherplatz verfügbar wird.<br /><br /> Der Standard ist 10.|  
|maxReceivedMessageSize|Eine positive ganze Zahl, die die maximale Nachrichtengröße in Bytes einschließlich Header angibt, die in einem für diese Bindung konfigurierten Kanal beim Nachrichtenempfang zulässig ist.  Der Absender einer Nachricht, die diese Grenze überschreitet, erhält einen SOAP\-Fehler.  Der Empfänger verwirft die Nachricht und erstellt einen Eintrag des Ereignisses im Ablaufverfolgungsprotokoll.  Der Standard ist 65536.|  
|Name|Eine Zeichenfolge, die den Konfigurationsnamen der Bindung enthält.  Dieser Wert sollte eindeutig sein, da er von der Bindung zur Identifizierung verwendet wird.  Ab [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)] müssen Bindungen und Verhalten keinen Namen aufweisen.  Weitere Informationen zu Standardkonfiguration und zu namenlosen Bindungen und Verhalten finden Sie unter [Vereinfachte Konfiguration](../../../../../docs/framework/wcf/simplified-configuration.md) und [Vereinfachte Konfiguration für WCF\-Dienste](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).|  
|openTimeout|Ein <xref:System.TimeSpan>\-Wert, der das Zeitintervall für den Abschluss eines Öffnungsvorgangs angibt.  Dieser Wert muss größer oder gleich <xref:System.TimeSpan.Zero> sein.  Der Standardwert ist 00:01:00.|  
|portSharingEnabled|Ein boolescher Wert, der angibt, ob die TCP\-Anschlussfreigabe für diese Verbindung aktiviert ist.  Wenn dies `false` ist, verwendet jede Bindung ihren eigenen Anschluss.  Diese Einstellung ist nur für Dienste relevant, da Clients nicht betroffen sind.|  
|receiveTimeout|Ein <xref:System.TimeSpan>\-Wert, der das Zeitintervall für den Abschluss eines Empfangsvorgangs angibt.  Dieser Wert muss größer oder gleich <xref:System.TimeSpan.Zero> sein.  Der Standardwert ist 00:10:00.|  
|sendTimeout|Ein <xref:System.TimeSpan>\-Wert, der das Zeitintervall für den Abschluss eines Sendevorgangs angibt.  Dieser Wert muss größer oder gleich <xref:System.TimeSpan.Zero> sein.  Der Standardwert ist 00:01:00.|  
|transactionFlow|Ein boolescher Wert, der angibt, ob die Bindung geleitete WS\-Transaktionen unterstützt.  Die Standardeinstellung ist `false`.|  
|transactionProtocol|Gibt das Transaktionsprotokoll an, das mit dieser Bindung verwendet werden soll.  Folgende Werte sind gültig:<br /><br /> -   OleTransactions<br />-   WSAtomicTransactionOctober2004<br /><br /> Der Standardwert ist OleTransactions.  Dieses Attribut ist vom Typ <xref:System.ServiceModel.TransactionProtocol>.|  
|transferMode|Ein <xref:System.ServiceModel.TransferMode>\-Wert, der angibt, ob Nachrichten bei einer Anforderung oder Antwort gepuffert oder per Stream übertragen werden.|  
  
### Untergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|------------------|  
|[\<Sicherheit\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-nettcpbinding.md)|Definiert die Sicherheitseinstellungen für die Bindung.  Dieses Element ist vom Typ <xref:System.ServiceModel.Configuration.NetTcpSecurityElement>.|  
|[\<readerQuotas\>](../Topic/%3CreaderQuotas%3E.md)|Definiert die Beschränkungen der Komplexität von SOAP\-Nachrichten, die von Endpunkten verarbeitet werden können, die mit dieser Bindung konfiguriert wurden.  Dieses Element ist vom Typ <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>.|  
|[reliableSession](http://msdn.microsoft.com/de-de/9c93818a-7dfa-43d5-b3a1-1aafccf3a00b)|Gibt an, ob zuverlässige Sitzungen zwischen Kanalendpunkten aufgebaut werden.|  
  
### Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|------------------|  
|[\<Bindungen\>](../../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)|Dieses Element enthält eine Auflistung von standardmäßigen und benutzerdefinierten Bindungen.|  
  
## Hinweise  
 Diese Bindung generiert standardmäßig eine Laufzeitkommunikation, die Transportsicherheit, TCP zur Nachrichtenübermittlung und eine binäre Nachrichtencodierung verwendet.  Diese Bindung ist eine entsprechende, vom [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)]\-System bereitgestellte Wahl für die Kommunikation über ein Intranet.  
  
 Die Standardkonfiguration für die `netTcpBinding` ist schneller als die von `wsHttpBinding` bereitgestellte Kommunikation, ist aber ausschließlich für [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)]\-zu\-[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)]\-Kommunikation vorgesehen.  Das Sicherheitsverhalten ist mit dem optionalen `securityMode`\-Attribut konfigurierbar.  Die Verwendung von WS\-ReliableMessaging ist mit dem optionalen `reliableSessionEnabled`\-Attribut konfigurierbar.  Zuverlässiges Messaging ist jedoch standardmäßig deaktiviert.  Die vom System bereitgestellten HTTP\-Bindungen, wie z.&\#160;B. `wsHttpBinding` und `basicHttpBinding` sind im Allgemeinen so konfiguriert, dass Funktionen standardmäßig aktiviert werden ,während die `netTcpBinding`\-Bindung Funktionen standardmäßig deaktiviert, sodass Sie die Unterstützung für eine der WS\-\*\-Spezifikationen explizit übernehmen müssen.  Das bedeutet, dass die Standardkonfiguration für TCP Meldungen zwischen Endpunkten schneller austauscht als die standardmäßig für die HTTP\-Bindungen festgelegten Konfigurationen.  
  
## Beispiel  
 Die Bindung wird in den Konfigurationsdateien für den Client und Dienst angegeben.  Der Bindungstyp wird im `binding`\-Attribut des `<endpoint>`\-Elements angegeben.  Wenn Sie die netTcpBinding\-Bindung konfigurieren und einige der Einstellungen ändern möchten, müssen Sie eine Bindungskonfiguration definieren.  Der Endpunkt muss auf die Bindungskonfiguration mithilfe des `bindingConfiguration`\-Attributs verweisen.  Im folgenden Beispiel wird eine Bindungskonfiguration definiert.  
  
```  
<services>  
  <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
           behaviorConfiguration="CalculatorServiceBehavior">  
    ...  
    <endpoint address=""  
              binding="netTcpBinding"  
              contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    ...  
  </service>  
</services>  
  
<bindings>  
  <netTcpBinding>  
    <binding   
             closeTimeout="00:01:00"  
             openTimeout="00:01:00"   
             receiveTimeout="00:10:00"   
             sendTimeout="00:01:00"  
             transactionFlow="false"   
             transferMode="Buffered"   
             transactionProtocol="OleTransactions"  
             hostNameComparisonMode="StrongWildcard"   
             listenBacklog="10"  
             maxBufferPoolSize="524288"   
             maxBufferSize="65536"   
             maxConnections="10"  
             maxReceivedMessageSize="65536">  
      <readerQuotas maxDepth="32"   
                    maxStringContentLength="8192"   
                    maxArrayLength="16384"  
                    maxBytesPerRead="4096"   
                    maxNameTableCharCount="16384" />  
      <reliableSession ordered="true"   
                       inactivityTimeout="00:10:00"  
                       enabled="false" />  
      <security mode="Transport">  
        <transport clientCredentialType="Windows" protectionLevel="EncryptAndSign" />  
      </security>  
    </binding>  
  </netTcpBinding>  
</bindings>  
```  
  
## Siehe auch  
 <xref:System.ServiceModel.NetTcpBinding>   
 <xref:System.ServiceModel.Configuration.NetTcpBindingElement>   
 [Bindungen](../../../../../docs/framework/wcf/bindings.md)   
 [Konfigurieren der vom System bereitgestellten Bindungen](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/de-de/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<Bindung\>](../../../../../docs/framework/misc/binding.md)