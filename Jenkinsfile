#!groovy

node {
   // ------------------------------------
   // -- ETAPA: Compilar
   // ------------------------------------
   stage 'Build / Compilacion'
   
   // -- Configura variables
   echo 'Configurando variables'
   def mvnHome = tool 'M3'
   env.PATH = "${mvnHome}/bin:${env.PATH}"
   echo "var mvnHome='${mvnHome}'"
   echo "var env.PATH='${env.PATH}'"
   
   // -- Descarga código desde SCM
   echo 'Descargando código de SCM'
   sh 'rm -rf *'
   checkout scm
   
    // ------------------------------------
   // -- ETAPA: Sonarqube
   // ------------------------------------
   //stage 'Sonarqube'
   //echo '*executing ... Sonarqube*'
  // sh 'mvn clean install sonar:sonar -P qa-ui -Dmaven.test.skip=true -f ./pom.xml'
   
   // -- Compilando
   echo 'Compilando aplicación'
   sh 'mvn clean compile'
   
   // ------------------------------------
   // -- ETAPA: Test
   // ------------------------------------
   // stage 'Test'
   //echo 'Ejecutando tests'
   //try{
      //sh 'mvn verify'
      //step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
   //}catch(err) {
     // step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
      //if (currentBuild.result == 'UNSTABLE')
         //currentBuild.result = 'FAILURE'
      //throw err
   //}
   
   // ------------------------------------
   // -- ETAPA: Instalar
   // ------------------------------------
   stage 'Install'
   echo 'Instala el paquete generado en el repositorio maven'
   sh 'mvn install -Dmaven.test.skip=true'
   
   // ------------------------------------
   // -- ETAPA: Archivar
   // ------------------------------------
   stage 'Deploy/Archive'
   echo 'Archiva el paquete el paquete generado en Jenkins'
   step([$class: 'ArtifactArchiver', artifacts: '**/target/*.jar, **/target/*.war', fingerprint: true])
}
