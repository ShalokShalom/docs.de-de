---
title: "ServiceModel-Transaktionskonfiguration | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Transaktionen [WCF], ServiceModel-Konfiguration"
ms.assetid: 5636067a-7fbd-4485-aaa2-8141c502acf3
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# ServiceModel-Transaktionskonfiguration
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] stellt drei Attribute zum Konfigurieren von Transaktionen für einen Dienst bereit: `transactionFlow`, `transactionProtocol` und `transactionTimeout`.  
  
## Konfigurieren des transactionFlow\-Attributs  
 Die meisten von [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] bereitgestellten vordefinierten Bindungen enthalten die Attribute `transactionFlow` und `transactionProtocol`, was bedeutet, dass Sie die Bindung so konfigurieren können, dass eingehende Transaktionen für einen bestimmten Endpunkt unter Verwendung eines bestimmten Transaktionsflussprotokolls akzeptiert werden.Darüber hinaus können Sie mit dem `transactionFlow`\-Element und dessen `transactionProtocol`\-Attribut Ihre eigene Bindung zu erstellen.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] zum Festlegen der Konfigurationselemente finden Sie unter [\<Bindung\>](../../../../docs/framework/misc/binding.md) und [WCF\-Konfigurationsschema](../../../../docs/framework/configure-apps/file-schema/wcf/index.md).  
  
 Das `transactionFlow`\-Attribut gibt an, ob der Transaktionsfluss für Dienstendpunkte aktiviert ist, die die Bindung verwenden.  
  
## Konfigurieren des transactionProtocol\-Attributs  
 Das `transactionProtocol`\-Attribut gibt das Transaktionsprotokoll an, das für die Dienstendpunkte verwendet werden soll, die die Bindung verwenden.  
  
 Nachstehend finden Sie ein Beispiel für einen Konfigurationsabschnitt, mit dem die angegebene Bindung so konfiguriert wird, dass der Transaktionsfluss unterstützt und das WS\-AtomicTransaction\-Protokoll verwendet wird.  
  
```  
<netNamedPipeBinding>  
   <binding name="test"  
      closeTimeout="00:00:10"  
      openTimeout="00:00:20"   
      receiveTimeout="00:00:30"  
      sendTimeout="00:00:40"  
      transactionFlow="true"  
      transactionProtocol="WSAtomicTransactionOctober2004"  
      hostNameComparisonMode="WeakWildcard"  
      maxBufferSize="1001"  
      maxConnections="123"   
      maxReceivedMessageSize="1000">  
   </binding>  
</netNamedPipeBinding>  
```  
  
## Konfigurieren des transactionTimeout\-Attributs  
 Sie können das `transactionTimeout`\-Attribut für Ihren [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Dienst im `behavior`\-Element der Konfigurationsdatei konfigurieren.Das folgende Codebeispiel veranschaulicht, wie Sie dabei vorgehen müssen:  
  
```  
<configuration>  
   <system.serviceModel>  
      <behaviors>  
         <behavior name="NewBehavior" transactionTimeout="00:01:00" /> <!-- 1 minute timeout -->  
      </behaviors>  
   </system.serviceModel>  
</configuration>  
```  
  
 Das `transactionTimeout`\-Attribut legt den Zeitraum fest, innerhalb dessen eine neue, für den Dienst erstellte Transaktion abgeschlossen sein muss.Dieses Attribut wird als <xref:System.Transactions.TransactionScope>\-Timeout für alle Vorgänge verwendet, die zu einer neuen Transaktion führen. Wird <xref:System.ServiceModel.OperationBehaviorAttribute> angewendet, wird die <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A>\-Eigenschaft auf `true` gesetzt.  
  
 Der Timeout gibt den Zeitraum von der Erstellung der Transaktion bis zum Abschluss von Phase 1 im Zweiphasencommit\-Protokoll an.  
  
 Wenn dieses Attribut in einem `service`\-Konfigurationsabschnitt festgelegt wird, sollten Sie mindestens eine Methode des zugehörigen Diensts mit <xref:System.ServiceModel.OperationBehaviorAttribute>, in dem die <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A>\-Eigenschaft auf `true` gesetzt ist, anwenden.  
  
 Beachten Sie, dass als Timeoutwert der kleinere Wert von dieser `transactionTimeout`\-Konfigurationseinstellung und allen <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A>\-Eigenschaften verwendet wird.  
  
## Siehe auch  
 [\<Bindung\>](../../../../docs/framework/misc/binding.md)   
 [WCF\-Konfigurationsschema](../../../../docs/framework/configure-apps/file-schema/wcf/index.md)