# [WCF-Konfigurationsschema](index.md)
## [<system.serviceModel>](system-servicemodel.md)
### [<Verhalten>](behaviors.md)
#### [<endpointBehaviors>](endpointbehaviors.md)
##### [<Verhalten>](behavior-of-endpointbehaviors.md)
###### [<clientCredentials>](clientcredentials.md)
####### [<clientCertificate>](clientcertificate-of-clientcredentials-element.md)
####### [<httpDigest>](httpdigest-element.md)
####### [<issuedToken>](issuedtoken.md)
######## [<issuerChannelBehaviors>](issuerchannelbehaviors-element.md)
######### [<add>](add-of-issuerchannelbehaviors.md)
######## [<localIssuer>](localissuer.md)
######### [<Kopfzeilen>](headers-element.md)
####### [<peer>](peer-of-clientcredentials-element.md)
######## [<certificate>](certificate-element.md)
######## [<messageSenderAuthentication>](messagesenderauthentication-element.md)
######## [<peerAuthentication>](peerauthentication-element.md)
####### [<serviceCertificate>](servicecertificate-of-clientcredentials-element.md)
######## [<Authentifizierung>](authentication-of-servicecertificate-element.md)
######## [<defaultCertificate>](defaultcertificate-element.md)
######## [<scopedCertificates>](scopedcertificates-element.md)
######### [<add>](add-of-scopedcertificates-element.md)
####### [<Fenster>](windows-of-clientcredentials-element.md)
###### [<callbackDebug>](callbackdebug.md)
###### [<callbackTimeouts>](callbacktimeouts.md)
###### [<clientVia>](clientvia.md)
###### [<dataContractSerializer>](datacontractserializer.md)
###### [<dispatcherSynchronization>](dispatchersynchronization.md)
###### [<enableWebScript>](enablewebscript.md)
###### [<endpointDiscovery>](endpointdiscovery.md)
####### [<scopes>](scopes.md)
######## [<add>](add-of-scopes.md)
####### [<Erweiterungen>](extensions.md)
###### [<soapProcessing>](soapprocessing.md)
###### [<synchronousReceive>](synchronousreceive-element.md)
###### [<transactedBatching>](transactedbatching.md)
###### [<webHttp>](webhttp.md)
#### [<serviceBehaviors>](servicebehaviors.md)
##### [<Verhalten>](behavior-of-servicebehaviors.md)
###### [<dataContractSerializer>](datacontractserializer-element.md)
###### [<persistenceProvider>](persistenceprovider.md)
###### [<Routing>](routing-of-servicebehavior.md)
###### [<serviceAuthenticationManager>](serviceauthenticationmanager.md)
###### [<serviceAuthorization>](serviceauthorization-element.md)
####### [<authorizationPolicies>](authorizationpolicies.md)
######## [<add>](add-of-authorizationpolicies.md)
###### [<serviceCredentials>](servicecredentials.md)
####### [<clientCertificate>](clientcertificate-of-servicecredentials.md)
######## [<authentication>](authentication-of-clientcertificate-element.md)
######## [<certificate>](certificate-of-clientcertificate-element.md)
####### [<issuedTokenAuthentication>](issuedtokenauthentication-of-servicecredentials.md)
######## [<allowedAudienceUris>](allowedaudienceuris.md)
######### [<add>](add-of-allowedaudienceuris.md)
######## [<knownCertificates>](knowncertificates.md)
######### [<add>](add-of-knowncertificates.md)
####### [<peer>](peer-of-servicecredentials.md)
######## [<certificate>](certificate-of-peer.md)
######## [<messageSenderAuthentication>](messagesenderauthentication.md)
######## [<peerAuthentication>](peerauthentication.md)
####### [<serviceCertificate>](servicecertificate-of-servicecredentials.md)
####### [<secureConversationAuthentication>](secureconversationauthentication-of-servicecredential.md)
####### [<userNameAuthentication>](usernameauthentication.md)
####### [<windowsAuthentication>](windowsauthentication-of-servicecredentials.md)
###### [<serviceDebug>](servicedebug.md)
###### [<serviceDiscovery>](servicediscovery.md)
###### [<serviceMetadata>](servicemetadata.md)
###### [<serviceSecurityAudit>](servicesecurityaudit.md)
###### [<serviceThrottling>](servicethrottling.md)
###### [<serviceTimeouts>](servicetimeouts.md)
###### [<workflowRuntime>](workflowruntime.md)
####### [<commonParameters>](commonparameters.md)
######## [<add>](add-of-commonparameters.md)
####### [<Dienste>](services-of-workflowruntime.md)
######## [<add>](add-of-services.md)
###### [<useRequestHeadersForMetadataAddress>](userequestheadersformetadataaddress.md)
####### [<defaultPorts>](defaultports.md)
######## [<add> von <defaultPorts>](add-of-defaultports.md)
### [<Bindungen>](bindings.md)
#### [<basicHttpBinding>](basichttpbinding.md)
##### [<Sicherheit>](security-of-basichttpbinding.md)
###### [<message>](message-of-basichttpbinding.md)
###### [<transport>](transport-of-basichttpbinding.md)
#### [<basicHttpContextBinding>](basichttpcontextbinding.md)
#### [<mexHttpBinding>](mexhttpbinding.md)
#### [<mexHttpsBinding>](mexhttpsbinding.md)
#### [<mexNamedPipeBinding>](mexnamedpipebinding.md)
#### [<mexTcpBinding>](mextcpbinding.md)
#### [<msmqIntegrationBinding></msmqIntegrationBinding>](msmqintegrationbinding.md)
##### [<Sicherheit>](security-of-msmqintegrationbinding.md)
###### [<transport>](transport-of-msmqintegrationbinding.md)
#### [<NetMsmqBinding>](netmsmqbinding.md)
##### [<Sicherheit>](security-of-netmsmqbinding.md)
###### [<message>](message-of-netmsmqbinding.md)
###### [<transport>](transport-of-netmsmqbinding.md)
#### [<netNamedPipeBinding>](netnamedpipebinding.md)
##### [<Sicherheit>](security-of-netnamedpipebinding.md)
###### [<transport>](transport-of-netnamedpipebinding.md)
#### [<netPeerTcpBinding>](netpeertcpbinding.md)
##### [<resolver>](resolver.md)
###### [<Benutzerdefiniert>](custom.md)
##### [<Sicherheit>](security-of-netpeerbinding.md)
###### [<transport>](transport-of-netpeertcpbinding.md)
#### [<netTcpBinding>](nettcpbinding.md)
##### [<Sicherheit>](security-of-nettcpbinding.md)
###### [<transport>](transport-of-nettcpbinding.md)
###### [<message>](message-element-of-nettcpbinding.md)
#### [<netTcpContextBinding>](nettcpcontextbinding.md)
#### [<webHttpBinding>](webhttpbinding.md)
##### [<Sicherheit>](security-of-webhttpbinding.md)
###### [<transport>](transport-of-webhttpbinding.md)
#### [<wsDualHttpBinding>](wsdualhttpbinding.md)
##### [<Sicherheit>](security-of-wsdualhttpbinding.md)
###### [<message>](message-of-wsdualhttpbinding.md)
#### [<wsFederationHttpBinding>](wsfederationhttpbinding.md)
##### [<Sicherheit>](security-of-wsfederationhttpbinding.md)
###### [<message>](message-element-of-wsfederationhttpbinding.md)
####### [<claimTypeRequirements>](claimtyperequirements-for-message.md)
######## [<add>](add-of-claimtyperequirements-element.md)
######## [<remove>](remove-of-claimtyperequirements-element.md)
######## [<clear>](clear-of-claimtyperequirements-element.md)
####### [<issuer>](issuer.md)
####### [<issuerMetadata>](issuermetadata.md)
####### [<tokenRequestParameters>](tokenrequestparameters.md)
######## [<xmlElement>](xmlelement.md)
#### [<wsHttpBinding>](wshttpbinding.md)
##### [<Sicherheit>](security-of-wshttpbinding.md)
###### [<message>](message-of-wshttpbinding.md)
###### [<transport>](transport-of-wshttpbinding.md)
#### [<wsHttpContextBinding>](wshttpcontextbinding.md)
#### [<ws2007FederationHttpBinding>](ws2007federationhttpbinding.md)
##### [<Sicherheit>](security-element-of-ws2007federationhttpbinding.md)
###### [<message>](message-element-of-ws2007federationhttpbinding.md)
#### [<ws2007HttpBinding>](ws2007httpbinding.md)
##### [<Sicherheit>](security-of-ws2007httpbinding.md)
###### [<message>](message-of-ws2007httpbinding.md)
###### [<transport>](transport-of-ws2007httpbinding.md)
#### [<customBinding>](custombinding.md)
##### [<compositeDuplex>](compositeduplex.md)
##### [<discoveryClient>](discoveryclient.md)
##### [Nachrichtenverschlüsselung](message-encoding.md)
###### [<binaryMessageEncoding>](binarymessageencoding.md)
###### [<mtomMessageEncoding>](mtommessageencoding.md)
###### [<textMessageEncoding>](textmessageencoding.md)
###### [<webMessageEncoding>](webmessageencoding.md)
###### [<byteStreamMessageEncoding>](bytestreammessageencoding.md)
##### [<oneWay>](oneway.md)
###### [<channelPoolSettings>](channelpoolsettings.md)
##### [<pnrpPeerResolver>](pnrppeerresolver.md)
##### [<privacyNoticeAt>](privacynoticeat.md)
##### [<<reliableSession>>](reliablesession.md)
##### [<Sicherheit>](security-of-custombinding.md)
###### [<issuedTokenParameters>](issuedtokenparameters.md)
####### [<additionalRequestParameters>](additionalrequestparameters-element.md)
####### [<claimTypeRequirements>](claimtyperequirements-element.md)
######## [<add>](add-of-claimtyperequirements.md)
####### [<issuer>](issuer-of-issuedtokenparameters.md)
####### [<issuerMetadata>](issuermetadata-of-issuedtokenparameters.md)
###### [<localClientSettings>](localclientsettings-element.md)
###### [<localServiceSettings>](localservicesettings-element.md)
###### [<secureConversationBootstrap>](secureconversationbootstrap.md)
##### [<sslStreamSecurity>](sslstreamsecurity.md)
##### [<transactionFlow>](transactionflow.md)
##### [Transportprotokolle](transports.md)
###### [<httpTransport>](httptransport.md)
###### [<httpsTransport>](httpstransport.md)
###### [<msmqIntegration>](msmqintegration.md)
####### [<msmqTransportSecurity>](msmqtransportsecurity.md)
###### [<msmqTransport>](msmqtransport.md)
###### [<namedPipeTransport>](namedpipetransport.md)
####### [<connectionPoolSettings> von <namedPipeTransport>](connectionpoolsettings.md)
###### [<peerTransport>](peertransport.md)
####### [<Sicherheit>](security-of-peertransport.md)
######## [<transport>](transport-of-peertransport.md)
###### [<tcpTransport>](tcptransport.md)
####### [<connectionPoolSettings>](connectionpoolsettings-of-tcptransport.md)
##### [<unrecognizedPolicyAssertion>](unrecognizedpolicyassertion.md)
##### [<useManagedPresentation>](usemanagedpresentation.md)
##### [<windowsStreamSecurity>](windowsstreamsecurity.md)
#### [<netHttpBinding>](nethttpbinding.md)
##### [<Sicherheit>](security-of-nethttpbinding.md)
###### [<message>](message-of-nethttpbinding.md)
###### [<transport>](transport-of-nethttpbinding.md)
##### [<webSocketSettings>](websocketsettings.md)
#### [<netHttpsBinding>](nethttpsbinding.md)
#### [<udpBinding>](udpbinding.md)
### [<client>](client.md)
#### [<Endpunkt (endpoint)>](endpoint-of-client.md)
##### [<Kopfzeilen>](headers.md)
##### [<Identität>](identity.md)
###### [<certificate>](certificate-for-identity.md)
###### [<certificateReference>](certificatereference-for-identity.md)
###### [<dns>](dns.md)
###### [<rsa>](rsa.md)
###### [<servicePrincipalName>](serviceprincipalname.md)
###### [<userPrincipalName>](userprincipalname.md)
#### [<Metadaten>](metadata.md)
##### [<wsdlImporters>](wsdlimporters.md)
###### [<wsdlImporter>](wsdlimporter.md)
##### [<policyImporters>](policyimporters.md)
###### [<policyImporter>](policyimporter.md)
### [<comContracts>](comcontracts.md)
#### [<comContract>](comcontract.md)
##### [<exposedMethods>](exposedmethods.md)
###### [<exposedMethod>](exposedmethod.md)
##### [<persistableTypes>](persistabletypes.md)
###### [<persistableType>](persistabletype.md)
##### [<userDefinedTypes>](userdefinedtypes.md)
###### [<userDefinedType>](userdefinedtype.md)
### [<commonBehaviors>](commonbehaviors.md)
### [<Diagnose>](diagnostics.md)
#### [<endToEndTracing>](endtoendtracing.md)
#### [<messageLogging></messageLogging>](messagelogging.md)
##### [<Filter>](filters.md)
###### [<add>](add-of-filters.md)
### [<Erweiterungen>](extensions-section.md)
#### [<behaviorExtensions>](behaviorextensions.md)
#### [<bindingElementExtensions>](bindingelementextensions.md)
#### [<bindingExtensions>](bindingextensions.md)
#### [<endpointExtensions>](endpointextensions.md)
### [<protocolMapping>](protocolmapping.md)
#### [<add>](add-of-protocolmapping.md)
### [<Routing>](routing.md)
#### [<backupLists>](backuplists.md)
##### [<backupList>](backuplist.md)
###### [<add>](add-of-backuplist.md)
#### [<Filter>](filters-of-routing.md)
##### [<Filter>](filter.md)
#### [<filterTables>](filtertables.md)
##### [<filterTable>](filtertable.md)
###### [<entries>](entries.md)
####### [<add>](add-of-entries.md)
#### [<namespaceTable>](namespacetable.md)
##### [<add> von <namespaceTable>](add-of-namespacetable.md)
### [<serviceHostingEnvironment>](servicehostingenvironment.md)
#### [<baseAddressPrefixFilters>](baseaddressprefixfilters.md)
##### [<add>](add-of-baseaddressprefixfilter.md)
#### [<serviceActivations>](serviceactivations.md)
##### [<add>](add-of-serviceactivations.md)
#### [<transportConfigurationTypes>](transportconfigurationtypes.md)
##### [<add>](add-of-transportconfigurationtype.md)
### [<Dienste>](services.md)
#### [<service>](service.md)
##### [<Host>](host.md)
###### [<baseAddresses>](baseaddresses.md)
####### [<add>](add-of-baseaddresses.md)
###### [<timeOuts>](timeouts.md)
##### [<Endpunkt (endpoint)>](endpoint-element.md)
### [<standardEndpoints>](standardendpoints.md)
#### [<announcementEndpoint>](announcementendpoint.md)
#### [<discoveryEndpoint>](discoveryendpoint.md)
#### [<dynamicEndpoint>](dynamicendpoint.md)
##### [<discoveryClientSettings>](discoveryclientsettings.md)
###### [<findCriteria>](findcriteria.md)
####### [<contractTypeNames>](contracttypenames.md)
######## [<add>](add-of-contracttypenames.md)
#### [<mexEndpoint>](mexendpoint.md)
#### [<udpAnnoucementEndpoint>](udpannoucementendpoint.md)
##### [<udpTransportSettings>](udptransportsettings-of-udpannouncementendpoint.md)
#### [<udpDiscoveryEndpoint>](udpdiscoveryendpoint.md)
##### [<udpTransportSettings>](udptransportsettings.md)
#### [<webHttpEndpoint>](webhttpendpoint.md)
#### [<webScriptEndpoint>](webscriptendpoint.md)
#### [<workflowControlEndpoint>](workflowcontrolendpoint.md)
### [<Verfolgen>](tracking-of-wcf.md)
#### [<participants>](participants-of-wcf.md)
##### [<add>](add-of-wcf.md)
#### [<trackingProfile>](trackingprofile-of-wcf.md)
##### [<Workflow>](workflow-of-wcf.md)
###### [<activityScheduledQueries>](activityscheduledqueries-of-wcf.md)
####### [<activityScheduledQuery>](activityscheduledquery-of-wcf.md)
###### [<activityStateQueries>](activitystatequeries-of-wcf.md)
####### [<activityStateQuery>](activitystatequery-of-wcf.md)
###### [<bookmarkResumptionQueries>](bookmarkresumptionqueries-of-wcf.md)
####### [<bookmarkResumptionQuery>](bookmarkresumptionquery-of-wcf.md)
###### [<cancelRequestedQueries>](cancelrequestedqueries-of-wcf.md)
####### [<cancelRequestedQuery>](cancelrequestedquery-of-wcf.md)
###### [<customTrackingQueries>](customtrackingqueries-of-wcf.md)
####### [<customTrackingQuery>](customtrackingquery-of-wcf.md)
###### [<faultPropagationQueries>](faultpropagationqueries-of-wcf.md)
####### [<faultPropagationQuery>](faultpropagationquery-of-wcf.md)
###### [<workflowInstanceQueries>](workflowinstancequeries-of-wcf.md)
####### [<workflowInstanceQuery>](workflowinstancequery-of-wcf.md)
######## [<Zustände>](states-of-wcf-workflowinstancequery.md)
######### [<-Zustand>](state-of-wcf-workflowinstancequery.md)
## [<system.serviceModel.activation>](system-servicemodel-activation.md)
### [<Diagnose>](diagnostics-for-activation.md)
### [<net.pipe>](net-pipe.md)
#### [<allowAccounts>](allowaccounts.md)
##### [<add>](add-of-allowaccounts.md)
### [<net.tcp>](net-tcp.md)
## [<system.runtime.serialization>](system-runtime-serialization.md)
### [<dataContractSerializer>](datacontractserializer-of-system-runtime-serialization.md)
#### [<declaredTypes>](declaredtypes.md)
##### [<add>](add-of-declaredtypes-element.md)
###### [<knownType>](knowntype.md)
####### [<-Parameter von >](parameter.md)