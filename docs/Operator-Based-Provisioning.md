### Operator-based provisioning

The Intersmash Library provides support for operator-based provisioning, i.e. it automates the behavior needed to deploy
a given service on cloud environments via APIs that leverage the
[Operator Framework](https://github.com/operator-framework).

Intersmash makes this feature available for currently supported products (see the table below), but that can be
extended easily, since Intersmash _provisioners_ are pluggable components.

| Service                          | Supported Operator version | Channel name | Repository                                                | Notes                                                                                                                                                                              |
|:---------------------------------|:---------------------------|:-------------|:----------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ActiveMQ Artemis                 | 1.0.11                     | upstream     | https://github.com/artemiscloud/activemq-artemis-operator | We are using a custom index image, i.e. quay.io/jbossqe-eap/intersmash-activemq-operator-catalog:v1.0.11, built as described in https://github.com/Intersmash/intersmash/issues/32 |
| Red Hat AMQ Broker               | 7.11.6-opr-2               | 7.11.x       | https://github.com/rh-messaging/activemq-artemis-operator | As available on the OpenShift OperatorHub                                                                                                                                          |  
| Infinispan                       | 2.4.0                      | 2.4.x        | https://github.com/infinispan/infinispan-operator         | As available on the OpenShift OperatorHub (community-operators)                                                                                                                    |
| Red Hat DataGrid                 | 8.4.15                     | 8.4.x        | https://github.com/infinispan/infinispan-operator         | As available on the OpenShift OperatorHub                                                                                                                                          | 
| Kafka provided by Strimzi        | 0.38.0                     | stable       | https://github.com/strimzi/strimzi-kafka-operator         |                                                                                                                                                                                    |
| Red Hat AMQ Streams              | 2.6.0-2                    | stable       | https://github.com/strimzi/strimzi-kafka-operator         | As available on the OpenShift OperatorHub                                                                                                                                          |
| Keycloak                         | 24.0.3                     | fast         | https://github.com/keycloak/keycloak/tree/main/operator   | Latest Keycloak, based on Quarkus. Supports a limited number of CR (Keycloak and KeycloakRealmImport): more to come in upcoming versions                                           |
| Red Hat Build of keycloak (RHBK) | 24.0.3-opr.1               | stable-v24   | https://github.com/keycloak/keycloak/tree/main/operator   | Latest Keycloak, based on Quarkus.                                                                                                                                                 |
| Red Hat SSO - **DEPRECATED**     | 7.6.8-opr-001              | stable       | https://github.com/keycloak/keycloak-operator             | Latest Red Hat SSO Operator, based on legacy Keycloak                                                                                                                              |
| WildFly                          | 1.0.0                      | alpha        | https://github.com/wildfly/wildfly-operator               | As available on https://operatorhub.io/operator/wildfly                                                                                                                            |
| Red Hat JBoss EAP                | 3.0.0                      | stable       | https://github.com/wildfly/wildfly-operator               | As available on the OpenShift OperatorHub                                                                                                                                          |
| Hyperfoil                        | 0.24.2                     | alpha        | https://github.com/Hyperfoil/hyperfoil-operator           | We force the CRs version for the used Hyperfoil runtime to be 0.24.2, see https://github.com/Hyperfoil/hyperfoil-operator/issues/18                                                |

Intersmash operator-based provisioners implement a common contract and high level behavior which is defined by the
[OperatorProvisioner](../core/src/main/java/org/jboss/intersmash/provision/openshift/operator/OperatorProvisioner.java)
class.