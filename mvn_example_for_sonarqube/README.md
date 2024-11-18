# devops

```sh
docker run --rm -v "$(pwd)":/app -w /app maven:3.8.4-openjdk-11 mvn clean package


docker run --rm -e SONAR_HOST_URL="http://192.168.9.145:9000"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -D"sonar.projectKey=hello2" -D"sonar.sources=." -D"sonar.host.url=http://192.168.9.145:9000" -D"sonar.token=sqp_ff60e5c442939c51b9cc49951cc26c62916a1f64"

ERROR: Error during SonarScanner execution
org.sonar.java.AnalysisException: Your project contains .java files, please provide compiled classes with sonar.java.binaries property, or exclude them from the analysis with sonar.exclusions property.



```

```sh
docker run --rm -e SONAR_HOST_URL="http://192.168.9.145:9000" -v ".:/usr/src" sonarsource/sonar-scanner-cli \
-D"sonar.projectKey=hello2" \
-D"sonar.sources=." \
-D"sonar.host.url=http://192.168.9.145:9000" \
-D"sonar.token=sqp_ff60e5c442939c51b9cc49951cc26c62916a1f64" \
-D"sonar.java.binaries=./target/classes"
```