# Pulsar on Oracle Cloud Infrastructure Demo

## Set KUBECONFIG and PATH
As a different Kube config is used it is set again 
```bash
export KUBECONFIG=$HOME/.kube/configOCI
export PATH=/home/robert/bin:$PATH
```

## Connect with bash terminal within kubernete pod
Command-line functions can be done using pulsar toolset pod

```bash
kubectl exec -it -n pulsar pulsar-mini-toolset-0 /bin/bash
```

## Use pulsar admin to perform cluster management
The following command are usefull for cluster/tenant/topic management

### **Get cluster list**
Get list of Pulsar clusters

```bash
bin/pulsar-admin clusters list
```

### **Get tenants list**
Get list of tenants

```bash
bin/pulsar-admin tenants list
```

### **Create a new tenant**
Create new tenant aioug with role webinarAdmin

```bash
bin/pulsar-admin tenants create aioug -r webinarAdmin
```

### **Get the new tenant**
Get information about the tenant aioug

```bash
bin/pulsar-admin tenants get aioug
```

### **Create a new namespace**
Create a new namespace for tenant aioug for the webinar

```bash
bin/pulsar-admin namespaces create aioug/webinar
```

### **List namespace**
List namespaces related to tenant aioug

```bash
bin/pulsar-admin namespaces list aioug
```

### **Create a new partitioned topic**
```bash
bin/pulsar-admin topics create-partitioned-topic persistent://aioug/webinar/incidents -p 2
```

### **Consume messages using pulsar client**
```bash
bin/pulsar-client consume \
persistent://aioug/webinar/metrics \
--num-messages 0 \
--subscription-name example-sub \
--subscription-type Exclusive
```

### **Produce message using pulsar client**
```bash
bin/pulsar-client produce \
persistent://aioug/webinar/metrics \
--num-produce 1 \
--messages "Hello AIOUG" 
```

### **Delete a partitioned topic**
Topic can only be deleted when there are no active consumers
```bash
bin/pulsar-admin topics delete-partitioned-topic persistent://aioug/webinar/incidents
```

### **List topic statistics**
```bash
bin/pulsar-admin topics stats persistent://aioug/webinar/incidents-partition-1
```

### Explore Pulsar UIs
> [Pulsar Admin](http://193.122.14.136:9527/#/login)
> 
> [Grafanan Dashboard](http://130.61.14.119:3000/login)