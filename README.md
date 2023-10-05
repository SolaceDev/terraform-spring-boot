
# Terraform Client
Add the following dependency to your project's `pom.xml` will enable you to use the `TerraformClient` class.

```xml
<dependency>
    <groupId>com.solace.maas</groupId>
    <artifactId>terraform-client</artifactId>
    <version>1.0.0</version>
</dependency>
```

And now you are able to provision terraform resources in your Java application. Make sure you have already put a terraform file `storage.tf` under `/some/local/path/` folder; and then use the Java code snippet below to invoke `terraform` executable operate on the resources defined in `storage.tf`. In this example, we also assume that you are provisioning Azure specific resource, which means you need to set some Azure related credentials.

```java
try (TerraformClient client = new TerraformClient()) {
    client.setOutputListener(System.out::println);
    client.setErrorListener(System.err::println);

    client.setWorkingDirectory("/some/local/path/");
    client.plan().get();
    client.apply().get();
}
```
