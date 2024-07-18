# bamoe-canvas-quarkus-accelerator

Sample project demonstrating process add-on capabilities explained in this [blog post](https://karinavarela.me/2024/07/18/events-addon-current-state-and-insights/).

Project requires:
- JDK 17
- Kafka
- Maven deps configured as explained [here](https://www.ibm.com/docs/en/ibamoe/9.1.x?topic=installing-configuring-maven-bamoe-binaries).


Start quarkus in dev mode:
 `mvn quarkus:dev`

Your application will up at http://localhost:8080.

The OpenAPI spec will be available at http://localhost:8080/q/openapi or http://localhost:8080/q/openapi?format=json.

The Swagger interface will be at http://localhost:8080/q/swagger-ui.

More tools available via Quarkus Dev UI http://localhost:8080/q/dev.


