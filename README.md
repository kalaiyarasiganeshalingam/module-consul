[![Build Status](https://travis-ci.org/wso2-ballerina/module-consul.svg?branch=master)](https://travis-ci.org/wso2-ballerina/module-consul)

# Ballerina Consul Connector

The Consul Connector allows you to register services and checks, deregister services and checks, create, read and 
delete keys, list the details of 
the services, list the details of the check by state such as passing, warning, or critical etc.

## Compatibility
| Ballerina Language Version | Consul API version  |
| -------------------------- | ------------------- |
|  0.991.0                   | v1                  |


The following sections provide you with information on how to use the Ballerina Consul Connector.

- [Contribute To Develop](#contribute-to-develop)
- [Working with Consul Connector actions](#working-with-consul-connector-actions)
- [Example](#example)

### Contribute To develop

Clone the repository by running the following command 
```ballerina
git clone https://github.com/wso2-ballerina/module-consul.git
```

### Working with Consul Connector actions

All the actions return valid response or error. If the action is a success, then the requested resource will 
be returned. Else error will be returned.

In order for you to use the Consul Connector, first you need to create a Consul Client endpoint.

```ballerina
    consul:ConsulConfiguration consulConfig = {
         uri: "http://localhost:8500",
         aclToken: "",
         clientConfig: {}
    };
    
    consul:Client consulClient = new(consulConfig);
```

##### Example

```ballerina
import ballerina/io;
import ballerina/test;
import wso2/consul;

consul:ConsulConfiguration consulConfig = {
     uri: "http://localhost:8500",
     aclToken: "",
     clientConfig: {}
};

consul:Client consulClient = new(consulConfig);
    
public function main() {
    json jsonPayload = { "ID":"redis", "Name":"redis1", "Address":"localhost", "port":8000, "EnableTagOverride":false };
    var serviceRegistrationResponse = consulClient->registerService(jsonPayload);
    if (serviceRegistrationResponse is boolean) {
        io:println("Status of service registration: ", serviceRegistrationResponse);
    } else {
        io:println("Error: ", <string>serviceRegistrationResponse.detail().message);
    }
}
```
